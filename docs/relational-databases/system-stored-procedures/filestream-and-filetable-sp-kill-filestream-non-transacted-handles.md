---
title: sp_kill_filestream_non_transacted_handles (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_kill_filestream_non_transacted_handles_TSQL
- sp_kill_filestream_non_transacted_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sp_kill_filestream_non_transacted_handles
ms.assetid: 7188353e-ab29-49a0-8f25-7fb8ab122589
author: stevestein
ms.author: sstein
ms.openlocfilehash: 98c986c26c8d0d0cc6e2b8ff3573f0a20d938975
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942266"
---
# <a name="spkillfilestreamnontransactedhandles-transact-sql"></a>sp_kill_filestream_non_transacted_handles (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  FileTable データに対する非トランザクション ファイル ハンドルを閉じます。  
  
## <a name="syntax"></a>構文  
  
```sql  
sp_kill_filestream_non_transacted_handles [[ @table_name = ] 'table_name', [[ @handle_id = ] @handle_id]]  
```  
  
## <a name="arguments"></a>引数  
 *table_name*  
 非トランザクション ハンドルを閉じるテーブルの名前。  
  
 渡すことができます*table_name*せず*handle_id* FileTable に対する非トランザクション ハンドルを開くすべてを閉じます。  
  
 値に NULL を渡すことが*table_name*現在のデータベース内のすべての Filetable の非トランザクション ハンドルを開くすべてを閉じます。 既定値は NULL です。  
  
 *handle_id*  
 閉じる個々のハンドルのオプションの ID です。 取得することができます、 *handle_id*から、 [sys.dm_filestream_non_transacted_handles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)動的管理ビュー。 各 ID は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内で一意です。 指定した場合*handle_id*の値を指定する必要も*table_name*します。  
  
 値に NULL を渡すことが*handle_id*で指定された FileTable に対する非トランザクション ハンドルを開くすべてを閉じます*table_name*します。 既定値は NULL です。  
  
## <a name="return-code-value"></a>リターン コード値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-set"></a>結果セット  
 [なし] :  
  
## <a name="general-remarks"></a>全般的な解説  
 *Handle_id*によって必要な**sp_kill_filestream_non_transacted_handles** session_id またはその他で使用される作業単位には関連しない**kill**コマンド。  
  
 詳細については、「 [FileTable の管理](../../relational-databases/blob/manage-filetables.md)」を参照してください。  
  
## <a name="metadata"></a>メタデータ  
 開いている非トランザクション ファイル ハンドルのについては、動的管理ビューに対してクエリ[sys.dm_filestream_non_transacted_handles &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)します。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 必要があります**VIEW DATABASE STATE**からファイル ハンドルを取得するアクセス許可、 **sys.dm_FILESTREAM_non_transacted_handles**動的管理ビューおよび実行する**sp_kill_filestream_non_transacted_handles**します。  
  
## <a name="examples"></a>使用例  
 次の例を呼び出す方法を示して**sp_kill_filestream_non_transacted_handles**を FileTable データに対する非トランザクション ファイル ハンドルを閉じます。  
  
```sql  
-- Close all open handles in the current database.  
sp_kill_filestream_non_transacted_handles  
  
-- Close all open handles in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = 'myFileTable'  
  
-- Close a specific handle in myFileTable.  
sp_kill_filestream_non_transacted_handles @table_name = 'myFileTable', @handle_id = 0xFFFAAADD  
```  
  
 次の例では、スクリプトを使用して取得する方法を示しています、 *handle_id*して閉じます。  
  
```sql  
DECLARE @handle_id varbinary(16);  
DECLARE @table_name sysname;  
  
SELECT TOP 1 @handle_id = handle_id, @table_name = Object_name(table_id)  
FROM sys.dm_FILESTREAM_non_transacted_handles;  
  
EXEC sp_kill_filestream_non_transacted_handles @dbname, @table_name, @handle_id;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [FileTable の管理](../../relational-databases/blob/manage-filetables.md)  
 [Filestream および FileTable 動的管理ビュー (TRANSACT-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
 <br>[Filestream および FileTable のカタログ ビュー (TRANSACT-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
 <br>[sp_filestream_force_garbage_collection (TRANSACT-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)
  
