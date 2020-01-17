---
title: '[ジョブ ステップのプロパティ][新しいジョブ ステップ] ([詳細設定] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.stepadvanced.f1
ms.assetid: bdecfd4f-bcd8-4ba2-8ada-fbb636314f40
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f9395e9d1f7af28f0ff8a7d3f50d25eb665b7bb9
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263302"
---
# <a name="job-step-properties---new-job-step-advanced-page"></a>[ジョブ ステップのプロパティ]/[新しいジョブ ステップ] ([詳細設定] ページ)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このページを使用すると、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ ステップのプロパティを表示したり、変更したりできます。  
  
## <a name="options"></a>および  
**[成功した場合のアクション]**  
ジョブ ステップが成功した場合に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行するアクションを設定します。  
  
**[再試行回数]**  
失敗したジョブ ステップを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで再試行する回数を設定します。  
  
**[再試行間隔 (分)]**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが再試行する間隔を設定します。  
  
**[失敗した場合のアクション]**  
ジョブ ステップが失敗した場合に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行するアクションを設定します。  
  
## <a name="options-for-transact-sql-job-steps"></a>Transact-SQL ジョブ ステップのオプション  
**[出力ファイル]**  
ジョブ ステップからの出力に使用するファイルを設定します。 このオプションは、 **sysadmin** 固定サーバー ロールのメンバーである場合にのみ使用できます。  
  
**[...]**  
ジョブ ステップからの出力に使用するファイルを参照します。  
  
**[表示]**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、このボタンを使用して出力ファイルを表示することはできません。 代わりに、メモ帳を使用してジョブ ステップの出力ファイルを表示します。  
  
**[既存のファイルに出力を追加する]**  
ファイルの既存の内容に出力を追加します。 このオプションを指定しなければ、ジョブ ステップが実行されるたびに前のファイルの内容が上書きされます。  
  
**[テーブルにログ記録する]**  
**msdb** データベースの **sysjobstepslogs** テーブルに、ジョブ ステップの出力のログを記録します。  
  
**[表示]**  
ジョブ ステップを 1 回以上実行した後で **[表示]** をクリックすると、出力がテーブルに表示されます。  
  
**[テーブル内の既存のエントリに出力を追加する]**  
テーブルの既存の内容に出力を追加します。 このオプションを指定しなければ、ジョブ ステップが実行されるたびに前のテーブルの内容が上書きされます。  
  
**[履歴にステップ出力を含める]**  
このオプションを選択すると、ジョブ ステップの出力がジョブ履歴に含められます。  
  
**[実行時のユーザー]**  
**sysadmin** 固定サーバー ロールのメンバーであれば、別の SQL ログインを選択してこのジョブ ステップを実行できます。  
  
## <a name="options-for-operating-system-cmdexec-job-steps"></a>オペレーティング システム (CmdExec) ジョブ ステップのオプション  
**[出力ファイル]**  
ジョブ ステップからの出力に使用するファイルを設定します。  
  
**[...]**  
ジョブ ステップからの出力に使用するファイルを参照します。  
  
**[表示]**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、このボタンを使用して出力ファイルを表示することはできません。 代わりに、メモ帳を使用してジョブ ステップの出力ファイルを表示します。  
  
**[既存のファイルに出力を追加する]**  
ジョブ ステップを実行するたびに、その出力を前のファイルの内容に追加します。  
  
**[テーブルにログ記録する]**  
**msdb** データベースの **sysjobstepslogs** テーブルに、ジョブ ステップの出力のログを記録します。  
  
**[表示]**  
ジョブ ステップを 1 回以上実行した後で **[表示]** をクリックすると、出力がテーブルに表示されます。  
  
**[テーブル内の既存のエントリに出力を追加する]**  
テーブルの既存の内容に出力を追加します。 このオプションを指定しなければ、ジョブ ステップが実行されるたびに前のテーブルの内容が上書きされます。  
  
**[履歴にステップ出力を含める]**  
このオプションを選択すると、ジョブ ステップの出力がジョブ履歴に含められます。  
  
## <a name="options-for-powershell-job-steps"></a>PowerShell ジョブ ステップのオプション  
**[出力ファイル]**  
ジョブ ステップからの出力に使用するファイルを設定します。  
  
**[...]**  
ジョブ ステップからの出力に使用するファイルを参照します。  
  
**[表示]**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、このボタンを使用して出力ファイルを表示することはできません。 代わりに、メモ帳を使用してジョブ ステップの出力ファイルを表示します。  
  
**[既存のファイルに出力を追加する]**  
ジョブ ステップを実行するたびに、その出力を前のファイルの内容に追加します。  
  
**[テーブルにログ記録する]**  
**msdb** データベースの **sysjobstepslogs** テーブルに、ジョブ ステップの出力のログを記録します。  
  
**[表示]**  
ジョブ ステップを 1 回以上実行した後で **[表示]** をクリックすると、出力がテーブルに表示されます。  
  
**[テーブル内の既存のエントリに出力を追加する]**  
テーブルの既存の内容に出力を追加します。 このオプションを指定しなければ、ジョブ ステップが実行されるたびに前のテーブルの内容が上書きされます。  
  
**[履歴にステップ出力を含める]**  
このオプションを選択すると、ジョブ ステップの出力がジョブ履歴に含められます。  
  
## <a name="options-for-replication-queue-reader-job-steps"></a>レプリケーション キュー リーダーのジョブ ステップのオプション  
**[サーバー]**  
レプリケーション キュー リーダーのジョブ ステップを使用するように、サーバーを設定します。  
  
**[データベース]**  
レプリケーション キュー リーダーのジョブ ステップを使用するように、データベースを設定します。  
  
## <a name="options-for-sql-server-analysis-services-job-steps"></a>SQL Server Analysis Services ジョブ ステップのオプション  
**[出力ファイル]**  
ジョブ ステップからの出力に使用するファイルを設定します。 このオプションは、 **sysadmin** 固定サーバー ロールのメンバーである場合にのみ使用できます。  
  
**[...]**  
ジョブ ステップからの出力に使用するファイルを参照します。  
  
**表示**  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、このボタンを使用して出力ファイルを表示することはできません。 代わりに、メモ帳を使用してジョブ ステップの出力ファイルを表示します。  
  
**[既存のファイルに出力を追加する]**  
ファイルの既存の内容に出力を追加します。 このオプションを指定しなければ、ジョブ ステップが実行されるたびに前のファイルの内容が上書きされます。  
  
**[テーブルにログ記録する]**  
**msdb** データベースの **sysjobstepslogs** テーブルに、ジョブ ステップの出力のログを記録します。  
  
**[表示]**  
ジョブ ステップを 1 回以上実行した後で **[表示]** をクリックすると、出力がテーブルに表示されます。  
  
**[テーブル内の既存のエントリに出力を追加する]**  
テーブルの既存の内容に出力を追加します。 このオプションを指定しなければ、ジョブ ステップが実行されるたびに前のテーブルの内容が上書きされます。  
  
**[履歴にステップ出力を含める]**  
このオプションを選択すると、ジョブ ステップの出力がジョブ履歴に含められます。  
  
## <a name="see-also"></a>参照  
[ジョブ ステップの管理](../../ssms/agent/manage-job-steps.md)  
  
