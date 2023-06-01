{:title "Ethereum's Decade: Network and Narrative 🦄 💎 🚀"
 :layout :post
 :toc true
 :tags  ["template"]}

<div align="center">
    <img src="/img/ethereum-timeline.png" alt="Ethereum Road Map" style="width:100%">
</div>
<b>Figure 1: </b> Ethereum timeline from 2013 until mid 2023, depicting the different phases of the Ethereum project: "pre-launch", "proof-of-work", "beacon-chain-live", and "proof-of-stake". Events relating to the network are denoted by a left-headed arrow across the x-axis of the plot, other significant ecosystem events in DeFi, NFTs, and ICOs are shown with a dashed left-headed arrow of smaller size.
<p></p>

<span style="font-size:2em;">O</span>ver the past decade, Ethereum has experienced remarkable transformations. The project narrative has evolved, the network has expanded, and use cases have emerged. This post unveils the story of the Ethereum project from 2013 until 2023, encompassing its initial goals, significant implementation upgrades, and major phases. The story is told through the lens of a timeline of major milestones, releases and events shown in Figure 1. In addition to the major network events [[^1]], ecosystem events surrounding the protocol from NFTs, to DAOs, to DeFi are discussed.



## 🚧 <u>Pre-Launch</u> 🚧: (2013-11-27 to 2015-07-30)
<div align="center">
    <img src="/img/ethereum-timeline-pre-launch.png" alt="Ethereum Pre-Launch" style="width:100%">
</div>
<b>Figure 2: </b> Ethereum timeline between 2013-11-27 until 2015-07-30, the so called "Pre-Launch" phase.

<span style="font-size:2.0em">T</span>he time between the release of the Ethereum whitepaper and before the release of the Ethereum production blockchain is often referred to as the "pre-launch" or "pre-mainnet" phase. During this period, Ethereum was being developed and tested to ensure its stability, security, and functionality.

 + **Testnets**: Several testnets were released to allow developers to experiment, identify and fix bugs, and provide feedback. The final testnet before the mainnet called Olympic was launched on May 1st 2015.
 + **Ethereum Foundation**: The Ethereum Foundation was established as a non-profit organisation to support the development and promotion of the Ethereum platform. The foundation continues to play a pivotal role in coordinating development efforts, providing financial support, and fostering community engagement. The foundation organises an annual conference for developers "DevCon", a key gathering for developers and enthusiasts to share knowledge and showcase projects. The eight Ethereum founders had differing visions of how the Ethereum project should be managed, with some advocating a hierarchical corporate structure, and others a more organic and potentially more chaotic non-profit foundation structure.
 + **Geth Ethereum Client**:The original Ethereum client, also known as the reference client, was called "Go Ethereum" or "Geth" for short. Geth was the first implementation of the Ethereum protocol and was developed primarily in the Go programming language. Geth was created by the Ethereum Foundation and released alongside the Ethereum network in July 2015. It played a crucial role in the early days of Ethereum's development and adoption. Geth provided the foundation for running Ethereum nodes, participating in the network, and interacting with the Ethereum blockchain.

The pre-launch phase of Ethereum was vital in establishing the culture, organisation, governance for the Ethereum project and preparing the code for its live deployment and ensuring a smooth transition to a production-ready blockchain. These efforts were essential in laying the groundwork for Ethereum's success as a pioneering blockchain technology.

<div align="center">
  <table>
    <tr>
      <td style="padding-right: 10px;">
        <img src="/img/ethereum-whitepaper.png" alt="Ethereum Whitepaper" style="max-width: 99%;">
      </td>
      <td style="padding-right: 10px;">
        <img src="/img/ethereum-yellowpaper.png" alt="Testnet Logos" style="max-width: 100%;">
      </td>
      <td>
        <img src="/img/ethereum-sale.png" alt="Ethereum Foundation" style="max-width: 90%;">
      </td>
    </tr>
  </table>
</div>
<b>Figure 3: </b>Whitepaper, yellow paper, and Ethereum Foundation blog post on Launching the Ether Sale
Posted by Vitalik Buterin.

### Whitepaper 📄
In late 2013, Vitalik Buterin published a whitepaper describing Ethereum a blockchain "with a built-in fully fledged Turing-complete programming language that can be used to create "contracts" encoding arbitrary state transition functions" [[^2]]. Having a built in Turing complete programming language means that the language used for writing smart contracts on Ethereum, which is Solidity, has the necessary features to express any computable function or algorithm. This is important because it enables developers to create complex and sophisticated applications on the Ethereum platform. They can implement various logic, loops, conditionals, and other computational structures to build powerful and flexible smart contracts.

Ethereum was inspired by the principles of Bitcoin but went beyond its scope of peer-to-peer transactions. It introduced a versatile distributed computing platform, allowing developers to build and run decentralised applications with enhanced flexibility and capabilities.

 + **Smart contracts**: Smart contracts are self-executing agreements with predefined rules and conditions that automatically execute actions based on the fulfillment of those conditions. The idea of smart contracts was first discussed in the 1990s by Nick Szabo, referring to "a set of promises, specified in digital form, including protocols within which the parties perform on these promises" [[^3]]. Ethereum is the first fully fledged general purpose computer able to store long term state, that enables it to be the first at scale attempt of a distributed smart contract platform.

 + **Ethereum Virtual Machine (EVM)**: The Ethereum Virtual Machine is a key component described in the whitepaper. It serves as the runtime environment for executing smart contracts. The EVM enables developers to write code that can run on the Ethereum network, where each computational step is paid for in a unit of Gas which is priced depending on the demand on the blockchain.

 + **Modified Greedy Heaviest-Observed Sub-Tree (GHOST)**: The GHOST protocol is a consensus algorithm that was adopted by Ethereum to address limitations in traditional blockchain systems. Unlike the longest-chain rule used in Bitcoin, GHOST considers uncle blocks (valid but not included in the main chain) when determining consensus. This innovation brings two major advances. Firstly, it significantly reduces block confirmation times by including uncle blocks, allowing for faster transaction finality. Secondly, the inclusion of uncle blocks incentivises network participation and reduces the risk of centralisation, as miners are still rewarded for contributing to the network even if their blocks don't become part of the main chain.

