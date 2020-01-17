---
title: 'オプション (クエリの実行: SQL Server: [詳細] ページ) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionAdvanced
ms.assetid: 3ec788c7-22c3-4216-9ad0-81a168d17074
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 5323054b77ed26a3ada816f44c1bf6764ded931d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089370"
---
# <a name="options-query-executionsql-serveradvanced-page"></a>オプション ([クエリ実行]: [SQL Server]: [詳細設定] ページ)
  SET コマンドを使用する場合は、いくつかのオプションを使用できます。 このページを使用すると、SQL Server クエリ エディターで [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリを実行するための **set** オプションを指定できます。 他のコード エディターには影響しません。 これらのオプションに加えられた変更は、新しい [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリだけに適用されます。 現在のクエリのオプションを変更するには、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] クエリ ウィンドウの **[クエリ]** メニューまたはショートカット メニューの **[クエリ オプション]** をクリックします。 **[実行]** の **[詳細設定]** をクリックします。 各オプションの詳細については、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オンライン ブックを参照してください。  
  
## <a name="options"></a>および  
 **SET NOCOUNT**  
 結果セットのメッセージとして、行数を返しません。 既定では、このチェック ボックスはオフになっています。  
  
 **SET NOEXEC**  
 クエリを実行しません。 既定では、このチェック ボックスはオフになっています。  
  
 **SET PARSEONLY**  
 各クエリの構文をチェックするだけで、クエリを実行しません。 既定では、このチェック ボックスはオフになっています。  
  
 **SET CONCAT_NULL_YIELDS_NULL**  
 このチェック ボックスがオンの場合、既存の値と NULL を連結するクエリは、結果として常に NULL を返します。 このチェック ボックスがオフの場合、既存の値と NULL を連結するクエリは、既存の値を返します。 既定では、このチェック ボックスはオンになっています。  
  
 **SET ARITHABORT**  
 このチェック ボックスがオンの場合、式の評価中に INSERT、DELETE、または UPDATE ステートメントで算術エラー (オーバーフロー、0 による除算、またはドメイン エラー) が発生すると、クエリまたはバッチは終了します。 このチェック ボックスがオフの場合、可能であればその値に対して NULL が与えられ、クエリが続行されます。さらに、結果にメッセージが含められます。 詳細については、「[SET ARITHABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql)」をご覧ください。 既定では、このチェック ボックスはオンになっています。  
  
 **SET SHOWPLAN_TEXT**  
 このチェック ボックスがオンの場合、各クエリに対してクエリ プランがテキスト形式で返されます。 既定では、このチェック ボックスはオフになっています。  
  
 **SET STATISTICS TIME**  
 このチェック ボックスがオンの場合、各クエリに対して時間統計情報が返されます。 既定では、このチェック ボックスはオフになっています。  
  
 **SET STATISTICS IO**  
 このチェック ボックスがオンの場合、各クエリに対して入力および出力に関する統計情報が返されます。 既定では、このチェック ボックスはオフになっています。  
  
 **SET TRANSACTION ISOLATION LEVEL**  
 既定では READ COMMITTED トランザクション分離レベルが設定されます。 詳細については、「[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql)」を参照してください。 SNAPSHOT トランザクション分離レベルは使用できません。 SNAPSHOT 分離を使用するには、次の [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを追加します。  
  
```  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
```  
  
 **デッドロックの優先度を設定**  
 既定値の [Normal] の場合、デッドロックが発生したときに各クエリに同じ優先度が与えられます。 このクエリが、デッドロックの競合で常に優先されずに終了するクエリとして選択されるようにするには、優先度に [Low] を選択してください。  
  
 **SET LOCK TIMEOUT**  
 既定値の -1 は、トランザクションが完了するまでロックが保持されることを示します。 値が 0 の場合は、待ち時間はありません。ロックがかかるとすぐにメッセージが返されます。 トランザクションを終了するまでのロックを 0 ミリ秒よりも長く保持する必要がある場合は、0 より大きい値を指定します。  
  
 **SET QUERY_GOVERNOR_COST_LIMIT**  
 **[QUERY_GOVERNOR_COST_LIMIT]** オプションは、クエリを実行できる時間の上限を指定する場合に使用します。 クエリ コストとは、特定のハードウェア構成でクエリを完了するために必要とされる予測所要時間を秒単位で表したものです。 既定値の 0 は、クエリの実行に関して時間的制限がないことを示します。  
  
 **プロバイダー メッセージ ヘッダーを抑制します。**  
 このチェック ボックスがオンの場合、プロバイダー (SQLClient プロバイダーなど) からの状態メッセージは表示されません。 既定では、このチェック ボックスはオンになっています。 プロバイダー レベルで失敗するクエリのトラブルシューティングを行うときにプロバイダー メッセージを表示するには、このチェック ボックスをオフにします。  
  
 **クエリの実行後に切断します。**  
 このチェック ボックスがオンの場合、クエリが完了した後に [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] への接続が終了します。 既定では、このチェック ボックスはオフになっています。  
  
 **既定値にリセット**  
 このページ上のすべての値を元の既定値にリセットします。  
  
  
