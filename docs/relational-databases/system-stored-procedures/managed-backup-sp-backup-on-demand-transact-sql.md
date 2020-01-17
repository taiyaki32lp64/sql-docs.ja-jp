---
title: managed_backup sp_backup_on_demand (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- smart_admin.sp_backup_on_demand
- smart_admin.sp_backup_on_demand_TSQL
- sp_backup_on_demand_TSQL
- sp_backup_on_demand
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.sp_backup_on_demand
- sp_backup_on_demand
ms.assetid: 638f809f-27fa-4c44-a549-9cf37ecc920c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e34cf20585ea7dcd3690d80ee415fc274bf852ca
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155399"
---
# <a name="managed_backupsp_backup_on_demand-transact-sql"></a>managed_backup sp_backup_on_demand (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  指定[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]されたデータベースのバックアップを実行するように要求します。  
  
 このストアド プロシージャを使用すると、[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]で構成されるデータベースに対してアドホック バックアップを実行できます。 これにより、バックアップチェーンと[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]プロセスの中断が認識され、バックアップが同じ Azure Blob ストレージコンテナーに格納されます。  
  
 バックアップが正常に完了すると、完全バックアップファイルのパスが返されます。 これには、バックアップ操作の結果として生成される新しいバックアップファイルの名前と場所が含まれます。  
  
 が指定された[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]データベースの指定された種類のバックアップを実行中の場合、エラーが返されます。 この場合、返されるエラー メッセージには、現在のバックアップのアップロード先となるバックアップ ファイルの完全なパスが含まれます。  
   
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
EXEC managed_backup.sp_backup_on_demand   
[@database_name  =]  'database name',[@type = ] { 'Database' | 'Log' }  
  
```  
  
##  <a name="Arguments"></a> 引数  
 @database_name  
 バックアップの実行対象となるデータベースの名前。 @database_nameは **SYSNAME** します。  
  
 @type  
 実行するバックアップの種類。データベースまたはログ。 パラメーターは**NVARCHAR (32)** です。 @type  
  
## <a name="return-code-value"></a>リターン コード値  
 0 (成功) または 1 (失敗)  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 **Db_backupoperator**データベースロールのメンバーシップ、 **ALTER ANY CREDENTIAL**権限、および**Sp_delete_backuphistory**ストアドプロシージャに対する**EXECUTE**権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、データベース ' TestDB ' のデータベースバックアップ要求を作成します。 このデータベースは[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]有効になっています。  
  
```  
Use MSDB  
Go  
EXEC managed_backup.sp_backup_on_demand  
 @database_name = 'TestDB'  
,@type = 'Database'  
  
```  
  
 各コードでは、言語属性フィールドで "tsql" を選択します。  
  
  