In addition to these important concepts the whitepaper discussed potential applications including:
 + Token Systems,
 + Financial derivatives,
 + Identity and Reputation Systems,
 + Decentralized File Storage, and
 + Decentralized Autonomous Organizations.

Whilst describing the initial aspirations of Ethereum in the whitepaper Vitalik highlighted the "open-ended design" of the protocol, giving room for evolution and adaption:

<blockquote style="background:#f5f5f5;">
The concept of an arbitrary state transition function as implemented by the Ethereum protocol provides for a platform with unique potential; rather than being a closed-ended, single-purpose protocol intended for a specific array of applications in data storage, gambling or finance, Ethereum is open-ended by design, and we believe that it is extremely well-suited to serving as a foundational layer for a very large number of both financial and non-financial protocols in the years to come. - Ethereum Whitepaper
</blockquote>

The whitepaper notably does not discuss proof-of-stake, solutions for scaling, or the smart contract execution model.

### Yellow Paper 📄
The Ethereum Yellow Paper is a technical document written by Gavin Wood, a co-founder of Ethereum, in 2014 [[^4]]. It serves as a formal specification of the Ethereum Virtual Machine (EVM) and the underlying protocols of the Ethereum platform. The Yellow Paper provides detailed explanations of various aspects of Ethereum's architecture, including:

 + **Ethereum Virtual Machine (EVM)**: the runtime environment for executing smart contracts on the Ethereum platform. It outlines the EVM's instruction set, memory layout, stack operations, storage model, and the process of executing transactions and smart contract bytecode.

 + **Gas Cost Model**: Gas is the unit used to measure the computational effort required to execute operations in the EVM. The paper describes the different gas costs assigned to various EVM operations to ensure fair and efficient resource allocation. The gas cost model helps prevent abuse and encourages economically efficient smart contract execution.

 + **Blockchain and Consensus**: details on Ethereum's blockchain structure, including block headers, transaction format, and the process of block validation. It also explains the Ethereum consensus algorithm at the time, which was based on Proof of Work (PoW). The paper outlines the process of state transition, mining, and the validation of transactions and blocks.

 + **Network Protocol**: covers topics such as network messaging, block propagation, peer discovery, and synchronisation of the blockchain across nodes. The paper provides technical specifications for the Ethereum network protocol, facilitating the interoperability and communication between Ethereum nodes.

 + **Cryptography and Security**: cryptographic primitives and algorithms employed in Ethereum, such as cryptographic hashing functions, elliptic curve cryptography, digital signatures, and Merkle trees. It explains how these cryptographic tools are used to secure transactions, protect account balances, and ensure the integrity of the blockchain.

### Ethereum Sale 💰
A crowdsale of Ethereum was announced by Vitalik Buterin on July 22, 2014 to fund the development and launch of the Ethereum platform [[^5]]. The initial fundraising goal was set at 60,000 Bitcoin (BTC), equivalent to around $18 million at that time. During the sale period of 42 days, Ether (ETH) tokens were sold to participants in exchange for Bitcoin (BTC). The exchange rate for Ether was set at 2,000 ETH per BTC, and participants could contribute any amount of BTC they desired. The sale was widely publicised and garnered significant attention within the cryptocurrency community. It attracted a diverse range of participants, including individual investors, early cryptocurrency adopters, and institutional investors. The project managed to raise 31,591 BTC during this period, falling short of its initial fundraising goal of 60,000 BTC.

 + **Legaltity and compliance**: For the crowd-sale measures were taken to ensure legality and compliance. This included setting clear terms and conditions, implementing investor protections like contribution limits, making public announcements, ensuring transparent fund management, and obtaining a legal opinion suggesting that Ethereum's native token, Ether (ETH), should be considered a utility token rather than a security token. These measures aimed to address potential regulatory concerns and ensure compliance with applicable laws during the crowd-sale.
 + **Criticism**: The Ethereum crowdsale garnered both praise and criticism. Critics argue that the sale resulted in an unequal distribution of Ether, with a few early investors and participants holding significant amounts, potentially leading to wealth inequality and concentrated influence. Concerns were also raised about pre-mining, as Ether was generated and distributed to founders and early contributors before the public launch, disadvantaging later adopters. Additionally, the lack of regulatory oversight during the crowdsale period raised worries about investor protection and potential fraudulent activities. Furthermore, technical challenges and delays in Ethereum's development caused frustration among supporters awaiting the platform's release.

The sale of Ethereum marked a significant milestone in the project's history, providing the necessary resources to bring the Ethereum platform to fruition.


## ⛏️ <u>Proof-Of-Work</u> ⛏️: (2015-07-30 to 2020-12-01)
<div align="center">
    <img src="/img/ethereum-timeline-proof-of-work.png" alt="Ethereum Pre-Launch" style="width:100%": >
</div>
<b>Figure 4: </b> Ethereum timeline between 2015-07-30 until 2020-12-01, the so called "Proof-of-Work" phase, where Ethereum consensus relied on proof-of-work consensus.

