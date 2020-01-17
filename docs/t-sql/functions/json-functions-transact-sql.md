---
title: JSON 関数 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: genemi
ms.technology: t-sql
ms.topic: language-reference
helpviewer_keywords:
- JSON functions
ms.assetid: ec97d451-06af-44a3-8304-305d410cfc8e
author: jovanpop-msft
ms.author: jovanpop
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 5b83e6f6eefce1cf56b71e7d433dca19cb4575d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109426"
---
# <a name="json-functions-transact-sql"></a>JSON 関数 (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

このセクションのページで説明されている関数を使用して、JSON テキストを検証または変更するか、単純または複雑な値を抽出します。  
  
|機能|[説明]|  
|--------------|-----------------|  
|[ISJSON](../../t-sql/functions/isjson-transact-sql.md)|文字列に有効な JSON が含まれているかどうかをテストします。|  
|[JSON_VALUE](../../t-sql/functions/json-value-transact-sql.md)|JSON 文字列からスカラー値を抽出します。|  
|[JSON_QUERY](../../t-sql/functions/json-query-transact-sql.md)|JSON 文字列からオブジェクトまたは配列を抽出します。|  
|[JSON_MODIFY](../../t-sql/functions/json-modify-transact-sql.md)|JSON 文字列内のプロパティの値を更新し、更新された JSON 文字列を返します。|

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] での JSON の組み込みサポートの詳細については、「[SQL Server の JSON データ](../../relational-databases/json/json-data-sql-server.md)」を参照してください。  

## <a name="see-also"></a>参照

 - [組み込み関数を使用した JSON データの検証、クエリ、変更 &#40;SQL Server&#41;](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md)
 - [JSON パス式 &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)
 - [JSON データ &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
