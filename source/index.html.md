---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://circlepay.ai/#howtouse'>Sign Up for CirclePay</a>

includes:
  - errors
  - validations

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the CirclePay API
---

# Introduction

CirclePay is a platform that enables merchants to develop their projects by connecting many electronic payment gateways located in Egypt in one place with the freedom to choose the appropriate payment method.

# Integration Process

To consume CirclePay Apis you should:

* **First of all setup your account, payment gateways and payment methods:**

**1**. Add account key and token to your platform 

**2**. Create a merchant:<br/>
&nbsp;2.1. <a href="https://sandbox-openapi.circlepay.ai/swagger-ui.html#!/Merchants/createMerchantUsingPOST" target="_blank" style="text-decoration: none;">POST /merchants/create</a><br/>
&nbsp;2.2. <a href="https://sandbox-openapi.circlepay.ai/swagger-ui.html#!/Merchants/sendOTPUsingPOST" target="_blank" style="text-decoration: none;">POST /merchants/send/otp</a><br/>
&nbsp;2.3. <a href="https://sandbox-openapi.circlepay.ai/swagger-ui.html#!/Merchants/verifyMerchantUsingPOST" target="_blank" style="text-decoration: none;">POST /merchants/verify</a><br>

**3**. List Payment Gateways in the system:<br/>
&nbsp;3.1. <a href="https://sandbox-openapi.circlepay.ai/swagger-ui.html#!/Merchants/listPaymentGatewayUsingGET" target="_blank" style="text-decoration: none;">GET /payment/gateway/list</a><br>

**4**. Enable Payment Gateway for a merchant:<br/>
&nbsp;4.1. <a href="https://sandbox-openapi.circlepay.ai/swagger-ui.html#!/Merchants/enablePaymentGatewayUsingGET" target="_blank" style="text-decoration: none;">GET /merchants/payment/gateway/enable/{payment_gateway_id}</a><br>

**5**. List Payment Method in the System:<br/>
&nbsp;5.1. <a href="https://sandbox-openapi.circlepay.ai/swagger-ui.html#!/Merchants/listPaymentMethodsUsingGET" target="_blank" style="text-decoration: none;">GET /payment/methods/list/{paymentGatewayId}</a><br>

**6**. Enable Payment Method:<br/>
&nbsp;6.1. <a href="https://sandbox-openapi.circlepay.ai/swagger-ui.html#!/Merchants/enablePaymentMethodUsingGET" target="_blank" style="text-decoration: none;">GET /merchants/payment/method/enable/{payment_method_id}</a><br>

* **After setup you can create and pay invoices:**

**7**. Create invoice:<br/>
&nbsp;7.1. <a href="https://sandbox-openapi.circlepay.ai/swagger-ui.html#!/Invoice/createInvoiceUsingPOST" target="_blank" style="text-decoration: none;">POST /invoice/create</a><br>

**8**. Pay Invoice:<br/>
&nbsp;8.1. <a href="https://sandbox-openapi.circlepay.ai/swagger-ui.html#!/Invoice/payInvoiceUsingPOST" target="_blank" style="text-decoration: none;">POST /invoice/pay</a><br>

* **Now you can list transactions:**

**9**. List Transactions:<br/>
&nbsp;9.1. <a href="https://sandbox-openapi.circlepay.ai/swagger-ui.html#!/Payment/getAllPaymentsUsingPOST" target="_blank" style="text-decoration: none;">POST /payment/list</a><br>

##############################################################################

# Payment Gateway

To process online transactions, you will need both a payment gateway and a payment method. 

<span style="color: red">A payment gateway</span> is the technology that captures and transfers payment data from the customer to the acquirer. 

<span style="color: red">A payment method</span> is a way that customers pay for a product or service. 

<aside class="notice">
Each transaction requires a definition for a payment gateway and a payment method.
</aside>

<img src="https://devathon.com/wp-content/uploads/2020/02/Patement-gateway-process-Devathon.png" >

## List Payment Gateways

```shell
curl -X GET --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
     'https://circlepay.ai/apis/payment/gateway/list'
```

> The above command returns JSON structured like this:

```json
{
  "message": "Successful",
  "errorCode": 0,
  "details": "",
  "data": [
    {
      "id": "610b2c486df621209c85215a",
      "name": "MyFatoorah"
    },
    {
      "id": "613927082de6eb5dc061d516",
      "name": "Fawry"
    },
  ],
  "isError": false
}
```

Retrieves all payment gateways to the merchant.

### Parameters
No Parameters.

### Returns

Returns payment gateway list.

########################################################################

## Retrieve a Payment Gateway

```shell
curl -X GET --header 'Content-Type: application/json'
     --header 'Accept: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
     'https://circlepay.ai/apis/payment/gateway/get/{payment_gateway_ID}'
```

> The above command returns JSON structured like this:

```json
{
  "message": "Successful",
  "errorCode": 0,
  "details": "",
  "data": [
    {
      "id": "610b2c486df621209c85215a",
      "name": "MyFatoorah"
    }
  ],
  "isError": false
}
```

Retrieves a specific payment gateway.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
payment_gateway_ID |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -|Unique identifier for the payment gateway object.


### Returns
Return a payment gateway object.

