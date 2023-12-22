# Архитектура Хранилищ

## Пример потока хранилищ

<figure><img src="broken-reference" alt=""><figcaption></figcaption></figure>

1. Пользователь вносит 100 ETH в T-ETH-C (колл ETH).
2. В пятницу в 8 утра UTC хранилище закрывает раунд предыдущей недели и затем использует 100% своих средств для майнинга 100 otokens, которые являются ERC20-представлениями опционных контрактов. 100 ETH блокируются на неделю в Opyn.
3. Получив 100 отокенов, хранилище выставляет его на аукцион [Paradigm](https://www.paradigm.co/).
   * Зарегистрированные пользователи могут участвовать в торгах и делать ставки на отокены. Они платят премию за отокены в ETH. Paradigm может использовать различные виды аукционов для максимизации прибыли вкладчиков (например, [слепые аукционы](https://en.wikipedia.org/wiki/First-price\_sealed-bid\_auction))
   * По окончании аукциона хранилище получает 1 ETH в виде премии.
   * Все оставшиеся отокены, которые не были куплены, сжигаются, выкупая 1 отокен за 1 единицу залога у Опина.
4. В следующую пятницу 8 утра UTC,
   * Если срок действия опционов истекает в деньгах, хранилище выводит из Opyn менее 100 ETH.
   * Если опционы заканчиваются не в деньгах, хранилище снимает ровно 100 ETH.
5. Предположим, что срок действия контракта закончился не в деньгах. Хранилище повторяет шаг 2 с 101 ETH (первоначальные 100 ETH + 1 ETH премии).

### Codebase

| Name                                                                                                                                               | Description                                                                                                        |
| -------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| [libraries/Vault.sol](https://github.com/ribbon-finance/ribbon-v2/blob/master/contracts/libraries/Vault.sol)                                       | Contains all data structures shared across all vault types                                                         |
| [libraries/VaultLifecycle.sol](https://github.com/ribbon-finance/ribbon-v2/blob/master/contracts/libraries/VaultLifecycle.sol)                     | Contains all logic related to how the Vault functions on a weekly basis                                            |
| [vaults/BaseVaults/base/RibbonVault.sol](https://github.com/ribbon-finance/ribbon-v2/blob/master/contracts/vaults/BaseVaults/base/RibbonVault.sol) | Contains all common logic like accounting and options rolling shared across RibbonThetaVault and RibbonDeltaVault. |
| [vaults/BaseVaults/RibbonThetaVault.sol](https://github.com/ribbon-finance/ribbon-v2/blob/master/contracts/vaults/BaseVaults/RibbonThetaVault.sol) | Theta Vault contract that creates short options position with Opyn on a weekly basis                               |

## Deposit Flow

IMPORTANT: this is a _technical_ explanation, if you need assistance on making a deposit please refer to [this page](broken-reference)!

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

1. The user deposits 1 ETH into TV.
2. We first check if they have an existing `DepositReceipt` from the past `round`. Using the `round` and `amount`, we update the `unredeemedShares` field. This essentially tracks how many shares the user owns, but has not yet redeemed.

```
struct DepositReceipt {
	round
	amount
	unredeemedShares
}
```

1. We create the DepositReceipt with the new details.
2. At `rollToNextOption`, the vault will mint all the shares that are owed to users to `address(this)`. This increments the `vaultState.round`.
3. Since the round is concluded, the user's vault shares should show up by calling `RibbonVault.shares(account)`

The end result:

* Their shares show up automatically once the round concludes.
* `DepositReceipt`s are used to track all the user's unredeemed shares. This is used for withdrawals and redemptions in the future.

## Withdrawal Flow

IMPORTANT: this is a _technical_ explanation, if you need assistance on making a withdrawal please refer to [this page](broken-reference)!

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

The withdrawal flow is slightly more involved. We have two types of withdrawals - Standard and Instant withdrawals.

### **Standard withdrawals**

* Withdrawals are created with the `initiateWithdraw` function, which queues the shares to be burned.
* Withdrawals are completed with `completeWithdraw` function, which burns the shares, and returns the assets.
* Users can only call `completeWithdraw` only AFTER the week's Friday 10am UTC. For example, the user calls `initiateWithdraw` on Wednesday. They can only complete the withdrawal after the same week's Friday 10am UTC.
* Withdrawals stack on top of each other. This means that if I do `initiateWithdraw(10)`, and I do `initiateWithdraw(20)` again, I will have a total withdrawal of 30 shares by Friday.

### **Instant withdrawals**

* Instant withdrawals are only accessible to funds that are deposited mid-week.
* For example, user deposits 10 ETH into TV on Wednesday. They can call `withdrawInstantly` to return up to 10 ETH, from Wednesday till Friday.

## Share Redemption Flow

IMPORTANT: this is a _technical_ explanation, if you need assistance on redeeming your vault shares please refer to [this page](broken-reference)!

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

As mentioned before, when the user deposits into the vault, the vault mints and holds custody of the user's shares on `address(this)`. This is not ideal for protocols or Meta-Vaults that want to hold custody of their shares. By calling the `redeem` or `maxRedeem` function, contracts are able to take custody of their vault shares.

The share redemption flow is also triggered implicitly when users call `initiateWithdraw`.

## Access Control

| Name  | Privileges                                                                                                                                                                                                                                          |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Owner | <p>The owner can set key parameters of the vault such as feeRecipient, performanceFee, managementFee, deposit cap etc.</p><p>Some functions in the vault's lifecycle is only limited to the owner, such as commitAndClose and rollToNextOption.</p> |
| Admin | The admin can upgrade the proxy's implementation address.                                                                                                                                                                                           |

Both of these privileged roles use a Gnosis Safe multisig wallet.
