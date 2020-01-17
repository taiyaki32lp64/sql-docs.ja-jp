---
title: ジョブ ステップの成功時または失敗時の動作を設定する方法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, action flow logic
- successful jobs [SQL Server]
- failed jobs [SQL Server]
- jobs [SQL Server Agent], action flow logic
ms.assetid: 23041ccf-8a07-41d3-85b9-c449a54b7e1e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7e9412ee0bd2be7b44dff2a06bd674abee0da34a
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798169"
---
# <a name="set-job-step-success-or-failure-flow"></a>Set Job Step Success or Failure Flow
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを作成するとき、ジョブの実行中にエラーが発生した場合に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行するアクションを指定できます。 各ジョブ ステップの成功時または失敗時に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行するアクションを決定します。 その後、次のプロシージャを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用したジョブ ステップ アクション フロー ロジックを構成します。  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **ジョブ ステップの成功時または失敗時の動作を設定する方法:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 管理オブジェクト](#SMO)  
  
## <a name="before-you-begin"></a>作業を開始する準備  
  
###  <a name="Security"></a> Security  
 詳細については、「 [SQL Server エージェントのセキュリティの実装](implement-sql-server-agent-security.md)」をご覧ください。  
  
##  <a name="SSMS"></a> SQL Server Management Studio の使用  
  
#### <a name="to-set-job-step-success-or-failure-flow"></a>ジョブ ステップの成功時または失敗時の動作を設定するには  
  
1.  **オブジェクト エクスプローラー**で、 **[SQL Server エージェント]**、 **[ジョブ]** の順に展開します。  
  
2.  編集するジョブを右クリックして、 **[プロパティ]** をクリックします。  
  
3.  **[ステップ]** ページを選択し、ステップをクリックし、 **[編集]** をクリックします。  
  
4.  **[ジョブ ステップのプロパティ]** ダイアログ ボックスの **[詳細設定]** ページを選択します。  
  
5.  **[成功した場合のアクション]** 一覧で、ジョブ ステップが正常に完了した場合に実行するアクションをクリックします。  
  
6.  **[再試行回数]** ボックスに、ジョブ ステップが失敗したと見なされるまでにそのステップを繰り返す回数を 0 ～ 9999 の範囲で入力します。 **[再試行回数]** ボックスに 0 を超える値を入力した場合は、ジョブ ステップが再試行されるまでの経過時間 (分単位) を 1 ～ 9999 の範囲で **[再試行間隔 (分)]** ボックスに入力します。  
  
7.  **[失敗した場合のアクション]** ボックスの一覧で、ジョブ ステップが失敗した場合に実行するアクションをクリックします。  
  
8.  ジョブが [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトの場合は、以下の方法から選択できます。  
  
    -   **[出力ファイル]** ボックスに、スクリプトの出力が書き込まれる出力ファイルの名前を入力します。 既定では、ジョブ ステップの実行ごとに出力ファイルが上書きされます。 出力ファイルを上書きしない場合は、 **[既存のファイルに出力を追加する]** チェック ボックスをオンにします。  
  
    -   ジョブ ステップのログをデータベース テーブルに記録する場合は、 **[テーブルにログ記録する]** チェック ボックスをオンにします。 既定では、ジョブ ステップの実行ごとにテーブルの内容が上書きされます。 テーブルの内容を上書きしない場合は、 **[テーブル内の既存のエントリに出力を追加する]** チェック ボックスをオンにします。 ジョブ ステップの実行後にこのテーブルのコンテンツを表示するには、 **[表示]** をクリックします。  
  
    -   ステップの履歴に出力を含める場合は、 **[履歴にステップ出力を含める]** チェック ボックスをオンにします。 エラーがない場合にのみ、出力は表示されます。 また、出力が切り捨てられる場合があります。  
  
9. **[実行時のユーザー]** ボックスの一覧を使用できる場合、ジョブで使用する資格情報を持つプロキシ アカウントを選択します。  
  
##  <a name="TSQL"></a> Transact-SQL の使用  
  
#### <a name="to-set-job-step-success-or-failure-flow"></a>ジョブ ステップの成功時または失敗時の動作を設定するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、**[実行]** をクリックします。  
  
    ```sql
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Set database to read only',  
        @subsystem = N'TSQL',  
        @command = N'ALTER DATABASE SALES SET READ_ONLY',   
        @on_success_action = 1;  
    GO  
    ```  
  
 詳細については、「 [sp_add_jobstep &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)」を参照してください。  
  
##  <a name="SMO"></a>SQL Server 管理オブジェクトの使用  

### <a name="to-set-job-step-success-or-failure-flow"></a>ジョブ ステップの成功時または失敗時の動作を設定するには
  
 Visual Basic、ビジュアルC#、PowerShell などのプログラミング言語で `JobStep` クラスを使用します。 詳細については、「 [SQL Server 管理オブジェクト (SMO) プログラミング ガイド](https://msdn.microsoft.com/library/ms162169.aspx)」を参照してください。  