<span style="font-size:2.0em;">I</span>n proof-of-work miners compete to find a specific value, called a "nonce," that, when combined with the data of a block, produces a hash value that meets specific criteria, usually a certain number of leading zeros. The hash function used is designed to be computationally intensive, requiring miners to make numerous attempts by varying the nonce until a valid hash is found. This process involves performing repetitive calculations using computational power, with the goal of finding a hash that satisfies the difficulty requirements set by the network. This computationally intensive puzzle-solving serves as a mechanism to secure the blockchain network, as it ensures that a significant amount of work has been done to validate and append a new block to the blockchain.

Despite being in its nascent stage, the nearly five and a half years of Ethereum's existence as a proof-of-work network have been turbulent but ultimately successful. During this time, the blockchain has gained significant traction and trust, and the ecosystem surrounding smart contracts has flourished with a multitude of intriguing use cases being trialled.

 + **Mainnet Launch**: On Jul-30-2015 03:26:13 PM +UTC, the first block of the Ethereum mainnet was mined [[^6]]. Ethereum was launched on the mainnet, introducing a decentralised platform for smart contracts and decentralised applications (DApps).

 + **DAO exploit**: During this proof-of-work period the network suffered a major setback with the DAO hack in 2016, leading to a hard fork and the emergence of Ethereum and Ethereum Classic as separate blockchains. Additional distributed denial of service (DDoS) attacks made 2016 a very difficult year for the Ethereum developers and community.

 + **Upgrades:** To enhance scalability and functionality, Ethereum underwent important upgrades like Byzantium and Constantinople, which integrated zk-SNARKs and lowered transaction fees. These upgrades also laid the foundation for a shift from Proof of Work (PoW) to Proof of Stake (PoS) consensus. On December 1, 2020, Ethereum took its first step towards Ethereum 2.0 with the launch of the Beacon Chain. This marked the beginning of the transition from PoW to PoS consensus, aiming to improve scalability, security, and energy efficiency.

 + **Initial Coin Offerings (ICOs)**:In addition to the Ethereum network improving, the ecosystem also exploded with an array of smart contract applications during this time period. The rise of Initial Coin Offerings (ICOs) on the Ethereum blockchain marked a significant turning point in the cryptocurrency landscape. Using smart contracts, projects were able to conduct crowdsales and issue tokens, attracting unprecedented levels of investment and attention. This phenomenon began in 2016 and continued through 2018, as ICOs became a popular means of fundraising. The programmability of Ethereum allowed for the creation of diverse tokens that served different purposes, ranging from utility tokens for platform access to investment tokens representing shares in a project. The legitimacy of many of these projects and the legality of the ICO sales have since been called into question.

 + **Non-fungible tokens (NFTs)**: Around the same time as the ICO boom, NFTs gained momentum. In 2017, the world took notice of Cryptokitties, a blockchain-based game built on Ethereum that introduced the concept of unique digital assets. This marked a breakthrough for NFTs, demonstrating their potential for representing ownership of digital collectibles, artwork, and other unique items. Cryptokitties captured the imagination of the public and paved the way for the broader adoption of NFTs in various industries, such as art, gaming, and virtual real estate. The introduction of the ERC-20 token standard in 2017 brought standardisation to the creation of fungible tokens on the Ethereum platform. ERC-20 tokens became the de facto standard for conducting token sales and representing digital assets. This standardisation allowed for seamless interoperability between different projects and contributed to the rapid growth of the ICO market on Ethereum.

 + **Decentralised Finance (DeFi)**: More recently DeFi has emerged as a major force in the Ethereum ecosystem. Building on the foundations of earlier developments, DeFi applications provide a range of financial services without the need for intermediaries. The year 2020 saw a significant surge in DeFi activity, with lending platforms, decentralised exchanges, and yield farming protocols gaining traction. DeFi has introduced new opportunities for financial inclusion, liquidity provision, and yield generation, challenging traditional financial systems and opening up innovative possibilities for global financial interactions.

In summary, the rise of ICOs on Ethereum paved the way for new fundraising models, followed by the introduction of NFTs and the standardisation of ERC-20 tokens. These advancements set the stage for the explosive growth of decentralised finance, revolutionising the financial landscape and creating a vibrant ecosystem on the Ethereum blockchain.

<div align="center">
  <table>
    <tr>
      <td style="padding-right: 10px; max-width:50%;">
        <img src="/img/ethereum-mining.png" style="max-width: 100%;">
        <img src="/img/ethereum-cryptopunk.png" style="max-width: 100%;">
      </td>
      <td style="max-width:50%;">
        <img src="/img/ethereum-dragon.png" style="max-width: 100%;">
        <img src="/img/ethereum-beeple.png" style="max-width: 100%;">
      </td>
    </tr>
  </table>
</div>
<b>Figure 5: </b>Clockwise from top right: (1) a GPU mining rig performing proof-of-work used to secure the Ethereum blockchain, (2) the most valuable cryptokitty NFT sold for 600 ETH, (3) a cryptopunk sold for 8000 ETH, and (4) Beeple's artwork, "Everydays: The First 5000 Days," was sold for a staggering 42,329 ETH. The sale took place at a Christie's auction on March 11, 2021.


#### Frontier: Mainnet Launch 🏞️
The Ethereum proof-of-work chain was launched with the release of the Frontier network on July 30, 2015.

