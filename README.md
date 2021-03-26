# DieselBank - Backend Challenge

A digital wallet is an app that allows you to perform cash-in and cash-out operations using a lot of different methods. For instance, BinoBank's digital wallet allows you to perform cash-ins by receiving a PIX or by paying a deposit-boleto, and to perform cash-outs by paying bills, paying with your card or transferring money by PIX, TED. These methods are provided by different payment-providers and the users's account has only a single balance and single statement containing all cash-ins and cash-outs!

As a member of BinoBank's Software Engineering team, you were assigned the task to implement an algorithm that will be triggered by webhooks when a payment-provider sends a new cash-in or cash-out request. The main goal is to assert that the balance and statement of any user is always correct and up-to-date!

### Premises and requirements:
- Every payment-provider has the capability of sending cash-ins and cash-outs requests of any type.
- Cash-ins and Cash-outs requests can happen at the same time. Therefore, some concurrency problems will arise. How will your algorithm deal with these problems?
- There is only one user.
- There are only 2 payment-providers.
- The balance can't get negative. So, there might be transactions that can't be authorized by your algorithm.
- The balance and statement of any user is always correct and up-to-date!

**The indicator of success of your algorithm will be the result of the unit tests that you must create to show us that it meets the requirements.**

This is the model of a transaction entry (use this model for the providers and BinoBank statements) :

```json
[
  {
    "transaction-id": "{{UUID}}",
    "payment-provider-id": "{{UUID}}",
    "description": "CASH{{IN|OUT}} VIA {{TYPE}}",
    "transaction-type": "PIX|CARD",
    "entry-date": "yyyy-MM-dd'T'HH:mm:ss",
    "amount": 1000,
    "type": "CREDIT|DEBIT" // obs: CARD transactions are only DEBIT
  }
]
```

This is the model of a webhook cashin/cashout request from a payment-provider:

```json
{
    "id": "{{UUID}}",
    "description": "CASH{{IN|OUT}} VIA {{TYPE}}",
    "transaction-type": "PIX|CARD",
    "entry-date": "yyyy-MM-dd'T'HH:mm:ss",
    "amount": 1000,
    "type": "CREDIT|DEBIT" // obs: CARD transactions are only DEBIT
}
```

This is the model of the user (shared resource):

```json
{
  "balance": 0
}
```

## Obs:
- You can use any language that support multi-threading. Feel free to modularize your code, choose any design pattern you prefer.
- Implement any unit tests you deem necessary, but assert that no statement entries will be duplicated and the balance will still be the correct one even with the concurrency access/writing, of multiple threads (webhook handlers) executing the algorithm, on BinoBank's statement/balance.
- Create a repository and share with us when you are done.
- Provide instructions to setup and run your project unit tests locally in a READ-ME file.
- Good coding! Have fun and show us what you got! :)