<aside class="notice">
The error codes used when you fail to get specific payment gateway are <a href="#1110">1110</a> , <a href="#7111">7111</a>
</aside>

##############################################################################

# Payment Methods

<span style="color: red">A payment method</span> is a way that customers pay for a product or service. CirclePay gives customers the freedom to choose between payment methods like: cash, credit cards, prepaid cards, debit cards, or mobile payments.


MyFatoorh | Fawry | Paymob | 
--------- | ---------|----------|
Visa|Visa|Visa|
MasterCard|MasterCard|MasterCard
meeza|meeza|Kiosk Payments
Mobile Wallet|E-wallet Payment|Cash Collection
ValU|Reference Number|ValU
SADAD|ValU|Mobile Wallets
mada||SOUHOOLA
ApplePay |   |
Knet|   |
American express|   |     

<aside class="notice">
<span style="color: red">Paymob, Fawry, MyFatoorah</span> are payment gateways. Each of these payment gateways are supporting a number of payment methods. So, a payment method won't be available unless you enable the corresponding payment gateway.
</aside>

## List a Payment Methods

```shell
curl -X GET --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
     'https://circlepay.ai/apis/payment/methods/list/{paymentGatewayId}
'
```

> The above command returns JSON structured like this:

```json
{
  "message": "Successful",
  "errorCode": 0,
  "details": "",
  "data": [
    {
      "id": "61bf27e54b8bcfac495f997c",
      "name": "Wallet",
      "gateway_id": "610b2c486df621209c85215a"
    },
    {
      "id": "61c0401b253faaefc6af1993",
      "name": "Meeza",
      "gateway_id": "610b2c486df621209c85215a"
    }
  ],
  "isError": false
}
```

Retrieves all payment methods of the specific gateway.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
payment_gateway_ID |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -|Unique identifier for the payment gateway object.


### Returns

Returns a payment methods list.

<aside class="notice">
The error codes used when you fail to list payment methods are <a href="#1110">1110</a> , <a href="#7111">7111</a>
</aside>

#################################################################################

## Retrieve a Payment Method

```shell
curl -X GET --header 'Content-Type: application/json'
     --header 'Accept: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
     'https://circlepay.ai/apis/PaymentMethod/get/{payment_method_id}'
```

> The above command returns JSON structured like this:

```json
{
  "message": "Successful",
  "errorCode": 0,
  "details": "",
  "data": [
    {
      "id": "610b2c486df621209c85215c",
      "name": "AMEX",
      "gateway_id": "610b2c486df621209c85215a"
    }
  ],
  "isError": false
}
```

Retrieves a specific payment method.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
payment_method_ID |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -|Unique identifier for the payment method object.


### Returns

Returns a payment method object.

<aside class="notice">
The error codes used when you fail to get a specific payment method are <a href="#1110">1110</a> , <a href="#7113">7113</a>
</aside>

##########################################################################################

# Merchants

<span style="color: red">Merchant</span> is the person or company engaged in the business of selling products or services. For example, wholesaler or retail store owner.

## Create a Merchant

```shell
curl -X POST --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     -d first_name="Ahmed"
     -d last_name="Khaled"
     -d email="ahmedkahled@gmail.com"
     -d mobile_number="+201001414133"
	 -d Business_Name="E-commerce"
     -d Business_Address="El-maadi"
	 -d callback_url="https://bit.ly/3KXl3iA"
     'https://circlepay.ai/apis/merchants/create'
```

> The above command returns JSON structured like this:

```json
{
  "message": "Successful",
  "errorCode": 0,
  "details": "",
  "data": [
    {
      "merchant_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9eyJpZCI6Nzk3LCJpc1ZlcmlmaWVkIjpmYWxz"
    }
  ],
  "isError": false
}
```

This endpoint helps you to create new merchant.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
first_name |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The merchant's first name. |
last_name |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The merchant's last name. |
email |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The merchant's email. |
mobile_number|String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The merchant's phone number. |
Business_Name |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The business name. |
Business_Address |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The business address. |
callback_url |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| A callback URL will be invoked by the API method you're calling after it's done. |

<aside class="notice">
Password will be auto generated.
</aside>

### Returns

Returns the merchant id if the merchant created successfully. Returns an error if create parameters are invalid.

<aside class="notice">
The error codes used when you fail to create a merchant are <a href="#8110">8110</a> , <a href="#1110">1110</a> , <a href="#1112">1112</a>
</aside>

### Callback Service

You as a platform or a merchant will implement or develop this callback so you can know transaction status. The specification of this callback is made by CirclePay.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
transaction_id |String|<span style="color: red;">required</span> |&nbsp;&nbsp; &nbsp; -|Unique identifier of transaction object. |
transaction_type |Integer|<span style="color: red;">required</span> |&nbsp;&nbsp; &nbsp; -|The type of transaction (1 for payments, 2 for refund). |
transaction_status |String|<span style="color: red;">required</span> |&nbsp;&nbsp; &nbsp; -|Can be used to track the state or condition of the transaction record for example, "pending". |
payment_gateway_name |String|<span style="color: red;">required</span> |&nbsp;&nbsp; &nbsp; -|The name of payment gateway. |
payment_method_name |String|<span style="color: red;">required</span> |&nbsp;&nbsp; &nbsp; -|The name of payment method. |

