---
weight: 1
title: GET /v0/transactions/:id
---

# GET `/v0/transactions/:id`

Fetching the transaction lifecycle associated with the provided parameter `:id`.


## Usage

{{< exampleRequest id="search-transactions" url="https://mainnet.eos.dfuse.io/v0/transactions/1d5f57e9392d045ef4d1d19e6976803f06741e11089855b94efcdb42a1a41253" >}}

This method returns transaction information regardless of the actual lifecycle
state be it deferred, executed, failed or cancelled. This means that deferred
transactions are handled by this method, via a transaction with a `delay_sec`
argument pushed to the chain or created by a smart contract.

Refers to the [TransactionLifecycle]({{< ref "../types/TransactionLifecycle" >}}) to have a better
overview of lifecycle related properties that are available in the response.

#### Input parameters

{{< method-list-item name="id" type="String" required="true" >}}
  Contract account targeted by the action.
{{< /method-list-item >}}

#### Response

Here is a sample response, for transaction id `1d5f57e9392d045ef4d1d19e6976803f06741e11089855b94efcdb42a1a41253` on EOS Mainnet:

{{< tabs "fetch-transaction-example" >}}
{{< tab lang="json" >}}
{
  "transaction_status": "executed",
  "id": "1d5f57e9392d045ef4d1d19e6976803f06741e11089855b94efcdb42a1a41253",
  "transaction": {
    "expiration": "2019-04-16T14:36:11",
    ...,
    "actions": [
      {
        "account": "eosio.token",
        "name": "transafer",
        ...,
      }
    ],
  },
  "execution_trace": {
    "id": "1d5f57e9392d045ef4d1d19e6976803f06741e11089855b94efcdb42a1a41253",
    ...,
    "receipt": {
      "status": "executed",
      "cpu_usage_us": 1191,
      "net_usage_words": 12
    },
    "elapsed": 85570,
    "net_usage": 96,
    "scheduled": false,
    "action_traces": [
      {
        "receipt": {
          "receiver": "eosio.token",
          ...,
        },
        ...,
        "inline_traces": [
          ...,
        ]
      }
    ]
  }
}
{{< /tab >}}
{{< /tabs >}}

Returns a [TransactionLifecycle]({{< ref "../types/TransactionLifecycle" >}}).