+++
title = 'Spring Transactions Cheatsheet'
date = 2023-09-13T21:09:21+03:00
draft = false
+++

## Propagation behaviours:

| level         | existing tx      | missing tx |
|---------------|------------------|------------|
| NEVER         | fail             | -          |
| SUPPORTS      | reuse            | -          |
| REQUIRED      | reuse            | create     |
| MANDATORY     | reuse            | fail       |
| NESTED        | save pt + create | create     |
| NOT_SUPPORTED | suspend          | -          |
| REQUIRES_NEW  | suspend + create | create     |

## Isolation levels:

| #   | isolation        | solved problem             |
|-----|------------------|----------------------------|
| 1   | READ_UNCOMMITTED | -                          |
| 2   | READ_COMMITTED   | Dirty read                 |
| 3   | REPEATABLE_READ  | Nonrepeatable read + above |
| 4   | SERIALIZABLE     | Phantom read + above       |

## Isolation problems:

- Dirty read: read the uncommitted change of a concurrent transaction
- Nonrepeatable read: get different value on re-read of a row if a concurrent transaction updates the same row and commits
- Phantom read: get different rows after re-execution of a range query if another transaction adds or removes some rows in the range and commits

## See also

- https://www.baeldung.com/spring-transactional-propagation-isolation
