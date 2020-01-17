---
title: ログオン トリガー | Microsoft Docs
ms.custom: ''
ms.date: 03/19/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- logon triggers
- login triggers
helpviewer_keywords:
- triggers [SQL Server], logon
ms.assetid: 2f0ebb2f-de10-482d-9806-1a5de5b312b8
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ebc4f10802f7a90dc828bab4b6f2aa1d01d6ccd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058620"
---
# <a name="logon-triggers"></a>ログオン トリガー
[!INCLUDE[tsql-appliesto-ss2008-appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
  ログオン トリガーは、LOGON イベントに応答してストアド プロシージャを起動します。 このイベントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスでユーザー セッションが確立されるときに発生します。 ログオン トリガーは、ログインの認証段階が終了した後、ユーザー セッションが実際に確立されるまでの間に発生します。 したがって、通常、エラー メッセージや PRINT ステートメントからのメッセージはユーザーに通知されますが、このトリガー内で発生したすべてのメッセージは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログに記録されます。 認証に失敗した場合は、ログオン トリガーが作動しません。  
  
 ログオン トリガーを使用すると、ログインの利用状況を追跡したり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]へのログインを制限したり、特定のログインのセッション数を制限したりすることで、サーバー セッションを監査し制御できます。 たとえば、次のコードでは、ログイン [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login_test *によってユーザー セッションが既に 3 つ生成されている場合、ログオン トリガーは、そのログインが開始する* へのログイン試行を拒否します。  
  
```  
USE master;  
GO  
CREATE LOGIN login_test WITH PASSWORD = '3KHJ6dhx(0xVYsdf' MUST_CHANGE,  
    CHECK_EXPIRATION = ON;  
GO  
GRANT VIEW SERVER STATE TO login_test;  
GO  
CREATE TRIGGER connection_limit_trigger  
ON ALL SERVER WITH EXECUTE AS 'login_test'  
FOR LOGON  
AS  
BEGIN  
IF ORIGINAL_LOGIN()= 'login_test' AND  
    (SELECT COUNT(*) FROM sys.dm_exec_sessions  
            WHERE is_user_process = 1 AND  
                original_login_name = 'login_test') > 3  
    ROLLBACK;  
END;  
```  
  
 LOGON イベントが AUDIT_LOGIN SQL トレース イベントに対応していることに注意してください。このトレース イベントは、 [イベント通知](../../relational-databases/service-broker/event-notifications.md)で使用できます。 トリガーとイベント通知の主な相違点は、トリガーがイベントと同期的に発生するのに対し、イベント通知は非同期的に発生することです。 つまり、セッションが確立されないようにする場合は、ログオン トリガーを使用する必要があります。 この目的では、AUDIT_LOGIN イベントのイベント通知を使用できません。  
  
## <a name="specifying-first-and-last-trigger"></a>最初と最後のトリガーの指定  
 LOGON イベントでは、複数のトリガーを定義できます。 [sp_settriggerorder](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md) システム ストアド プロシージャを使用すると、定義したトリガーの 1 つを、イベントで起動される最初または最後のトリガーとして指定できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、残りのトリガーの実行順序は保証されません。  
  
## <a name="managing-transactions"></a>トランザクションの管理  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってログオン トリガーが起動される前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、任意のユーザー トランザクションに依存しない暗黙のトランザクションが作成されます。 その結果、最初のログオン トリガーが起動し始めると、トランザクション数は 1 になります。 すべてのログオン トリガーの実行が完了すると、トランザクションがコミットされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、他の種類のトリガーと同様に、トランザクション数が 0 の状態でログオン トリガーの実行が完了すると、エラーが返されます。 ROLLBACK TRANSACTION ステートメントは、入れ子になったトランザクション内で実行される場合でも、トランザクション数を 0 にリセットします。 COMMIT TRANSACTION を実行すると、トランザクション数が 0 まで減少することがあります。 そのため、ログオン トリガー内では COMMIT TRANSACTION ステートメントを実行しないことをお勧めします。  
  
 ログオン トリガー内で ROLLBACK TRANSACTION ステートメントを使用する場合は、次の点を考慮してください。  
  
-   ROLLBACK TRANSACTION が実行されるまでに行われたデータ変更がすべてロールバックされます。 これには、現在のトリガーによる変更、および同じイベントで先に実行されたトリガーによる変更が含まれます。 特定のイベントに対する残りのトリガーは実行されません。  
  
-   現在のトリガーは、ROLLBACK ステートメントの後にある残りのステートメントすべてを引き続き実行します。 これらのステートメントのいずれかがデータを変更する場合、その変更はロールバックされません。  
  
 LOGON イベントでトリガーを実行中に次のいずれかの状況が発生すると、ユーザー セッションは確立されません。  
  
-   元の暗黙のトランザクションがロールバックされるか失敗した。  
  
-   重大度が 20 を超えるエラーがトリガー内部で発生した。  
  
## <a name="disabling-a-logon-trigger"></a>ログオン トリガーを無効にする  
 ログオン トリガーを使用すると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] sysadmin **固定サーバー ロールのメンバーを含むすべてのユーザーの** への接続を効率的に禁止できます。 ログオン トリガーによって接続が禁止されているときでも、 **sysadmin** 固定サーバー ロールのメンバーは、専用管理者接続を使用するか、または [!INCLUDE[ssDE](../../includes/ssde-md.md)] を最小構成モード (-f) で起動することにより、接続できます。 詳細については、「 [データベース エンジン サービスのスタートアップ オプション](../../database-engine/configure-windows/database-engine-service-startup-options.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスク|トピック|  
|----------|-----------|  
|ログオン トリガーの作成方法について説明します。 ログオン トリガーは、どのデータベースからでも作成できますが、サーバー レベルで登録されるため **master** データベースに存在します。|[CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)|  
|ログオン トリガーを変更する方法について説明します。|[ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)|  
|ログオン トリガーを削除する方法について説明します。|[DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)|  
|ログオン トリガーに関する情報を取得する方法について説明します。|[sys.server_triggers &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)<br /><br /> [sys.server_trigger_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql.md)|  
|ログオン トリガーのイベント データをキャプチャする方法について説明します。||  
  
## <a name="see-also"></a>参照  
 [DDL トリガー](../../relational-databases/triggers/ddl-triggers.md)  
  
  