### Returns

Http response will be 200 in success, else it will be other http response.

########################################################################################

## Retrieve a Merchant

```shell
curl -X GET --header 'Content-Type: application/json'
     --header 'Accept: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
     'https://circlepay.ai/apis/merchants/get'
```

> The above command returns JSON structured like this:

```json
{
  "message": "Successful",
  "errorCode": 0,
  "details": "",
  "data": [
    {
      "first_name": "ahmed",
      "last_name": "khaled",
      "email": "medy@circlepay.ai",
      "mobile_number": "+201005081863",
      "business_name": "E-commerceEgypt",
      "business_address": "El-maadi",
      "refund_policy": null,
      "shipping_policy": null,
      "status": "1",
      "merchant_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6Mjk4LCJpc1Zlcmlm"
    }
  ],
  "isError": false
}
```

Retrieves a specific merchant.

### Parameters
No Parameters.

### Returns

Returns the merchant object for a valid identifier.

#################################################################################

## Update a Merchant

```shell
curl -X PUT --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
	 -d first_name="ahmed"
	 -d last_name="khaled"
	 -d email="ahmed@gmail.com"
	 -d mobile_number="+201001215155"
	 -d business_name="ecommerce"
	 -d business_address="el-maadi"
	 -d callback_url="https://bit.ly/3KXl3iA"
     'https://circlepay.ai/apis/merchants/update'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
   [
	{
	 "first_name": "ahmed",
	 "last_name": "khaled",
	 "email": "ahmed@gmail.com",
	 "mobile_number": "+201001212155",
	 "business_name": "ecommerce",
	 "business_address": "el-maadi",
	 "refund_policy": "Refunds and exchanges, right to cancel your order",
	 "shipping_policy": "Original sales receipt must accompany returns",
	 "status": "1",
	 "merchant_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MTIsImZpcnN0Tm"
	}
   ],
   "isError" : False
}
```

Updates the specified merchant by setting the values of the parameters passed. Any parameters not provided will be left unchanged.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
first_name |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The merchant's first name. |
last_name |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The merchant's last name. |
email |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The merchant's email. |
Business_Name |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The business name. |
Business_Address |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The business address. |
callback_url |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| A callback URL will be invoked by the API method you're calling after it's done. |

### Returns

Returns the merchant object if the update succeeded. Returns an error if update parameters are invalid.

<aside class="notice">
The error codes used when you fail to update a merchant are <a href="#8116">8116</a> , <a href="#1110">1110</a> , <a href="#1112">1112</a>
</aside>

#################################################################################

## List all merchants

```shell
curl -X GET --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/merchants/list'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
   [
	{
	 "first_name": "ahmed",
	 "last_name": "khaled",
	 "email": "ahmed@gmail.com",
	 "mobile_number": "+201001212155",
	 "business_name": "ecommerce",
	 "business_address": "el-maadi",
	 "refund_policy": "Refunds and exchanges, right to cancel your order",
	 "shipping_policy": "Original sales receipt must accompany returns",
	 "status": 2
	},
	{
	 "first_name": "ibrahim",
	 "last_name": "salah",
	 "email": "ibrahim@gmail.com",
	 "mobile_number": "+201001812155",
	 "business_name": "nike",
	 "business_address": "el-maadi",
	 "refund_policy": "Refunds and exchanges, right to cancel your order",
	 "shipping_policy": "Original sales receipt must accompany returns",
	 "status": 0
	}
   ],
    "isError" : False
}
```

Retrieves all merchants.

### Parameters
No Parameters.

### Returns

Returns an array. Each entry in the array is a separate user object.This request should never return an error.

#################################################################################

## Enable gateway

```shell
curl -X GET --header 'Content-Type: application/json'
     --header 'Accept: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/merchants/payment/gateway/enable/{payment_gateway_id}'
```

> The above command returns JSON structured like this:

```json
{
  "message": "Successful",
  "errorCode": 0,
  "details": "",
  "data": [
    {
      "payment_gateway_id": "610b2c486df621209c85215b"
    }
  ],
  "isError": false
}
```

This endpoint enable specific payment gateway.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
payemnt_gateway_id |String|<span style="color: red;">required</span> |&nbsp;&nbsp; &nbsp; -| Unique identifier for the payment gateway object. |

### Returns

Returns id of enabled payment gateway.

<aside class="notice">
The error codes used when you fail to enable gateway are <a href="#7110">7110</a> , <a href="#7111">7111</a>
</aside>

####################################################################################

## Disable gateway

```shell
curl -X DELETE --header 'Content-Type: application/json'
     --header 'Accept: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/merchants/payment/gateway/disable/{payment_gateway_id}'
```

> The above command returns JSON structured like this:

```json
{
  "message": "Successful",
  "errorCode": 0,
  "details": "",
  "data": [
    {
      "payment_gateway_id": "610b2c486df621209c85215b"
    }
  ],
  "isError": false
}
```

This endpoint disable specific gateway and it's related payment methods.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
payment_gateway_ID |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -|Unique identifier for the payment gateway object.

### Returns

