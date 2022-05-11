---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://circlepay.ai/#howtouse'>Sign Up for CirclePay</a>

includes:

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the CirclePay API
---

# Introduction

This documentation helps you to make An API integration between CirclePay and your platform, via CirclePay's Open APIs. Also it shows the dependencies which you should consider to complete integration process. 

You can use the CirclePay API in test mode(SandBox), which doesn't affect your live data. The account key and token you use to authenticate the request determines whether the request is live mode or test mode(SandBox).

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