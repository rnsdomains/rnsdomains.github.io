---
layout: rns
title: Reverse suite
---

Reverse RNS records are stored in the RNS hierarchy in the same fashion as regular records, under a reserved domain, `addr.reverse`.

> Compatible with [EIP-181](https://eips.ethereum.org/EIPS/eip-181).

<img src="/img/addr_suite.png" class="img-fluid" alt="addr_suite" />

## Reverse resolving

To generate the RNS name for a given account's reverse records, convert the account to hexadecimal representation in lower-case, and append `addr.reverse`. For instance, the RNS registry's address at `0x112234455c3a32fd11230c42e7bccd4a84e02010` has any reverse records stored at `112234455c3a32fd11230c42e7bccd4a84e02010.addr.reverse`.

```js
function reverseResolve (address) {
  const reverseName = `${address.slice(2).toLowerCase}.addr.reverse`;
  const node = namehash(reverseName);
  const resolver = rns.resolver(node);
  const name = resolver.name(node);
  return name;
}
```

## Register a reverse resolution

The owner of the `addr.reverse` domain is a registrar that permits the caller to take ownership of the reverse record for their own address.

```js
function registerReverse (address, owner) {
  reverseRegistrar.claim(owner, { from: address });
}
```

## Architecture

- [Reverse Registrar](/Architecture/ReverseRegistrar)
- [Name Resolver](/Architecture/NameResolver)