Returns the id of disabled payment gateway.

<aside class="notice">
The error codes used when you fail to disable gateway are <a href="#7111">7111</a> , <a href="#8117">8117</a>
</aside>

####################################################################################

## List payment gateways

```shell
curl -X GET --header 'Content-Type: application/json'
     --header 'Accept: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/merchants/payment/gateway/list'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
[
    {
      "id": "610b2c486df621209c85215a",
      "name": "MyFatoorah",
      "status": false,
      "config": {
        "id": 1,
        "apiKey": "RY6GXFd6KJKBZ98PHPLJOpmXthqkppqM3FF79cbUhv_MACpIAQ4LD3R5MemgqnA3BgVtEa-NeIItV4fFawY4XalaXuRKqcYM2MXIaYbvJnudshMQSOrQwWcvetktUzdNxQxUsoPAu6vEKlynpVkf0VYqr-9SLYSfvxKiMe6rnqGmtwMC5fcUdkfgrVznxCTr4B7dqQX09vU1_YC_gFzLxQPTP5z3Juum1JAxxv8kJ7RShclqMcWM_g2tNWzy3omqGqUflWobBBe3ebdiLtIF9pzYTqOvHsVi6k9HM6AnKR79hTQbfVICTacdhvNGKhy6HbjsaShDfI6gg4DgZ5dBjOboth9lPtqSb2OBB_3vbvUjyeOa71I5DbyEWx4Nx96luiybyvjf0ig8_yAs5HeuPz2BPPeglaila0fhW79KsKfMs9CBjKLDsJJ4EPMR6TALwefsBebOPLX6fqUvYzAuu4T8lUTAl1LlV_QeI1sc6IAc5KmkHzodRw-lQdq201a9SG6qfOH61QP_hQwS98tObIdBqQAhu2_oMNDOhYQ9kTVrSgQTrCkYTmhDI3xTp8TA09OtH7I80g-gUVf_y_zYEbJXomFVrRcPHHrt9tl1DJ9wAiaL6P9o1QrEVf7zAmLn8FedgGLdeBjOcIFjcCCQd0eLQZxTC7krBHYAXZeZbW0-RfaD",
        "signature": "",
        "merchantCode": "",
        "merchantRefNum": ""
      }
    },
    {
      "id": "610b2c486df621209c85215b",
      "name": "PayMob",
      "status": false,
      "config": {
        "CARD": {
          "iframeID": "64969",
          "integrationID": "33483"
        },
        "CASH": {
          "iframeID": "",
          "integrationID": ""
        },
        "Kiosk": {
          "iframeID": "",
          "integrationID": "107439"
        },
        "Wallet": {
          "iframeID": "",
          "integrationID": "104351"
        },
        "apiKey": "ZXlKaGJHY2lPaUpJVXpVeE1pSXNJblI1Y0NJNklrcFhWQ0o5LmV5SndjbTltYVd4bFgzQnJJam94TkRnM01Td2libUZ0WlNJNkltbHVhWFJwWVd3aUxDSmpiR0Z6Y3lJNklrMWxjbU5vWVc1MEluMC4ybzdQVld2UHJTR0MzR0xCaDF4VzZjQWhiNUVFMS1uN3lIeGVTTFNENVF5OFlHeDBQQzY3OGM5dXJnZ2R4MHZSSDR5NHdHcG01VXM4NmJ1bWNMeU4xdw==",
        "SUHOOLA": {
          "iframeID": "326757",
          "integrationID": "33483"
        }
      }
    },
    {
      "id": "613927082de6eb5dc061d516",
      "name": "Fawry",
      "status": false,
      "config": {
        "id": 4,
        "apiKey": "f19f9720-6462-466d-b9bc-4128f772bafb",
        "signature": "as",
        "merchantCode": "siYxylRjSPx5Hw/oRBKFwQ==",
        "merchantRefNum": "as"
      }
    }
  ],
  "isError" : False
}
```

This endpoint list merchant's payment gateways.

### Parameters

No Parameters.

### Returns

Returns the payment gateways list for merchant.

####################################################################################

## Enable payment method

```shell
curl -X GET --header 'Content-Type: application/json'
     --header 'Accept: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/merchants/payment/method/enable/{payment_method_ID}'
```

> The above command returns JSON structured like this:

```json
{
  "message": "Successful",
  "errorCode": 0,
  "details": "",
  "data": [
    {
      "payment_method_id": "610b2c486df621209c85215c"
    }
  ],
  "isError": false
}
```

This endpoint enable specific payment method.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
payment_method_ID |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -|Unique identifier for the payment method object.

### Returns

Returns id of enabled payment method.

<aside class="notice">
The error codes used when you fail to enable payment method are <a href="#7112">7112</a> , <a href="#7113">7113</a> , <a href="#1110">1110</a>
</aside>

#######################################################################################

## Disable payment method

```shell
curl -X DELETE --header 'Content-Type: application/json'
     --header 'Accept: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/merchants/payment/method/enable/{payment_method_ID}'
```

> The above command returns JSON structured like this:

```json
{
  "message": "Successful",
  "errorCode": 0,
  "details": "",
  "data": [
    {
      "payment_method_id": "610b2c486df621209c85215c"
    }
  ],
  "isError": false
}
```

