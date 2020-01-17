---
title: managed_backup.sp_set_parameter (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_set_parameter_TSQL
- sp_set_parameter
- smart_admin.sp_set_parameter
- smart_admin.sp_set_parameter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_parameter
- smart_admin.sp_set_parameter
ms.assetid: bd8ae5fd-1337-4b7f-b0a4-153cbca9fa5f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 838a8b0d998476a37b0dd4d30cab5041ad4276a0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942032"
---
# <a name="managedbackupspsetparameter-transact-sql"></a>managed_backup.sp_set_parameter (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  指定された Smart Admin システム パラメーターの値を設定します。  
  
 使用可能なパラメーターは、[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]に関連します。 これらのパラメーターは、電子メール通知を設定し、特定の拡張イベントを有効にする、ユーザー ポリシー ベースの管理ポリシーの設定を有効にするに使用されます。 パラメーター名とパラメーター値のペアを指定する必要があります.  

  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
EXEC managed_backup.sp_set_parameter   
    [@parameter_name = ] {'SSMBackup2WANotificationEmailIds' | 'SSMBackup2WAEnableUserDefinedPolicy' | 'SSMBackup2WADebugXevent' | 'FileRetentionDebugXevent' | 'StorageOperationDebugXevent'}  
    ,[@parameter_value = ] 'parameter_value'  
```  
  
##  <a name="Arguments"></a> 引数  
 @parameter_name  
 値を設定するパラメーターの名前。 @parameter_name nvarchar (128) です。 使用可能なパラメーター名は**SSMBackup2WANotificationEmailIds**、 **SSMBackup2WADebugXevent**、 **SSMBackup2WAEnableUserDefinedPolicy**、 **FileRetentionDebugXevent**、および**StorageOperationDebugXevent**します。  
  
 @parameter_value  
 設定するパラメーターの値。 @parameter 値は、nvarchar (128) です。  許容されているパラメーターの名前と値のペアは次のとおりです。  
  
-   @parameter_name = 'SSMBackup2WANotificationEmailIds': @parameter_value = '電子メール'  
  
-   @parameter_name = 'SSMBackup2WAEnableUserDefinedPolicy': @parameter_value = {'true' |false'}  
  
-   @parameter_name = 'SSMBackup2WADebugXevent': @parameter_value = {'true' |false'}  
  
-   @parameter_name = 'FileRetentionDebugXevent' : @parameter_value  = { 'true' | 'false' }  
  
-   @parameter_name = 'StorageOperationDebugXevent' = { 'true' | 'false' }  
  
## <a name="return-code-value"></a>リターン コード値  
 0 (成功) または 1 (失敗)  
  
## <a name="best-practices"></a>ベスト プラクティス  
 ステートメントまたはルーチンを実行するときに、ユーザーが知っておく必要がベスト プラクティスについて説明する省略可能なセクションです。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 必要があります**EXECUTE**に対する**managed_backup.sp_set_parameter**ストアド プロシージャ。  
  
## <a name="examples"></a>使用例  
 次の例では、運用を有効にし、拡張イベントをデバッグします。  
  
```  
-- to enable operational events  
Use msdb;  
Go  
         EXEC managed_backup.sp_set_parameter 'FileRetentionOperationalXevent', 'True'  
--  to enable debug events  
Use msdb;  
Go  
         EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
```  
  
 次の例では、エラーおよび警告の電子メール通知を有効にしに通知の送信に使用する emailID を設定します。  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_set_parameter @parameter_name = 'SSMBackup2WANotificationEmailIds', @parameter_value = '<email address>'  
  
```  
  
  
