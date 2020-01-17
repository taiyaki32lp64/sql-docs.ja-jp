---
title: CLOSE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CLOSE_TSQL
- CLOSE
dev_langs:
- TSQL
helpviewer_keywords:
- closing cursors
- cursors [SQL Server], closing
- CLOSE statement
ms.assetid: 21546874-97e3-4b93-970f-87c27f6b78c7
author: rothja
ms.author: jroth
ms.openlocfilehash: 63234f9f337bd6427c4c5ed33c146e2ed3a714c9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950326"
---
# <a name="close-transact-sql"></a>CLOSE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在の結果セットを解放し、カーソルが置かれている行に設定されているカーソル ロックを解除して、開いているカーソルを閉じます。 `CLOSE` では、再度開けるようにデータ構造がアクセス可能なままになりますが、フェッチや位置指定更新は、カーソルを再度開くまで実行できません。 `CLOSE` は開いているカーソル上で実行する必要があります。宣言されただけのカーソルや、既に閉じているカーソルでは実行できません。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
CLOSE { { [ GLOBAL ] cursor_name } | cursor_variable_name }  
```  
  
## <a name="arguments"></a>引数  
 GLOBAL  
 *cursor_name* でグローバル カーソルを参照することを指定します。  
  
 *cursor_name*  
 開いているカーソルの名前です。 グローバルとローカル カーソルの両方が存在かどうか *cursor_name* いう名前の *cursor_name* GLOBAL が指定されている、それ以外の場合はグローバル カーソルを参照 *cursor_name* は、ローカル カーソルを参照します。  
  
 *cursor_variable_name*  
 開いているカーソルに関連付けられたカーソル変数の名前です。  
  
## <a name="examples"></a>使用例  
 次の例では、カーソルを使用した処理での `CLOSE` ステートメントの正しい位置を示しています。  
  
```sql  
DECLARE Employee_Cursor CURSOR FOR  
SELECT EmployeeID, Title FROM AdventureWorks2012.HumanResources.Employee;  
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
 [カーソル](../../relational-databases/cursors.md)   
 [カーソル &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