<blockquote style="background:#f5f5f5;">
Frontier is a live, but barebone implementation of the Ethereum project. It's intended for technical users, specifically developers. During the Frontier release, we expect early adopters and application developers to establish communities and start forming a live ecosystem. Like their counterparts during the American Frontier, these settlers will be presented with vast opportunities, but will also face many dangers. If building from source and command lines interfaces aren't your cup of tea, we strongly encourage you to wait for a more user-friendly release of the Ethereum software before diving in. - Ethereum Foundation Blog
</blockquote>

In the Frontier network, the default gas limit for a transaction was 5000 gas. This meant that a transaction could consume up to 5000 gas during its execution. If the gas consumed by a transaction exceeded the gas limit, the transaction would fail and any changes made by that transaction would be reverted [[^7]].

During the Frontier Thawing fork of August 2015, the gas limit was increased to 21,000, allowing the Ethereum network to adapt to increasing transaction volumes while minimising potential disruptions or instability that could arise from sudden changes. The purpose of Frontier Thawing was to strike a balance between scalability and network stability.

The difficulty bomb was also introduced in the Frontier Thawing fork to ensure a future hard-fork to proof-of-stake. This is a mechanism implemented in the Ethereum network to gradually increase the mining difficulty over time, incentivising the transition from the proof-of-work consensus mechanism to the proof-of-stake consensus mechanism.

#### Homestead 🔀
The second major version release of the Ethereum platform was realeased on March 14 (Pi day) 2016. This release included several protocol changes and a networking change. It enhanced security, repriced gas costs for fairer fees, hardened the network against attacks, improved the Ethereum Virtual Machine (EVM), and established protocol consistency. These changes ensured a more secure and efficient platform for developers and users, setting the stage for further advancements in the Ethereum ecosystem.


#### The DAO Hack: ~~Code is Law~~ 🐱‍💻💔
The Decentralized Autonomous Organization (DAO) known as "The DAO" was a prominent project built on the Ethereum blockchain. It was launched in April 2016 and aimed to create a decentralised venture capital fund, allowing participants to submit proposals and vote on investment decisions using digital tokens called DAO tokens. This project attempted to be the first major instantiation of a Decentralized Autonomous Organization (DAO).

The DAO quickly became one of the most successful crowdfunding campaigns in history, raising over $150 million worth of Ether (ETH) during its token sale. However, the DAO's complex code and structure had at least one critical vulnerability, that created a colossal chasm in the Ethereum community.

The hack took advantage of a vulnerability in the DAO's smart contract code. The attacker exploited a recursive call bug in the contract, allowing them to repeatedly execute a function that allowed them to withdraw funds multiple times before the balance was updated. In technical jargon this is known as a recursive call re-entrancy attack.

Here is a simplified example of how a recursive call bug can lead to a reentrancy attack:

``` solidity
contract DAO {
    mapping(address => uint) public balances;

    function withdraw(uint amount) public {
        if (balances[msg.sender] >= amount) {
            // Update sender's balance before sending the funds
            uint balance = balances[msg.sender];
            balances[msg.sender] -= amount;
            // External function call
            msg.sender.call.value(amount)("");
            // Revert if the external call fails
            if (balances[msg.sender] != balance - amount) {
                revert("Failed to send funds");
            }
        }
    }
}
```
In the above example, the withdraw function allows an account to withdraw a specified amount of Ether. However, the problem arises when an external function call (e.g., a fallback function in another contract) is made after updating the sender's balance but before checking the balance again. This creates an opportunity for a malicious contract to call the withdraw function recursively before the balance is deducted. The reentrancy attack occurs when a malicious contract takes advantage of this recursive behaviour to repeatedly call the withdraw function, draining the contract's balance multiple times.

In the case of the DAO hack, the attacker exploited a similar vulnerability to drain a significant amount of Ether from the DAO contract. The attacker exploited the vulnerability in the DAO smart contract code and managed to drain approximately 3.6 million ETH, which was worth around $50 million at the time of the hack. This made it one of the largest cryptocurrency hacks in history. This led to a controversial situation within the Ethereum community, as it raised questions about governance, and the security and robustness of smart contracts.

After the DAO hack, the Ethereum community decided to fork the Ethereum blockchain to recover the stolen funds. This resulted in two separate chains: Ethereum (ETH) and Ethereum Classic (ETC), with ETH being the chain that implemented the fork and returned the funds to the original DAO token holders. The decision to perform a hard fork was met with controversy within the Ethereum community. Some argued that the immutability and decentralisation of blockchain should be maintained, and the hack was a consequence of the DAO's code vulnerability. Others believed that the fork was necessary to protect the integrity of the Ethereum ecosystem and return the stolen funds.

The DAO hack shook investor confidence in the security of smart contracts and decentralised applications (dApps) built on the Ethereum blockchain. It highlighted the importance of thorough code audits, formal verification, and secure development practices in the blockchain industry. The hack also raised legal and regulatory questions surrounding the status of DAOs and the responsibilities of developers and contributors to such projects. It prompted discussions about potential regulatory frameworks and increased scrutiny from authorities.

In Feburary 2022, Laura Shin host of the "Unchained" podcast published an article for Forbes [[^8]], the article gives a compelling case as to the identity of the DAO hacker the investigation was conducted with the help of Chainalysis [[^9]].

<div align="center">
    <img src="/img/ethereum-dao-forbes.png" alt="Ethereum Road Map" style="width:90%">
</div>
<center><b>Figure 6: </b> Forbes article with investigative journalism providing evidence of the likely identity of the DAO hacker.</center>
<p></p>



#### Spurious Dragon and Tangerine Whistle 🔀
The Spurious Dragon and Tangerine Whistle upgrades played a critical role in addressing security vulnerabilities and mitigating Distributed Denial of Service (DDoS) attacks on the Ethereum network. In late 2016 during DevCon1, the Ethereum network faced targeted DDoS attacks that exploited specific weaknesses in its protocol, causing network congestion and disruptions.