This endpoint disable specific payment method.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
payment_method_ID |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -|Unique identifier for the payment method object.

### Returns

Returns id of the disabled payment method.

<aside class="notice">
The error code used when you fail to disable payment method is <a href="#7113">7113</a>
</aside>

#######################################################################################

## List payment methods

```shell
curl -X GET --header 'Content-Type: application/json'
     --header 'Accept: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/merchants/payment/method/list'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
      [ 
        {
          "id": "610b2c496df621209c852168",
          "name": "Visa",
          "gateway_id": "1",
          "status": true
        },
        {
          "id": "610b2c496df621209c8521we",
          "name": "MasterCard",
          "gateway_id": "1",
          "status": 0
        }
      ],
	   "isError" : False
}
```

This endpoint list allowed payment methods to the merchant.

### Parameters

No parameters.

### Returns

Returns a payment methods list of the merchant.

####################################################################################

## Send OTP

```shell
curl -X POST --header 'Content-Type: application/json'
     --header 'Accept: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
     -d merchant_mobile="+201012794709"
	 -d country_code="+20"
     'https://circlepay.ai/apis/merchants/send/otp'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
   [
    {
      "status": true
    }
   ],
   "isError" : False
}
```

This endpoint sends the OTP to validate the merchant.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
merchant_mobile |String|<span style="color: red;">required</span> |&nbsp;&nbsp; &nbsp; -| The merchant's mobile number. |
country_code |String|<span style="color: red;">required</span> |&nbsp;&nbsp; &nbsp; -| The country code for example, the country code for egypt is +20

### Returns

Returns the status (true or false).

<aside class="notice">
The error codes used when you fail to send otp to merchant are <a href="#8118">8111</a> , <a href="#8113">8113</a>
</aside>

########################################################################################

## Verify Merchant

```shell
curl -X POST --header 'Content-Type: application/json'
     --header 'Accept: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
     'https://circlepay.ai/apis/merchants/verify'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" : null,
 "isError" : False,
}
```

This endpoint allow you to verify merchant.

### Parameters

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
Merchant_mobile |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| Merchant's mobile number. |
otp |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| One-time password (OTP) systems provide a mechanism for logging on to a network or service using a unique password that can only be used once. |

### Returns

Verify merchant mobile to compelete registration.

<aside class="notice">
The error code used when you fail to verify merchant is <a href="#2111">2111</a>
</aside>

####################################################################################

# Customers

## Create a Customer

```shell
curl -X POST --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     -d First_Name="Ahmed"
     -d Last_Name="Khaled"
     -d email="ahmedkahled@gmail.com"
     -d mobile_number="+201001616166"
	 -d country="Egypt"
     -d city="cairo"
     'https://circlepay.ai/apis/customer/create'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
   [
    {  
       "customer_mobile_number": "+201001212144"
    }
   ],
    "isError" : False
}
```

This endpoint helps you to create new customer.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
First_Name |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's first name. |
Last_Name |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's last name. |
email |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's email. |
mobile_number|String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's phone number. |
country |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's country. |
governorate |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's governorate. |
city |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's city. |
address |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's address. |
apt_num |Numeric|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's apartment number. |

### Returns

Returns the customer mobile number if the customer's creation succeeded. Returns an error if parameters are invalid.

<aside class="notice">
The error codes used when you fail to create a customer are <a href="#3111">3111</a> , <a href="#1110">1110</a>
</aside>

########################################################################################

## Update a Customer

```shell
curl -X PUT --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     -d First_Name="Ahmed"
     -d Last_Name="Khaled"
     -d email="ahmedkahled@gmail.com"
     -d mobile_number="+201001717177"
	 -d country="Egypt"
     -d city="cairo"
     'https://circlepay.ai/apis/customer/update'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
   [
    {  
       "customer_mobile_number": "+201001212144"
    }
   ],
    "isError" : False
}
```

This endpoint helps you to update customer details.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
First_Name |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's first name. |
Last_Name |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's last name. |
email |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's email. |
mobile_number|String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's phone number. |
country |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's country. |
governorate |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's governorate. |
city |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's city. |
address |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's address. |
apt_num |Numeric|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -| The customer's apartment number. |

### Returns

Returns the customer mobile number if the customer's update succeeded. Returns an error if parameters are invalid.

<aside class="notice">
The error codes used when you fail to update a customer are <a href="#3110">3110</a> , <a href="#1110">1110</a>, <a href="#1117">1117</a>
</aside>

########################################################################################

## Retrieve a customer

```shell
curl -X GET --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/customer/get/{customer_mobile_number}'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
   [
    {  
       "first_name": "Ibrahim",
       "last_name": "Salah",
       "email": "ibrahim@gmail.com",
       "mobile_number": "+201001212144",
       "country": "Egypt",
       "governorate": "cairo",
       "city": "nasr",
       "address": "72 gamal st",
       "apt_num": "5"
    }
   ],
    "isError" : False
}
```

Retrieves a specific customer.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
customer_mobile_number |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -|Customer's mobile number.

### Returns

Returns the Customer object for a valid mobile number.

<aside class="notice">
The error code used when you fail to retrieve a specific customer is <a href="#3110">3110</a>
</aside>

