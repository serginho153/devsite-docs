---
sites_supported:
    - mla
    - mlb
    - mlm
    - mco
    - mlc
    - mpe
    - mlu
    - global
---
# Test the integration

Before going into production, it is very important to test the payments flow, checking whether the configurations you made at the preference level are effectively reflected in the checkout.

You should check if:

+ The information about the product or service to be paid is correct.
+ If you recognize the customer’s account to send the email.
+ It offers the payment methods you wish.
+ The payment experience is adequate and the payment result is reported.

## How to test my integration

**Test users allow you to test your integration** by generating payment flows in an exact copy of your integration.

User types | Description
------------ | -------------
Seller | It is the test account you use to **configure the application and credentials for collection.**
Buyer | It is the test account you use to **test the purchase process.**<br/>

## How to create users
To perform the tests **it is necessary that you have at least two users:** a buyer and a seller.

Execute the following curl to generate a test user:

### Request

```curl
curl -X POST \
-H "Content-Type: application/json" \
"https://api.mercadopago.com/users/test_user?access_token=PROD_ACCESS_TOKEN" \
-d '{"site_id":"[FAKER][GLOBALIZE][UPPER_SITE_ID]"}'
```

### Response

```json
{
    "id": 123456,
    "nickname": "TT123456",
    "password": "qatest123456",
    "site_status": "active",
    "email": "test_user_123456@testuser.com"
}
```

>WARNING
>
>Important
>
> * You can generate up to 10 test user accounts simultaneously. Therefore, we recommend you _save each email and password._
> * Test users expire after 60 days without activity in Mercado Pago.
> * To make test payments we recommend using low amounts.
> * Both buyer and seller must be test users.
> * Use test cards, since it is not possible to withdraw money.


### To test the integration, follow the steps below:

1. Configure the [Public Key]([FAKER][CREDENTIALS][URL]) in your application.
2. Create the preference on your server with the [Access Token]([FAKER][CREDENTIALS][URL]).
3. Complete the form, entering the digits of a test card. On the expiration date you must enter any date after the current date and a 3-or 4-digit security code, depending on the card.
4. To **test different payment results,** complete the information you want in the name of the cardholder:

- APRO: Payment approved.
- CONT: Payment pending.
- OTHE: Rejected by general error.
- CALL: Rejected with validation to authorize.
- FUND: Rejected for insufficient amount.
- SECU: Rejected by invalid security code.
- EXPI: Rejected due to problem with expiration date.
- FORM: Rejected by error in the form.

## Test Cards

Use these test cards to test the different payment results.

Card | Number | CVV | Expiration Date
------------ | ------------- | ------------- | -------------
Mastercard | 5031 7557 3453 0604 | 123 | 11/25
Visa | 4170 0688 1010 8020 | 123 | 11/25
American Express | 3711 8030 3257 522 | 1234 | 11/25

You can also [use test credit cards from local payment methods in each country](https://www.mercadopago.com.ar/developers/en/guides/localization/local-cards).