# DHK Subdomain Register

The goal of this project is to create a contract for DHK members to claim a subdomain on ENS. The contract will be deployed Optimism L2.


## Who can claim a subdomain?

TBC


## Think Out Loud

1. Can we use the ENS registry contract to store the subdomain owner?
2. Can we deploy the contract on L2 and manage the subdomain on L1?

### Subdomain Registration Flow

1. **Load ENS Contract Addresses and Wallet Client**:
   - Load contract addresses from a `.env` file.
   - Initialize the wallet client and set necessary constants.

2. **Get ENS Contract Instances**:
   - Get instances of `ENSRegistry`, `BaseRegistrarImplementation`, `NameWrapper`, and `PublicResolver` contracts.

3. **Set Approvals and Wrap Domain**:
   - Set approval for `NameWrapper` in both `BaseRegistrar` and `ENSRegistry`.
   - Call `wrapETH2LD` on `NameWrapper` to wrap the main domain.

4. **Create Subdomains**:
   - Use `setSubnodeOwner` on `NameWrapper` to create subdomains.
   - Set resolver and text records for subdomains using `setResolver` and `setText` methods.

5. **Set Fuses**:
   - Set restrictions (fuses) on the subdomains using `setFuses`.

6. **(Optional) Unwrap Domain**:
   - Use `unwrap` method to unwrap a subdomain if necessary.


## ENS Contracts

### NameWrapper
The NameWrapper contract in ENS is used to wrap ENS names into ERC-721 compliant NFTs. It allows for additional functionality such as setting permissions ("fuses") to restrict certain actions, like unwrapping the name or changing the resolver.

### Resolver
The Resolver contract is a generic interface that includes multiple resolver functions for ENS. It allows setting and retrieving various types of records for ENS names, such as addresses, content hashes, text records, and more.

### EnsRegistry
The EnsRegistry contract is the core registry of ENS. It maintains the mapping from domain names to their respective owners and resolvers. It allows for the registration and transfer of domain names.

### BaseRegistrar

The BaseRegistrar contract manages the registration of second-level domains (2LDs) under a specific top-level domain (TLD), such as .eth. It handles the issuance and renewal of domain names and interacts with the ENS registry.

### Holesky Updated: 27/1/24

ENSRegistry: 0x00000000000C2E074eC69A0dFb2997BA6C7d2e1e
BaseRegistrarImplementation: 0x57f1887a8BF19b14fC0dF6Fd9B2acc9Af147eA85
ETHRegistrarController: 0x179Be112b24Ad4cFC392eF8924DfA08C20Ad8583
PublicResolver: 0x9010A27463717360cAD99CEA8bD39b8705CCA238
NameWrapper: 0xab50971078225D365994dc1Edcb9b7FD72Bb4862
UniversalResolver: 0x2548a7E09deE955c4d97688dcB6C5b24085725f5
ReverseRegistrar: 0x132AC0B116a73add4225029D1951A9A707Ef673f

### Sepolia Updated: 27/1/24

ENSRegistry: 0x00000000000C2E074eC69A0dFb2997BA6C7d2e1e
BaseRegistrarImplementation: 0x57f1887a8BF19b14fC0dF6Fd9B2acc9Af147eA85
ETHRegistrarController: 0xFED6a969AaA60E4961FCD3EBF1A2e8913ac65B72
PublicResolver: 0x8FADE66B79cC9f707aB26799354482EB93a5B7dD
NameWrapper: 0x0635513f179D50A207757E05759CbD106d7dFcE8
UniversalResolver: 0xBaBC7678D7A63104f1658c11D6AE9A21cdA09725
ReverseRegistrar: 0xA0a1AbcDAe1a2a4A2EF8e9113Ff0e02DD81DC0C6

### Mainnet Updated 27/1/24

ENSRegistry: 0x00000000000C2E074eC69A0dFb2997BA6C7d2e1e
BaseRegistrarImplementation: 0x57f1887a8BF19b14fC0dF6Fd9B2acc9Af147eA85
ETHRegistrarController: 0x253553366Da8546fC250F225fe3d25d0C782303b
PublicResolver: 0x231b0Ee14048e9dCcD1d247744d114a4EB5E8E63
NameWrapper: 0xD4416b13d2b3a9aBae7AcD5D6C2BbDBE25686401
UniversalResolver: 0x8cab227b1162f03b8338331adaad7aadc83b895e
ReverseRegistrar: 0xa58E81fe9b61B5c3fE2AFD33CF304c454AbFc7Cb


## References

https://github.com/ensdomains/subdomain-registrar
https://github.com/ensdomains/ens-contracts/blob/5421b5689e695531dc9739f0ad861839bdd231cb/tasks/seed.ts#L12