####################################################################################

## List all customers

```shell
curl -X GET --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/customer/list'
```

> The above command returns JSON structured like this:

```json

{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
   [
    {  
       "first_name": "Ibrahim",
       "last_name": "Salah",
       "email": "ibrahim@gmail.com",
       "mobile_number": "+201001212144",
       "country": "Egypt",
       "governorate": "cairo",
       "city": "nasr",
       "address": "72 gamal st",
       "apt_num": "5"
    },
    {  
       "first_name": "Tamer",
       "last_name": "Aly",
       "email": "taly@hotmail.com",
       "mobile_number": "+20133444144",
       "country": "Egypt",
       "governorate": "alex",
       "city": "nasr",
       "address": "12 roshdy st",
       "apt_num": "35"
    }
   ],
    "isError" : False
}
```

Retrieves a list of your customers.

### Parameters

No parameters.

<aside class="notice">
List all customers using filters.
</aside>

### Returns

Returns customer list, If no more customers are available, the resulting array will be empty. This request should never return an error.

################################################################################

# Payment

## Get a payment 

```shell
curl -X GET --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/payment/get/{transactionId}'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
    [
     {
        "id": 2,
        "transaction_id": 5,
        "external_ref_id": 2,
        "init_date": 2022-02-22,
        "update_date": 2022-02-23,
        "customer_mobile": "+201101212888",
        "status": "initialized",
        "payment_link_url": "",
        "invoice_num": "CIR_INV_1643670030264",
        "value": 99.0,
        "net_fees": 1.0,
        "currency": "EGP",
        "payment_method_id": "610b2c496df621209c852162",
        "payment_method_name": "MasterCard",
        "payment_gateway_name": "MyFatoorh"
      }
    ],
	 "isError" : False
}
```

Retrieves the details of an existing payment.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
transaction_id |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -|Unique identifier for the payment object.

### Returns

Returns a payment object if a valid identifier was provided, and returns an error otherwise.

<aside class="notice">
The error code used when you fail to get payment object is <a href="#9111">9111</a>
</aside>

######################################################################################

## List all payments

```shell
curl -X GET --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/payment/list'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
    [
      {
        "id": 1,
        "transaction_id": 6,
        "external_ref_id": 3,
        "init_date": 2022-02-22,
        "update_date": 2022-02-23,
        "customer_mobile": "+201001212888",
        "status": "pending",
        "payment_link_url": "https://bit.ly/3KXl3iA",
        "invoice_num": "",
        "value": 99.0,
        "net_fees": 1.0,
        "currency": "EGP",
        "payment_method_id": "610b2c496df621209c852168",
        "payment_method_name": "Visa",
        "payment_gateway_name": "MyFatoorh"
      },
      {
        "id": 2,
        "transaction_id": 5,
        "external_ref_id": 2,
        "init_date": 2022-02-22,
        "update_date": 2022-02-23,
        "customer_mobile": "+201101212888",
        "status": "initialized",
        "payment_link_url": "",
        "invoice_num": "CIR_INV_1643670030264",
        "value": 99.0,
        "net_fees": 1.0,
        "currency": "EGP",
        "payment_method_id": "610b2c496df621209c852162",
        "payment_method_name": "MasterCard",
        "payment_gateway_name": "MyFatoorh"
      }
    ],
	 "isError" : False
}
```

Retrieves all payments.

### Parameters

No parameters

### Returns

Returns a payment list which has the details of the payment like: status, amount paid and payment method.


######################################################################################

# Refund

Allows you to refund a charge that has previously been created but not yet refunded.

## Request a refund

```shell
curl -X POST --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/refund/request'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
   [
    {
     "refund_id": "2"
    }
   ],
    "isError" : False
}
```
This endpoint helps you to request refund.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
transaction_id |Integer|<span style="color: red;">required</span> |&nbsp;&nbsp; &nbsp; -| Unique identifier for the transaction object.|


### Returns

Returns the refund id. Status in refund object will be in pending state.

<aside class="notice">
Default value of refund is equal to payment value.
</aside>

<aside class="notice">
The error code used when you fail to request refund is <a href="#9112">9112</a>
</aside>

######################################################################################

## List all refunds

```shell
curl -X POST --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/refund/list'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
    [
     {
        "refund_id": "1",
        "external_ref_id": 2,
        "init_date": 2022-02-22,
        "update_date": 2022-02-23,
        "value": 40.0,
        "transaction_id": 3,
        "status": "pending"
     },
     {
        "refund_id": "2",
        "external_ref_id": 3,
        "init_date": 2022-02-22,
        "update_date": 2022-02-23,
        "value": 90.0,
        "transaction_id": 3,
        "status": "paid"
     }
    ],
	"isError" : False
}
```
List refund objects.

### Parameters

No parameters

### Returns

Returns refund object list. If no more refunds are available, the resulting array will be empty.

#######################################################################################

## Get refund 

```shell
curl -X GET --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/refund/get/{refundId}'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
   [
    {
     "refund_id": "2",
     "external_ref_id": 3,
     "init_date": 2022-02-22,
     "update_date": 2022-02-23,
     "value": 90.0,
     "transaction_id": 3,
     "status": "paid"
    }
   ],
    "isError" : False
}
```
Retrieves the refund object.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
refund_id |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -|Unique identifier for the refund object.

