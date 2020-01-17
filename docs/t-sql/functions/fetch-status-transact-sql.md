---
title: '@@FETCH_STATUS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@FETCH_STATUS'
- '@@FETCH_STATUS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- FETCH statement
- status information [SQL Server], FETCH
- '@@FETCH_STATUS function'
ms.assetid: 93659193-e4ff-4dfb-9043-0c4114921b91
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d07892e1a47025107205f590d6a41aebebbb571a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071563"
---
# <a name="x40x40fetchstatus-transact-sql"></a>&#x40;&#x40;FETCH_STATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

この館数は、接続によって現在オープンされているカーソルに対して最後に実行した FETCH ステートメントの状態を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
@@FETCH_STATUS  
```  
  
## <a name="return-type"></a>戻り値の型  
 **整数 (integer)**  
  
## <a name="return-value"></a>戻り値  
  
|戻り値|[説明]|  
|------------------|-----------------|  
|&nbsp;0|FETCH ステートメントは正常に実行されました。|  
|-1|FETCH ステートメントが失敗したか、または行が結果セットに収まりません。|  
|-2|フェッチした行がありません。|
|-9|カーソルはフェッチ操作を実行しません。|  
  
## <a name="remarks"></a>Remarks  
`@@FETCH_STATUS` は接続時のすべてのカーソルに対してグローバルであるため、慎重に使用してください。 FETCH ステートメントを実行した後、別のカーソルに対して他の FETCH ステートメントを実行する前に、`@@FETCH_STATUS` を調べる必要があります。 接続時にフェッチが実行されるまで、`@@FETCH_STATUS` は未定義です。  
  
たとえば、ユーザーがあるカーソルからの FETCH ステートメントを実行します。次に、別のカーソルからの結果を開いて処理するためのストアド プロシージャを呼び出します。 呼び出したストアド プロシージャから制御が戻された時点で、`@@FETCH_STATUS` は、ストアド プロシージャを呼び出す前に実行された FETCH ステートメントではなく、ストアド プロシージャ内で最後に実行された FETCH ステートメントを反映します。  
  
特定のカーソルの最後のフェッチの状態を取得するには、動的管理関数 **sys.dm_exec_cursors** の **fetch_status** 列のクエリを実行します。  
  
## <a name="examples"></a>使用例  
この例では、`@@FETCH_STATUS` を使用して `WHILE` ループ内のカーソルの動作を制御します。  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT BusinessEntityID, JobTitle  
FROM AdventureWorks2012.HumanResources.Employee;  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      FETCH NEXT FROM Employee_Cursor;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [カーソル関数 &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  
