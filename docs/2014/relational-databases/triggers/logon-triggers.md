---
title: ログオン トリガー | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 867c341443b7ce1c459806eaac5427a06a8bbebe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62473233"
---
# <a name="logon-triggers"></a>ログオン トリガー
  ログオン トリガーは、LOGON イベントに応答してストアド プロシージャを起動します。 このイベントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスでユーザー セッションが確立されるときに発生します。 ログオン トリガーは、ログインの認証段階が終了した後、ユーザー セッションが実際に確立されるまでの間に発生します。 したがって、通常、エラー メッセージや PRINT ステートメントからのメッセージはユーザーに通知されますが、このトリガー内で発生したすべてのメッセージは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログに記録されます。 認証に失敗した場合は、ログオン トリガーが作動しません。  
  
 ログオン トリガーを使用すると、ログインの利用状況を追跡したり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]へのログインを制限したり、特定のログインのセッション数を制限したりすることで、サーバー セッションを監査し制御できます。 たとえば、次のコードでは、ログイン [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] login_test *によってユーザー セッションが既に 3 つ生成されている場合、ログオン トリガーは、そのログインが開始する* へのログイン試行を拒否します。  
  
 [!code-sql[TriggerDDL#LogonTrigger1](../../snippets/tsql/SQL14/tsql/triggerddl/transact-sql/snippet_create_alter_drop_trigger.sql#logontrigger1)]  
  
 LOGON イベントが AUDIT_LOGIN SQL トレース イベントに対応していることに注意してください。このトレース イベントは、 [イベント通知](../service-broker/event-notifications.md)で使用できます。 トリガーとイベント通知の主な相違点は、トリガーがイベントと同期的に発生するのに対し、イベント通知は非同期的に発生することです。 つまり、セッションが確立されないようにする場合は、ログオン トリガーを使用する必要があります。 この目的では、AUDIT_LOGIN イベントのイベント通知を使用できません。  
  
## <a name="specifying-first-and-last-trigger"></a>最初と最後のトリガーの指定  
 LOGON イベントでは、複数のトリガーを定義できます。 [sp_settriggerorder](/sql/relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql) システム ストアド プロシージャを使用すると、定義したトリガーの 1 つを、イベントで起動される最初または最後のトリガーとして指定できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、残りのトリガーの実行順序は保証されません。  
  
## <a name="managing-transactions"></a>トランザクションの管理  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってログオン トリガーが起動される前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、任意のユーザー トランザクションに依存しない暗黙のトランザクションが作成されます。 その結果、最初のログオン トリガーが起動し始めると、トランザクション数は 1 になります。 すべてのログオン トリガーの実行が完了すると、トランザクションがコミットされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、他の種類のトリガーと同様に、トランザクション数が 0 の状態でログオン トリガーの実行が完了すると、エラーが返されます。 ROLLBACK TRANSACTION ステートメントは、入れ子になったトランザクション内で実行される場合でも、トランザクション数を 0 にリセットします。 COMMIT TRANSACTION を実行すると、トランザクション数が 0 まで減少することがあります。 そのため、ログオン トリガー内では COMMIT TRANSACTION ステートメントを実行しないことをお勧めします。  
  
 ログオン トリガー内で ROLLBACK TRANSACTION ステートメントを使用する場合は、次の点を考慮してください。  
  
-   ROLLBACK TRANSACTION が実行されるまでに行われたデータ変更がすべてロールバックされます。 これには、現在のトリガーによる変更、および同じイベントで先に実行されたトリガーによる変更が含まれます。 特定のイベントに対する残りのトリガーは実行されません。  
  
-   現在のトリガーは、ROLLBACK ステートメントの後にある残りのステートメントすべてを引き続き実行します。 これらのステートメントのいずれかがデータを変更する場合、その変更はロールバックされません。  
  
 LOGON イベントでトリガーを実行中に次のいずれかの状況が発生すると、ユーザー セッションは確立されません。  
  
-   元の暗黙のトランザクションがロールバックされるか失敗した。  
  
-   重大度が 20 を超えるエラーがトリガー内部で発生した。  
  
## <a name="disabling-a-logon-trigger"></a>ログオン トリガーを無効にする  
 ログオン トリガーを使用すると、`sysadmin` 固定サーバー ロールのメンバーを含むすべてのユーザーの[!INCLUDE[ssDE](../../../includes/ssde-md.md)]への接続を効率的に禁止できます。 ログオン トリガーによって接続が禁止されているときでも、`sysadmin` 固定サーバー ロールのメンバーは、専用管理者接続を使用するか、または[!INCLUDE[ssDE](../../../includes/ssde-md.md)]を最小構成モード (-f) で起動することにより、接続できます。 詳細については、「[データベース エンジン サービスのスタートアップ オプション](../../database-engine/configure-windows/database-engine-service-startup-options.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスク|トピック|  
|----------|-----------|  
|ログオン トリガーの作成方法について説明します。 ログオン トリガーは、どのデータベースからでも作成できますが、サーバー レベルで登録されるため **master** データベースに存在します。|[CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)|  
|ログオン トリガーを変更する方法について説明します。|[ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)|  
|ログオン トリガーを削除する方法について説明します。|[DROP TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-trigger-transact-sql)|  
|ログオン トリガーに関する情報を取得する方法について説明します。|[sys.server_triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)<br /><br /> [sys.server_trigger_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql)|  
|ログオン トリガーのイベント データをキャプチャする方法について説明します。||  
  
## <a name="see-also"></a>参照  
 [DDL トリガー](../triggers/ddl-triggers.md)  
  
  