### Returns

Returns refund object if a valid refund id is provided.

<aside class="notice">
The error code used when you fail to get refund status is <a href="#9111">9111</a>
</aside>

##############################################################################

# Invoice

An invoice is an itemized list that records the products or services you provided to your customers, the total amount due, and a method for them to pay you for those items or services. Invoices can be paid in one payment or in installments.

## Create an invoice

```shell
curl -X POST --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
     --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     -d "customer[email]"="ahmed@gmail.com"
     -d "customer[city]"="mansoura"
     -d "invoice[invoice_number]"=55
     'https://circlepay.ai/apis/invoice/create'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
   [
    {
     "invoice_number": "CIR_INV_16436703344261",
     "invoice_url" : "complete checkout url"
    }
   ],
    "isError" : False
}
```
This endpoint creates an invoice for a given customer. The invoice created will be in "pending" status.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
invoice |Object|<span style="color: red;">required</span> |&nbsp;&nbsp; &nbsp; -|The details of the invoice object. |

The table below contains invoice object attributes.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
invoice_number |String|<span style="color: lightblue;">optional</span> |&nbsp;&nbsp; &nbsp; -|The invoice number. |
items |Array|<span style="color: red;">required</span> |&nbsp;&nbsp; &nbsp; -|Array of item object which has the details of items in invoice for example: name,description,quantity and price. |
customer_mobile |String|<span style="color: red;">required</span> |&nbsp;&nbsp; &nbsp; -|The customer mobile number. |
status |Integer|<span style="color: lightblue;">optional</span> |&nbsp;&nbsp; &nbsp; -|The status of invoice for example: 0 means Due, 1 means Over_Due, 2 means Paid, 3 means  Deactivated. |
create_date |Date|<span style="color: lightblue;">optional</span> |&nbsp;&nbsp; &nbsp; -|The creation date of invoice. |
due_date |Date|<span style="color: red;">required</span> |&nbsp;&nbsp; &nbsp; -|The due date of invoice which is the latest payment can be made on an invoice or debt before it's considered overdue. |
pref_payment_method |String|<span style="color: lightblue;">optional</span> |&nbsp;&nbsp; &nbsp; -|The preferred payment method and it's related payment gateway for example: CARD/PayMob means method_name/gateway_name. |
shipping_fees |Float|<span style="color: lightblue;">optional</span> |&nbsp;&nbsp; &nbsp; -|The shipping fees on invoice's items. |
discount_value |Float|<span style="color: lightblue;">optional</span> |&nbsp;&nbsp; &nbsp; -|The discount value on total cost of items. |
discount_type |String|<span style="color: lightblue;">optional</span> |&nbsp;&nbsp; &nbsp; -|The discount type, it can be value or percent. |
discount_value_calculated |Float|<span style="color: lightblue;">optional</span> |&nbsp;&nbsp; &nbsp; -|The discount value calculated if the discount type is percent. |
tax |Float|<span style="color: lightblue;">optional</span> |&nbsp;&nbsp; &nbsp; -|The tax in percent. |
tax_value |Float|<span style="color: lightblue;">optional</span> |&nbsp;&nbsp; &nbsp; -|The calculated tax amount. |
shipping_policy |String|<span style="color: lightblue;">optional</span> |&nbsp;&nbsp; &nbsp; -|The shipping policy contains potential delays due to a high volume of orders or postal service problems that are outside of your control, Domestic Shipping Rates and Estimates, local delivery policy and international shipping policy. |
return_policy |String|<span style="color: lightblue;">optional</span> |&nbsp;&nbsp; &nbsp; -|The rules a retailer or merchant creates to manage how customers return and exchange unwanted merchandise they purchased for example, Amazon.com and most sellers on Amazon.com offer returns for items within 30 days of receipt of shipment. |
extra_notes |String|<span style="color: lightblue;">optional</span> |&nbsp;&nbsp; &nbsp; -|The notes or comments to make invoice more clear. |


### Returns

Returns an invoice object that has been created. Returns error if the customer ID provided is invalid.

<aside class="notice">
The error codes used when you fail to create an invoice are <a href="#5101">5101</a> , <a href="#1110">1110</a>
</aside>

####################################################################################

## Retrieve an invoice

```shell
curl -X GET --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/invoice/get/{invoice_number}'
```

> The above command returns JSON structured like this:

```json
{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
   [
    {
     "invoice_number": "CIR_INV_1643670030261",
     "items": [{"name":"shoe","description":"","quantity": 4,"price":90.0}],
     "customer_mobile": "+201001212333",
     "status": 1,
     "create_date": 2022-12-20,
     "due_date": 2022-12-25,
     "pref_payment_method": "CARD/PayMob",
     "shipping_fees": 4.0,
     "discount_value": 11.0,
     "discount_type": "percent",
     "discount_value_calculated": 9.9,
     "tax": 10.0,
     "tax_value": 9.0,
     "shipping_policy": "shipping options you offer (overnight, standard, air mail, international)",
     "return_policy": "Amazon.com and most sellers on Amazon.com offer returns for items within 30 days of receipt of shipment.",
     "extra_notes":
    }
 ],
 "isError" : False
}
```
Retrieves the invoice with the given invoice number.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
invoice_number |String|<span style="color: red;">required</span>|&nbsp;&nbsp; &nbsp; -|The invoice number.