<blockquote style="background:#f5f5f5;">
URGENT ALL MINERS: The network is under attack. The attack is a computational DDoS, ie. miners and nodes need to spend a very long time processing some blocks. This is due to the EXTCODESIZE opcode, which has a fairly low gasprice but which requires nodes to read state information from disk; the attack transactions are calling this opcode roughly 50,000 times per block. The consequence of this is that the network is greatly slowing down, but there is NO consensus failure or memory overload. We have currently identified several routes for a more sustainable medium-term fix and have developers working on implementation. - Ethereum Foundation Blog
</blockquote>

During these attacks, an anonymous individual or group took a short position and invested approximately 150,000 Ether (ETH), equivalent to millions of dollars, to execute these attacks. The attacker took advantage of a vulnerability in the Ethereum protocol to generate a significant number of transactions, overwhelming the network with spam transactions. The spam transactions congested the network and made it difficult for legitimate users to process their transactions effectively.

In response to these challenges, the Ethereum development community swiftly enacted the Spurious Dragon and Tangerine Whistle upgrades. The Spurious Dragon upgrade, implemented in November 2016, focused on resolving security vulnerabilities and improving the network's resilience against further attacks. It introduced critical fixes and enhancements to strengthen the Ethereum protocol.

This incident highlighted the importance of addressing security vulnerabilities in the Ethereum network and prompted the community to work on improving the protocol's robustness against similar attacks in subsequent updates and hard forks. While the Tangerine Whistle and Spurious Dragon forks did not specifically target this particular attack, they were part of the ongoing efforts to enhance the security and stability of the Ethereum blockchain.

#### Byzantium 🔀
The Byzantium upgrade in October 2017 introduced nine Ethereum Improvement Proposals (EIPs) to the network, including:

 + EIP 98: (an improvement to elliptic curve pairing operations),
 + EIP 140: (introducing the REVERT opcode for better error handling),
 + EIP 196: (implementation of zero-knowledge proofs that significantly enhanced privacy and security), enabling more private transactions.

This upgrade also laid the groundwork for the future implementation of the Metropolis hard fork. The wider impact of Byzantium was the improvement of Ethereum's overall functionality, efficiency, and privacy, making the network more attractive for developers and users.

#### Constantinople 🔀
The Constantinople upgrade in February 2019 implemented five EIPs, including:

 + EIP 1014 (enabling state channels), State channels are a technique used to facilitate off-chain transactions between parties while still leveraging the security and decentralization of the underlying blockchain. They enable participants to conduct multiple transactions without having to record each one on the blockchain, reducing transaction costs and increasing scalability. By moving transactions off-chain and reducing the number of transactions recorded on the blockchain, state channels help alleviate network congestion, increase scalability, and enhance the overall efficiency of the blockchain network. They enable faster and cheaper transactions, providing an effective solution to address the limitations of on-chain transactions while still benefiting from the security and decentralization of the underlying blockchain protocol.
 + EIP 1234 (reducing block rewards), this delayed the Ethereum network's difficulty bomb and reduced block rewards to ensure a smoother transition to Ethereum 2.0 and manage the issuance of Ether tokens,
 + EIP 1283 (optimizing storage costs), also known as the "Net Gas Metering for SSTORE Without Dirty Maps" proposal, addresses gas cost optimizations for the storage (SSTORE) operation in Ethereum smart contracts. It modifies the gas cost calculations to reduce the cost of certain storage updates, improving efficiency and making smart contract interactions more cost-effective for users.

The wider impact of Constantinople was the reduction of transaction fees, improved contract functionality, and laying the foundation for future network upgrades, such as Ethereum 2.0.

#### Istanbul 🔀
Istanbul introduced six EIPs, including EIP 1679 (optimized gas cost for certain operations) and EIP 2200 (restructuring gas costs). This upgrade focused on enhancing the security, interoperability, and scalability of the Ethereum network. Istanbul enabled greater privacy through the implementation of zero-knowledge proofs (EIP 152), improved Ethereum Virtual Machine (EVM) efficiency, and increased compatibility with other blockchain networks. The wider impact of Istanbul was the strengthening of the Ethereum ecosystem, fostering innovation, and enabling smoother integration with other blockchain platforms.

The Istanbul Ethereum upgrade, implemented in December 2019, introduced several Ethereum Improvement Proposals (EIPs) to enhance the functionality, security, and interoperability of the Ethereum network.

 + EIP 1108 (Reduce alt_bn128 precompile gas costs). This EIP aimed to reduce the gas costs associated with certain cryptographic operations, specifically the alt_bn128 precompile, which is used for elliptic curve pairing. By lowering the gas costs, EIP 1108 made cryptographic operations more affordable, enabling more efficient usage of these operations in smart contracts and promoting the development of privacy-preserving applications.
 + EIP 1344 (CHAINID opcode). Introduced a new opcode called CHAINID, which retrieves the unique identifier of the Ethereum chain being executed. The CHAINID opcode provides a standardised way for smart contracts to determine the chain they are running on. This is useful for implementing chain-specific logic or enabling compatibility with multiple Ethereum networks.
 + EIP 1884 (Repricing for trie-size-dependent opcodes): adjusted the gas costs of trie-size-dependent opcodes, including SLOAD, BALANCE, and EXTCODESIZE, to more accurately reflect the computational resources required for these operations. The repricing of these opcodes aimed to align the gas costs with the computational effort required, incentivising efficient smart contract design and preventing potential abuse or resource exhaustion.
 + EIP 2028 (Calldata gas cost reduction): reduced the gas costs associated with certain operations involving calldata, which is read-only input data for smart contracts. By lowering the gas costs, EIP 2028 made it more affordable to perform operations with calldata, encouraging cost-effective interactions with external contracts and enhancing overall gas efficiency.

