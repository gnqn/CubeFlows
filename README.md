# CubeFlow
A native SQL engine that optimizes multidimensional query chain execution using the cube flow paradigm, with support for generalized cube structures and pipelined execution.

# SQLChains: A Native SQL Engine for Multidimensional Query Chain Execution

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

SQLChains is a native SQL engine that optimizes the execution of multidimensional query chains using the **cube flow paradigm**. It treats query chains as first-class citizens, reusing intermediate results as cubes and supporting generalized cube structures with pipelined execution.

## Features

- **Query Chain Execution**: Execute complex analytical workflows as dependent query sequences
- **Cube Flow Paradigm**: Intermediate results flow as cubes between queries
- **Generalized Cube Model**: Support for non-standard cubes (one-to-many coordinate-to-cell mappings)
- **Multiple Execution Modes**: Step-by-step or pipelined execution
- **Interactive Shell**: Continuous command input until `quit`
- **Multi-Database Support**: Compatible with DuckDB and ClickHouse SQL dialects

## Quick Start

### Prerequisites
- Java 8 or higher
- [DuckDB](https://duckdb.org/) (for data preparation and validation)

### Running
java -Xmx4g -Xms2g -jar dist/SQLChains.jar

Once started, you can enter commands interactively. Type `quit` to exit.

## Commands

### `list` - List and View Queries

# List all available query chains
list

# List queries in a specific chain
list TPC-C1

# Show full SQL for a specific query
list tpc-c1.q14

# Options for list command
list tpc-c1.q14 --size=3        # Use 3x scale factor for tables
list tpc-c1.q14 --ClickHouse     # Output ClickHouse-compatible SQL
list tpc-c1.q14 --nosort         # Remove ORDER BY clauses (except input queries)



| Chain | Dataset | Len | #Input (def/exec) | Description |
|-------|---------|-----|-------------------|-------------|
| **TPC-C1** | TPC-H (SF=1) | 14 | 3/2 | Multi-branch merge: min-max difference, ranking, branch aggregation, ratio computation, final merge |
| **TPC-C2** | TPC-H (SF=1) | 9 | 1/1 | Monthly shipment trend: daily aggregation, monthly share ratio, MoM delta |
| **S-C1** | Stocks (3-day) | 12 | 1/1 | Anomaly detection: rolling range, percentile filter, deviation count |
| **S-C2** | Stocks (3-day) | 14 | 1/1 | Pearson correlation: minute-over-minute returns, covariance, norm, correlation |
| **OR-C1** | Online Retail | 10 | 1/1 | Market basket analysis: self-join for item pairs, COUNT(DISTINCT), Lift computation |
| **OR-C2** | Online Retail | 9 | 1/1 | Cosine similarity: user-item vectors, dot product, L2 norm, similarity computation |