### Returns

Returns an invoice object if a valid invoice number was provided. Returns an error otherwise.

<aside class="notice">
The error code used when you fail to retrieve an invoice is <a href="#5111">5111</a>
</aside>

####################################################################################

## list invoices

```shell
curl -X GET --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/invoice/list/{customer_mobile}'
```

> The above command returns JSON structured like this:

```json
List the invoices

{
 "message" : "Successful",
 "errorCode" : 0,
 "details" : "",
 "data" :
   [
    {
     "invoice_number": "CIR_INV_1643670030261",
     "items": [{"name":"shoe","description":"","quantity": 4,"price":90.0}],
     "customer_mobile": "+201001212333",
     "status": 1,
     "create_date": 2022-12-20,
     "due_date": 2022-12-25,
     "pref_payment_method": "CARD/PayMob",
     "shipping_fees": 4.0,
     "discount_value": 11.0,
     "discount_type": "percent",
     "discount_value_calculated": 9.9,
     "tax": 10.0,
     "tax_value": 9.0,
     "shipping_policy": "shipping options you offer (overnight, standard, air mail, international)",
     "return_policy": "Amazon.com and most sellers on Amazon.com offer returns for items within 30 days of receipt of shipment.",
     "extra_notes":
    }
  ],
   "isError" : False
}
```
This endpoint list invoices for a given customer.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
customer_mobile |String|<span style="color: lightblue;">optional</span>|&nbsp;&nbsp; &nbsp; -|Customer's mobile number.
Filter |String|<span style="color: lightblue;">optional</span>|&nbsp;&nbsp; &nbsp; -|invoices list returned based on this filter object.

### Returns

Returns list of invoice objects.

########################################################################################

## Delete an invoice

```shell
curl -X DELETE --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
     'https://circlepay.ai/apis/invoice/delete/{invoice_number}'
```

> The above command returns JSON structured like this:

```json
{
  "message": "Successful",
  "errorCode": 0,
  "details": "",
  "data": [
    {
      "invoice_number": "CIR_INV_1645465416865"
    }
  ],
  "isError": false
}
```
Delete an invoice ONLY IF the invoice has no transactions.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
invoice_num |String|<span style="color: red;">required</span> |&nbsp;&nbsp; &nbsp; -| Invoice's number.|

### Returns

Returns the deleted invoice number.

<aside class="notice">
The error code used when you fail to delete an invoice is <a href="#5111">5111</a>
</aside>

####################################################################################

## Pay an invoice

```shell
curl -X POST --header 'Accept: application/json'
     --header 'Content-Type: application/json'
     --header 'account_key: de40f1f2-98a8-32bd-bc2c-96280c7b4b6b'
	 --header 'account_token: Bearer eyJhbGciOiJkaXIiLCJlbmMiOiJBMTI4Q0J'
	 --header 'merchant_token: Bearer 402880824ff933a4014ff9345d7c0002'
	 -d invoice_number="CIR_INV_16436702430261"
     'https://circlepay.ai/apis/invoice/pay'
```

> The above command returns JSON structured like this:

```json
{
  "message": "Successful",
  "errorCode": 0,
  "details": null,
  "data": [
    {
      "transaction_id": "1645895596175",
      "invoice_url": "https://staging.circlepay.ai/payment/make-payment/ddb411b2b2ecca4508ec1645465416853/eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJxdWVyeVBhcmFtcyI6Ij9zdGVwPTMmT1BFeHRlcm5hbD0xNjQ1ODk1NTk2MTc1JnNlbGVjdGVkUGF5bWVudE1ldGhvZD1DQVJEJnNlbGVjdGVkUGF5bWVudEdhdGV3YXk9UGF5TW9iJnNvdXJjZT1leHRlcm5hbCIsImlhdCI6MTY0NTg5NTU5Nn0.c4526On6Nk7KgaIRaarolHnC5GXwvPC8ISnXbTLu6nI"
    }
  ],
  "isError": false
}
```

Pay an invoice.

Parameter|Type|Required|Default|Description|
---------|--------|---------|--------|-----|
invoice_number |String|<span style="color: red;">required</span> |&nbsp;&nbsp; &nbsp; -| Invoice's number.|
customer_mobile |String|<span style="color: lightblue;">optional</span> |&nbsp;&nbsp; &nbsp; -| The customer mobile number.|
payment_method_id |String|<span style="color: lightblue;">optional</span> |&nbsp;&nbsp; &nbsp; -| The unique identifier of payment method.|

<aside class="notice">
Payment method and payment gateway must be together, can't send only one.
</aside>

<aside class="notice">
The error codes used when you fail to pay an invoice are <a href="#5111">5111</a> , <a href="#5114">5114</a> , <a href="#7113">7113</a> , <a href="#7111">7111</a> 
</aside>

### Returns

Pay the invoice if a valid invoice number was provided. Returns an error otherwise.

####################################################################################