By optimising gas costs, introducing new opcodes, and aligning computational resources, Istanbul facilitated the development of innovative applications, promoted scalability, and ensured a more user-friendly and cost-effective experience for Ethereum users and developers.

#### Muir Glacier 🔀
The Muir Glacier Ethereum upgrade was a minor upgrade implemented on January 1, 2020, to delay the Ethereum network's Difficulty Bomb by adjusting the block timestamps in EIP 2384.


#### Staking Deposit Contract 🏦 & Beacon Chain Genesis 🌟
The Staking deposit contract and Beacon chain genesis were crucial milestones for the so called "Ethereum 2.0" upgrade, marking the transition from a proof-of-work (PoW) consensus mechanism to a proof-of-stake (PoS) mechanism.

**Proof-of-Stake (PoS)** is a consensus algorithm used in blockchain networks as an alternative to Proof-of-Work. In PoS, validators are chosen to create new blocks and validate transactions based on the amount of cryptocurrency they hold and "stake" in the network. Rather than relying on computational work, PoS selects validators probabilistically, taking into account their stake as well as other factors like their reputation or age of the stake. Validators are incentivised to act honestly because their staked cryptocurrency serves as collateral, which can be slashed in case of malicious behavior. This approach reduces the energy consumption associated with PoW, enhances scalability, and allows for faster block confirmation times. PoS offers a more energy-efficient and environmentally friendly consensus mechanism while maintaining the security and decentralisation of the blockchain network.

The Staking deposit contract was introduced to enable Ethereum holders to lock up their Ether (ETH) as a stake in the upcoming Ethereum 2.0 network [[^10]]. Participants could deposit a minimum of 32 ETH into the contract, which acted as a validator deposit to join the PoS consensus and participate in block validation.

The Beacon chain genesis marked the launch of the Beacon chain, which is the first phase of Ethereum 2.0. It serves as the PoS consensus and coordination layer for the Ethereum network. The Beacon chain introduced a new set of validators responsible for proposing and validating blocks, replacing the role of traditional miners in the PoW model. It facilitated the synchronisation of validator balances, network participation, and the consensus protocol for Ethereum 2.0.

The significance of the Staking deposit contract and Beacon chain genesis is multifold:

 + **Transition to PoS**: This marked a major step in Ethereum's transition from PoW to PoS consensus. PoS offers several advantages such as increased scalability, energy efficiency, and security through economic incentives for validators.

 + **Enhanced Security**: The introduction of the Beacon chain and PoS consensus helps improve the overall security of the Ethereum network by mitigating the risks associated with PoW mining, such as 51% attacks.

 + **Validator Participation**: The Staking deposit contract allowed Ethereum holders to actively participate in the consensus process and contribute to network security by becoming validators and earning rewards for their staked ETH.

 + **Ethereum 2.0 Roadmap**: The Staking deposit contract and Beacon chain genesis represented significant progress in the Ethereum 2.0 roadmap, which aims to address scalability challenges and introduce new features like shard chains and improved smart contract capabilities.

Overall, the Staking deposit contract and Beacon chain genesis were pivotal moments in Ethereum's evolution, signaling the shift towards a more scalable and sustainable network architecture based on PoS consensus. It attracted significant attention from the Ethereum community and marked a crucial step towards the realisation of Ethereum 2.0's ambitious goals.

## 🟢 <u>Beacon-Chain-Live</u> 🟢: (2020-12-01 to 2022-09-15)
<div align="center">
    <img src="/img/ethereum-timeline-beacon-chain-live.png" alt="Ethereum Beacon Chain Live" style="width:100%">
</div>
<b>Figure 7: </b> Ethereum timeline for "Beacon Chain Live" phase, between 2020-12-01 to 2022-09-15.

<span style="font-size:2.0em;">B</span>etween December 1, 2020 and September 15, 2022 the Beacon Chain was launched but Ethereum was still relying on proof-of-work for consensus.

**The Beacon Chain** serves as the coordinating mechanism for the new Proof-of-Stake (PoS) consensus protocol. Validators are Ethereum network participants who lock up a certain amount of Ether as collateral (stake) to participate in block proposal and validation. The Beacon Chain randomly selects validators based on their stake, ensuring a fair and decentralised selection process. Selected validators take turns proposing new blocks by including transactions and other relevant data. They are responsible for creating blocks and including attestations from other validators to validate its authenticity. Validators also participate in the attestation process, where they validate and attest to the validity of proposed blocks. By voting on the blocks they consider valid, they contribute to the consensus mechanism. The Beacon Chain's Finality Gadget algorithm determines the finalised state of the Ethereum network by establishing a threshold of attestations, ensuring irreversible block finality. Validators are incentivised to act honestly and perform their duties faithfully. They can earn rewards in the form of additional Ether for their participation and contribution to block validation. However, validators may also face penalties, such as having their staked Ether slashed if they exhibit malicious behavior or fail to perform their duties correctly.

During the phase in which the Beacon Chain was launched a number of upgrades were performed to prepare the Ethereum network for the long-awaited merge, in which the consensus protocol would switch from proof-of-work to proof-of-stake. During this time Ethereum experienced a significant surge in adoption and market value, with the price of Ether (ETH) reaching all-time highs and decentralised finance (DeFi) protocols gaining popularity.

