lightning-decodepay -- Command for decoding a bolt11 string (low-level)
=======================================================================

SYNOPSIS
--------

**decodepay** *bolt11* [*description*]

DESCRIPTION
-----------

The **decodepay** RPC command checks and parses a *bolt11* string as
specified by the BOLT 11 specification.

RETURN VALUE
------------

[comment]: # (GENERATE-FROM-SCHEMA-START)
On success, an object is returned, containing:

- **currency** (string): the BIP173 name for the currency
- **created\_at** (u64): the UNIX-style timestamp of the invoice
- **expiry** (u64): the number of seconds this is valid after *timestamp*
- **payee** (pubkey): the public key of the recipient
- **payment\_hash** (hex): the hash of the *payment_preimage* (always 64 characters)
- **signature** (signature): signature of the *payee* on this invoice
- **min\_final\_cltv\_expiry** (u32): the minimum CLTV delay for the final node
- **amount\_msat** (msat, optional): Amount the invoice asked for
- **description** (string, optional): the description of the purpose of the purchase
- **description\_hash** (hex, optional): the hash of the description, in place of *description* (always 64 characters)
- **payment\_secret** (hex, optional): the secret to hand to the payee node (always 64 characters)
- **features** (hex, optional): the features bitmap for this invoice
- **payment\_metadata** (hex, optional): the payment_metadata to put in the payment
- **fallbacks** (array of objects, optional): onchain addresses:
  - **type** (string): the address type (if known) (one of "P2PKH", "P2SH", "P2WPKH", "P2WSH")
  - **hex** (hex): Raw encoded address
  - **addr** (string, optional): the address in appropriate format for *type*
- **routes** (array of arrays, optional): Route hints to the *payee*:
  - hops in the route:
    - **pubkey** (pubkey): the public key of the node
    - **short\_channel\_id** (short\_channel\_id): a channel to the next peer
    - **fee\_base\_msat** (msat): the base fee for payments
    - **fee\_proportional\_millionths** (u32): the parts-per-million fee for payments
    - **cltv\_expiry\_delta** (u32): the CLTV delta across this hop
- **extra** (array of objects, optional): Any extra fields we didn't know how to parse:
  - **tag** (string): The bech32 letter which identifies this field (always 1 characters)
  - **data** (string): The bech32 data for this field

[comment]: # (GENERATE-FROM-SCHEMA-END)

Technically, the *description* field is optional if a
*description\_hash* field is given, but in this case **decodepay** will
only succeed if the optional *description* field is passed and matches
the *description\_hash*. In practice, these are currently unused.

AUTHOR
------

Rusty Russell <<rusty@rustcorp.com.au>> is mainly responsible.

SEE ALSO
--------

lightning-pay(7), lightning-getroute(7), lightning-sendpay(7).

[BOLT
\#11](https://github.com/lightning/bolts/blob/master/11-payment-encoding.md).

RESOURCES
---------

Main web site: <https://github.com/ElementsProject/lightning>

[comment]: # ( SHA256STAMP:c98fd8cac46b5446ff2d01ede6b082f64a83d4b5745d06e410af3e1dd91be8e2)
