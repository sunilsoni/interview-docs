---
title: Database
has_children: true
nav_order: 2
permalink: docs/database
resource: true
desc: "Database interview questions and answers."
categories: [Database]
---

# Database
{: .no_toc }

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

## Increase SQL performance

- Every index increases the time takes to perform INSERTS, UPDATES, and DELETES, so the number of indexes should not be too much. Try to use maximum 4-5 indexes on one table, not more. If you have read-only table, then the number of indexes may be increased.

- Keep your indexes as narrow as possible. This reduces the size of the index and reduces the number of reads required to read the index.

- Try to create indexes on columns that have integer values rather than character values.

- If you create a composite (multi-column) index, the orders of the columns in the key are very important. Try to order the columns in the key as to enhance selectivity, with the most selective columns to the leftmost of the key.

- If you want to join several tables, try to create surrogate integer keys for this purpose and create indexes on their columns. Create surrogate integer primary key (identity for example) if your table will not have many insert operations.

- Clustered indexes are more preferable than nonclustered, if you need to select by a range of values or you need to sort results set with GROUP BY or ORDER BY. If your application will be performing the same query over and over on the same table, consider creating a covering index on the table.

- You can use the SQL Server Profiler Create Trace Wizard with "Identify Scans of Large Tables" trace to determine which tables in your database may need indexes. This trace will show which tables are being scanned by queries instead of using an index.


### Reasons of poor performance of query.

Following are the reasons for the poor performance of a query:

-  No indexes.
-  Excess recompilations of stored procedures.
-  Procedures and triggers without SET NOCOUNT ON.
-  Poorly written query with unnecessarily complicated joins.
-  Highly normalized database design.
-  Excess usage of cursors and temporary tables.
-  Queries with predicates that use comparison operators between different columns of the same table.
-  Queries with predicates that use operators, and any one of the following are true:
-  There are no statistics on the columns involved on either side of the operators.
-  The distribution of values in the statistics is not uniform, but the query seeks a highly selective value set. This situation can be especially true if the operator is anything other than the equality (=) operator.
-  The predicate uses the not equal to (!=) comparison operator or the NOT logical operator.
-  Queries that use any of the SQL Server built-in functions or a scalar-valued, user-defined function whose argument is not a constant value.
-  Queries that involve joining columns through arithmetic or string concatenation operators.
-  Queries that compare variables whose values are not known when the query is compiled and optimized.


