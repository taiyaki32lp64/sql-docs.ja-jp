---
title: 集計関数 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], aggregate
- aggregate functions [SQL Server], about aggregate functions
- summarizing functions
- aggregate functions [SQL Server]
ms.assetid: 0c06ae42-eb0a-4d77-9d74-aa1e7f344009
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 935d0b9bd98c9be5bb1fa4c7000a26fcd4299035
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040392"
---
# <a name="aggregate-functions-transact-sql"></a>集計関数 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

集計関数は、値の集まりに対して計算を実行し、1 つの値を返します。 `COUNT` を除くその他の集計関数は NULL 値を無視します。 集計関数は、SELECT ステートメントの GROUP BY 句と共によく使用されます。
  
集計関数はすべて決定的です。 つまり集計関数は、特定の入力値のセットと共に呼び出された場合、そのたびに同じ値を返します。 関数の決定性の詳細については、「[決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。 [OVER 句](../../t-sql/queries/select-over-clause-transact-sql.md)は、STRING_AGG、GROUPING、または GROUPING_ID 関数を除くすべての集計関数の後に使用できます。
  
集計関数は、次の状況でのみ式として使用できます。
-   SELECT ステートメントの選択リスト (サブクエリまたは外部クエリ)。  
-   HAVING 句  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] には、次の集計関数が用意されています。
  
|||
|-|-|
|[APPROX_COUNT_DISTINCT](../../t-sql/functions/approx-count-distinct-transact-sql.md)| [MIN](../../t-sql/functions/min-transact-sql.md)|
|[AVG](../../t-sql/functions/avg-transact-sql.md)|[STDEV](../../t-sql/functions/stdev-transact-sql.md)|
|[CHECKSUM_AGG](../../t-sql/functions/checksum-agg-transact-sql.md)|[STDEVP](../../t-sql/functions/stdevp-transact-sql.md)|
|[COUNT](../../t-sql/functions/count-transact-sql.md)|[STRING_AGG](../../t-sql/functions/string-agg-transact-sql.md)|
|[COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md)|[SUM](../../t-sql/functions/sum-transact-sql.md)|
|[GROUPING](../../t-sql/functions/grouping-transact-sql.md)|[VAR](../../t-sql/functions/var-transact-sql.md)|
|[GROUPING_ID](../../t-sql/functions/grouping-id-transact-sql.md)|[VARP](../../t-sql/functions/varp-transact-sql.md)|
|[MAX](../../t-sql/functions/max-transact-sql.md)||
  
## <a name="see-also"></a>参照
[組み込み関数 &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[OVER 句 &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