#### Berlin 🔀
Berlin was an upgrade on the Ethereum network that occurred on April 15, 2021. It introduced several important Ethereum Improvement Proposals (EIPs) to enhance the functionality and performance of the network. Some notable EIPs included:
 + EIP-2565 (ModExp Gas Cost)
 + EIP-2929 (Gas cost increases for state access opcodes), and
 + EIP-2718 (Typed Transaction Envelope).

 The Berlin upgrade aimed to optimise gas costs, improve security, and prepare the network for future upgrades.

#### Altair 🔀
Altair was an upgrade specifically for the Ethereum 2.0 Beacon Chain. The upgrade took place on August 3, 2021, and marked the first significant update to the Beacon Chain. Altair introduced several enhancements to the protocol, including improvements to the beacon chain's efficiency, better handling of penalties, and support for light clients.

#### Arrow Glacier 🔀
Arrow Glacier was another significant upgrade for the Ethereum 2.0 Beacon Chain. It occurred on November 24, 2021, and introduced important improvements to the protocol. The upgrade focused on enhancing the robustness and security of the Beacon Chain network. It included optimisations to network synchronisation, better protection against denial-of-service attacks, and the introduction of the "sync committee" to improve chain finality.

An Ethereum **Sync Committee** is a group of validators that is responsible for helping synchronise shard chains with the Beacon Chain, the network will be divided into multiple shard chains to improve scalability. The main function of the Sync Committee is to periodically produce and publish signatures on specific shard block roots. These signatures, known as sync aggregates, serve as checkpoints that allow the Beacon Chain to verify the accuracy and validity of shard chain data. The composition of the Sync Committee changes over time through a randomised process. Validators are selected to participate in the Sync Committee based on their stake and participation in the Beacon Chain consensus. By having a committee dedicated to synchronising shard chains, the Ethereum network ensures that the various shards remain consistent and up-to-date with the latest block information. This synchronisation enables efficient communication and data transfer between the Beacon Chain and the shard chains.

#### Gray Glacier 🔀
The Gray Glacier upgrade was a network upgrade on the Ethereum blockchain that occurred on June 30, 2022. The upgrade pushed back the difficulty bomb by 700,000 blocks, or roughly 100 days.
 + EIP-5133: The Gray Glacier upgrade included EIP-5133, which made changes to the difficulty bomb algorithm. The changes were designed to make it easier to push back the difficulty bomb in the future.
 + Block gas limit: The Gray Glacier upgrade also increased the block gas limit from 15 million to 15.5 million. The increase in the block gas limit will allow for more transactions to be processed per block.

The Gray Glacier upgrade was a successful step in the transition to proof-of-stake. The upgrade gave Ethereum developers more time to work on the transition, reduced the risk of network disruption, and increased confidence in the Ethereum network.

## 🏛️ <u>Proof-of-Stake</u> 🏛️: (2022-09-15 to present)
<div align="center">
    <img src="/img/ethereum-timeline-proof-of-stake.png" alt="Ethereum Beacon Chain Live" style="width:100%">
</div>
<b>Figure 7: </b> Ethereum timeline for the "Proof-of-Stake" chain phase, from 2022-09-15 to the present.

<span style="font-size:2.0em;">T</span>he merge of the Beacon Chain consensus layer and execution layer occurred on September 15th 2022. This is the most significant upgrade in Ethereum's history and effectively swaps out proof-of-work consensus mechanism with a proof-of-stake consensus mechanism.

<blockquote style="background:#f5f5f5;">
“It’s almost like changing the engines on a plane whilst flying it . . . a significant engineering feat,” - Walter Estlander
</blockquote>

Whilst the merge was a huge engineering success, and was achieved without any significant incident, the wider cryptocurrency ecosystem has been in turmoil. FTX, a cryptocurrency exchange founded in 2019, filed for bankruptcy in November 2022. The company had been struggling financially for months, and the collapse was triggered by a number of factors, including a major fraud, and a sharp decline in the price of cryptocurrencies. The collapse of FTX sent shockwaves through the cryptocurrency industry, and it raised concerns about the stability of the market.

During this period layer 2 scaling solutions also started to become used. These solutions increase the scalability of Ethereum by allowing Ethereum users to transact off-chain, which means that the transactions are not processed on the main Ethereum blockchain. Instead, the transactions are processed on a separate blockchain, and then the results of the transactions are submitted to the main Ethereum blockchain.

There are a number of different Ethereum Layer 2 scaling solutions available, each with its own advantages and disadvantages. Some of the most popular Ethereum Layer 2 scaling solutions include:

 + Arbitrum: a rollup-based Layer 2 scaling solution. Rollups are a type of Layer 2 scaling solution that bundles multiple transactions together and submits them to the main Ethereum blockchain as a single transaction. This can significantly reduce transaction fees.
 + Optimism: another rollup-based Layer 2 scaling solution. Optimism uses a fraud proof mechanism to ensure the validity of transactions. If a transaction is found to be invalid, it is rolled back.
 + Polygon: a sidechain-based Layer 2 scaling solution. Sidechains are separate blockchains that are connected to the main Ethereum blockchain. This allows Ethereum users to transact on the sidechain, which can significantly reduce transaction fees.

