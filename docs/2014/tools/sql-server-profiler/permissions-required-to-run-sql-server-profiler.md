---
title: SQL Server Profiler の実行に必要なアクセス許可 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], permissions
- traces [SQL Server], replaying
- replaying traces
- SQL Server Profiler, permissions
- security [SQL Server], SQL Server Profiler
ms.assetid: 5c580a87-88ae-4314-8fe1-54ade83f227f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bed2868b74087cd0e4c119ada7e29f0c5db73ce5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240521"
---
# <a name="permissions-required-to-run-sql-server-profiler"></a>SQL Server Profiler の実行に必要な権限
  既定では、[!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] の実行には、トレースの作成に使用した Transact-SQL ストアド プロシージャと同じユーザー権限が必要です。 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] を実行するには、ユーザーに ALTER TRACE アクセス権を許可する必要があります。 詳細については、「[GRANT (サーバーの権限の許可) &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-server-permissions-transact-sql)」を参照してください。  
  
> [!IMPORTANT]  
>  SHOWPLAN 権限、ALTER TRACE 権限、または VIEW SERVER STATE 権限を持つユーザーは、プラン表示出力にキャプチャされたクエリを表示できます。 これらのクエリには、パスワードなどの機密情報が含まれている場合があります。 したがって、これらの権限は、機密情報を表示することが認められているユーザー (たとえば db_owner 固定データベース ロールのメンバーや sysadmin 固定サーバー ロールのメンバー) のみに付与することをお勧めします。 また、プラン表示ファイルまたはプラン表示関連のイベントを含むトレース ファイルのみを保存すること、保存先は NTFS ファイル システムが使用されている場所とすること、および機密情報を表示する権限を持つユーザーのみにアクセスを制限することをお勧めします。  
  
## <a name="permissions-used-to-replay-traces"></a>トレースの再生に使用される権限  
 トレースを再生するには、トレースを再生するユーザーに ALTER TRACE 権限が許可されている必要があります。  
  
 ただし、再生中に、再生されるトレース内で Audit Login イベントが検出されると、 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] によって EXECUTE AS コマンドが使用されます。 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] はログイン イベントに関連付けられたユーザーの権限を借用するために、EXECUTE AS コマンドを使用します。  
  
 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] によって再生されるトレース内でログイン イベントが検出されると、次の権限のチェックが実行されます。  
  
1.  ALTER TRACE 権限のある User1 が、トレースの再生を開始します。  
  
2.  再生されるトレースで、User2 のログイン イベントが検出されます。  
  
3.  [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] は User2 の権限を借用するために、EXECUTE AS コマンドを使用します。  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は User2 の認証を試みます。認証の結果に応じて、次のいずれかが行われます。  
  
    1.  User2 を認証できない場合、 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] はエラーを返し、User1 としてトレースの再生を続行します。  
  
    2.  User2 を正しく認証できた場合、User2 としてのトレースの再生を続行します。  
  
5.  対象のデータベースで User2 の権限がチェックされます。チェックの結果に応じて、次のいずれかが行われます。  
  
    1.  User2 が対象のデータベースに権限を所持している場合、権限の借用に成功し、User2 としてトレースが再生されます。  
  
    2.  User2 が対象のデータベースに権限を所持していない場合、サーバーではそのデータベースの Guest ユーザーがチェックされます。  
  
6.  対象のデータベースに Guest ユーザーが存在するかどうかがチェックされます。チェックの結果に応じて、次のいずれかが行われます。  
  
    1.  Guest アカウントが存在する場合、Guest アカウントとしてトレースが再生されます。  
  
    2.  対象のデータベースに Guest アカウントが存在しない場合、エラーが返され、User1 としてトレースが再生されます。  
  
 次の図に、トレース再生時の権限のチェック プロセスを示します。  
  
 ![SQL Server Profiler のトレースを再生するための権限](../../database-engine/media/replaytracedecisiontree.gif "SQL Server Profiler のトレースを再生するための権限")  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler のストアド プロシージャ &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)   
 [トレースの再生](replay-traces.md)   
 [トレースの作成 &#40;SQL Server Profiler&#41;](create-a-trace-sql-server-profiler.md)   
 [トレース テーブルを再生する &#40;SQL Server Profiler&#41;](replay-a-trace-table-sql-server-profiler.md)   
 [トレース ファイルを再生する &#40;SQL Server Profiler&#41;](replay-a-trace-file-sql-server-profiler.md)  
  
  
