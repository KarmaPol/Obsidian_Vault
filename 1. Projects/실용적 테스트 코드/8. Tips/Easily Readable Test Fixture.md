# Test Fixture
- "Base" data for the test
## How about set base test fixture as common SQL?
- Some base data is common and could be used as one SQL
- But,
  We can't track test data if test getting larger
- Instead,
  **Use Builder method to create a test object** for each test fixture
### Too many test fixture builder method
- If some parameters are different by test
  -> Should create too many builder constructor which is bad
- But don't gather all builder method in one class
  -> It's more hard to read and different by test case
  -> Set it in the same test class with test method
## How about use setUp()?
- Use only if we don't have to understand it
  and if it doesn't have any influence
  
[[테스트는 Document다]]
[[One topic by each paragraph]]

