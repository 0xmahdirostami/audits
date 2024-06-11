# **Kintsu Audit Competition on Hats.finance** 

- Prepared by: [Hats.finance](https://Hats.finance)
- Audit Competition: [Kintsu](https://kintsu.xyz/)
- Lead Auditors: [0xmahdirostami](https://x.com/0xmahdirostami)
- Date: May 16, 2024

## About Hats.finance

Hats.finance builds autonomous security infrastructure for integration with major DeFi protocols to secure users' assets. 
It aims to be the decentralized choice for Web3 security, offering proactive security mechanisms like decentralized audit competitions and bug bounties. 
The protocol facilitates audit competitions to quickly secure smart contracts by having auditors compete, thereby reducing auditing costs and accelerating submissions. 
This aligns with their mission of fostering a robust, secure, and scalable Web3 ecosystem through decentralized security solutions​.

## About Kintsu

Kintsu is a Liquid Staking Protocol. Kintsu mission is to boost the GDP of Proof-of-Stake blockchains by allowing users to participate in on-chain activities while also benefitting from the yield-bearing staking that secures the blockchain. Kintsu solves a number of challenges faced by Proof-of-Stake blockchains around liquidity, accessibility, and more.

## About Hats Audit Competition

Hats Audit Competitions offer a unique and decentralized approach to enhancing the security of web3 projects. Leveraging the large collective expertise of hundreds of skilled auditors, these competitions foster a proactive bug hunting environment to fortify projects before their launch. Unlike traditional security assessments, Hats Audit Competitions operate on a time-based and results-driven model, that ensures that only successful auditors are rewarded for their contributions. This pay-for-results ethos not only allocates budgets more efficiently by paying exclusively for identified vulnerabilities but also retains funds if no issues are discovered. With a streamlined evaluation process, Hats prioritizes quality over quantity by rewarding the first submitter of a vulnerability, thus eliminating duplicate efforts and attracting top talent in web3 auditing. The process embodies Hats Finance's commitment to reducing fees, maintaining project control, and promoting high-quality security assessments, setting a new standard for decentralized security in the web3 space​​.

## Competition Details

- Type: A public audit competition hosted by Kintsu
- Duration: 14 days
- Prize Pool: $40,000
- Maximum Reward: $12,800 for a high severity submission
- Total Submissions: 64
- Valid Submissions: 15
- Total Payout: $40,000 distributed.
- competition link: [link](https://app.hats.finance/audit-competitions/kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/rewards)
  
## Severity levels

- **High:**
Issues that lead to the loss of user funds. Such issues include:
	- Direct theft of any user funds, whether at rest or in motion.
	- Long-term freezing of user funds.
	Theft or long term freezing of unclaimed yield or other assets.
	- Protocol insolvency
- **Medium:**
  Issues that lead to an economic loss but do not lead to direct loss of on-chain assets. Examples are:
	- Gas griefing attacks (make users overpay for gas)
	- Attacks that make essential functionality of the contracts temporarily unusable or inaccessible.
	- Short-term freezing of user funds.
- **Low:**
  Issues where the behavior of the contracts differs from the intended behavior (as described in the docs and by common sense), but no funds are at risk.

## Overview

| Project Name |                                               Kintsu                                                |
| :----------: | :---------------------------------------------------------------------------------------------------: |
|  Repository  |                         [Link](https://github.com/WaterCoolerStudiosInc/kintsu-contracts/)                         |
| Commit Hash  | [29dbb0d](https://github.com/WaterCoolerStudiosInc/kintsu-contracts/tree/29dbb0da84780cc2a6a8ec37d90ee518bc18102c) |
|     Docs     |              [Link](https://docs.kintsu.xyz/gitbook/networks/aleph-zero)               |
|   Methods    |                                             Manual Review                                             |

### Scope

|     File      |
| :-----------: |
| nomination_agent|
| registry |
| share_token |
| vault |

### Compatibilities

- Chain(s) to deploy contract to: AlephZero

### Known Issues

None

### Issues found

|   Severity    | Count |
| :-----------: | :---: |
|     High      |   1   |
|    Medium     |   7   |
|      Low      |   7   |

## High severity issues

- **Malicious users can prevent other users from redeeming rewards by manipulating total_pooled with duplicate withdrawal requests**

  Users who stake AZERO must call `request_unlock` to start withdrawing their stakes. After a waiting period, they call `send_batch_unlock_requests` to move their tokens to a vault, and then call `redeem`. The contract checks if a `batch_id` has been unlocked already and stops if it has. However, users can send the same `batch_id` multiple times, causing the `total_pooled` amount to decrease incorrectly. This can bring `total_pooled` close to zero, making future `send_batch_unlock_requests` calls fail and preventing users from withdrawing their tokens.

  **Link**: [Issue #28](https://github.com/hats-finance/Kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/issues/28)

  **Auditor:** [krikoeth](https://x.com/krikoeth)

## Medium severity issues

- **Inconsistency in Nomination Pool Joining Logic**

  The nomination_pools module uses the staked variable to determine whether an agent can join a nomination pool. However, the reduction of self.staked occurs in the start_unbond function, not in the withdraw_unbonded function. This leads to an inconsistency where an agent may attempt to rejoin a pool after being unbonded but not withdrawn(the agent reaped in the withdrawn step, not the unbound step), causing a potential denial-of-service (DOS) vulnerability in the stake function.

  **Link**: [Issue #29](https://github.com/hats-finance/Kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/issues/29)

  **Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **Potential DOS in delegate_compound Function**

  The delegate_compound function iterates over all agents and calls compound on them. However, if there is a revert in one of the agents' compound calls, the entire compound function will revert. The nomination_agent::compound function might revert if an agent has not yet joined the nomination pool or has already reaped from it.

  **Link**: [Issue #30](https://github.com/hats-finance/Kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/issues/30)

  **Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **Minimum Stake Not Checked for Each Nomination Agent**

  The minimum stake for a nomination pool is 10 AZERO, and the contract checks this amount. However, it should check the minimum stake for each agent individually, not just the total stake. Without this check, the stake function can fail if the amounts split between agents fall below 10 AZERO per agent, causing a Denial of Service (DoS) scenario.

  **Link**: [Issue #48](https://github.com/hats-finance/Kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/issues/48)

  **Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **GasToken(AZERO) might be stuck in nomination_agent contract when the pool is in destroy mode**

  When a nomination pool is in destroy mode and someone other than the depositor calls `nomination-pools.withdraw_unbonded`, GasToken (AZERO) is sent to `nomination_agent`. If the vault doesn't call `nomination_agent.withdraw_unbonded` before this, the GasToken won't transfer to the vault, as `withdrawn = after - before` would result in zero.

  **Link**: [Issue #50](https://github.com/hats-finance/Kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/issues/50)

  **Auditor:** Unknown

- **Nomination Agents Linked to Pools in Destroying or Blocked State Cause Revert in Compound and Stake Functions**

  Nomination agents that are linked to pools in a destroying or blocked state will cause the compound and stake functions to revert. This is because any attempt to bond extra or join these pools will fail.

  **Link**: [Issue #51](https://github.com/hats-finance/Kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/issues/51)

  **Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **Dos in send_batch_unlock_requests function due to invalid range for agent's boned AZERO**

  In the current implementation, agents must either unbond entirely or maintain at least the minimum required bond (minimum_stake) after the unbond function. However, the delegate_unbonding function does not consider this requirement. If one agent reverts in the unbond function, it causes a revert in send_batch_unlock_requests, leading to a denial of service (DoS) due to incorrect calculations. If send_batch_unlock_requests tries to unbond an amount resulting in an agent's stake between 0 and 10 AZERO, it will revert, causing a DoS on the functionality.

  **Link**: [Issue #61](https://github.com/hats-finance/Kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/issues/61)

  **Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **unsynced staked value when unbond open for DOS**

  Unbounding process will be triggered via this start_unboud function below:
  The issue here is staked value will be unsynced due to the unbond can be permissionlessly called by anyone when the pool is destroying and the member is not the depositor.
  Thus when someone trigger this unbond operation for a pool, this staked value is not updated.
  This staked var is fetched via get_staked_value then it finally called in get_weight_imbalances. Using outdated staked value, this can affect delegate_unbonding allocation.
  Also, when the staked value is not synced, and there is a delegate_unbonding, at the end this will revert due to unbond more than existing amount bonded, another DOS will happen.

  **Link**: [Issue #63](https://github.com/hats-finance/Kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/issues/63)

  **Auditor:** Unknown

## Low severity issues

- **Missing events for deposit and withdraw functions accessed by vault**

  The `nomination_agent` contract lacks event emissions for functions such as `deposit()`, `start_unbond()`, `withdraw_unbonded()`, and `compound()`, which result in changes to staked token balances. Events are crucial for transparency, allowing off-chain tools/interfaces to track changes and users to evaluate their impact on protocol trustworthiness or profitability. Directly querying on-chain state for changes is impractical, and missing events hinder transparency, potentially leading users to exit the protocol, reducing liquidity, and impacting TVL and reputation. To ensure transparency and on-chain information about staked balance changes, events should be emitted in these functions within the `nomination_agent` contract..

  **Link**: [Issue #4](https://github.com/hats-finance/Kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/issues/4)

  **Auditor:** [0xRizwann](https://x.com/0xRizwann)

- **Agents amount limitation due to ink! storage Vec**

  The function add_agent is used to add new agents to the system. However, these are added to a Vec, which is a Packed struct in ink!. This limits it's size to the default size of one storage cell in ink!, which is by default ~16MB. This means that it will be only possible to only a limited amount of agents, and after that, the add_agent function will always panic.

  **Link**: [Issue #9](https://github.com/hats-finance/Kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/issues/9)

  **Auditor:** [krikoeth](https://x.com/krikoeth)

- **Not using a more precise YEAR value, like AZERO staking**

  The calculation of a year as a multiplication of days by 365.25 is more precise than using 365, aligning with the average number of days in the Julian calendar. This approach is adopted in AZERO staking reward documentation for accurate staking reward calculation. Given the relevance of Kintsu to staking AZERO, it's advisable to maintain consistency by using this standard.

  **Link**: [Issue #11](https://github.com/hats-finance/Kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/issues/11)

  **Auditor:** Unknown

- **Insufficient Check in remove_agent Function**

  Description: The remove_agent function currently only checks the weight of the agent but does not verify whether the agent has bonded AZERO tokens or not. This lack of verification poses a risk, as an agent with bonded AZERO tokens could potentially be removed from the list of agents.

  **Link**: [Issue #12](https://github.com/hats-finance/Kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/issues/12)

  **Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **Inconsistency in Fee Calculation in update_fees Function**

  In the current implementation of the update_fees function, the calculation of fee accumulation does not consider the owner's virtual shares (total_shares_virtual). Instead, it only considers total_shares_minted. owners shares should be considered in total shares just like get_total_shares function. This leads to the owner losing some fee.

  **Link**: [Issue #18](https://github.com/hats-finance/Kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/issues/18)

  **Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

- **NominationAgent contract lack of transfer admin function**

  Looking on how vault contract designed, the upgrade (set_code) can be done by role_owner, and if we look at the contract, there is a function transfer_role_owner to transfer this ownership.
  Unlike the vault, this NominationAgent contract lack of this admin transfer ownership function

  **Link**: [Issue #22](https://github.com/hats-finance/Kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/issues/22)

  **Auditor:** Unknown

- **Wrong Value in Compound Emit Event**

  The vault::compound function emits an event with an incorrect value for virtual shares. The current implementation directly uses self.data.total_shares_virtual instead of calculating the virtual shares at the current time.

  **Link**: [Issue #56](https://github.com/hats-finance/Kintsu-0x7d70f9442af3a9a0a734fa6a1b4857f25518e9d2/issues/56)

  **Auditor:** [0xmahdirostami](https://x.com/0xmahdirostami)

## Conclusion

The audit competition for the Kintsu protocol on the hats.finance platform revealed 1 high severity, 7 medium severity and 7 low severity issues. The audit involved a comprehensive examination of numerous aspects of Kintsu's code. Various issues identified included inaccurate input check, Dos in staking and unstaking, .... Each identified issue was accompanied by a proposed solution for resolving the problem. 

## Disclaimer

This report does not assert that the audited contracts are completely secure. Continuous review and comprehensive testing are advised before deploying critical smart contracts.
The Kintsu audit competition illustrates the collaborative effort in identifying and rectifying potential vulnerabilities, enhancing the overall security and functionality of the platform.
Hats.finance does not provide any guarantee or warranty regarding the security of this project. Smart contract software should be used at the sole risk and responsibility of users.

This report was generated with the help of openAI. 
