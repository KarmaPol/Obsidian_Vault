- Remove non-controllable area of test code
  (ex. LocalDateTime.now())
  -> **Fixed date is recommended**
## LocalDateTime.now()?
- It could be okay for a single code.
  But It will spread.
- Also each server time can be different

[[테스트하기 어려운 범위 분리하기]]