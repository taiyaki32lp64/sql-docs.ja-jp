---
title: データ型の優先順位 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- precedence [SQL Server]
- data types [SQL Server], converting
- data types [SQL Server], precedence
- converting data types [SQL Server], precedence
- precedence [SQL Server], data types
ms.assetid: f4c804ab-ed3f-43b1-a024-c9ac6944b66b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bcf14745af6da26cc625e928d75f510e0da9a2e8
ms.sourcegitcommit: 823d7bdfa01beee3cf984749a8c17888d4c04964
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70030353"
---
# <a name="data-type-precedence-transact-sql"></a>データ型の優先順位 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md.md](../../includes/tsql-appliesto-ss2012-all-md.md)]

演算子でデータ型が異なる 2 つの式を結合すると、最初に優先順位の低いデータ型が優先順位の高いデータ型に変換されます。 暗黙的な変換がサポートされていない場合は、エラーが返されます。 同じデータ型を持つオペランド式を結合する演算子の場合、演算の結果も同じデータ型になります。
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、次のデータ型の優先順位が使用されます。
  
1.  ユーザー定義データ型 (最高)  
1.  **sql_variant**  
1.  **xml**  
1.  **datetimeoffset**  
1.  **datetime2**  
1.  **datetime**  
1.  **smalldatetime**  
1.  **date**  
1. **time**  
1. **float**  
1. **real**  
1. **decimal**  
1. **money**  
1. **smallmoney**  
1. **bigint**  
1. **int**  
1. **smallint**  
1. **tinyint**  
1. **bit**  
1. **ntext**  
1. **text**  
1. **image**  
1. **timestamp**  
1. **uniqueidentifier**  
1. **nvarchar** (**nvarchar(max)** など)  
1. **nchar**  
1. **varchar** (**varchar(max)** など)  
1. **char**  
1. **varbinary** (**varbinary(max)** など)  
1. **binary** (最低)  
  
## <a name="see-also"></a>参照
[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
