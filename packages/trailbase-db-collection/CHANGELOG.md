# @tanstack/trailbase-db-collection

## 0.0.8

### Patch Changes

- Updated dependencies [[`e04bd12`](https://github.com/TanStack/db/commit/e04bd1252f612d4638104368d17cb644cc85295b)]:
  - @tanstack/db@0.0.32

## 0.0.7

### Patch Changes

- Updated dependencies [[`3e9a36d`](https://github.com/TanStack/db/commit/3e9a36d2600c4f700ca7bc4f720c189a5a29387a)]:
  - @tanstack/db@0.0.31

## 0.0.6

### Patch Changes

- Updated dependencies [[`6bdde55`](https://github.com/TanStack/db/commit/6bdde554f36f54c0c4f4dacb74bef5da45811855)]:
  - @tanstack/db@0.0.30

## 0.0.5

### Patch Changes

- feat: Replace string-based errors with named error classes for better error handling ([#297](https://github.com/TanStack/db/pull/297))

  This comprehensive update replaces all string-based error throws throughout the TanStack DB codebase with named error classes, providing better type safety and developer experience.

  ## New Features

  - **Root `TanStackDBError` class** - all errors inherit from a common base for unified error handling
  - **Named error classes** organized by package and functional area
  - **Type-safe error handling** using `instanceof` checks instead of string matching
  - **Package-specific error definitions** - each adapter has its own error classes
  - **Better IDE support** with autocomplete for error types

  ## Package Structure

  ### Core Package (`@tanstack/db`)

  Contains generic errors used across the ecosystem:

  - Collection configuration, state, and operation errors
  - Transaction lifecycle and mutation errors
  - Query building, compilation, and execution errors
  - Storage and serialization errors

  ### Adapter Packages

  Each adapter now exports its own specific error classes:

  - **`@tanstack/electric-db-collection`**: Electric-specific errors
  - **`@tanstack/trailbase-db-collection`**: TrailBase-specific errors
  - **`@tanstack/query-db-collection`**: Query collection specific errors

  ## Breaking Changes

  - Error handling code using string matching will need to be updated to use `instanceof` checks
  - Some error messages may have slight formatting changes
  - Adapter-specific errors now need to be imported from their respective packages

  ## Migration Guide

  ### Core DB Errors

  **Before:**

  ```ts
  try {
    collection.insert(data)
  } catch (error) {
    if (error.message.includes("already exists")) {
      // Handle duplicate key error
    }
  }
  ```

  **After:**

  ```ts
  import { DuplicateKeyError } from "@tanstack/db"

  try {
    collection.insert(data)
  } catch (error) {
    if (error instanceof DuplicateKeyError) {
      // Type-safe error handling
    }
  }
  ```

  ### Adapter-Specific Errors

  **Before:**

  ```ts
  // Electric collection errors were imported from @tanstack/db
  import { ElectricInsertHandlerMustReturnTxIdError } from "@tanstack/db"
  ```

  **After:**

  ```ts
  // Now import from the specific adapter package
  import { ElectricInsertHandlerMustReturnTxIdError } from "@tanstack/electric-db-collection"
  ```

  ### Unified Error Handling

  **New:**

  ```ts
  import { TanStackDBError } from "@tanstack/db"

  try {
    // Any TanStack DB operation
  } catch (error) {
    if (error instanceof TanStackDBError) {
      // Handle all TanStack DB errors uniformly
      console.log("TanStack DB error:", error.message)
    }
  }
  ```

  ## Benefits

  - **Type Safety**: All errors now have specific types that can be caught with `instanceof`
  - **Unified Error Handling**: Root `TanStackDBError` class allows catching all library errors with a single check
  - **Better Package Separation**: Each adapter manages its own error types
  - **Developer Experience**: Better IDE support with autocomplete for error types
  - **Maintainability**: Error definitions are co-located with their usage
  - **Consistency**: Uniform error handling patterns across the entire codebase

  All error classes maintain the same error messages and behavior while providing better structure and package separation.

- Updated dependencies [[`ced0657`](https://github.com/TanStack/db/commit/ced0657e72646e35343dfea8389d96e213710cdf), [`dcfef51`](https://github.com/TanStack/db/commit/dcfef51d4d94c756bf77e40e7015e47b7982c09a), [`360b0df`](https://github.com/TanStack/db/commit/360b0dfa411ba9f8a93f6b737aa1df8fb37dd036), [`608be0c`](https://github.com/TanStack/db/commit/608be0c14dc5ae9577deebf436557a1eace46733), [`5260ee3`](https://github.com/TanStack/db/commit/5260ee3098d12eccc58a5cf903ea479908681402)]:
  - @tanstack/db@0.0.29

## 0.0.4

### Patch Changes

- Updated dependencies [[`bb85522`](https://github.com/TanStack/db/commit/bb8552210a97dd05d3ca6fdd080a3fd25c1023a6), [`e9e8e5e`](https://github.com/TanStack/db/commit/e9e8e5e20c23fb7f98865d6b8aab05ad5322e5f7)]:
  - @tanstack/db@0.0.28

## 0.0.3

### Patch Changes

- Updated dependencies [[`bec8620`](https://github.com/TanStack/db/commit/bec862004deef5fdd560f70107ebd59f7c27656e)]:
  - @tanstack/db@0.0.27

## 0.0.2

### Patch Changes

- Add initial release of TrailBase collection for TanStack DB. TrailBase is a blazingly fast, open-source alternative to Firebase built on Rust, SQLite, and V8. It provides type-safe REST and realtime APIs with sub-millisecond latencies, integrated authentication, and flexible access control - all in a single executable. This collection type enables seamless integration with TrailBase backends for high-performance real-time applications. ([#228](https://github.com/TanStack/db/pull/228))

- Updated dependencies [[`09c6995`](https://github.com/TanStack/db/commit/09c6995ea9c8e6979d077ca63cbdd6215054ae78)]:
  - @tanstack/db@0.0.26
