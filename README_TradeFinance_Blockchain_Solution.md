### Smart Contracts and Blockchain, a solution to the Modern Trade Finance 

# What is Trade Finance:

According to the World Trade Organization nearly 80-90% of world trade is faciliated by Trade Finance, which involves financial institutions providing short-term finance in the form of letters of credit or guarantees to facilitate the the exchange of goods and services. Trade finance originated thousands of years ago in Mesopotamia, the oldest examples of trade finance instruments, such as promissory notes and letters of credits, can be found in Babylonian clay tablets dated around 3000 BC. 

According to the analysis by the Boston Consulting Group, the global trade flows are estimated to hit a record US $24 Trillion by 2026, and the trade finance revenues projected at US $48 Billion in the next three years, with a growth rate exceeding at 6% a year. rage  


# Challenges with Trade Finance - 

Labor and Paper Flow Intensive Processes for Trade Contract Creation and Review, Logistical and Operational inefficiencies, AML Implementation, Slow Documentation and Verification Checks, Manual and Expensive Reconciliation, Multiple Trade Systems and Poor Visibility into Trade Transactions, Fraudulence, No Standardization of Process and Documentation, Non-Compliance and Lack of Collaboration. 

Buyer side - No clear understanding on the counterparty, Shipping delays--Many touchpoints, increased & time consuming paperwork, Possibilty of fraud due to multiple touchpoints, Possibility of damaged goods on receipt and inspection

Seller side - No clear understanding on the counterparty's credibility, Increased paperwork, No assurance of payment at the time of shipment, Possibility of delayed payment/no payment, Delay in recieving acknowledgement of reciept of goods

## Implementing our Smart Contracts for Trade Finance

The increased transparency behind blockchain makes the trade finance process faster and if designed correctly, blockchain technology can reduce the motivation for misconduct. Using a public blockchain such as Ethereum for trade finance transactions is problematic in terms of privacy issues, since everyone can participate without proof of identity and everyone is able to track a wallet's transaction history, including the correspondent input data. Given this, we encryted some of our inputs using the one-way hash function. 
For our smart contracts, we suppose that the owner knows the roles and the corresponding public addresses of each participant. In addition, we assume the financing party comply with the anti-money laundering (AML) guidance for blockchain, which requires entities to know their opposite parties when trading with each other. Any transaction with an anonymous party are forbidden. 

In addition the AML requirements, we implement a whitelist contract which admits wallet addresses that want to finance  a deal in our second smart contract. We assume a know your client (KYC) check has been completed beforehand and the identities behind the wallet addreses are known by the buyer. All other involved parties do not need to know the identities, since the rules implemented in the smart contract manage the addresses. By setting the minimum requirements, a balance that is clearly higher than the required funding amount for the trading deal, one is able to control who can join the whitelist. Additionally, the applicant  must exceed a specific score, which is similar to an investment score. Only financiers who fulfill the conditions of a sufficent wallet balance and score will be approved. 

# Digitalization of trade finance processes and real-time collaboration are the key element that can help all the three parties involved i.e. buyers, sellers and banks to conduct trade transactions in a frictionless and timely manner. 

Banks in particular can overcome the trade finance lifecycle and operational challenges faced by imbibing digitial restructing into their trade finance operations such as Artificial Intelligence, Blockchain, Internet of Things and Machine Learning. 

According to the Boston Consulting Group, an integrated digital solution having functions like intelligent automation, collaborative digitization and other advanced technology solutions would help global trade banks save US $2.5-$6Billon with the potential to increse revenue by 20%-35% over 3 to 5 years. 

Banks can deliver a frictionless trade finance experience by - Eliminating the need for manual paperwork, Speed up trade processes, Enhance collaboration with trading counterparties, Automated Workflows, Centralized Trade Finance Operations, Seamless Experience across Multiple Channels, Provide delivery assurance to buyers through trade asset tokenization.

Three key features of Blockchain are instrumental in treating the major pain points of trade finance: 
The Cryptographic security underlying blockchain technology enables information immutability and credibility, the distributed ledger architecture provides transaction transparency and traceability, the network consensus mechanism provides a single source of truth for enabling native issuance of financial assets (trade receivables and other payment obligations can be natively issued in blockchain to reduce fraud and enable banks to offer more attractive financing. 

## References
Riqueza Finolutions Ltd (March 11th,2021), Ploytrade White Paper Shaping the Future of Trade Finance

Cognizant (August 2017) Digital Business, How Blockchain Can Revitalize Trade Finance (Part 1)

Oracle Financial Services (December 11th, 2018), White Paper, Fostering Smarter Trade Finance Operations Digital Engagement in Trade Finance
