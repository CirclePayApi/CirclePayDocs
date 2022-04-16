# Errors

Error code is a numeric or alphanumeric code that helps you to determine the nature of an error and why it occurred. The CirclePay API uses the following error codes:

## General

Error&nbsp;Code | Error Text | Error Message
--------- | ----------|------------
<span id="1110">1110</span>   | Data missing | {ATTRIBUTE} is missing.
<span id="1111">1111</span>   | Invalid request structure | The object structure sent is invalid. If you follow the documentation and still facing the same issue, please contact the support team.
<span id="1112">1112</span>   | Invalid request data | The {ATTRIBUTE} has invalid value.
<span id="1114">1114</span>   | Field length error | The field {ATTRIBUTE} length must be less than {ATTRIBUTE} and more than {ATTRIBUTE}.
<span id="1115">1115</span>   | Invalid date format | The date format is invalid. Please refer to the documentation for the right date format.
<span id="1116">1116</span>   | Invalid email | The email format is invalid.
<span id="1117">1117</span>   | Invalid phone number format | The phone number format is invalid (International format is required).

## Authentication

Error&nbsp;Code | Error Text | Error Message
--------- | ----------|------------
<span id="2110">2110</span>   | Merchant key is incorrect | The merchant key might be incorrect or doesn't exist.
<span id="2111">2111</span>   | Invalid verification code | The provided verification code is incorrect.
<span id="2112">2112</span>   | Password is invalid | The provided password isn't following the password requirements.
<span id="2113">2113</span>   | Password isnot matching | The password entered is not matching the first password field.

## Customer

Error&nbsp;Code | Error Text | Error Message
--------- | ----------|------------
<span id="3110">3110</span>   | Cannot find the customer | The customer phone number might be incorrect or doesn't exist.
<span id="3111">3111</span>   | Customer already exist | Another customer exists with the same phone number.

## Payment Links

Error&nbsp;Code | Error Text | Error Message
--------- | ----------|------------
<span id="4101">4101</span>   | Cannot create Payment link | Cannot create a payment link for an unknown reason. Please contact CirclePay support team.
<span id="4111">4111</span>   | Cannot find the payment link | The Payment link URL might be incorrect or doesn't exist.
<span id="4112">4112</span>   | Expire date cannot be in the past | Cannot add a past date for a payment link {ATTRIBUTE}.
<span id="4115">4115</span>   | Payment link is expired | Cannot pay an expired payment link.
<span id="4211">4211</span>   | Cannot find form | The form id might be incorrect or doesn't exist.
<span id="4212">4212</span>   | Cannot update the form | Cannot update the form as it might include responses.
<span id="4311">4311</span>   | Cannot find coupon | The coupon code might be incorrect or doesn't exist.
<span id="4312">4312</span>   | Cannot update the coupon | Cannot update the coupon as it might be linked to payments.
<span id="4313">4313</span>   | Cannot delete the coupon | Cannot delete the coupon as it might be linked to payments.

## Invoices

Error&nbsp;Code | Error Text | Error Message
--------- | ----------|------------
<span id="5101">5101</span>   | Cannot create an invoice | Cannot create an invoice for an unknown reason. Please contact CirlepPay support team.
<span id="5111">5111</span>   | Cannot find the invoice | The invoice number might be incorrect or doesn't exist.
<span id="5112">5112</span>   | Cannot create the invoice | Cannot add a past date for an invoice {ATTRIBUTE}.
<span id="5113">5113</span>   | Cannot delete the invoice | Cannot delete the invoice as it might be linked to other fields.
<span id="5114">5114</span>   | Customer phone number is incorrect | Cannot change the customer phone attached to the invoice.


## Payment gateways

Error&nbsp;Code | Error Text | Error Message
--------- | ----------|------------
<span id="7110">7110</span>   | Cannot enable the payment gateway | Cannot enable the payment gate for an unknow reason. Please contact CirclePay support team.
<span id="7111">7111</span>   | Cannot find the payment gateway | The payment gateway ID might be incorrect or doesn't exist.
<span id="7112">7112</span>   | Cannot enable the payment method | Cannot enable the payment method for an unknow reason. Please contact CirclePay support team.
<span id="7113">7113</span>   | Cannot find the payment method | The payment method ID might be incorrect or doesn't exist.
<span id="7114">7114</span>   | Cannot set the payment method fee | Cannot set the payment method fee. Please contact the support team.


## Merchant

Error&nbsp;Code | Error Text | Error Message
--------- | ----------|------------
<span id="8110">8110</span>   | Cannot create a merchant | The merchant phone number is being used by another account.
<span id="8111">8111</span>   | Cannot find the merchant | The merchant key might be incorrect or doesn't exist.
<span id="8112">8112</span>   | Config file has incorrect structure | The config JSON file structure is incorrect.
<span id="8113">8113</span>   | Cannot send OTP | The service failed to send an OTP to the merchant.
<span id="8114">8114</span>   | Invalid Callback URL | Callback URL structure is invalid.
<span id="8115">8115</span>   | Merchant account is inactive | Cannot do this operation as the account is inactive.
<span id="8116">8116</span>   | Cannot update the merchant phone number | Cannot update the merchant phone number as it's being used by another account.


## Transactions

Error&nbsp;Code | Error Text | Error Message
--------- | ----------|------------
<span id="9110">9110</span>   | Transaction data request is missing | The transaction data request is missing {ATTRIBUTE}.
<span id="9111">9111</span>   | Cannot find the transaction | The transaction ID might be incorrect or doesn't exist.
<span id="9112">9112</span>   | Refund request rejected | The payment gateway rejected the refund request for the following reason {ATTRIBUTE}.









