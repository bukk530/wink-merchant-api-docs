---
title: Wink Merchant API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://dashboard.getwinkpayments.com'>Wink Merchant Dashboard</a>

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Wink Merchants API
---

# Introduction

Welcome to the Wink Merchant API! You can use our API to access your merchant data.

# Authentication

> To authorize, use this code:

```shell
# With curl, you can just pass the correct header with each request
curl "https://api.getwinkpayments.com/v1/" \
  -H "X-Wink-MerchantId: merchant-[...]"
  -H "X-Wink-SecretKey: sk-[env]-[...]"
```

> Make sure to use your Merchant Id and Secret Key.

Wink Merchant API uses keys to authorize each request. You can get your API keys on your [Wink Merchant Dashboard](http://dashboard.getwinkpayments.com).

You must include your API keys in all API requests to the server using two Wink specific headers that looks like the following:

`X-Wink-MerchantId: merchant-[...]`

`X-Wink-SecretKey: sk-[env]-[...]`

<aside class="notice">
You must replace <code>merchantId</code> and <code>secret key</code> with the values provided in your Wink Merchant Dashboard.
</aside>

# Environments

We provide two separate environment:
* Sandbox
* Production

You should always first test your implementation on our Sandbox environment before going live.

## Endpoints

|Url|Environment|
---|---|
|https://api-sandbox.getwinkpayments.com|Sandbox|

# Checkout

## Redirect your customer to Wink Checkout

```html
<html>
  <head>
    <title>Buy cool new product</title>
  </head>
  <body>
    <form action="/create-checkout-session" method="POST">
      <button type="submit">Checkout</button>
    </form>
  </body>
</html>
```

> The above will send a POST request to your server, use the below code in your backend to redirect users to Wink Checkout


Add a checkout button to your website that calls a server-side endpoint to create a Checkout Session.

A Checkout Session is the programmatic representation of what your customer sees when they’re redirected to the payment form. You can configure it with options such as:

* Line Items
* Taxes
* Discounts
* Total Price
* Currency

<aside class="notice">
Your customers will be charged the Total Price you specify in your request. All other items are just displayed in the checkout page as a reference for the customer. Please make sure all numbers adds up!
</aside>

The currency you specify in your checkout request must be either your Merchant's currency or Bitcoins.
If you decide to use another currency you will incur in exchange fees.

You also need to specify:

* A Success Url, a page on your website to redirect your customer after they complete the payment.
* A Cancel Url, a page on your website to redirect your customer if they click your logo in Checkout.

<aside class="notice">
Checkout Sessions expire 1 hour after creation
</aside>


## Testing

> Test your endpoint by starting your web server (e.g. localhost:4242) and running the following command:


```json
curl -X POST -is "http://localhost:4242/create-checkout-session" -d ""
```

> The above command should return the following:

```json
HTTP/1.1 303 See Other
Location: https://checkout.getwinkpayments.com/pay/...
```

You should now have a working checkout button that redirects your customer to Wink Checkout.

* Click the checkout button.
* You’re redirected to the Wink Checkout payment page.

If your integration isn’t working:

* Open the Network tab in your browser’s developer tools.
* Click the checkout button and see if an XHR request is made to your server-side endpoint (POST /create-checkout-session).
* Verify the request is returning a 200 status.
* Use console.log(session) inside your button click listener to confirm the correct data is returned.

## Show a success page

```html
<html>
  <head><title>Thanks for your order!</title></head>
  <body>
    <h1>Thanks for your order!</h1>
    <p>
      We appreciate your business!
      If you have any questions, please email
      <a href="mailto:orders@example.com">orders@example.com</a>.
    </p>
  </body>
</html>
```

It’s important for your customer to see a success page after they successfully submit the payment form. This success page is hosted on your site.



# Customers

## List all customers

### HTTP Endpoint

`GET /v1/customers`

## Get a customer

### HTTP Endpoint

`GET /v1/customers/{customerId}'


# Transactions

## List all transactions

### HTTP Endpoint

`GET /v1/transactions`

## Get a transaction


### HTTP Endpoint

`GET /v1/transactions/{transactionId}`

# Refunds

## Issue a Refund


### HTTP Endpoint

`POST /v1/refunds`


## Get all refunds


### HTTP Endpoint

`GET /v1/refunds`


## Get a refund

`GET /v1/refunds/{refundId}`

