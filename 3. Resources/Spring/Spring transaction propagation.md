# Physical, Logical Transaction
- Physical
  real DB transaction with connection
- Logical
  transaction by Spring
## Principle
1. All local transaction should be committed then physical commit
2. If one logical transaction is rollbacked, physical too
# Spring transaction attributes
- REQUIRED
  if transaction not exists, create new one.
  if exists, join
- SUPPORTS
- MANDATORY
- REQUIRES_NEW
  always create new one
- NOT_SUPPORTED
- NEVER
- NESTED

[[Cleansing Test Fixture]]
[[Transaction 전파