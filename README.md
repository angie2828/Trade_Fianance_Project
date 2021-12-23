### Smart Contracts and Blockchain, a solution to the Modern Trade Finance 

# What is Trade Finance:

According to the World Trade Organization nearly 80-90% of world trade is faciliated by Trade Finance, which involves financial institutions providing short-term finance in the form of letters of credit or guarantees to facilitate the the exchange of goods and services. Trade finance originated thousands of years ago in Mesopotamia, the oldest examples of trade finance instruments, such as promissory notes and letters of credits, can be found in Babylonian clay tablets dated around 3000 BC. 

According to the analysis by the Boston Consulting Group, the global trade flows are estimated to hit a record US $24 Trillion by 2026, and the trade finance revenues projected at US $48 Billion in the next three years, with a growth rate exceeding at 6% a year. rage  

## What is a Ethereum Blockchain:

A progression of the Bitcoin blockchain which is used to transfer financial values such as Bitcoin in a peer to peer network. It is an account based model in which every account has a 20-byte address and state. Each Ethereum account consists of a nonce, ether balance, contract code  hash and storage root. The nonce symbolizes a security mechanism against the double-spending problem so that each transaction can be used just once. The Ether balance shows the amount of the account of Ether.

## What is a Smart Contract: 

An application of DApps on the Ethereum blockchain. The code of a smart contract is written in the Solidity programming language and consists of two parts, the application binary interface (ABI), which contains the functions of the contract and the byte code that, after compilation, will be executed on the blockchain.


# Challenges with Trade Finance - 

Labor and Paper Flow Intensive Processes for Trade Contract Creation and Review, Logistical and Operational inefficiencies, AML Implementation, Slow Documentation and Verification Checks, Manual and Expensive Reconciliation, Multiple Trade Systems and Poor Visibility into Trade Transactions, Fraudulence, No Standardization of Process and Documentation, Non-Compliance and Lack of Collaboration. 

Buyer side - No clear understanding on the counterparty, Shipping delays--Many touchpoints, increased & time consuming paperwork, Possibilty of fraud due to multiple touchpoints, Possibility of damaged goods on receipt and inspection

Seller side - No clear understanding on the counterparty's credibility, Increased paperwork, No assurance of payment at the time of shipment, Possibility of delayed payment/no payment, Delay in recieving acknowledgement of reciept of goods

## Implementing our Smart Contracts for Trade Finance

The increased transparency behind blockchain makes the trade finance process faster and if designed correctly, blockchain technology can reduce the motivation for misconduct. Using a public blockchain such as Ethereum for trade finance transactions is problematic in terms of privacy issues, since everyone can participate without proof of identity and everyone is able to track a wallet's transaction history, including the correspondent input data. Given this, we encryted some of our inputs using the one-way hash function. 
For our smart contracts, we suppose that the owner knows the roles and the corresponding public addresses of each participant. In addition, we assume the financing party comply with the anti-money laundering (AML) guidance for blockchain, which requires entities to know their opposite parties when trading with each other. Any transaction with an anonymous party are forbidden. 

In addition the AML requirements, we implement a whitelist contract which admits wallet addresses that want to finance  a deal in our second smart contract. We assume a know your client (KYC) check has been completed beforehand and the identities behind the wallet addreses are known by the buyer. All other involved parties do not need to know the identities, since the rules implemented in the smart contract manage the addresses. By setting the minimum requirements, a balance that is clearly higher than the required funding amount for the trading deal, one is able to control who can join the whitelist. Additionally, the applicant  must exceed a specific score, which is similar to an investment score. Only financiers who fulfill the conditions of a sufficent wallet balance and score will be approved. 

## Process flow of Smart Contract-based transaction

Before the smart contract get deployed, both parties the seller and the buyer negotiate the terms and conditions for trading. The seller deploys the the Smart Contract and adds an order including the agreed parameters. If the buyer agrees to the conditions, the order is confirmed. As the buyer knows the value of the trade, they set this amount equal to the minimum amount in the whitelist to search for an appropriate candidiate. The fastest financier adds a payment by sending the funds to the smart contract's address. All the participating parties can observe that the payment is guaranteed by th financier and will be paid out following the rules of the contract. The seller prepares the goods to be ready for shipment and hands them over to the frieght company. When the goods arrive at the freight company, it confirms the receipt of the goods. To prevent this company from keeping the products and not sending them to the next station, the customs broker, takes place after a successful payment transfer. Afterwards the seller is paid by the smart contract after the goods arrived there. The buyer recieves the goods and confirms this event. After the smart contract has taken place, the seller can deposit their money in the bank and the buyer can negotiate individual conditions concerning their payback of the financier.
The parties involved have no incentives to deviate from the envisaged rules. The seller for one does not have an incentive not to hand over the goods, since they want to earn money. For the buyer, not paying is impossible, since the financier's payment is a necessary action before the seller sends goods to the buyer. Not confirming receipt of the order is also not an option, since the customs broker does not get a fee. If the buyer decides not to pay the financier, the financier can enforce their rights in court. Both the freight company and the customs broker do not have anhy incentive to not deliver their service as expected, given the reputational risks, they do not gain any advantage from a deviation. The same holds true for the financier, who sees no advantage to not paying on behalf of the buyer except the loss of interest payments. 

