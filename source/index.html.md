---
title: Transit API

# language_tabs: # must be one of https://git.io/vQNgJ
#  - shell

toc_footers:
  - <a href='https://services.transitwarehouse.com'>Transit Customer Zone</a>

includes:
  - products
  - orders
  - inventory
  - pricing
  - errors

search: true
---

# Introduction

Welcome to the **Transit API**.

You can use our API to access product information, submit new orders and view your order status in our database.

You can view code examples in the dark area to the right. Any language able to make HTTP calls will work. The examples use shell scripting curl commands.

**Please use the newest available APIs for all new implementations**

# Authentication

Transit uses API authentication tokens to allow access to the API. You can register a new Transit API auth token by communicating with your sales representative.

An API auth token is linked to a Transit Customer Zone account.

The linked Transit Customer Zone account defines the Transit warehouse and default ship-to location used by the API.

Transit expects for the API auth token to be included in all API requests to the server in a header that looks like the following:

`Authorization: Basic YourAuthTokenBase64`

<aside class="notice">
You must replace <code>YourAuthTokenBase64</code> with your API auth token, <a href="https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/btoa">Base64</a> encoded.
</aside>

The GET APIs are browser explorable: the browser will ask for the credentials. Enter the auth token in the username field and leave the password field empty.

# Test Environment

A simple sandbox feature is available to facilitate new integrations.
A special auth token `TEST` can be used with all endpoints. When you use this auth token, you will receive fake data in the HTTP response. This fake data is in the same format and encoding than real data.
