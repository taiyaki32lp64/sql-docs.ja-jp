---
title: managed_backup.fn_get_parameter (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- smart_admin.fn_get_parameter_TSQL
- smart_admin.fn_get_parameter
- fn_get_parameter_TSQL
- fn_get_parameter
dev_langs:
- TSQL
helpviewer_keywords:
- fn_get_parameter
- smart_admin.fn_get_parameter
ms.assetid: ed94e54d-4516-4806-a8ce-f013d3a04122
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 18a42273218bb73de55694b9b54877a4f2e0f669
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140652"
---
# <a name="managedbackupfngetparameter-transact-sql"></a>managed_backup.fn_get_parameter (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  パラメーターと値のペアから成る 0 行、1 行、または複数行を格納したテーブルを返します。  
  
 このストアド プロシージャを使用すると、Smart Admin のすべてまたは特定の構成設定を確認できます。  
  
 パラメーターがまだ構成されていない場合は、この関数は 0 行を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
managed_backup.fn_get_parameter ('parameter_name' | '' | NULL )  
```  
  
##  <a name="Arguments"></a> 引数  
 parameter_name  
 パラメーターの名前。 parameter_name は**nvarchar (128)** します。 NULL または空の文字列は、関数に引数として提供は、すべての名前と値のペアは Smart Admin のパラメーターが返されますを構成します。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|parameter_name|NVARCHAR (128)|パラメーターの名前。 次に、返されるパラメーターの現在の一覧を示します。<br/><br/>**FileRetentionDebugXevent**<br/><br/>**SSMBackup2WADebugXevent**<br/><br/>**SSMBackup2WANotificationEmailIds**<br/><br/>**SSMBackup2WAEnableUserDefinedPolicy**<br/><br/>**SSMBackup2WAEverConfigured**<br/><br/>**StorageOperationDebugXevent**|  
|parameter_value|NVARCHAR (128)|パラメーターの現在設定されている値。|  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 この関数に対する SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、少なくとも 1 回構成されたすべてのパラメーターとその現在の値を返します。  
  
```  
USE MSDB  
GO  
SELECT *   
FROM managed_backup.fn_get_parameter (NULL)  
  
```  
  
 次の例では、エラー通知の受信先として指定された電子メール ID を返します。 行に返しますがない場合、この電子メール通知のオプションが有効でないことを示します。  
  
```  
USE MSDB  
GO  
SELECT *  
FROM managed_backup.fn_get_parameter ('SSMBackup2WANotficationEmailIds')  
  
```  
  
## <a name="see-also"></a>関連項目  
 [Microsoft Azure への SQL Server マネージド バックアップ](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
