---
term: BIP119
---

Introduces a new opcode named `OP_CHECKTEMPLATEVERIFY` (CTV). CTV would allow for the creation of non-recursive covenants in transactions, in order to impose specific conditions on how a given coin can be spent, including in future transactions. More concretely, it would enable the definition of conditions on the `scriptPubKey` of a transaction's outputs based on the `scriptPubKey` of the UTXO spent as input. CheckTemplateVerify is designed to be simple and without dynamic state. Its implementation aims to extend Bitcoin's scripting capabilities to facilitate various applications such as transaction congestion control, the creation of non-interactive payment channels, DLCs, payment pools... This new opcode would be introduced as a replacement for `OP_NOP4`. This change would imply a soft fork.
