---
title: SQL Server 監査レコード | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- audit records [SQL Server]
ms.assetid: 7a291015-df15-44fe-8d53-c6d90a157118
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2681d021099e8b10150efd255e27cf436c665a90
ms.sourcegitcommit: b7618a2a7c14478e4785b83c4fb2509a3e23ee68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73926030"
---
# <a name="sql-server-audit-records"></a>SQL Server 監査レコード
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査機能を使用すると、サーバー レベルおよびデータベース レベルのイベントのグループおよびイベントを監査することができます。 詳しくは、「[SQL Server Audit &#40;データベース エンジン&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]」をご覧ください。  
  
 監査は、監査 *対象*に記録される 0 個以上の監査アクション項目で構成されます。 監査ターゲットには、バイナリ ファイル、Windows アプリケーション イベント ログ、または Windows セキュリティ イベント ログを使用できます。 ターゲットに送信されるレコードに含まれる可能性がある要素を次の表に示します。  
  
|列名|[説明]|型|常に使用可能かどうか|  
|-----------------|-----------------|----------|----------------------|  
|**event_time**|監査可能なアクションが発生した日付/時刻。|**datetime2**|はい|  
|**sequence_no**|大きすぎて監査の書き込みバッファーに収まらなかった 1 つの監査レコード内のレコードの順序を追跡します。|**int**|はい|  
|**action_id**|アクションの ID。<br /><br /> ヒント:**action_id** を述語として使用するには、文字列から数値に変換する必要があります。 詳細については、「 [Filter SQL Server Audit on action_id / class_type predicate (action_id/class_type 述語での SQL Server 監査のフィルター選択)](https://blogs.msdn.com/b/sqlsecurity/archive/2012/10/03/filter-sql-server-audit-on-action-id-class-type-predicate.aspx)」を参照してください。|**varchar (4)**|はい|  
|**succeeded**|監査イベントをトリガーするアクションのアクセス許可のチェックが成功または失敗したかどうかを示します。 |**bit**<br /> - 1 = 成功 <br />0 = 失敗|はい|  
|**permission_bitmask**|権限の許可、拒否、または取り消しを示します (該当する場合)。|**bigint**|いいえ|  
|**is_column_permission**|列レベル権限を示すフラグ。|**bit** <br />- 1 = True <br />0 = False|いいえ|  
|**session_id**|イベントが発生したセッションの ID。|**int**|はい|  
|**server_principal_id**|アクションが実行されるログイン コンテキストの ID。|**int**|はい|  
|**database_principal_id**|アクションが実行されるデータベース ユーザー コンテキストの ID。|**int**|いいえ|  
|**object_id**|監査が発生したエンティティのプライマリ ID。 この ID には次が可能です。<br /><br /> サーバー オブジェクト<br /><br /> データベース<br /><br /> データベース オブジェクト<br /><br /> スキーマ オブジェクト|**int**|いいえ|  
|**target_server_principal_id**|監査可能なアクションが適用されるサーバー プリンシパル。|**int**|はい|  
|**target_database_principal_id**|監査可能なアクションが適用されるデータベース プリンシパル。|**int**|いいえ|  
|**class_type**|監査が発生する監査可能なエンティティの種類。|**varchar(2)**|はい|  
|**session_server_principal_name**|セッションのサーバー プリンシパル。|**sysname**|はい|  
|**server_principal_name**|現在のログイン。|**sysname**|はい|  
|**server_principal_sid**|現在のログイン SID。|**varbinary**|はい|  
|**database_principal_name**|現在のユーザー。|**sysname**|いいえ|  
|**target_server_principal_name**|アクションの対象ログイン。|**sysname**|いいえ|  
|**target_server_principal_sid**|対象ログインの SID。|**varbinary**|いいえ|  
|**target_database_principal_name**|アクションの対象ユーザー。|**sysname**|いいえ|  
|**server_instance_name**|監査が発生したサーバー インスタンスの名前。 標準の machine\instance の形式を使用します。|**nvarchar(120)**|はい|  
|**database_name**|アクションが発生したデータベース コンテキスト。|**sysname**|いいえ|  
|**schema_name**|アクションが発生したスキーマ コンテキスト。|**sysname**|いいえ|  
|**object_name**|監査が発生したエンティティの名前。 この名前には次が可能です。<br /><br /> サーバー オブジェクト<br /><br /> データベース<br /><br /> データベース オブジェクト<br /><br /> スキーマ オブジェクト<br /><br /> TSQL ステートメント (あれば)|**sysname**|いいえ|  
|**statement**|TSQL ステートメント (あれば)|**nvarchar (4000)**|いいえ|  
|**additional_information**|XML として格納されるイベントに関する追加情報。|**nvarchar (4000)**|いいえ|  
  
## <a name="remarks"></a>Remarks  
 アクションに該当しないために列の値が設定されない場合もあります。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 監査は、監査レコードの文字フィールドに 4,000 文字のデータを格納します。 監査可能なアクションから返される **additional_information** と **statement** の値が 4,000 文字を超えていた場合は、そのデータを記録するために、 **sequence_no** 列を使用して 1 つの監査アクションの監査レポートに複数のレコードが書き込まれます。 このプロセスは次のとおりです。  
  
-   **statement** 列が 4,000 文字に分割されます。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分割されたデータが監査レコードの最初の行として書き込まれます。 他のすべてのフィールドは各行で複製されます。  
  
-   **sequence_no** の値が増加されます。  
  
-   すべてのデータが記録されるまでこのプロセスが繰り返されます。  
  
 このデータに接続するには、 **sequence_no** の値を使用して行を順番に読み取ります。アクションを識別するには、 **event_Time**、 **action_id** 、および **session_id** の各列を使用します。  
  
## <a name="related-content"></a>関連コンテンツ  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md)  
  
 [ALTER SERVER AUDIT  &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-audit-transact-sql.md)  
  
 [DROP SERVER AUDIT  &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-audit-transact-sql.md)  
  
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-specification-transact-sql.md)  
  
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-audit-specification-transact-sql.md)  
  
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-audit-specification-transact-sql.md)  
  
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-audit-specification-transact-sql.md)  
  
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-audit-specification-transact-sql.md)  
  
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-database-audit-specification-transact-sql.md)  
  
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-authorization-transact-sql.md)  
  
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)  
  
 [sys.server_audits &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)  
  
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)  
  
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)  
  
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)  
  
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)  
  
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)  
  
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)  
  
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)  
  
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)  
  
  
