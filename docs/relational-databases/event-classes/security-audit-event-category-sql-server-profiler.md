---
title: セキュリティ監査イベント カテゴリ - プロファイラー
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Security Audit event category [SQL Server]
- event classes [SQL Server], Security Audit event category
- SQL Server event classes, Security Audit event category
ms.assetid: e64f7695-2f23-4adb-b83d-52f147cc1a2f
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f07afead7d74b358c0220dc7ed22dbf31ebbf11a
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056048"
---
# <a name="security-audit-event-category-sql-server-profiler"></a>Security Audit イベント カテゴリ (SQL Server Profiler)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Security Audit** イベント カテゴリには、セキュリティ監査イベントが含まれています。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[Audit Add DB User イベント クラス](../../relational-databases/event-classes/audit-add-db-user-event-class.md)|データベース ユーザーとしてデータベースにログインが追加または削除されたことを示します。|  
|[Audit Add Login to Server Role イベント クラス](../../relational-databases/event-classes/audit-add-login-to-server-role-event-class.md)|固定サーバー ロールにログインが追加または削除されたことを示します。|  
|[Audit Add Member to DB Role イベント クラス](../../relational-databases/event-classes/audit-add-member-to-db-role-event-class.md)|ロールにログインが追加または削除されたことを示します。|  
|[Audit Add Role イベント クラス](../../relational-databases/event-classes/audit-add-role-event-class.md)|データベースにデータベース ロールが追加または削除されたことを示します。|  
|[Audit Addlogin イベント クラス](../../relational-databases/event-classes/audit-addlogin-event-class.md)|ログインが追加または削除されたことを示します。|  
|[Audit App Role Change Password イベント クラス](../../relational-databases/event-classes/audit-app-role-change-password-event-class.md)|アプリケーション ロールのパスワードが変更されたことを示します。|  
|[Audit Backup/Restore イベント クラス](../../relational-databases/event-classes/audit-backup-and-restore-event-class.md)|バックアップ ステートメントまたは復元ステートメントが発行されたことを示します。|  
|[Audit Broker Conversation イベント クラス](../../relational-databases/event-classes/audit-broker-conversation-event-class.md)|Service Broker ダイアログ セキュリティに関する監査メッセージを報告します。|  
|[Audit Broker Login イベント クラス](../../relational-databases/event-classes/audit-broker-login-event-class.md)|Service Broker トランスポート セキュリティに関する監査メッセージを報告します。|  
|[Audit Change Audit イベント クラス](../../relational-databases/event-classes/audit-change-audit-event-class.md)|監査トレースに変更が加えられたことを示します。|  
|[Audit Change Database Owner イベント クラス](../../relational-databases/event-classes/audit-change-database-owner-event-class.md)|データベースの所有者を変更する権限がチェックされたことを示します。|  
|[Audit Database Management イベント クラス](../../relational-databases/event-classes/audit-database-management-event-class.md)|データベースが作成、変更、または削除されたことを示します。|  
|[Audit Database Mirroring Login イベント クラス](../../relational-databases/event-classes/audit-database-mirroring-login-event-class.md)|データベース ミラーリングのトランスポート セキュリティに関する監査メッセージを報告します。|  
|[Audit Database Object Access イベント クラス](../../relational-databases/event-classes/audit-database-object-access-event-class.md)|スキーマなどのデータベース オブジェクトがアクセスされたことを示します。|  
|[Audit Database Object GDR イベント クラス](../../relational-databases/event-classes/audit-database-object-gdr-event-class.md)|データベース オブジェクトの GDR イベントが発生したことを示します。|  
|[Audit Database Object Management イベント クラス](../../relational-databases/event-classes/audit-database-object-management-event-class.md)|データベース オブジェクトで CREATE、ALTER、または DROP のいずれかのステートメントが実行されたことを示します。|  
|[Audit Database Object Take Ownership イベント クラス](../../relational-databases/event-classes/audit-database-object-take-ownership-event-class.md)|データベース スコープ内でオブジェクトの所有者が変更されたことを示します。|  
|[Audit Database Operation イベント クラス](../../relational-databases/event-classes/audit-database-operation-event-class.md)|チェックポイント処理やクエリ通知のサブスクライブなど、さまざまな操作が行われたことを示します。|  
|[Audit Database Principal Impersonation イベント クラス](../../relational-databases/event-classes/audit-database-principal-impersonation-event-class.md)|データベース スコープ内で権限の借用が行われたことを示します。|  
|[Audit Database Principal Management イベント クラス](../../relational-databases/event-classes/audit-database-principal-management-event-class.md)|データベースのプリンシパルが作成、変更、または削除されたことを示します。|  
|[Audit Database Scope GDR イベント クラス](../../relational-databases/event-classes/audit-database-scope-gdr-event-class.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のユーザーがステートメント権限に関して GRANT、REVOKE、DENY のいずれかを実行したことを示します。|  
|[Audit DBCC イベント クラス](../../relational-databases/event-classes/audit-dbcc-event-class.md)|DBCC コマンドが発行されたことを示します。|  
|[Audit Fulltext イベント クラス](../../relational-databases/event-classes/audit-fulltext-event-class.md)|フルテキスト イベントが発生したことを示します。|  
|[Audit Login Change Password イベント クラス](../../relational-databases/event-classes/audit-login-change-password-event-class.md)|ユーザーが自身の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン パスワードを変更したことを示します。|  
|[Audit Login Change Property イベント クラス](../../relational-databases/event-classes/audit-login-change-property-event-class.md)|**sp_defaultdb**、 **sp_defaultlanguage**、または ALTER LOGIN を使用してログインのプロパティが変更されたことを示します。|  
|[Audit Login イベント クラス](../../relational-databases/event-classes/audit-login-event-class.md)|ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に正常にログインしたことを示します。|  
|[Audit Login Failed イベント クラス](../../relational-databases/event-classes/audit-login-failed-event-class.md)|ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] へのログインを試みて失敗したことを示します。|  
|[Audit Login GDR イベント クラス](../../relational-databases/event-classes/audit-login-gdr-event-class.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ログインの権利が追加または削除されたことを示します。|  
|[Audit Logout イベント クラス](../../relational-databases/event-classes/audit-logout-event-class.md)|ユーザーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からログアウトしたことを示します。|  
|[Audit Object Derived Permission イベント クラス](../../relational-databases/event-classes/audit-object-derived-permission-event-class.md)|オブジェクトに対して CREATE、ALTER、または DROP が発行されたことを示します。|  
|[Audit Schema Object Access イベント クラス](../../relational-databases/event-classes/audit-schema-object-access-event-class.md)|オブジェクトの権限 (SELECT など) が使用されたことを示します。|  
|[Audit Schema Object GDR イベント クラス](../../relational-databases/event-classes/audit-schema-object-gdr-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のユーザーがスキーマ オブジェクト権限に関して GRANT、REVOKE、DENY のいずれかを実行したことを示します。|  
|[Audit Schema Object Management イベント クラス](../../relational-databases/event-classes/audit-schema-object-management-event-class.md)|サーバー オブジェクトが作成、変更、または削除されたことを示します。|  
|[Audit Schema Object Take Ownership イベント クラス](../../relational-databases/event-classes/audit-schema-object-take-ownership-event-class.md)|スキーマ オブジェクトの所有者を変更する権限がチェックされたことを示します。|  
|[Audit Server Alter Trace イベント クラス](../../relational-databases/event-classes/audit-server-alter-trace-event-class.md)|ALTER TRACE 権限がチェックされたことを示します。|  
|[Audit Server Object GDR イベント クラス](../../relational-databases/event-classes/audit-server-object-gdr-event-class.md)|スキーマ オブジェクトの GDR イベントが発生したことを示します。|  
|[Audit Server Object Management イベント クラス](../../relational-databases/event-classes/audit-server-object-management-event-class.md)|サーバー オブジェクトに対して CREATE、ALTER、または DROP のいずれかのイベントが発生したことを示します。|  
|[Audit Server Object Take Ownership イベント クラス](../../relational-databases/event-classes/audit-server-object-take-ownership-event-class.md)|サーバー オブジェクトの所有者が変更されたことを示します。|  
|[Audit Server Operation イベント クラス](../../relational-databases/event-classes/audit-server-operation-event-class.md)|サーバーで監査操作が行われたことを示します。|  
|[Audit Server Principal Impersonation イベント クラス](../../relational-databases/event-classes/audit-server-principal-impersonation-event-class.md)|サーバー スコープ内で権限の借用が行われたことを示します。|  
|[Audit Server Principal Management イベント クラス](../../relational-databases/event-classes/audit-server-principal-management-event-class.md)|サーバー プリンシパルに対して CREATE、ALTER、または DROP のいずれかが行われたことを示します。|  
|[Audit Server Scope GDR イベント クラス](../../relational-databases/event-classes/audit-server-scope-gdr-event-class.md)|サーバー権限の GDR イベントが発生したことを示します。|  
|[Audit Server Starts and Stops イベント クラス](../../relational-databases/event-classes/audit-server-starts-and-stops-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの状態が変更されたことを示します。|  
|[Audit Statement Permission イベント クラス](../../relational-databases/event-classes/audit-statement-permission-event-class.md)|ステートメント権限が使用されたことを示します。|  
  
## <a name="related-content"></a>関連コンテンツ  
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)  
  
  
