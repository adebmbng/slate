---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - http

toc_footers:
  - <a href='https://subagamilenia.com'>Documentation Powered by Subaga Inti Milenia</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the open SIM API! You can use this api to generate QRIS for payment. You need to request the secret key to our team, please send an email to [this](mailto:ade.bambang@subagamilenia.com)

# Authentication

SIM uses API keys to allow access to the API. You need to request the secret key to our team, please send an email to [this](mailto:ade.bambang@subagamilenia.com).

SIM expects for the API key to be included in all API requests to the server in a header that looks like the following:

`key: xxxxxxx`

<aside class="notice">
You must replace <code>xxxxxxx</code> with your personal API key.
</aside>

# QRIS Order

## Create QRIS Order

```shell
curl -X POST --location "https://sim.adebmbng.com/api/order/open/transaction" \
    -H "Content-Type: application/json" \
    -H "key: xxxxxx" \
    -d "{
          "orderType": "public-transaction",
          "merchantId": "subaga-parking",
          "price": 2500
        }"
```

```http
POST https://sim.adebmbng.com/api/order/open/transaction
Content-Type: application/json
key: xxxxxx

{
  "orderType": "public-transaction",
  "merchantId": "subaga-parking",
  "price": 2500
}
```

> The above command returns JSON structured like this:

```json
{
  "code": 200,
  "data": [
    {
      "qrString": "00020101021226660014ID.LINKAJA.WWW011893600911002411480002152004230411480010303UME51450015ID.OR.GPNQR.WWW02150000000000000000303UME520454995802ID5924Xendit Test - Do Not Pay6007Jakarta61061234566238011570ODN4RksMgs7HZ071570ODN4RksMgs7HZ53033605404250063042291",
      "invoiceId": "INVNVB3TN",
      "orderDetail": {
        "id": "caa8ad5d-9d76-4396-8b95-b98534981791",
        "invoiceId": "INVNVB3TN",
        "paymentStatus": "waitingForPayment",
        "price": 2500,
        "orderType": "public-transaction",
        "merchantId": "subaga-parking",
        "isActive": true,
        "merchantStatus": "orderReceived",
        "createdAt": "2021-07-07T16:24:58.709221+07:00",
        "updatedAt": "2021-07-07T16:24:58.709221+07:00"
      }
    }
  ],
  "message": "success"
}
```

This endpoint request an order that has QR payment.

### URL

`https://sim.adebmbng.com/api/order/open/transaction`

### Query Parameters

Parameter | Required | Default | Description
--------- | ------- | ------- | -----------
orderType | true | public-transaction | Use this as order type
merchantId | true | subaga-parking-## | You can change ## with your unique ID
price | true | 0 | Price minimum is 2500
ppn | false | false | Set ppn 10%
discount | false | 0 | Set discount price
additionalData | false | | Your unique data, it we return in callback

## Get order detail

```shell
curl -X GET --location "https://sim.adebmbng.com/api/order/open/transaction/INVPFN0PA" \
    -H "key: xxxxxxx"
```

```http
GET https://sim.adebmbng.com/api/order/open/transaction/INVPFN0PA
key: xxxxxxx
```

> The above command returns JSON structured like this:

```json
{
  "code": 200,
  "data": [
    {
      "id": "caa8ad5d-9d76-4396-8b95-b98534981791",
      "invoiceId": "INVNVB3TN",
      "paymentStatus": "waitingForPayment",
      "price": 2500,
      "orderType": "public-transaction",
      "merchantId": "subaga-parking",
      "isActive": true,
      "createdAt": "2021-07-07T16:24:58.709221Z",
      "updatedAt": "2021-07-07T16:24:58.709221Z",
      "qrPayment": "00020101021226660014ID.LINKAJA.WWW011893600911002411480002152004230411480010303UME51450015ID.OR.GPNQR.WWW02150000000000000000303UME520454995802ID5924Xendit Test - Do Not Pay6007Jakarta61061234566238011570ODN4RksMgs7HZ071570ODN4RksMgs7HZ53033605404250063042291"
    }
  ],
  "message": "success"
}
```

This endpoint retrieves a specific order detail.

### URL

`https://sim.adebmbng.com/api/order/open/transaction/{{invoice}}`

### URL Parameters

Parameter | Description
--------- | -----------
invoice | Invoice ID from the response of create order

## Payment callback

```shell
```

```http
```

> After we received the payment from user, we will send you this information:

```json
{
  "orderSerial": "",
  "orderStatus": "",
  "price": 9,
  "orderType": "",
  "userId": "",
  "merchantId": "",
  "isActive": true,
  "createdBy": "",
  "createdAt": "",
  "updatedBy": "",
  "updatedAt": "",
  "discount": 0,
  "ppn": 0,
  "voucherSerial": "",
  "additionalData": ""
}
```

SIM will send you this information after we received the payment. Please give us url of your payment callback