## Whitelist - 
We use Solidity version ^0.5.11 as the development environment. To avoid an overflow in arithmetic operation, we use the Safemath librarynfrom OpenZeppelin. We begin with the Whitelist smart contract, this is a separate contract from the TradeFinance contract to ensure that the Whitelist can be updated without generating conflicts and we can reutilise our main smart contract. Since the buyer needs funding, all functions in the Whitelist contract are restricted to the buyer. 

## Smart Contract Functions - 

1. The function below allows the buyer to set a minimum wallet amount and score that an applicant must fulfil to be accepted to the Whitelist. 

```python
function setMinimumRequirement(uint256 _minimumAmount, uint256 _minimumScore) public onlyBuyer 
```

2. If the buyer accepts the proposal from the sellre, the smart contract changes its state from Negotiation to Created to ensure that the seller cannot make changes afterwards. This is a security element to guarantee that fallbacks cannot occur.

```python
enum Orderstate {Negotiation, Created, Locked, Customs, Recieved, Cancelled}
```

3. The seller inserts the public wallet addresses of the buyer, freight company and customs broker so that the matching of addresses and functions is clear. The seller manages access for participation and setsa number as salt, to make the smart contract more secure.

```python
funtion access(address payable _buyer, address payable _freight, address payable _customs, bytes32 _order_Address, uint256 _salt)public    onlySeller   ---As type we use address payable becuase this allows the addresses to recieve Ether.
```

4. addOrder allows the seller to propose an order, including details such as order address, price and quantity. Since all the data the seller enters into the function are public observable, we use the corresponding hash value with a prefix of 0x because the values are in bytes32. We additionally use salt for added security. 

```python
funtion addOrder(bytes32 _orderAddress, adddress payable 
   _seller, address payable _buyer, bytes32 _priceSeller,
   bytes32 _quantitySeller, uint256 _weight, string memory
   _productname, uint256 _freightrate, uint256
  _orderAmountSeller, uint256 _customsDuty) public
  onlySeller
```

5. If the inputs match, the event OrderConfirmed is activated and leaves a comment for informational purposes. If the buyer's data differ from the seller's, the event OrderCancelled is initiated and the seller can reset the contract's parameters to use it for a new order. 

6. addGuarantee, at this point the financier transfers Ether to the smart contract TradeFinance, a financier is on a first-come, first-served basis. The smart contract escrows the funds and a payout to the various parties following the defined rules. The financier enter the order number again to have a match between the order and guarantee. If all requirements are fulfilled, the two events Guaranteed Active and OrderLocked change the smart contract's state. The following functions can then be excuted and the participating parties informed. 

```python
function addGuarantee(bytes32 _guaranteeAddress, bytes32
   _order Address, address_to) public payable
   ```
   
7. recieveOrderFreight, is used by the freight company to signal that the seller has delivered the goods and to inform the other parties about the shipping details. Entering the order address ensures the right match for each order. When this event has been confirmed the OrderRecievedCustom is actived to change the smart contract's state to Customs, which is a precondition for the next step, the transfer of the fees to the freight company and the order amount to the seller. The contract's balance is checked to make sure it equals the agreed amount as protection against function recalls. 

```python
function receiveOrderCustoms(bytes32 _OrderAddress) public
    inOrderState(OrderState.Locked) onlyCustoms returns (bool)
```



# Digitalization of trade finance processes and real-time collaboration are the key element that can help all the three parties involved i.e. buyers, sellers and banks to conduct trade transactions in a frictionless and timely manner. 

Banks in particular can overcome the trade finance lifecycle and operational challenges faced by imbibing digitial restructing into their trade finance operations such as Artificial Intelligence, Blockchain, Internet of Things and Machine Learning. 

According to the Boston Consulting Group, an integrated digital solution having functions like intelligent automation, collaborative digitization and other advanced technology solutions would help global trade banks save US $2.5-$6Billon with the potential to increse revenue by 20%-35% over 3 to 5 years. 

Banks can deliver a frictionless trade finance experience by - Eliminating the need for manual paperwork, Speed up trade processes, Enhance collaboration with trading counterparties, Automated Workflows, Centralized Trade Finance Operations, Seamless Experience across Multiple Channels, Provide delivery assurance to buyers through trade asset tokenization.

Three key features of Blockchain are instrumental in treating the major pain points of trade finance: 
The Cryptographic security underlying blockchain technology enables information immutability and credibility, the distributed ledger architecture provides transaction transparency and traceability, the network consensus mechanism provides a single source of truth for enabling native issuance of financial assets (trade receivables and other payment obligations can be natively issued in blockchain to reduce fraud and enable banks to offer more attractive financing. 

## References

Alexander Blum (November 18th, 2019) Master Thesis: Blockchain and Trade Finance: A Smart Contract-Based Solution

Riqueza Finolutions Ltd (March 11th,2021), Ploytrade White Paper Shaping the Future of Trade Finance

Cognizant (August 2017) Digital Business, How Blockchain Can Revitalize Trade Finance (Part 1)

Oracle Financial Services (December 11th, 2018), White Paper, Fostering Smarter Trade Finance Operations Digital Engagement in Trade Finance
