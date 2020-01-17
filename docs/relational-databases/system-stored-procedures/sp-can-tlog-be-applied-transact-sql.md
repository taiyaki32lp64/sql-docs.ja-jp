---
title: sp_can_tlog_be_applied (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_can_tlog_be_applied_TSQL
- sp_can_tlog_be_applied
dev_langs:
- TSQL
helpviewer_keywords:
- sp_can_tlog_be_applied
ms.assetid: 9c143b6c-27ac-4ab7-98d1-3b7b265f3963
author: stevestein
ms.author: sstein
ms.openlocfilehash: 279492503ba8ce31e3c5d4027d8fd184c4a81587
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045961"
---
# <a name="spcantlogbeapplied-transact-sql"></a>sp_can_tlog_be_applied (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  トランザクション ログ バックアップを適用できるかどうかを確認、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。 **sp_can_tlog_be_applied**データベースは Restoring 状態である必要があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_can_tlog_be_applied [ @backup_file_name = ] 'backup_file_name'   
        , [ @database_name = ] 'database_name'   
        , [ @result = ] result OUTPUT  
```  
  
## <a name="arguments"></a>引数  
`[ @backup_file_name = ] 'backup_file_name'` バックアップ ファイルの名前です。 *backup_file_name*は**nvarchar (128)** します。  
  
`[ @database_name = ] 'database_name'` データベースの名前です。 *database_name* は **sysname** です。  
  
`[ @result = ] _result_ OUTPUT` トランザクション ログをデータベースに適用できるかどうかを示します。 *結果*は**ビット**します。  
  
 1 = ログを適用できる  
  
 0 = ログを適用することはできません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールが実行できる**sp_can_tlog_be_applied**します。  
  
## <a name="examples"></a>使用例  
 次の例では、結果を格納するローカル変数 `@MyBitVar` を宣言します。  
  
```  
USE master;  
GO  
DECLARE @MyBitVar BIT;  
EXEC sp_can_tlog_be_applied  
     @backup_file_name =   
N'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup\AdventureWorks2012.bak',  
     @database_name = N'AdventureWorks2012',  
     @result = @MyBitVar OUTPUT;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
