# Bidding on Aevo RFQ

Moving forward, most of the Ribbon's Theta Vault will trade on Aevo's RFQ platform. This is a guide on how the auction process would be on Aevo.



To see the list of open RFQs: [https://app.aevo.xyz/rfq](https://app.aevo.xyz/rfq)

To create a new RFQ: [https://app.aevo.xyz/rfq/create](https://app.aevo.xyz/rfq/create)



1. Before participating the auction, please ensure that the account has sufficient USDC to pay for premiums. All premiums are paid in USDC.
2. First, the auction will be posted in this [Telegram channel](https://t.me/RibbonAuctions). The schedule will be communicated a day before. We will also notify when the auction is opened. It will only be open for 10 minutes.

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

2.  When the auction is opened on Aevo, there would be a new RFQ listed in the RFQ listing page. In the example below, there are a few details to cover:

    1. The RFQ created is a "BTC Buy". This is a short BTC call strategy that is requesting for a quote.
    2. The block size is the quantity of contracts to be traded.
    3. The leg size "x1" is the ratio of the legs within the block. This can be ignored for the purposes of the vault auctions.

    <figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>
3. To place a bid order, click the "Bid" button. You are able to specify the bid price in the form.

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

4. Once you bid is placed, you are able to see a "Cancel" button. This button removes your bid. Only the Best Bid is shown. Since the RFQ is only limited to full size for now, only the top bid will get filled.

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

5. When the RFQ creator accepts the quote, the RFQ will be removed from the RFQ Listing. This trade will show up in the account's trade history, under the order type of "Request for Quotation".

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>
