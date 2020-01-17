---
title: ISNUMERIC (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ISNUMERIC
- ISNUMERIC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], valid numeric type
- numeric data
- ISNUMERIC function
- verifying valid numeric type
- valid numeric type [SQL Server]
- checking valid numeric type
ms.assetid: 7aa816de-529a-4f6c-a99f-4d5a9ef599eb
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 75693068e1aa030f9027b1918becd27e8ec9cc5c
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843612"
---
# <a name="isnumeric-transact-sql"></a>ISNUMERIC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  式が数値型として有効かどうかを調べます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
ISNUMERIC ( expression )  
```  
  
## <a name="arguments"></a>引数  
 *式 (expression)*  
 評価対象となる[式](../../t-sql/language-elements/expressions-transact-sql.md)を指定します。  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
## <a name="remarks"></a>Remarks  
 ISNUMERIC は、入力式が有効な数値データ型であると判断される場合に 1 を返します。それ以外の場合は 0 を返します。 有効な[数値データ型](../../t-sql/data-types/numeric-types.md)は次のとおりです。  

|||
|-|-|
| [真数](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md) | **bigint**、**int**、**smallint**、**tinyint**、**bit** |
| [固定有効桁数](../../t-sql/data-types/decimal-and-numeric-transact-sql.md) | **decimal**、**numeric** |
| [概数](../../t-sql/data-types/float-and-real-transact-sql.md) | **float**、**real** |
| [通貨値](../../t-sql/data-types/money-and-smallmoney-transact-sql.md) | **money**、 **smallmoney** |

  
> [!NOTE]  
>  ISNUMERIC は、数字以外の一部の文字に対して 1 を返します。たとえばプラス (+)、マイナス (-)、ドル記号 ($) などの通貨記号がこれに該当します。 通貨記号の完全な一覧を参照してください[ money および smallmoney &#40;Transact-SQL&#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md).  
  
## <a name="examples"></a>使用例  
 この例では、`ISNUMERIC` を使用して数値型でないすべての郵便番号を返しています。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, PostalCode  
FROM Person.Address   
WHERE ISNUMERIC(PostalCode)<> 1;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 この例では、`ISNUMERIC` を使用して数値型でないすべての郵便番号を返しています。  
  
```  
USE master;  
GO  
SELECT name, isnumeric(name) AS IsNameANumber, database_id, isnumeric(database_id) AS IsIdANumber   
FROM sys.databases;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  

