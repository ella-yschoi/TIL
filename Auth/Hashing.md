# Hashing

## 1. What is Hashing?

- The most commonly used encryption method
- Unlike other encryption methods that can be decrypted, **hashing can only encrypt**
- Encryption is performed using hash functions
- Hash function characteristics

  - **Always returns a string of the same length**
  - When the same hash function is used on different strings, different results are guaranteed
  - When the same hash function is used on identical strings, the same result is always produced

- Rainbow table
  - A table created to find out values before they go through hash functions, using the characteristic that the same result always comes out
  - Can be a security threat
- Salt

  - Adds random values to values before hashing to make them difficult to figure out

- Purpose of hashing
  - Not to use the data itself, but to verify whether the same value data is being used
  - Even without knowing the exact value, if the hashed values match, login requests can be processed using only the hashed value
  - In other words, **a one-way encryption method that reduces the risk of data leakage while verifying validity in situations where sensitive data must be handled**
