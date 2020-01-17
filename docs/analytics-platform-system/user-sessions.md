---
title: ユーザー セッション
description: Analytics Platform System の Parallel Data Warehouse のユーザーセッション。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a0e5b338cc616be214ef39527551ee4a6ffd8f56
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399406"
---
# <a name="user-sessions-in-analytics-platform-system"></a>Analytics Platform System のユーザーセッション
適切なアクセス許可を持つログインでは、次の操作の実行を含め、SQL Server PDW アプライアンス上のすべてのログインのセッションを管理できます。  
  
-   アクティブなセッションとアイドル状態のセッションの両方を含む、アプライアンス上の現在のセッションを表示します。  
  
-   セッションのアクティブなクエリと最近使用したクエリを表示します。  
  
-   アクティブなセッションを終了します。  
  
これらのアクションを実行するには、次に示すように、[管理コンソールを使用してアプライアンスを監視](monitor-the-appliance-by-using-the-admin-console.md)するか、SQL コマンドを使用して[システムビュー](tsql-system-views.md)を使用します。  
  
どちらの方法でもセッションを管理するために必要なアクセス許可は同じであり、「[ログイン、ユーザー、およびデータベースロールを管理するためのアクセス許可を付与する](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles)」で説明されています。  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>管理コンソールを使用したセッションの管理  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>管理コンソールを使用して現在のセッションを表示するには  
  
1.  上部のメニューで、[**セッション**] をクリックします。  
  
2.  結果の一覧には、最近のすべてのセッションが表示されます。 "アクティブ" または "アイドル" のセッションのみを表示するには、[**状態**] 列のヘッダーをクリックして、結果を状態で並べ替えます。  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>管理コンソールを使用してセッションのアクティブおよび最近のクエリを表示するには  
  
1.  上部のメニューで、[**セッション**] をクリックします。  
  
2.  結果の一覧で、目的のセッションのセッション ID をクリックします。  
  
3.  結果のクエリリストには、セッションの最近のクエリが表示されます。 クエリの詳細を表示する方法については、「[アクティブなクエリの監視](monitoring-active-queries.md)」を参照してください。  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>管理コンソールを使用してセッションを終了するには  
  
1.  上部のメニューで、[**セッション**] をクリックします。  
  
2.  キャンセルするセッションのセッション ID を検索します。  
  
3.  セッション ID の左側にある赤い**X 印**をクリックしてセッションを終了します。 状態が "アクティブ" または "アイドル" のセッションのみが赤色の**X 印**を持つこれらのセッションだけを終了できます。  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>システムビューと SQL コマンドを使用したセッションの管理  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>システムビューを使用して現在のセッションを表示するには  
現在のセッションの一覧を生成するには、 [dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)を使用します。  
  
この例では、状態が "アクティブ" または "アイドル" のすべてのセッションの session_id、login_name、および状態が返されます。  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>システムビューを使用してセッションのアクティブおよび最近のクエリを表示するには  
セッションに関連付けられているアクティブなクエリと最近完了したクエリを表示するには、 [dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)および[dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)ビューを使用します。 このクエリは、アクティブまたはアイドル状態のすべてのセッションの一覧と、各セッション ID に関連付けられているアクティブまたは最近のクエリを返します。  
  
```sql  
SELECT es.session_id, es.login_name, es.status AS sessionStatus,   
er.request_id, er.status AS requestStatus, er.command   
FROM sys.dm_pdw_exec_sessions es   
LEFT OUTER JOIN sys.dm_pdw_exec_requests er   
ON (es.session_id=er.session_id)   
WHERE (es.status='Active' OR es.status='Idle') AND   
(er.status!= 'Completed' AND er.status!= 'Failed' AND er.status!= 'Cancelled');  
```  
  
### <a name="to-end-sessions-by-using-sql-commands"></a>SQL コマンドを使用してセッションを終了するには  
現在のセッションを終了するには、 [KILL](../t-sql/language-elements/kill-transact-sql.md)コマンドを使用します。 プロセスを終了するには、そのセッション ID が必要です。これは、 [dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)ビューを使用して取得できます。  
  
この例では、[login_name]、[session_id]、[状態] の値を選択して、ログイン名に基づいてセッションを検索します。  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
"アクティブ" または "アイドル" 状態のセッションを終了するには、KILL コマンドを使用します。  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
