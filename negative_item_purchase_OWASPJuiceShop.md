# Negatve Quantity Manipulation Leads to Unlimited Wallet Credit

## Target
OWASP Juice Shop

## Severity
High

## Description
The application allows users to manipulate item quantities to negative values, creating transaction with negative totals. This allows attackers to generate unlimited credit and perform free purchases on the store

## Steps to reproduce
1. Intercept HTTP traffic with a proxy tool such as Burp Suite
2. Add any item to basket
3. Send the intercepted POST request to repeater
4. Change `productID` to a different valid product ID to avoid duplicate item rest
5. Set the `quantity` parameter to a negative ammount
6. Forward the modified request to browser
7. Procceed to checkout using wallet balance as payment method
8. Finish the payment and watch the wallet balance increase

##Proof of concept (PoC)
POST /api/BasketItems/ HTTP/1.1
Host: 127.0.0.1:3000
Content-Type: application/json;

{
  "ProductId":13,
  "BasketId":"6",
  "quantity":-900
}

## Impact
Allows attackers to manipulate the `quantity` parameter to a negative value, resulting in negative transaction totals that, when processed, increase the attacker's wallet balance. This allows unlimited generation of in-appcurrency, total bypass of payment methods and free purchase of products

## Recommendation
Reject requests with zero or negative values for item quantities. Validate transaction ammounts before processing payments. Implement server-side validation on all numeric inputs
