|Corda Network|[Document history]({{ site.github.repository_url }}/blame/master/{{page.path}})|

Choosing the node's X500 name
=============================

Any node on Corda Network must have a Distinguished Name (DN) or X500 name in its [participation certificate](https://docs.corda.net/corda-network/index.html#identity-service). This must, at minimum, have 4 fields included (Organisation (O), Locality (L), Country (C), Organisation Unit (OU)). It may include up to 6 fields (optional 2 additional fields are: State (S), and Common Name(CN)). These 6 fields are explained below. For now, the maximum number of characters  in the whole x500 name (across all 6 fields) is **128 characters**.

A X500 must be unique within Corda Network. The combination of O and OU are used for the uniqueness check, and the other fields are considered as attributes of the identity. 

All data fields must adhere to the following constraints:
* Only uses Latin, common and inherited unicode scripts
* Upper-case first letter
* At least two letters
* No leading or trailing whitespace
* Does not include the following characters: , , = , $ , " , ' , \
* Is in NFKC normalization form
* Does not contain the null character

Organisation (O) must represent a legal entity name - which is the beneficial owner of states on the ledger. For guidance on what exact legal entity name to write, see [here](https://corda.network/participation/legalentity.html)

Overall, the DN is one of the most common points of error in joining Corda Network, so take care to fill this out correctly. As part of standard onboarding checks for Corda Network, the Identity Operator may verify that these details have been accurately populated and reject requests where the population of these fields does not appear to be correct.

| | Mandatory | Max length (chars) | Validation | Purpose |
| --- | --- | --- | --- | --- |
| **Organisation (O)** | Y | 110 | As per above, and additionally: No double-spacing. May not contain the words &quot;node&quot; or &quot;server&quot;. | The O field for the legal entity defines the beneficial owner of states on the ledger. This should be set to the **legal name** of the organisation, as it appears on the official trade register within the jurisdiction in which the entity is registered. This is used to define the owning organisation of the node / certificate. |
| **Organisation Unit (OU)** | N | 64 | As per above | This field is generally used to denote sub-divisions or units of the organisation (legal entity). It may be used by node operators for internal purposes to separate nodes used for different purposes by the same legal entity. |
| **Locality (L)** | Y | 64 | As per above | The city or town in which the registered head-office of the legal entity is located. If the company operates from New York City but is registered in Wilmington, Delaware then please use Wilmington |
| **Country (C)** | Y | 2 | 2-digit ISO code | The country in which the registered head-office of the legal entity is located. |
| **State (S)** | N | 64 | As per above | If your country operates a State or Province system (e.g. USA and Canada) please add the State in which the registered head-office of the legal entity is located. Do not abbreviate. For example, &quot;CA&quot; is not a valid state name. &quot;California&quot; is correct. If the company operates from New York but is registered in Delaware, please use Delaware |
| **Common Name (CN)** | N | 64 | As per above | Available for use by the node operator for their own internal purposes. Often used for home website urls in www. |

**Please note** - the max number of characters in the whole x500 name should be **128 characters in total (including spaces)**. In addition, guidance has been given above on the max length on a per field basis.
