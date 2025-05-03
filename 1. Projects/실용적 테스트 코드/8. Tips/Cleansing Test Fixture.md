# 1. @AfterEach
 - Useful to clean test data after each test
## Foreign key when deleting
- Depends on deleting order
### JPA deleteAll VS. deleteAllInBatch
- deleteAllInBatch
  1 query to delete
- deleteAll
  1 query to get data
  N query to delete -> **More cost**
# 2. @Transactional
- Easy to use 
- But there would be complexity between transactions (e.g. batch process)

[[Easily Readable Test Fixture]]

