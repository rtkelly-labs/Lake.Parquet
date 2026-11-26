---
title: "Tests: the hard-coded decimal is a decimal literal"
kind: code   # tests only: verify requires it to pass
status: fork-only
depends_on: []
---

# 0089 Tests: the hard-coded decimal is a decimal literal

## What and why

`ParquetReaderTest.Read_hardcoded_decimal` expects `(decimal)1.2`: the double `1.2` converted to `decimal`. That
conversion used to give `1.2` (the test passed in CI on 1 November 2026). The runtimes CI and a local machine have now
(.NET 10.0.15) give the double's exact binary value, `1.1999999999999999555910790150`, so the test fails although the
reader returns the column's value, `1.2`, correctly. The expected value becomes the literal `1.2m`. No library code changes.

## Evaluation

- On .NET 10.0.15, before: both cases (`complex-primitives.parquet`, `.v2.parquet`) fail with
  `Expected: 1.1999999999999999555910790150, Actual: 1.2`, as in CI since November 2026. After: both pass.

## Upstream

Upstream (`aloneguid/parquet-dotnet`) has been deleted; there is nowhere to propose it.

## Compatibility

Test-only.
