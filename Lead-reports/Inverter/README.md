# **Inverter Network Audit Competition on Hats.finance** 

- Prepared by: [Hats.finance](https://hats.finance/)
- Audit Competition: [Inverter](https://www.inverter.network/)
- Lead Auditors: [0xmahdirostami](https://x.com/0xmahdirostami), [Plamen Tsanev](https://x.com/p_tsanev)
- Date: July 16, 2024


## About Hats.finance


Hats.finance builds an autonomous security infrastructure for integration with major DeFi protocols to secure users' assets. 
It aims to be the decentralized choice for Web3 security, offering proactive security mechanisms like decentralized audit competitions and bug bounties. 
The protocol facilitates audit competitions to quickly secure smart contracts by having auditors compete, thereby reducing auditing costs and accelerating submissions. 
This aligns with their mission of fostering a robust, secure, and scalable Web3 ecosystem through decentralized security solutions​.

## About Inverter 

Inverter is a decentralized coordination protocol that enables programmable issuance and asset flow between parties. The protocol is designed to support any project or use case that requires hatching a token economy, and defining the exchange of its resources between participating entities while ensuring openness, adaptability, and ease of use.

## About Hats Audit Competition

Hats Audit Competitions offer a unique and decentralized approach to enhancing the security of web3 projects. Leveraging the large collective expertise of hundreds of skilled auditors, these competitions foster a proactive bug hunting environment to fortify projects before their launch. Unlike traditional security assessments, Hats Audit Competitions operate on a time-based and results-driven model, that ensures that only successful auditors are rewarded for their contributions. This pay-for-results ethos not only allocates budgets more efficiently by paying exclusively for identified vulnerabilities but also retains funds if no issues are discovered. With a streamlined evaluation process, Hats prioritizes quality over quantity by rewarding the first submitter of a vulnerability, thus eliminating duplicate efforts and attracting top talent in web3 auditing. The process embodies Hats Finance's commitment to reducing fees, maintaining project control, and promoting high-quality security assessments, setting a new standard for decentralized security in the web3 space​​.


## Competition Details


- Type: A public audit competition hosted by Inverter Network
- Duration: 15 days
- Prize Pool: 24,000 UMA ~= $70,000 at the time of writing
- Maximum Reward: 5,700 UMA ~= $16,700 for a high severity submission
- Total Submissions: 160
- Valid Submissions: 53
- Total Payout: 24,000 UMA

## Scope of Audit
The scope includes the project's core privileged modules, logic modules, factories and Orchestrator/Module manager.

## Project overview

Inverter is a decentralized coordination solution for various protocols, aimed at creating easily customizable, modular smart contract systems, deployable at a click of a button. At its core, the Inverter Protocol consists of a modular architecture that seamlessly integrates different modules and existing protocols. This modular approach enables developers to create new modules that can be added to the protocol, allowing for an ever-expanding range of use cases and applications.
 
Inverter Protocol is built on the Ethereum Virtual Machine and leverages the latest standards and best practices in smart contract development. The protocol uses EIP-1167-based proxies for deploying new contracts, ensuring a gas-efficient and cost-effective solution. By utilizing these proxies, builders only pay a fraction of the cost of deploying their contracts compared to traditional methods. In addition to its modularity, one of the key benefits of the Inverter Protocol is its focus on security. The protocol comprises audited and community-accepted modules that have been tested, audited, and proven to work. Moreover, the Inverter Protocol follows an open development process, allowing anyone to vet, verify, and contribute to the codebase, further enhancing the protocol's transparency and reliability.

While Inverter was initially conceived as a dynamic funding protocol for projects and contributors with multiple funders, it has evolved to become much more than that. It is now a programmable tokenomic engine that can be used in a wide variety of use cases, from conditioned payment streams over dynamic staking mechanisms to fully-fledged protocols.

A core focus of the Inverter Protocol is to enable the programmable and dynamic issuance and distribution of tokens through Primary Issuance Markets (PIMs). PIMs employ algorithms to dynamically issue tokens based on real-time data and market conditions tailored to meet specific goals and KPIs relevant to each token's custom use case. By focusing on PIMs, the Inverter Protocol aims to drive innovation in tokenizing real-world assets and credit products, unlocking new possibilities for collaborative finance and circular economies.

Inverter Protocol's modular design ensures that each component, from token issuance to utility management, can be customized independently yet interoperate seamlessly. The protocol offers a library of ready-made, upgradable, and interoperable token mechanisms and DeFi integrations, together with an algorithm library for custom pricing algorithms. In addition, our protocol stack will integrate an agent library for verifiable arbitrage agents and a customizable admin panel for streamlined tokenization through configuration, deployment, and operation of token economies.

As the Inverter Protocol continues to evolve, it strives to create a strong and unified ecosystem for token design with its robust infrastructure and open library, making the powers of tokenization accessible to a wide range of applications and industries.


## Audit competition scope

The following files in the directory at https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb are all in scope:

```
src
├── common
│   └── LinkedIdList.sol
├── external
│   ├── fees
│   │   ├── FeeManager_v1.sol
│   │   └── interfaces
│   │       └── IFeeManager_v1.sol
│   ├── forwarder
│   │   └── interfaces
│   │       └── ITransactionForwarder_v1.sol
│   │   └── TransactionForwarder_v1.sol
│   ├── governance
│   │   └── interfaces
│   │       └── IGovernor_v1.sol
│   │   └── Governor_v1.sol
│   └── interfaces
│       └── IERC2771Context.sol
├── factories
│   ├── interfaces
│   │   ├── IModuleFactory_v1.sol
│   │   └── IOrchestratorFactory_v1.sol
│   ├── ModuleFactory_v1.sol
│   └── OrchestratorFactory_v1.sol
├── modules
│   ├── authorizer
│   │   ├── IAuthorizer_v1.sol
│   │   └── extensions
│   │       ├── AUT_EXT_VotingRoles_v1.sol
│   │   └── role
│   │       ├── AUT_Roles_v1.sol
│   │       ├── AUT_TokenGated_Roles_v1.sol
│   │       └── interfaces
│   │           └── IAUT_TokenGated_Roles_v1.sol
│   │           └── IAUT_EXT_VotingRoles_v1.sol
│   ├── base
│   │   ├── IModule_v1.sol
│   │   └── Module_v1.sol
│   ├── fundingManager
│   │   ├── bondingCurve
│   │   │   ├── abstracts
│   │   │   │   ├── BondingCurveBase_v1.sol
│   │   │   │   ├── RedeemingBondingCurveBase_v1.sol
│   │   │   │   ├── VirtualCollateralSupplyBase_v1.sol
│   │   │   │   └── VirtualIssuanceSupplyBase_v1.sol
│   │   │   ├── FM_BC_Bancor_Redeeming_VirtualSupply_v1.sol
│   │   │   ├── FM_BC_Restricted_Bancor_Redeeming_VirtualSupply_v1.sol
│   │   │   ├── FM_BC_Tools.sol
│   │   │   ├── formulas
│   │   │   │   ├── BancorFormula.sol
│   │   │   │   └── Utils.sol
│   │   │   ├── interfaces
│   │   │   │   ├── IBancorFormula.sol
│   │   │   │   ├── IBondingCurveBase_v1.sol
│   │   │   │   ├── IERC20Issuance_v1.sol
│   │   │   │   ├── IFM_BC_Bancor_Redeeming_VirtualSupply_v1.sol
│   │   │   │   ├── IRedeemingBondingCurveBase_v1.sol
│   │   │   │   ├── IVirtualCollateralSupplyBase_v1.sol
│   │   │   │   └── IVirtualIssuanceSupplyBase_v1.sol
│   │   │   └── tokens
│   │   │       └── ERC20Issuance_v1.sol
│   │   ├── IFundingManager_v1.sol
│   │   └── rebasing
│   │       ├── abstracts
│   │       │   ├── ElasticReceiptTokenBase_v1.sol
│   │       │   ├── ElasticReceiptTokenUpgradeable_v1.sol
│   │       │   └── ElasticReceiptToken_v1.sol
│   │       ├── FM_Rebasing_v1.sol
│   │       └── interfaces
│   │           ├── IERC20Metadata.sol
│   │           ├── IERC20.sol
│   │           └── IRebasingERC20.sol
│   ├── lib
│   │   ├── LibMetadata.sol
│   │   └── SafeMath.sol
│   ├── logicModule
│   │   ├── abstracts
│   │   │   ├── ERC20PaymentClientBase_v1.sol
│   │   │   └── oracleIntegrations
│   │   │       └── UMA_OptimisticOracleV3
│   │   │           ├── IOptimisticOracleIntegrator.sol
│   │   │           ├── OptimisticOracleIntegrator.sol
│   │   │           └── optimistic-oracle-v3
│   │   │               ├── AncillaryData.sol
│   │   │               ├── ClaimData.sol
│   │   │               └── interfaces
│   │   │                   ├── OptimisticOracleV3CallbackRecipientInterface.sol
│   │   │                   └── OptimisticOracleV3Interface.sol
│   │   ├── interfaces
│   │   │   ├── IERC20PaymentClientBase_v1.sol
│   │   │   ├── ILM_PC_Bounties_v1.sol
│   │   │   ├── ILM_PC_PaymentRouter_v1.sol
│   │   │   ├── ILM_PC_KPIRewarder_v1.sol
│   │   │   ├── ILM_PC_RecurringPayments_v1.sol
│   │   │   └── ILM_PC_Staking_v1.sol
│   │   ├── LM_PC_Bounties_v1.sol
│   │   ├── LM_PC_PaymentRouter_v1.sol
│   │   ├── LM_PC_KPIRewarder_v1.sol
│   │   ├── LM_PC_RecurringPayments_v1.sol
│   │   └── LM_PC_Staking_v1.sol
│   ├── paymentProcessor
│   │   ├── interfaces
│   │   │   └── IPP_Streaming_v1.sol
│   │   ├── IPaymentProcessor_v1.sol
│   │   ├── PP_Simple_v1.sol
│   │   └── PP_Streaming_v1.sol
├── orchestrator
│   ├── abstracts
│   │   └── ModuleManagerBase_v1.sol
│   ├── interfaces
│   │   ├── IModuleManagerBase_v1.sol
│   │   └── IOrchestrator_v1.sol
│   └── Orchestrator_v1.sol
└── proxies
    ├── interfaces
    │   ├── IInverterBeacon_v1.sol
    │   ├── IInverterProxyAdmin_v1.sol
    │   └── IInverterTransparentUpgradeableProxy_v1.sol
    ├── InverterBeacon_v1.sol
    ├── InverterBeaconProxy_v1.sol
    ├── InverterProxyAdmin_v1.sol
    └── InverterTransparentUpgradeableProxy_v1.sol
```
 
## ISSUES
### Medium severity issues
- **Reorg issues in factories lead to loss of funds for users**

As the protocol plan to deploy on Polygon, where reorgs are common occurence and happen with an average depth of 15-20 per day, it is very important to be careful for reorg specific issues. Protocol is using factories to depoloy orchestrators and modules. Those factories are using create optoce for this action, which only consider factory nonce. This is very dangerous especially because deployed modules may hold funds -> deposit, which may lead to users loosing those. If a user deploy an orchestrator with a funding manager module, then deposit some funds to the funding manager in different transaction and reorg occur, this can lead to his funds being stolen.

**Link:** [Issue #18](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/18)

**Auditor:** Unknown

- **User may lost assets by depositing at FM_Rebasing_v1 funding manager**

orcehstrator can transfer assets from funding manager, so it's nessecirily to rebase user balances after every transfer ( updating _bitsPerToken ), it happes via _rebase function before every mint or burn, if supply target is zero _rebase wouldn't update _bitsPerToken and simply returns, since it's viable to have active bits but no supply target it leads to loss for new depositor, for example we have 1000 active bits + 500 supply target, in this case _bitsPerTokens would be 2, orchestrator transfers out 500 assets from funding manager and making supply target 0, now if a user tries to deposit, _rebase won't update _bitsPerTokens and it remains 2, after deposing if he decides to redeem he would receive less tokens since _bitsPerTokens would be updated before burn, part of deposited assets has been distributed between other users.

**Link:** [Issue #38](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/38)

**Auditor:** [MehdiKarimi](https://github.com/MehdiKarimi81)

- **Any module can drain the FundingManager of all funding tokens**

This vulnerability arises from two weaknesses in the system: 1) Every module has the same permission as the orchestrator owner, allowing any module to execute transactions via executeTxFromModule(), which should be restricted. 2) The funding manager's onlyOrchestrator access control is flawed, as it only checks if the msg.sender is the orchestrator, not the owner. This allows any module to exploit the funding manager's transferOrchestratorToken() function by calling executeTxFromModule(), bypassing access controls. The recommended fix is to use onlyOrchestratorOwner() for critical functions and remove onlyOrchestrator() to prevent similar issues.

**Link:** [Issue #50](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/50)

**Auditor:** [0xfuje](https://x.com/0xfuje)

- **User won't be able to get back their staked USDC/USDT token if their address is blacklisted in LM_PC_Staking_v1.sol**

The LM_PC_Staking_v1 contract allows users to stake tokens for rewards. If a user stakes USDC and their address gets blacklisted by the USDC admin, they won't be able to unstake and retrieve their tokens. The transfer attempt by LM_PC_Staking_v1 will fail due to the USDC transfer function's blacklisted check, preventing the user from reclaiming their staked tokens. This issue arises because the contract does not account for the potential blacklisting of addresses by tokens like USDC, which has a blacklist() function. The impact is significant, as blacklisted users are unable to recover their staked assets.

**Link:** [Issue #54](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/54)

**Auditor:** [0xRizwan](https://x.com/0xRizwan)

- **If InverterTransparentUpgradeableProxy_v1 won't not be affected by shut down implementation**

The protocol uses a beacon proxy pattern to deploy new modules, offering two types of proxies: InverterBeaconProxy_v1 and InverterTransparentUpgradeableProxy_v1. The former dynamically reads the implementation address from the beacon, while the latter sets the implementation at construction and reads it from storage. This design flaw means that if a beacon is shut down due to a security issue, only modules using InverterBeaconProxy_v1 will be affected, leaving those using InverterTransparentUpgradeableProxy_v1 vulnerable because they can't update to address(0) without reverting due to implementation checks. This creates a risk where compromised modules can't be effectively shut down. The proposed solution includes implementing a shutdown status mapping in the beacon and modifying InverterTransparentUpgradeableProxy_v1 to check this status dynamically.

**Link:** [Issue #55](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/55)

**Auditor:** [nmirchev8](https://x.com/nmirchev8)

- **LM_PC_KPIRewarder_v1.sol#assertionResolvedCallback() - LM_PC_KPIRewarder_v1 can be set as a callback address to another assertion in order to set assertionPending = false**

The `assertionResolvedCallback` function in the `LM_PC_KPIRewarder_v1` contract is vulnerable because it doesn't verify the existence of the provided `assertionId`. This allows an attacker to exploit the contract by setting the `callbackRecipient` to `LM_PC_KPIRewarder_v1` for an assertion that it did not create. The attacker can then resolve the assertion falsely, triggering the `assertionResolvedCallback` and bypassing the `assertionPending` check, allowing new assertions to be posted prematurely. This can lead to queued stakers receiving rewards incorrectly. The solution is to verify the existence of `assertionId` before processing it.

**Link:** [Issue #65](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/65)

**Auditor:** [EgisSec](https://x.com/EgisSec)

- **LM_PC_Staking_v1 can be used for pyramid scheme, because it is using current stakers funds to reward others**

The `LM_PC_Staking_v1` contract, inheriting from `ERC20PaymentClientBase_v1`, incorrectly handles staking funds, allowing a potential exploit. In this scenario, staked funds from users are used to incentivize other stakers. If a malicious party sets a high reward rate, it can attract users to stake their funds, creating a pyramid scheme. As users interact with the contract, rewards are processed and distributed using other stakers' funds. This can lead to a "pull-rug" situation where the last stakers are unable to retrieve their funds once the contract's balance is depleted. The proposed mitigation is to override the `_ensureTokenBalance` function in `LM_PC_Staking_v1` to ensure that only the funds provided by the funding manager are used for rewards, preventing staked funds from being used to incentivize others. This can be done by adjusting the current funds calculation to exclude the total staked amount:

```solidity
uint currentFunds = IERC20(token).balanceOf(address(this)) - totalSupply;
if (currentFunds < amount) {
    // Always withdraw reward funds from the funding manager
    ...
}
```

**Link:** [Issue #70](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/70)

**Auditor:** [EgisSec](https://x.com/EgisSec)

- **LM_PC_KPIRewarder_v1 if bond token has a blocklist and disputer set disputer address to a blocked address, result in DoS**

In LM_PC_KPIRewarder_v1 an asserter creates assertation to UMA oracle posting KPI data. UMA oracle accepts bond in different currencies, which is used to incertivies disputers and asserters to tell the truth. This defaultCurrency can be USDC/USDT, both of which has a blocklist functionality. The problem here is that if by any chance/mistake asserter has posted wrong info, untrusted diputer is able to dispute the assertation and provide arbitrary address as disputer. This address later recieves the bond reward, if dispute has been successful. The following would result in DoS of UMA settleAssertion function, which result in unreachability of LM_PC_KPIRewarder_v1::assertionResolvedCallback and so the whole LM_PC_KPIRewarder_v1 logic, because it would be impossible to create new assertions, before we have set assertionPending to false.

**Link:** [Issue #75](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/75)

**Auditor:** [EgisSec](https://x.com/EgisSec)

- **Admin Can Bypass Checks for Privileged Modules**

When an admin wants to add a new module to the orchestrator, if the module is IFundingManager_v1, IAuthorizer_v1, or IPaymentProcessor_v1, it must pass _enforcePrivilegedModuleInterfaceCheck and an additional check. The issue here is that the admin can bypass these checks.

**Link:** [Issue #77](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/77)

**Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **Admin Can Bypass Important Checks and Timelock Mechanism**

The admin can bypass _enforcePrivilegedModuleInterfaceCheck checks and other important checks and Timelock. The issue arises because executeSetAuthorizer, executeSetFundingManager, and executeSetPaymentProcessor do not verify that the provided address matches the one specified in initiateSetAuthorizerWithTimelock, initiateSetFundingManagerWithTimelock, and initiateSetPaymentProcessorWithTimelock.

**Link:** [Issue #78](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/78)

**Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **LM_PC_Bounties_v1::contributorsNotChangedcheck is not enough, could result in CLAIMANT adding additional contributors in the last minute**

The `LM_PC_Bounties_v1` contract has a vulnerability where the length of the `contributors` array provided by the verifier is not checked against the length of `_claimRegistry[claimId].contributors`. This allows a claimant to add new contributors to the end of the array before the verifier calls `verifyClaim`, resulting in unintended additional payments. In an attack scenario, a bounty program is active, with roles assigned for transparency. The claimant sets `_claimRegistry[claimId].contributors` to a list of five developers, each entitled to 1000 USDC, with a maximum bounty of 10,000 USDC. The verifier intends to pay the five developers and calls `verifyClaim` with their addresses and amounts (1000 USDC each). The claimant then updates `_claimRegistry[claimId].contributors` by adding their own address with a reward of 5000 USDC just before the verifier's transaction. The `contributorsNotChanged` function only checks up to the fifth element and does not verify the array length, passing the check. Consequently, the claimant receives an additional, unauthorized 5000 USDC.

**Link:** [Issue #82](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/82)

**Auditor:** [EgisSec](https://x.com/EgisSec)

- **PP_Streaming_v1.sol#_findAddressInActiveStreams() - activePaymentReceivers can become so large that it's impossible to process more payments, effectively bricking the processor**

The `PP_Streaming_v1` contract, used for payment processing through streams, keeps track of active payment receivers in the `activePaymentReceivers` mapping. This mapping is updated in the `_addPayment` function, which checks if a receiver is already active using `_findAddressInActiveStreams`. However, there is no limit to how large the `activePaymentReceivers[client]` array can grow, introducing a vulnerability. A malicious user can exploit this by creating a massive array of bogus streams, particularly through the `LM_PC_Staking_v1` contract, which allows any address to stake and claim rewards.

**Link:** [Issue #85](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/85)

**Auditor:** [EgisSec](https://x.com/EgisSec)

- **Payment Processors treat calls to non-contracts as a successful transfer calls**

The contracts PP_Simple_v1.sol and PP_Streaming_v1.sol contain raw calls to a token contract at lines 126 and 726, respectively. These raw calls can be problematic because if the token_ address is not a contract, the call will return true, falsely indicating a successful transfer. The line in the code that checks for success will pass, leading to the erroneous emission of the TokensReleased event and notifying the client that the tokens were paid, even though they were not. This issue creates an opportunity for phishing attacks due to the incorrect flow of code execution and the emission of the TokensReleased event, which could involve token addresses that are not yet deployed, such as those using create2 or LP tokens for undeployed pools of new tokens. As a result, the contract will incorrectly notify the client that the tokens were paid when they were not, potentially misleading users. Given the modular nature of the project, this code implies that hidden checks (e.g., verifying if the token is a contract) are necessary elsewhere in the system. The successful transfer flow is executed instead of failing the call, which might cause issues when integrating new modules with the current ones. This hidden dependency on the token being a contract could lead to unexpected behaviors and errors in the system. To address these problems, it's crucial to explicitly check whether the token_ address is a contract before attempting the raw call. By adding this check, you ensure that the token_ address is a contract before making the transfer, mitigating the risk of phishing attacks and integration issues.

**Link:** [Issue #118](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/118)

**Auditor:** Unknown

- **FM_Rebasing_v1 is vounerable to just in time liquidity**

The FM_Rebasing_v1 contract is vulnerable to Just-In-Time (JIT) liquidity attacks. Users can exploit this by front-running transactions that increase the bit value by depositing large amounts of assets just before the increase and then withdrawing them immediately after. This allows them to extract a portion of the rewards without any risk. 

For example, if there are 5,000 tokens in the rebasing vault with a bit-to-token ratio of 10, and the protocol sends an additional 1,000 tokens (20%) to the vault, a malicious user can see this transaction and front-run it by depositing 5,000 tokens, thereby owning 50% of the pool. After the 1,000 token increase, the new bit ratio will be 11. The malicious user can then withdraw their bits, claiming 50% of the tokens, which amounts to 5,500 tokens. In this scenario, the user has profited from 50% of the rewards that should have been distributed to active depositors. While real scenarios might not involve such large profits, the vulnerability still allows parts of the value increase to be exploited by malicious users using Miner Extractable Value (MEV) techniques.

**Link:** [Issue #128](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/128)

**Auditor:** [0x3b33](https://x.com/0x3b33)

- **FM_BC_Bancor_Redeeming_VirtualSupply_v1.setReserveRatioForSelling vulnerable to MEV**

FM_BC_Bancor_Redeeming_VirtualSupply_v1.setReserveRatioForSelling is susceptible to MEV attack if an attacker notices a reduction in the reserverRatioForSelling they could front run the transaction using a Flashloan to place a buy before the transaction and immediadetly sell after the transaction realising a profit in one transaction batch.

**Link:** [Issue #131](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/131)

**Auditor:** [rnemes4](https://x.com/rnemes4)

- **Sandwich attacks can empty FundingManager upon owner set virtual supply changes**

The problem is that the FundingManager's balance does not necessarily reflect it's virtual collateral and issuance supply. When these values are changed without organic buy and sell orders via setVirtualCollateralSupply() or setVirtualIssuanceSupply(), the total amount of change can be sandwiched risk-free by an attacker.

**Link:** [Issue #155](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/155)

**Auditor:** [0xfuje](https://x.com/0xfuje)

### Low severity issues

- **Anyone can initialize OrchestratorFactory_v1.sol and ModuleFactory_v1.sol implementation contracts**

OrchestratorFactory_v1.sol and ModuleFactory.sol are missing
_disableInitializers() call in the constructor. An implementation contract can be taken over by an attacker with calling the init function which may cause unexpected functionality (it is very dangerous with delegatecalls).

**Link:** [Issue #8](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/8)

**Auditor:** [0xfuje](https://x.com/0xfuje)

- **use safeTransfer instead of just transfer**

Failed transfers are not handled. Using safeTransfer instead of just transfer is prone to issues where some tomes return false instead of reverting. So this is an issue for all the collateral tokens that return false instead of reverting when transferring tokens.

**Link:** [Issue #10](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/10)

**Auditor:** Unknown

- **_ensureValidPaymentOrder missing start and end range check**

In PaymentClientBase, the PaymentOrder struct contains recipient, paymentToken, amount, start, cliff, and end fields. However, the validPaymentOrder modifier only checks recipient, token, and amount fields, omitting the crucial check that ensures the end timestamp is greater than or equal to the start timestamp. This oversight could lead to invalid payment orders with incorrect timelines being processed.

**Link:** [Issue #16](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/16)

**Auditor:** Unknown

- **Signature Malleability on ElasticReceiptTokenBase_v1.permit**

Using EVM's `ecrecover` is prone to signature malleability issues, and it is recommended to use `ECDSA.recover` from the OpenZeppelin library, which validates the `v` and `s` values of signatures. OpenZeppelin documents how `ecrecover` can result in malleable signatures and provides the `ECDSA.tryRecover` function to counter this by ensuring `s` values are in the lower half order and `v` values are either 27 or 28. 

In the `ERC20Permit.permit` function from OpenZeppelin, signatures are recovered using `ECDSA.recover`, which includes these validations. However, in the `ElasticReceiptTokenBase_v1.sol` file, the `permit` function uses `ecrecover` without additional validation. To enhance security and avoid signature malleability, it is recommended to replace the `ecrecover` usage with `ECDSA.recover` from the OpenZeppelin library. This change will ensure that only unique, non-malleable signatures are processed, reducing the risk of potential attacks.

**Link:** [Issue #17](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/17)

**Auditor:** Unknown

- **In BondingCurveFundingManagerBase consider minBuyAmount, because user can buy dust amounts to skip paying fee**

The vulnerability in the `BondingCurveFundingManagerBase` contract arises from the way transaction fees are calculated, particularly through integer division which can round down to zero for small transaction amounts. For instance, if the fee is set at 2% and the attacker repeatedly performs transactions of 49 tokens, the calculated fee can round down to zero due to integer truncation. This allows the attacker to avoid paying any fees while still buying tokens. On L2 chains where transaction costs are low, this exploitation can be especially profitable because the attacker can repeatedly make small transactions without incurring significant expenses. Over time, this could enable the attacker to accumulate a large amount of tokens without contributing to the protocol’s fee revenue, thereby undermining the economic model and potentially destabilizing the protocol. To mitigate this, it's crucial to ensure that fee calculations include checks to prevent fees from rounding down to zero and to consider implementing a minimum fee threshold to ensure all transactions contribute to the fee structure.

**Link:** [Issue #22](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/22)

**Auditor:** Unknown

- **Missing event emission in AUT_EXT_VotingRoles_v1.sol::castVote.**

The function AUT_EXT_VotingRoles_v1.sol::castVote is missing event emission. Emitting events when these actions occur is essential for transparency and informing users about important changes. Adding events for these functions will provide users with a clear record of when the votes has been casted.

**Link:** [Issue #27](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/27)

**Auditor:** [0xEricTee](https://x.com/0xEricTee)

- **Incorrect time check in src/modules/paymentProcessor/PP_Streaming_v1.sol::validTimes**

The `validTimes` function in `PP_Streaming_v1.sol` contains a critical implementation error in its time validation logic. It currently uses the logical `&&` operator when it should use the `||` operator to properly validate the start, cliff, and end times of a payment stream. This error means that certain invalid time conditions are incorrectly evaluated as valid. Specifically, if the start time is greater than or equal to the maximum value for a `uint` and the sum of the start time and cliff period is greater than the end time, this condition should trigger a validation failure. However, due to the incorrect use of the `&&` operator, the function may incorrectly validate some invalid time configurations as correct. This can lead to the protocol accepting streams with impossible or nonsensical time settings, potentially causing operational issues such as erroneous payment schedules or unexpected states within the protocol, which could be exploited to disrupt or manipulate the intended functionality of the streaming payments.

**Link:** [Issue #53](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/53)

**Auditor:** [0xEricTee](https://x.com/0xEricTee)

- **DoS in initiateSetFundingManagerWithTimelock, initiateSetAuthorizerWithTimelock, initiateSetPaymentProcessorWithTimelock Due to Module Limit**

The initiateSetFundingManagerWithTimelock, initiateSetAuthorizerWithTimelock, and initiateSetPaymentProcessorWithTimelock functions add a new module and remove the old module without changing the length of the modules. However, if the modules length has reached the maximum limit, these functions will revert. The owner would then need to remove a module first to replace these modules, which introduces a delay due to the additional timelock required for the module removal.

**Link:** [Issue #56](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/56)

**Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **Inadequate Module Limit Check in moduleLimitNotExceeded**

The moduleLimitNotExceeded function currently checks only the number of existing modules but does not account for modules that are pending addition. This oversight can allow the owner to initiate multiple initiateAddModuleWithTimelock calls, potentially bypassing the module limit.

**Link:** [Issue #57](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/57)

**Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **Duplicate Module Titles Cause Incorrect Module Address Retrieval**

When adding a new module to the orchestrator, the system does not check whether a module with the same title already exists. This can lead to duplicate module titles, which can result in incorrect values being returned by the _isModuleUsedInOrchestrator function.

**Link:** [Issue #58](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/58)

**Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **getStaticPriceForBuying() - potential precision loss due to supported ERC20's decimals**

The view function for retrieving the static price for buying, meant to be called from the UI, is susceptible to precision loss due to decimal differences between the tokens. This impacts only the view function, thus the off-chain monitoring, as the price can get rounded down to 0, while it is actually not on-chain.

**Link:** [Issue #59](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/59)

**Auditor:** [@p_tsanev](https://x.com/p_tsanev)

- **Unauthorized access to `Governor_v1.acceptOwnership()` function which breaks protocol intended design**

Due to an incorrectly used modifier, the team multi-sig address is able to accept new ownership of the contract. This is not critical, but not intended either, as only the community multi-sig is supposed to accept the proposed owner in the 2 step process. 

**Link:** [Issue #60](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/60)

**Auditor:** [0xRizwann](https://x.com/0xRizwan)

- **_buyOrder() - Computes function selector incorrectly**

Due to the misuse of `uint` during function selector calculation inside `_getFunctionFeesAndTreasuryAddresses `, a wrong fee amount will be returned and paid.

**Link:** [Issue #61](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/61)

**Auditor:** [EgisSec](https://x.com/EgisSec)

- **postAssertion() - Protocol assumes that asserter pays for the bond, but he doesn't**

The issue arises due to the fact that the code and comments assume that the passed asserter address pays for the bond. However the function did not check the asserter and made the sender of the message pay for the bond, breaking the above assumption and intention.

**Auditor:** [EgisSec](https://x.com/EgisSec)

**Link:** [Issue #64](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/64)

- **Complete takeover of AUT_EXT_VotingRoles_v1 due to low threshold allowed**

The Orchestrator's voting module allows and edge-case scenario where there is no voter threshold. This opens up the possibility of executing any motion from any voter, potentially creating negative impact on the other modules like stealing funds, bricking, etc.

**Auditor:** [0xfuje](https://x.com/0xfuje)

**Link:** [Issue #67](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/67)

- **OptimisticOracleIntegrator doesn't add IOptimisticOracleIntegrator/OptimisticOracleV3CallbackRecipientInterface interfaceId as supported interfaces**

While the contract is meant to follow ERC165, it breaks compatibility by not implementing a check for the interface id's, which could have impact on external integrations

**Auditor:** [EgisSec](https://x.com/EgisSec)

**Link:** [Issue #74](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/74)

- **Upgradeable contracts pattern is corruptible for some contracts**

Due to a missing storage gap variable in multiple upgradable contracts, during updates storage collisions could occur.

**Auditor:** [0xRizwan](https://x.com/0xRizwan)

**Link:** [Issue #84](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/84)

- **Orchestrator_v1.sol#initiateAddModuleWithTimelock() - indefinite amounts of privileged modules can be added**

The function for adding new logic modules is flawed, due to it missing checks for the added module. It can be a privileged module, passed as a logic one as they share the same interface, breaking the protocol invariant of having only 1 of each privileged modules.

**Link:** [Issue #86](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/86)

**Auditor:** [p_tsanev](https://x.com/p_tsanev)

- **`indexed` keyword in Events Causes Data Loss for Dynamic Array Variables**

When the `indexed` keyword is used for reference type variables, it will return the hash of the mentioned variables.
Thus, the event would emit a meaningless and obscure 32 bytes, confusing monitoring.

**Link:** [Issue #91](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/91)

**Auditor:** [0xEricTee](https://x.com/0xEricTee)

- **transferOrchestratorToken() - The function doesn't take into account `projectCollateralFeeCollected` when the function is called**

Due to a missing check for the currently accrued workflow fee, the `transferOrchestratorToken()` might transfer out those reserved fees to the modules instead. Thus the protocol receives less fees than supposed to.

**Link:** [Issue #101](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/101)

**Auditor:** [EgisSec](https://x.com/EgisSec)

- **`ElasticReceiptTokenBase_v1` is supposed to be compatible with ERC2771, but it isn't**

While the protocol and contract are supposed to be compatible with meta transactions, it invokes `msg.sender` instead of `_msgSender()`, breaking compatibility

**Link:** [Issue #104](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/104)

**Auditor:** [EgisSec](https://x.com/EgisSec)

- **New Modules with Updated Major Versions Do Not Remove Previous Versions**

Adding new modules with new major versions does not delete previous ones, allowing new users to use outdated versions. This could lead to incompatibility issues and security vulnerabilities as users might inadvertently use outdated and potentially flawed versions of the module.

**Link:** [Issue #108](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/108)

**Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **Attacker could abuse victim's vote to pass their own proposal**

Due to re-org possibilities and transaction ordering, proposal ids could get messed up as they only get incremented by 1 with each proposal, instead of being hashed with the sender's address.

**Link:** [Issue #117](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/117)

**Auditor:** Unknown

- **Reentrancy Vulnerability in `PP_Streaming_v1::claimPreviouslyUnclaimable` Results in Temporary Lock of Funds**

The `claimPreviouslyUnclaimable` function in first transfers tokens to the receiver and then calls the `amountPaid` function on the client. This introduces a reentrancy issue where the user can reenter the contract before `_outstandingTokenAmounts` is reduced in the amountPaid function.

**Link:** [Issue #119](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/119)

**Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **Rounding issue in rewards calculation in `LM_PC_KPIRewarder_v1.sol::assertionResolvedCallback`**

`rewardAmount += achievedReward * (trancheRewardValue / trancheEnd)` contains curly braces, that means if `trancheRewardValue < trancheEnd`, the value will be rounded down to zero. As a result, the rewards will be lost.

**Link:** [Issue #120](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/120)

**Auditor:** [0xEricTee](https://x.com/0xEricTee)

- **User can brick both staking contracts if he is first staker**

There are some tokens like cUSDCv3 that have a special case in their transfer logic. If the amount specified is type(uint256).max then the entire balance of the source will be transferred. This allows for the first depositor in both contracts to completely brick the contracts, as in both cases if another user stakes, a value will overflow, reverting the transaction.

**Link:** [Issue #126](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/126)

**Auditor:** [EgisSec](https://x.com/EgisSec)

- **Incorrect dev comment FM_BC_Bancor_Redeeming_VirtualSupply_v1**

Incorrect dev comment in relation to the maximum `_depositAmount` could be misleading.

**Link:** [Issue #132](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/132)

**Auditor:** [rnemes4](https://x.com/rnemes4)

- **Attacker can consume victim `TransactionForwarder_v1` nonce, but force the tx to revert**

OZ's EIP2771 implementation for multicall support opens the possibility for a malicious party to use a viticm's nonce, no matter if the corresponding tx succeeded, or not. When submitter transaction hit execution, it will revert, because the nonce has been already used.

**Link:** [Issue #133](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/133)

**Auditor:** [EgisSec](https://x.com/EgisSec)

- **`minimumStake` Check in stake Function Prevents Existing Users from Adding Smaller Amounts**

The stake function implements a `minimumStake` check to prevent anyone from filling the `stakingQueue` with small amounts. However, the issue arises when users who are already in the `stakingQueue` want to add a new amount that is lower than `minimumStake`. This check unnecessarily restricts existing users from staking additional smaller amounts.

**Link:** [Issue #136](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/136)

**Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **Missing Deadline Checks Allow Pending Transactions to be Maliciously Executed**

There are multiple functions in the contract that lack deadline checks, potentially causing issues. For example, although the `buyFor` and `sellFor` functions implement `_minAmountOut` checks, the absence of a deadline check in these functions can result in a loss of funds for the user.

**Link:** [Issue #137](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/58)

**Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **FM_BC_Bancor_Redeeming_VirtualSupply_v1 may get initialised in a way that will brick the contract**

It is possible to initialize with a mathematical combination of Issuance token decimals and initial issuance supply that will leave the contract in a state where it is impossible to call the buy function without it reverting.

**Link:** [Issue #139](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/139)

**Auditor:** [rnemes4](https://x.com/rnemes4)

- **Event emitted even when assertion is not resolved truthfully**

`OptimisticOracleIntegrator::assertionResolvedCallback(...)` is called by Optimistic Oracle V3 when an assertion is resolved. However, according to the UMA docs, the `DataAssertionResolved(...)` event is supposed to be emmited ONLY when the assertion was resolved truthfully but the implementation of `OptimisticOracleIntegrator::assertionResolvedCallback(...)` emits this event whether or not the assertion was `true`.

**Link:** [Issue #148](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/148)

**Auditor:** [audinarey](https://x.com/Audinarey)

- **Users can receive zero issuance or collateral tokens via buy or sell orders in FundingManager**

Users can lose expected value when BancorFormula returns zero: this can happen when issuance or collateral token supply is magnitudes bigger than the other or upon owner set virtual supply changes or when the user's amount is a lot smaller than the total supply

**Link:** [Issue #157](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/157)

**Auditor:** [0xfuje](https://x.com/0xfuje)

- **Floating Pragma in non-interface files can be potential security risk**

Majority of the soldiity files in the codebase are defined with concrete 0.8.23 version, but still there are these non-inteface files that have unspecific compiler versions in their pragma definitions

**Link:** [Issue #158](https://github.com/hats-finance/Inverter-Network-0xe47e52c4fea05e555920f1dcdcc6fb8eca103eeb/issues/158)

**Auditor:** [0xghost](https://x.com/imaybeghost)

## Systematic and Centralization risks

The architecture of the Inverter Network codebase is entirely modular, meant to be connectable through it's respective Orchestrator/Module Manager and are managed using upgradable contracts.
During the contest, there have been several OOS issues, regarding concerns about the power of the contract's orchestrator, orchestrator owner, "trusted" module roles, sustainability of the intertwined upgradable contracts as well as potential concerns when upgrading crucial module contracts like the AUT, FM, PP:
• Orchestrator owners have full control over the funds of the users and control over which modules are added, removed, what fees are paid, who receives those fee, upgrading the contracts (which is partially split to an independent admin). This is intended design and users should be aware of the power the respective protocol's orchestrator owner possesses and should be aware.
• Privileged module roles - Claimer, Verifier, Bounty_issuer, Asserter, Voters, possess special permissions and should be trusted to execute their respective functions non-maliciously. However users should be wary of the entities behind these roles, as they control the logic modules correct functioning.
• Upgrading core modules and replacing modules inside an Orchestrator contract should be carefully done as different module versions could conflict each other or impact unexpected parts of the system that rely heavily on the changed module 
 
## Conclusion

The audit competition for the Inverter protocol on the Hats.finance platform revealed 35 lows and 16 Mediums severity issues. The audit involved a comprehensive examination of numerous aspects of Inverter's code, such as reward distribution, staking functionality, access contorols, modules, and more. Each identified issue was acknowledged and accompanied by a proposed solution for resolving the problem. 


## Disclaimer

This report does not assert that the audited contracts are completely secure. Continuous review and comprehensive testing are advised before deploying critical smart contracts.
The Inverter audit competition illustrates the collaborative effort in identifying and rectifying potential vulnerabilities, enhancing the overall security and functionality of the platform.
Hats.finance does not provide any guarantee or warranty regarding the security of this project. Smart contract software should be used at the sole risk and responsibility of users.

This report was written with the help of lead auditor [Plamen Tsanev](https://x.com/p_tsanev) and [0xmahdirostami](https://x.com/0xmahdirostami).
