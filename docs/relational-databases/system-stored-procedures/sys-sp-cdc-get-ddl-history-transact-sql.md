---
title: sys.sp_cdc_get_ddl_history (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_get_ddl_history
- sp_cdc_get_ddl_history_TSQL
- sys.sp_cdc_get_ddl_history_TSQL
- sys.sp_cdc_get_ddl_history
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], querying metadata
- sp_cdc_get_ddl_history
- sys.sp_cdc_get_ddl_history
ms.assetid: 4dee5e2e-d7e5-4fea-8037-a4c05c969b3a
author: rothja
ms.author: jroth
ms.openlocfilehash: bb4622b36901afc7ff04eacbfe840a9adda5b214
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083733"
---
# <a name="syssp_cdc_get_ddl_history-transact-sql"></a>sys.sp_cdc_get_ddl_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  そのキャプチャ インスタンスに対して変更データ キャプチャが有効にされて、指定したキャプチャ インスタンスに関連付けられたデータ定義言語 (DDL) の変更履歴を返します。 変更データ キャプチャは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディッションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_get_ddl_history [ @capture_instance = ] 'capture_instance'  
```  
  
## <a name="arguments"></a>引数  
 [ @capture_instance =] '*capture_instance*'  
 ソース テーブルに関連付けられたキャプチャ インスタンスの名前です。 *capture_instance*は**sysname** NULL にすることはできません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|source_schema|**sysname**|ソース テーブルのスキーマ名です。|  
|source_table|**sysname**|ソース テーブルの名前。|  
|capture_instance|**sysname**|キャプチャ インスタンスの名前です。|  
|required_column_update|**bit**|DDL の変更で、ソース列に対して行われたデータ型の変更を反映するために、変更テーブルの列を更新する必要があったことを示します。|  
|ddl_command|**nvarchar(max)**|ソース テーブルに適用された DDL ステートメントです。|  
|ddl_lsn|**binary(10)**|ログ シーケンス番号 (LSN) の DDL の変更に関連付けられています。|  
|ddl_time|**datetime**|DDL の変更に関連付けられた時刻です。|  
  
## <a name="remarks"></a>コメント  
 ソース テーブルの列構造の追加や、列を削除する既存の列のデータ型の変更などを変更するソース テーブルに対する DDL の変更が保持されます、 [cdc.ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md)テーブル。 このストアド プロシージャでは、こうした変更をレポートできます。 cdc.ddl_history のエントリは、キャプチャ プロセスで、ログから DDL トランザクションが読み取られた時点で作成されます。  
  
## <a name="permissions"></a>アクセス許可  
 データベースのすべてのキャプチャ インスタンスの行を取得するには、db_owner 固定データベース ロールのメンバーシップが必要です。 それ以外のすべてのユーザーについては、ソース テーブルのすべてのキャプチャ対象列に対する SELECT 権限が必要です。さらに、キャプチャ インスタンスのゲーティング ロールが定義されている場合は、そのデータベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、ソース テーブルに列を追加`HumanResources.Employee`し、実行、`sys.sp_cdc_get_ddl_history`ストアド プロシージャは、キャプチャ インスタンスに関連付けられているソース テーブルに適用される DDL の変更を報告する`HumanResources_Employee`します。  
  
```  
USE AdventureWorks2012;  
GO  
ALTER TABLE HumanResources.Employee  
ADD Test_Column int NULL;  
GO  
-- Pause 10 seconds to allow the event to be logged.   
WAITFOR DELAY '00:00:10';  
GO   
EXECUTE sys.sp_cdc_get_ddl_history   
    @capture_instance = 'HumanResources_Employee';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sys.sp_cdc_help_change_data_capture &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
