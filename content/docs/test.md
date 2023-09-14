+++
title = 'Spring Transactions Cheatsheet'
date = 2023-09-13T21:09:21+03:00
draft = false
+++

## Propagation behaviours

| Propagation     | TX exists           | TX missing |
|-----------------|---------------------|------------|
| `NEVER`         | fail                | -          |
| `NOT_SUPPORTED` | suspend             | -          |
| `SUPPORTS`      | reuse               | -          |
| `MANDATORY`     | reuse               | fail       |
| `REQUIRED`      | reuse               | create     |
| `REQUIRES_NEW`  | suspend + create    | create     |
| `NESTED`        | save point + create | create     |

## Isolation levels

| Isolation        | Solved problem       | -      |
|------------------|----------------------|--------|
| READ_UNCOMMITTED | -                    | -      |
| READ_COMMITTED   | Dirty read           | -      |
| REPEATABLE_READ  | Nonrepeatable read   | +above |
| SERIALIZABLE     | Phantom read         | +above |

## Isolation problems

- Dirty read - read the uncommitted change of a concurrent transaction
- Nonrepeatable read: get different value on re-read of a row if a concurrent transaction updates the same row and commits
- Phantom read: get different rows after re-execution of a range query if another transaction adds or removes some rows in the range and commits

## See also

- https://www.baeldung.com/spring-transactional-propagation-isolation
