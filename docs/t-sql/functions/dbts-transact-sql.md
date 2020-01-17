---
title: '@@DBTS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@DBTS_TSQL'
- '@@DBTS'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@DBTS function'
- timestamp data type
ms.assetid: 91842ddd-91c0-4445-a03f-116f6bc991d0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 61743139f35ed3e8a5dd4bbac9bd1f4660cb2ec2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68136030"
---
# <a name="x40x40dbts-transact-sql"></a>&#x40;&#x40;DBTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

この関数は、現在のデータベースの現在の **timestamp** 型の値を返します。 現在のデータベースには、保証付きの一意のタイムスタンプ値が与えられます。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```
@@DBTS  
```  
  
## <a name="return-types"></a>戻り値の型
**varbinary**
  
## <a name="remarks"></a>Remarks  
@@DBTS は、現在のデータベースで最後に使用されたタイムスタンプを返します。 **timestamp** 列を持つ行を挿入するか更新すると、新しいタイムスタンプ値が生成されます。
  
トランザクション分離レベルでの変更は、@@DBTS 関数に影響を与えません。
  
## <a name="examples"></a>使用例  
この例は、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースから現在の **timestamp** を返します。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@DBTS;  
```  
  
## <a name="see-also"></a>参照
[構成関数 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)  
[カーソルのコンカレンシー &#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/properties/cursor-concurrency-odbc.md)  
[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40;Transact-SQL&#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)
  
  
