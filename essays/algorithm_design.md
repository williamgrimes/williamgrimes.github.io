---
layout: essay
type: essay
title: Blockchains, Electricity Usage, and Centralisation
# All dates must be YYYY-MM-DD format!
date: 2017-12-27
labels:
  - Bitcoin
  - Q&A
---

## Question
> <i>Really interested for a blockchain expert to set me straight on how we should understand it's costs and benefits...
Are we just trading off higher payment processing costs (distributed verification cost) against the benefits of fraud/corruption protection? If so, I don’t think it will be a cost people are willing to pay, in the developed world at least</i>


## Response
Currently the transaction fee on the bitcoin network makes bitcoin impractical as a day to day currency for small value transactions, hence bitcoin is increasingly being referred to as a "store of value" and a speculative asset. The high transaction fee on bitcoin is due to an imposed limitation on the blocksize, that is the number of transactions that can be recorded in one transaction cycle (approx 10 mins).

At the moment, the demand for transactions is higher than the supply so miners opt to validate the more lucrative transactions, this works in a kind of auction system, where the transactor can choose the reward they will offer. There are several proposed solutions to scale the bitcoin network, allowing for more transaction in a cycle, thereby reducing fees. These are in various stages of implementation, and include the lightning network. Bare in mind that the fundamentals of bitcoin were laid out in 2008, and it is an evolving entity, where that evolution happens in software development. 

I have no doubt that a system of distributed settlement will ultimately be more efficient than the current fragmented financial system, where a transaction involves multiple intermediaries. We can quantify the electricity usage of the bitcoin network (which presently uses energy equivalent to a small nation like Serbia). But how could we quantify the cost/energy/efficiency of the entire global financial system?

From the point of view of a user/consumer/transactor in a country with a stable and developed financial system, the value proposition of interacting with say bitcoin is more nuanced (aside from illicit uses). The fundamental difference with bitcoin and a traditional payment method is that you have full custody of your money. No single third party or central authority needs to be trusted, to transact on your behalf, you are guaranteed that the transaction occurs, and it is cryptographically secure.

Bitcoin is the first successful implementation of such a distributed cryptographic consensus mechanism, and money transfer the most obvious application for this. This has opened a Pandora's box unleashing a host of variations/extensions/alternatives of such networks to all manner of uses.

---
## Question
> <i>I think the electricity estimate is pretty crucial to costs and scale and viability. Given the scale of bitcoin is a drop in the ocean of global transactions, it being currently compared to Serbia’s entire energy usage is alarming.</i>

> <i>I also disagree that distributed is more efficient than centralised (albeit fragmented). Trust overcomes a huge amount of verification needs, so as long as we can trust these institutions - it will be cheaper to use fiat currencies IMO. What makes distributed more efficient in your view? Looking at it on a transaction by transaction basis I can’t see distributed being more efficient: trusting the entries in a database as opposed to constantly checking its accuracy is the principle I am applying on this.</i>

## Response
Agreed, this energy use is alarming and unsustainable. I think eventually bitcoin will be forced to find a more efficient solution, or will be replaced by another network that implements a better solution.

On the subject of energy consumption. Improvements have already been made, for example ethereum is now handling twice as many transactions per day than bitcoin using 1/3 the energy. The energy consumption of bitcoin is a function of price, as price increases miners are incentivised to join the network. Miners verify transactions using a system called proof-of-work, in which they simultaneously compete to solve a computationally difficult problem. Ethereum is now working towards implementing an alternative algorithm for establishing distributed consensus called proof-of-stake, which will be thousands of times more efficient.

On the point of distributed vs centralised. Yes, a centralised database will always theoretically be more efficient. If trust, security, and robustness are not an issue. For example in the current financial system the cost of the improved operational efficiency in having a centralised database is offset by overheads in security. So for example a bank has to create processes to ensure the databases are not tampered with, are consistent, and are durable. This involves hiring people, and requires substantial time and money. Then they also have to insure a client's assets in the case of fraud for example. At some level these costs will be passed down to the customer.

Patently there will be a series of trade-offs that will have to be considerd when deciding whether to implement a distributed blockchain or a centralised solution. Financial institutions have begun to realise the value of blockchain for immutability, automation, and security. This is demonstrated by the establishment of the R3 consortium, and increasing investment in blockchain research. It remains to be seen whether these institutional private permissioned blockchains will be successful. 

For what its worth whilst I cannot predict the future, I think these institutional solutions would be a temporary intermediary stage on our journey towards a future in which technology, automation, and code replace humans and organisations. As we have witnessed in so many industries already.

The decoupling of money from the state would certainly be a very interesting thing to see, and given the speed of development in this area, I think it could happen sooner than we imagine...

As an endnote, I think the applications of blockchain or similar technology for smart contracts, micro transactions, proof of ownership, and supply chain traceability, are potentially more interesting and transformative. Especially the interaction of these things with IOT and AI (to throw in a few more buzzwords).

---
### Sources:
* <https://www.multichain.com/blog/2016/03/blockchains-vs-centralized-databases/>
* <https://www.fjordnet.com/conversations/the-trust-trade-off-permissioned-vs-permissionless-blockchains/>
