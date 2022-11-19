# Iptables role

A role for configuring iptables rules.

## Requirements

- iptables

## Summary

There are three existing states with iptables ===>>>

1. there is no rules for iptables
2. there is correct rules for iptables
3. there are some garbage rules that should be overwritten
   Solution: we have to check three chains

- FILTERS: we are going to add some specific 'comment' at the ending rule
  of FILTERS chain, for example 'A', so if there is an 'A' in our rules we
  are going to assume that FILTERS chain is ok, other wise it is empty or
  garbage, so if there is no '-A FILTERS' we are going to assume chain is
  empty, otherwise we are going to flush the chain. flow:

```
if 'A' not in .stdout and '-A FILTERS' in .stdout:
  flush FILTERS
else:
  don't flush
```

- INPUT: we are going to add a specific comment 'B' when applying jump rule and then check it. flow:

```
if 'B' not in .stdout and '-A INPUT' in .stdout:
  flush INPUT
else:
  don't flush
```

- DOCKER-USER: we are going to do the same as INPUT chain.