#### The Merge (Paris Upgrade) 🐼
The Merge was a major milestone in the development of Ethereum, the merge was part of the Paris upgrade was triggered by the proof-of-work blockchain passing a terminal total difficulty of 58750000000000000000000. This happened at block 15537393 on 15th September 2022, triggering the Paris upgrade the next block. The major feature of the upgrade was switching off the proof-of-work mining algorithm and associated consensus logic and switching on proof-of-stake instead. Paris itself was an upgrade to the execution clients that enabled them to take instruction from their connected consensus clients. PoS, is a more energy-efficient process that relies on validators to stake their ETH to secure the network. The Merge reduced Ethereum's energy consumption by an estimated 99.95%. This is a major step towards making Ethereum a more sustainable blockchain.

<div align="center">
    <img src="/img/ethereum-pos-activated.png" alt="Ethereum Beacon Chain Live" style="width:60%">
</div>
<b>Figure 8: </b> Ethereum log message in Beacon Chain consensus client when proof-of-stake was activated with the Paris upgrade on 15th September 2022.

#### Shanghai / Capella 🔀
The Shanghai upgrade brought staking withdrawals to the execution layer. In tandem with the Capella upgrade, this enabled blocks to accept withdrawal operations, which allows stakers to withdraw their ETH from the Beacon Chain to the execution layer. This consensus layer upgrade brought the ability for stakers who did not provide withdrawal credentials with their initial deposit to do so, thereby enabling withdrawals. The upgrade also provided automatic account sweeping functionality, which continuously processes validator accounts for any available rewards payments or full withdrawals.

 + EIP-4895: This EIP allows stakers to withdraw their staked ETH. This was a major change, as previously stakers were locked in for a period of time. This change will allow stakers to more easily access their funds, and it will also help to improve the liquidity of the ETH market.
 + EIP-3651: This EIP introduces a warm COINBASE, which means that validators can start validating blocks before the network is fully synchronized. This will help to improve the network's scalability. Currently, validators must wait for the network to be fully synchronized before they can start validating blocks. This can take a long time, especially during periods of high network activity. The warm COINBASE will allow validators to start validating blocks as soon as they are connected to the network, which will help to improve the network's scalability.
 + EIP-3855: This EIP introduces the PUSH0 instruction, which allows validators to more efficiently process transactions. The PUSH0 instruction is a simple instruction that does nothing. However, it can be used to fill up empty space in a transaction, which can help to improve the network's efficiency.
 + EIP-3860: This EIP limits the amount of initcode that can be included in a transaction. The initcode is a piece of code that is executed when a contract is created. Limiting the amount of initcode that can be included in a transaction will help to improve the network's security.
 + EIP-6049: This EIP deprecates the SELFDESTRUCT opcode. The SELFDESTRUCT opcode was used to remove ETH from the network. However, it was often used in scams. Deprecating the SELFDESTRUCT opcode will help to reduce the number of scams on the network.


## 🚀 <u>Into the Future</u> 🚀
<span style="font-size:2.0em;">O</span>ver the past decade, Ethereum has revolutionised blockchain technology, enabling the development of decentralized applications and smart contracts. A turing complete blockchain has provided exciting opportunities for developers to build on the back of, and we have witnessed exciting uses. Introduced concepts like ERC-20 tokens, NFTs, ICOs, DAOs, and DeFi. While facing scalability challenges, Ethereum is actively working on solutions. Some exciting future developments expected to the Ethereum protocol are:
+ **Sharding**: The introduction of sharding allows for the network to be divided into smaller pieces called "shards," enabling independent transaction processing and higher throughput.
 + **Improved Security**: Validator penalties in the Proof-of-Stake system deter malicious behavior by penalising validators for validating invalid blocks, enhancing network security.
 + **Easier User Experience**: Account abstraction enables users to interact with multiple smart contracts using a single address, streamlining the user experience.
 + **More Efficient Smart Contracts**: The implementation of "eWASM," a faster and more efficient virtual machine, enables the execution of complex smart contracts while reducing gas fees.
 + **Lower Transaction Fees**: Gas optimizations and energy-efficient mechanisms contribute to reducing transaction fees, making transactions more cost-effective.
 + **Interoperability**: Cross-shard communication facilitates transactions across multiple shards, enhancing interoperability with other blockchains.
 + **Better Privacy**: The integration of "zk-SNARKs" technology allows for private transactions without revealing sensitive information.

Ethereum's journey continues to evolve and shape the future of blockchain technology.

<div align="center">
    <img src="/img/ethereum-leslie.jpg" alt="Ethereum Leslie" style="width:50%">
</div>

## References
[^1]: [Ethereum: The history of Ethereum](https://ethereum.org/en/history/)
[^2]: [Ethereum Whitepaper](https://ethereum.org/669c9e2e2027310b6b3cdce6e1c52962/Ethereum_Whitepaper_-_Buterin_2014.pdf)
[^3]: [Smart Contracts Building Blocks for Digital Markets](https://docslib.org/doc/246577/smart-contracts-building-blocks-for-digital-markets)
[^4]: [Ethereum: Yellowpaper](https://ethereum.github.io/yellowpaper/paper.pdf)
[^5]: [Ethereum: Launching the Ether Sale](https://blog.ethereum.org/2014/07/22/launching-the-ether-sale)
[^6]: [Ethereum: Block 0](https://etherscan.io/block/0)
[^7]: [Ethereum: Frontier](https://blog.ethereum.org/2015/07/22/frontier-is-coming-what-to-expect-and-how-to-prepare)
[^8]: [Laura Shin: DAO Hacker](https://www.forbes.com/sites/laurashin/2022/02/22/exclusive-austrian-programmer-and-ex-crypto-ceo-likely-stole-11-billion-of-ether/)
[^9]: [Chainalysis](https://www.chainalysis.com/)
[^10]: [Staking Deposit Contract](https://etherscan.io/address/0x00000000219ab540356cBB839Cbe05303d7705Fa)
