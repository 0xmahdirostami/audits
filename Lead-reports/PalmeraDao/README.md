# **Palmeradao Network Audit Competition on Hats.finance** 

- Prepared by: [Hats.finance](https://hats.finance/)
- Audit Competition: [palmeradao](https://www.palmeradao.xyz/)
- Lead Auditors: [0xmahdirostami](https://x.com/0xmahdirostami), [0xRizwan](https://x.com/0xRizwann)
- Date: July 16, 2024


## About Hats.finance


Hats.finance builds an autonomous security infrastructure for integration with major DeFi protocols to secure users' assets. 
It aims to be the decentralized choice for Web3 security, offering proactive security mechanisms like decentralized audit competitions and bug bounties. 
The protocol facilitates audit competitions to quickly secure smart contracts by having auditors compete, thereby reducing auditing costs and accelerating submissions. 
This aligns with their mission of fostering a robust, secure, and scalable Web3 ecosystem through decentralized security solutions​.

## About Palmera 

Palmera streamlines your Safes operations and treasury management across multiple chains, all from a single dashboard

## About Hats Audit Competition

Hats Audit Competitions offer a unique and decentralized approach to enhancing the security of web3 projects. Leveraging the large collective expertise of hundreds of skilled auditors, these competitions foster a proactive bug hunting environment to fortify projects before their launch. Unlike traditional security assessments, Hats Audit Competitions operate on a time-based and results-driven model, that ensures that only successful auditors are rewarded for their contributions. This pay-for-results ethos not only allocates budgets more efficiently by paying exclusively for identified vulnerabilities but also retains funds if no issues are discovered. With a streamlined evaluation process, Hats prioritizes quality over quantity by rewarding the first submitter of a vulnerability, thus eliminating duplicate efforts and attracting top talent in web3 auditing. The process embodies Hats Finance's commitment to reducing fees, maintaining project control, and promoting high-quality security assessments, setting a new standard for decentralized security in the web3 space​​.


## Competition Details


- Type: A public audit competition hosted by Palmera Dao
- Duration: 14 days
- Prize Pool: $24,000
- Maximum Reward: $7,200 for a high severity submission
- Total Submissions: 101
- Valid Submissions: 28(includes gas submission)
- Total Payout: $24,000


## Project overview

Palmera is a multi-safe and multi-chain treasury management platform helping customers simplify their financial on-chain management with these main functions:

- Users can visualize in a single dashboard all their Safes even if they are in different chains.

- We simplify the visualization of the treasury to have better information for financial management.

- Create transactions, receive notifications for new signatures, manage multisig settings, and add context to transaction history — all with ease, streamlining the operations of on-chain organizations.


## Audit competition scope


```
├── src
│   ├── DenyHelper.sol
│   ├── Helpers.sol
│   ├── PalmeraGuard.sol
│   ├── PalmeraModule.sol
│   ├── PalmeraRoles.sol
│   ├── ReentrancyAttack.sol
│   ├── SafeInterfaces.sol
│   ├── SigningUtils.sol
│   ├── libraries
│   │   ├── Constants.sol
│   │   ├── DataTypes.sol
│   │   ├── Errors.sol
│   │   └── Events.sol
```
 
## Issues

## High severity issues

### H-01 Insufficient Access Control in execTransactionOnBehalf Due to Broad Lead Role Check
**Issue Link:** [Issue #31](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/31) by [0xmahdirostami](https://x.com/0xmahdirostami)

In the execTransactionOnBehalf function, there is a check to bypass the signature verification if the caller is a Safe Lead. However, this check does not distinguish between the different Safe Lead roles (SAFE_LEAD, SAFE_LEAD_EXEC_ON_BEHALF_ONLY, and SAFE_LEAD_MODIFY_OWNERS_ONLY). The current implementation allows any lead role to bypass the signature check, which leads to insufficient access control.

### H-02 Ineffective Revocation of Multiple Roles in disableSafeLeadRoles Function
**Issue Link:** [Issue #37](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/37) by [0xmahdirostami](https://x.com/0xmahdirostami)

The disableSafeLeadRoles function is designed to revoke specific Safe Lead roles from a user. However, the current implementation only revokes the first role it encounters and skips the rest. This means if a user has multiple roles, only the first role in the conditional checks is revoked, leaving the other roles intact.

### H-03 isSafeLead Function Lacks Role Authorization Check, Leading to Unauthorized Access
**Issue Link:** [Issue #38](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/38) by [0xmahdirostami](https://x.com/0xmahdirostami)

The isSafeLead function determines if a user is a lead for a given safe by checking the _safe.lead attribute. However, this approach does not account for scenarios where the user's Safe Lead roles have been revoked through the disableSafeLeadRoles function. This can result in unauthorized access because the function does not verify the user's current roles in the RolesAuthority contract.

### H-04 Unauthorized Role Modification Vulnerability in setRole Function
**Issue Link:** [Issue #70](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/70) by [0xmahdirostami](https://x.com/0xmahdirostami)

In the `setRole` function, the `safeId` parameter is intended to specify the safe on which the user will have permissions, but the current implementation assigns roles to the user without considering the `safeId`, meaning roles are assigned to the user generally and not just for that specific `safeId`. This allows any root to enable or disable any role for any user without restriction, so the root of any organization can enable or disable roles for any user. For example, a malicious attacker can create an organization called XOrg and, as the root, call `setRole` with their `safeId` and another organization's user address to disable roles or assign unauthorized roles, effectively executing unauthorized transactions and causing denial of service. Additionally, a user with specific modify-only roles in one organization can create another organization, assign themselves broader roles using the new `safeId`, and gain unauthorized privileges. This flaw enables unauthorized role assignments and revocations, leading to potential security breaches and denial of service across different organizations.

### H-05 Unauthorized Access Control Due to Retained Root Role When Root Safe Exits and Joins New Org
**Issue Link:** [Issue #76](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/76) by [0xmahdirostami](https://x.com/0xmahdirostami)

When a root safe exits an organization and becomes a member of a new organization, it retains the root role, leading to unauthorized access as the contract assumes this safe is the root of the new organization. In the `_createOrgOrRoot` function, the code assigns the `ROOT_SAFE` role to the root safe. This creates a scenario where Safe A, which initially creates an organization and becomes the root, retains its root privileges even after exiting and joining a new organization. Consequently, the contract incorrectly assumes Safe A is the root of the new organization, granting it unauthorized access and control due to the retained `ROOT_SAFE` role, which compromises the security and access control of the new organization.

## Medium severity issues

### M-01 registerOrg Function Vulnerable to DoS and Gas Griefing Attacks
**Issue Link:** [Issue #3](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/3) by [0xmahdirostami](https://x.com/0xmahdirostami)

The registerOrg() function in the contract can be exploited by an attacker to perform denial-of-service (DoS) attacks or gas griefing against other users. The function allows for the creation of organizations, but it doesn't adequately handle the scenario where an organization name is already registered. An attacker can front-run a legitimate user's transaction to create an organization with a desired name, causing the legitimate user's transaction to fail. This forces the user to attempt the process again.
To prevent this attack, include the caller's address in the hash when creating an organization. This ensures that organization names are unique to each user, preventing front-running attacks.

### M-02 Updating depthtreelimit is ineffective
**Issue Link:** [Issue #4](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/4) by [mxuse](https://x.com/mxuse)

In `PalmeraModule.sol` the `updateDepthTreeLimit()` function allows for a new updated depth of the treelimit. At the end of the function the depthTreeLimit[org] gets updated to the newLimit. However due to the hardcoding of the depthTreeLimit inside several places of the contract, it will still remain 8. For example inside createRootSafe, the depth is hardcoded to 8 so any changes to the depth will not be reflected inside this function even though it should.
Its recommended to remove the hardcoded depthTreeLimit[name] = 8.

### M-03 Unbonded orgHash Could Result in Denial of Service (DOS)
**Issue Link:** [Issue #10](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/10) by [0xmahdirostami](https://x.com/0xmahdirostami)

Unbonded orgHash could result in a denial of service (DOS) in several functions, potentially leading to serious issues. The affected functions includes `getOrgBySafe()`,`removeOrg()` and `getOrgHashBySafe()`. Due to denial of service in core functions, potentially affecting the integrity and usability of the contract. A DOS attack in the removeOrg function can also cause issues when attempting to remove an organization from the list of organization hashes.

An attacker can exploit unbonded orgHash to cause these functions to fail, preventing legitimate users from interacting with the contract. 

For example:
1) An attacker creates lots of orgs..
2) The contract becomes unable to process legitimate orgHash values due to the presence of unbonded values, leading to DOS in the mentioned functions.

### M-04 Any contract can bypass isSafe restrictions
**Issue Link:** [Issue #24](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/24) by [0xfuje](https://x.com/0xfuje)

User can create a non-safe custom contract that returns 1 on getThreshold() calls to use PalmeraModule functionality. Non-safe contracts can registers organization, create a root safe, and be added as a safe in addSafe(), basically bypass the isSafe() restrictions.

Its recommended to implement stricter checks, for example: ERC165 supportsInterface() checks instead of only checking safe is a contract and threshold in isSafe().

### M-05 Incomplete Deletion of Organization State Leads to Residual Effects on New Users
**Issue Link:** [Issue #27](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/27) by [0xmahdirostami](https://x.com/0xmahdirostami)

When organizations are deleted, not all state information about them is completely removed. This can affect new users who register organizations with the same name. Some of these residual states include allowFeature, listed[org], and listCount.

Consider below Scenario:
1) User A registers an organization with the name "xyz".
2) User A calls addToList and enables the denylist with enableDenylist.
3) After some time, User A's organization "xyz" is deleted but not all related state variables are cleared.
4) A new user registers a new organization with the same name "xyz".
5) The new organization inherits the residual state from the old "xyz" organization.

Its recommended to clear all storage variable related to org in removeOrg().

### M-06 setRole Function Incorrectly Assigns _safe.lead without Validating enabled Parameter
**Issue Link:** [Issue #41](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/41) by [0xmahdirostami](https://x.com/0xmahdirostami)

The setRole function assigns the _safe.lead attribute to a user if the role is related to safe leadership (SAFE_LEAD, SAFE_LEAD_EXEC_ON_BEHALF_ONLY, SAFE_LEAD_MODIFY_OWNERS_ONLY). However, the function fails to check the enabled boolean parameter before updating _safe.lead. This can lead to unauthorized access control issues where users might be improperly assigned as safe leads.

This oversight can result in unauthorized access control, allowing users to be incorrectly recognized as safe leads even if their role was meant to be disabled. This compromises the security and integrity of the system.

Its recommended to ensure the enabled parameter is checked before updating _safe.lead.

### M-07 Malicious users can front-run host users safe management actions and add those safes as root for wrong org
**Issue Link:** [Issue #50](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/50) by [-]()

When creating a rootSafe for organization, we only check whether the calling address is a valid root safe and if provided address is a safe. Note that a user can provide any newRootSafe, without guarantee if he is related to it. This is a big problem because once added in the system, newRootSafe cannot be added again from another organization. If this is weaponised, exploiter can DoS the composability of the palmera module by calling createRootSafe with address of other honest organization safes from his malicious organization. This will brick safe orchestration provided by palmera. This is so, because expoiter can prevent actors from calling addSafe and composing a tree. For example, malicious organisation can front-run addSafe by calling createRootSafe with address of the caller of addSafe. When honest party hit execution, it will revert on the following [line](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/blob/dfd821e2fd7825c66c079c19be9460238f6e045a/src/PalmeraModule.sol#L357-L359):

When calling createRootSafe, make sure newRootSafe has agreed to become root safe for the given organization. You can introduce another state var mapping(bytes[] => mapping(address => bool))) becomeRootForOrg and a method, which would be called from corresponding safes to switch flags.

### M-08 Safe owner/s can prevent being removed from organization by indefinitely increasing their child array
**Issue Link:** [Issue #51](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/51) by [NicolaMirchev](https://x.com/NicolaMirchev)

Palmera module allow organizations to orchestrate different safes in hierarchy, where super safe can remove it's children. One problem here is that any arbitrary safe can become child of any superSafeId by calling addSafe. This will increment superSafeOrgSafe.child array. There is no limit on how many child a super safe can have (the limit is only for depth), but a child may have an unlimited amount of siblings.

Consider below scenario:
1) Organization A creates a root safe and adds Safe B as a chield.
2) Some times passes and A has created some siblings of B and want to remove B, because it has become malicious.
3) But B has already called addSafe with it's Id from 1_000_000 addresses and when removeSafe transaction hits execution, it will try to make those 1_000_000 addresses 4) children of A, but this would be a very large loop with guaranteed OOG error.
5) As a result organization A is compromised

Its recommended to implement a limit of safe.child array and check it when new safe is integrated.

### M-09 addSafe Function Lacks Validation for superSafeId State
**Issue Link:** [Issue #52](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/52) by [0xmahdirostami](https://x.com/0xmahdirostami)

The addSafe function does not check if the provided superSafeId is in a removed state. This oversight can lead to a scenario where a removed safe ID is incorrectly set as a superSafeId, potentially causing logical inconsistencies and security issues.

This would allow a removed safe ID to become a superSafeId can compromise the integrity of the hierarchical structure of safes. safes, that are removed, but not disconnected shouldn't become super safe again.

Its recommended to add a check to ensure that the superSafeId is not in a removed state before proceeding with the addition of the new safe.

### M-10 Potential Protocol insolvency in removeWholeTree and disconnectSafe
**Issue Link:** [Issue #55](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/55) by [0xmahdirostami](https://x.com/0xmahdirostami)

The _exitSafe function currently includes a check for getPreviewModule(caller) and reverts if it returns address(0). This can lead to a Denial of Service (DoS) issue because users can call disableModule on their own, causing subsequent calls to _exitSafe to fail.

This would allow DoS vulnerability in _exitSafe affects the removeWholeTree and disconnectSafe functions. If disableModule has been called by the user, it will result in a failure of _exitSafe, thereby preventing the proper execution of these functions, leading to Protocol insolvency.

Its recommended to consider getPreviewModule() as public function instead of internal function.

### M-11 Missing Validation in addSafe Function for Enabled Guard and Module
**Issue Link:** [Issue #57](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/57) by [0xmahdirostami](https://x.com/0xmahdirostami)

The addSafe() function currently does not validate whether the msg.sender has enabled the guard and the PalmeraModule. This oversight allows safes to be added to an organization without any guard, leading to potential security issues and possible Denial of Service (DoS) in the disconnectSafe and removeWholeTree functions.

This would allow unauthorized safes can be added to an organization without the necessary guard and DoS vulnerabilities in disconnectSafe and removeWholeTree due to lack of validation.

Its recommended to add a validation check in the addSafe function to ensure that the msg.sender has enabled the guard and the module before proceeding.

### M-12 Missing disableSafeLeadRoles Call for Root in removeWholeTree Function
**Issue Link:** [Issue #72](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/72) by [0xmahdirostami](https://x.com/0xmahdirostami)

In the removeWholeTree function, the disableSafeLeadRoles function is not called for the root safe. disableSafeLeadRoles is called for all safes but not for the root safe. 

The lack of disabling lead roles for the root will cause issues, especially if the root safe becomes a member in another organization. This can result in unexpected behavior and potential security risks, as the root safe will retain roles that should have been disabled.
Mitigation:

To mitigate this issue, ensure that disableSafeLeadRoles is also called for the root safe.

### M-13 getPreviewModule() Returns Incorrect Data
**Issue Link:** [Issue #78](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/78) by [AresAudits](https://x.com/AresAudits)

getPreviewModule() function in the Helpers.sol returns the 25 modules.However, there is a bug in the external call to safe.getModulesPaginated. In the version of Safe contracts that Palmera is using (version 1.3.0), the getPreviewModules() function returns an incorrect next pointer, resulting in incorrect data being returned. This issue has been fixed in newer versions of Safe contracts, but Palmera still uses version 1.3.0.

Its recommended to upgrade to a recent version of Safe.

## Low severity issues

### L-01 PALMERA_TX_TYPEHASH incorrectly calculated
**Issue Link:** [Issue #1](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/1) by [rotcivegaf](https://x.com/rotcivegaf)

The constant PALMERA_TX_TYPEHASH in the contract Constants is incorrectly calculated. Due to incorrect PALMERA_TX_TYPEHASH, the encoded transaction data for Palmera transactions would be incorrectly produced. Therefore, the transaction hashes requested for Palmera transaction would be incorrectly returned.

### L-02 Incorrect encoding of bytes for EIP712 digest in createDigestExecTx() functions thus not compatible with EIP712
**Issue Link:** [Issue #6](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/6) by [0xRizwann](https://x.com/0xRizwann)

According to EIP-712:
> The dynamic values bytes and string are encoded as a keccak256 hash of their contents.

Reference link: https://eips.ethereum.org/EIPS/eip-712#definition-of-encodedata

However, the digest has encoded the bytes data and signature as not keccak256 hashed as per the requirement of EIP-712 in `createDigestExecTx()` function. This violates EIP712 requirement and produce incorrect encoding.

### L-03 Enum is not present in EIP-712
**Issue Link:** [Issue #11](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/11) by [SBSecurity_](https://x.com/SBSecurity_)

Enum.Operation is not common type and cannot be used in EIP-712 hash. Enums are derived from uint and uint should be used instead, using Enum.Operation will make the hash wrong in `createDigestExecTx()` function.

### L-04 Use deprecated this in calculating domainSeparator()
**Issue Link:** [Issue #28](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/28) by [0xRizwann](https://x.com/0xRizwann)

`this` keyword is used for the smart contract when the solidity version is below 0.5.0, therefore use of this is deprecated in v5.0.0 .

The contracts have used solidity 0.8.23 so use of deprecated `this` should be avoided to prevent unexpected behaviour in contracts. The issue is in Helpers.domainSeparator() function where deprecated `this` is used to calculate the hash. Its always recommended to not use deprecated variables/functions, etc so instead of `this`, `address(this)` should be used.

### L-05 Incorrect access control on removeSafe()
**Issue Link:** [Issue #40](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/40) by [0xRizwann](https://x.com/0xRizwann)

removeSafe() is used to remove safe and reasign all child to the superSafe. The documentation states, removeSafe() MUST be called by root safe, however the current implementation does not implement it and unsafe from intended protocol design for removeSafe(). This would not ensure, the strict access control on removeSafe() as intended by Palmera protocol as the access to such critical function is given in wrong hands and no where it mentions to allow SafeRegistered() to access removeSafe(). The issue highlighted discrepancy in documentation and code.

Its recommended to correct the documentation so that code and docs should be inline with each other.

### L-06 Potential Vulnerability in execTransactionOnBehalf Function Allowing Destruction of targetSafe contract
**Issue Link:** [Issue #61](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/61) by
[batmanBinary](https://github.com/batmanBinary)

The execTransactionOnBehalf function in the PalmeraModule contract allows certain roles (Safe Lead, Super Safe, Root Safe) to execute transactions on behalf. However, there is a potential vulnerability that can be exploited if the to address is malicious. Specifically, if the operation is set to Enum.Operation.DelegateCall, a malicious contract at the to address can execute a selfdestruct operation, leading to the destruction of the targetSafe contract. This can severely disrupt the organization by breaking contract modules and halting all transactions.

To mitigate this vulnerability, additional checks should be implemented to ensure the to address is not malicious. Specifically, avoid using delegatecall with untrusted addresses.

### L-07 safeId was not removed from safe.child when promoteRoot() is called
**Issue Link:** [Issue #89](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/89) by [lanrebayode1](https://x.com/lanrebayode1)

safeRoot can call promoteRoot() to promote the safe to Root. The condition that must be met is that the safe must be a superSafe and the calling safe must be a Root and the direct parent to the safe. After updating the safe role to Root, safe.lead and safe.superSafe were cleared but the safeId was not cleared from the caller(Root/parent of safe). Since the safe.superSafe of the safeId has been cleared, the data should also be cleared from the parent safe.child array to shrink it.
Therefore its recommended to remove the promoted child from the parent child array to shrink it.

### L-08 A safe will still have SUPER_SAFE ROLE after exit
**Issue Link:** [Issue #92](https://github.com/hats-finance/Palmera-0x5fee7541ddcd51ba9f4af606f87b2c42eea655be/issues/92) by [lanrebayode1](https://x.com/lanrebayode1)

By design, afer a safe is removed from an org, it should not have any role and this was implemented partialy in the removeWholeTree(), all roles were revoked before making a call to _exitSafe() to delete the safe struct and remove the safe from the org safe array. The problem here is that super safe role of the root was not revoked with the assupmtion that root does not have a super safe role, however, it is possible for a root safe to have a super safe root.

Consider a scenario:
1) safe A is a super safe under root A
2) root A then promoted safe A to root but still has super safe role
3) The entire tree was then removed but the root B safe address still has the super safe role.

Its recommended to revoke the super safe role of a safe before granting it the root safe role

## Systematic and Centralization risks

There is no centralize risk in palmera dao contract, each organization has it's own root and the root of each organization have control over his org.

## Conclusion

The audit competition for the Palmera Dao protocol on the Hats.finance platform revealed 5 high, 13 medium and 8 low severity issues. The audit involved a comprehensive examination of numerous aspects of Palmera Dao's code, such as reward Signature, different roles, structure, and more. Various issues identified included incorrect access control, logic, .... Each identified issue was acknowledged and accompanied by a proposed solution for resolving the problem. 


## Disclaimer

This report does not assert that the audited contracts are completely secure. Continuous review and comprehensive testing are advised before deploying critical smart contracts.
The Palmera Dao audit competition illustrates the collaborative effort in identifying and rectifying potential vulnerabilities, enhancing the overall security and functionality of the platform.
Hats.finance does not provide any guarantee or warranty regarding the security of this project. Smart contract software should be used at the sole risk and responsibility of users.

This report was written with the help of lead auditor [0xmahdirostami](https://x.com/0xmahdirostami), [0xRizwan](https://x.com/0xRizwann).
