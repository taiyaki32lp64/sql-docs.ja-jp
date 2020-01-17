---
title: Transact-SQL ジョブ ステップのオプションを定義する | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: b2a47057-f6fb-432b-a7b6-5d61f33a5d9c
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c16a6829f55ef2d1a76a26306484ba19ca00ae53
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553018"
---
# <a name="define-transact-sql-job-step-options"></a>Define Transact-SQL Job Step Options
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Server 管理オブジェクトを使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] エージェントの [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ジョブ ステップのオプションを定義する方法について説明します。  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Security"></a>セキュリティ  
詳細については、「 [SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)」をご覧ください。  
  
## <a name="SSMS"></a>SQL Server Management Studio の使用  
  
#### <a name="to-define-transact-sql-job-step-options"></a>Transact-SQL ジョブ ステップのオプションを定義するには  
  
1.  **オブジェクト エクスプローラー**で、 **[SQL Server エージェント]** を展開し、 **[ジョブ]** を展開します。次に、編集するジョブを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[ステップ]** ページをクリックし、ジョブ ステップをクリックして、 **[編集]** をクリックします。  
  
3.  **[ジョブ ステップのプロパティ]** ダイアログ ボックスで、ジョブの種類が **[Transact-SQL スクリプト (T-SQL)]** であることを確認し、 **[詳細設定]** ページを選択します。  
  
4.  **[成功した場合のアクション]** ボックスで、ジョブが成功した場合に実行するアクションを指定します。  
  
5.  **[再試行回数]** ボックスに 0 ～ 9999 の数値を入力して、再試行回数を指定します。  
  
6.  **[再試行間隔]** ボックスに 0 ～ 9999 の数 (分) を入力して、再試行間隔を指定します。  
  
7.  **[失敗した場合のアクション]** ボックスで、ジョブが失敗した場合に実行するアクションを指定します。  
  
8.  ジョブが [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトの場合は、以下の方法から選択できます。  
  
    -   **[出力ファイル]** ボックスに、出力ファイルの名前を入力します。 既定では、ジョブ ステップの実行ごとに出力ファイルが上書きされます。 出力ファイルを上書きしない場合は、 **[既存のファイルに出力を追加する]** チェック ボックスをオンにします。 このオプションは、 **sysadmin** 固定サーバー ロールのメンバーだけが使用できます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、ユーザーはファイル システム上の任意のファイルを表示できないので、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用して、ファイル システムに書き込まれたジョブ ステップのログを表示できないことに注意してください。  
  
    -   ジョブ ステップのログをデータベース テーブルに記録する場合は、 **[テーブルにログ記録する]** チェック ボックスをオンにします。 既定では、ジョブ ステップの実行ごとにテーブルの内容が上書きされます。 テーブルの内容を上書きしない場合は、 **[テーブル内の既存のエントリに出力を追加する]** チェック ボックスをオンにします。 ジョブ ステップの実行後にこのテーブルのコンテンツを表示するには、 **[表示]** をクリックします。  
  
    -   ステップの履歴に出力を含める場合は、 **[履歴にステップ出力を含める]** チェック ボックスをオンにします。 エラーがない場合にのみ、出力は表示されます。 また、出力が切り捨てられる場合があります。  
  
9. **sysadmin** 固定サーバー ロールのメンバーで、このジョブ ステップを別の SQL ログインで実行する場合は、 **[実行時のユーザー]** ボックスで SQL ログインを選択します。  
  
## <a name="SMO"></a>SQL Server 管理オブジェクトの使用  
**Transact-SQL ジョブ ステップのオプションを定義するには**  
  
Visual Basic、Visual C#、PowerShell などの選択したプログラミング言語で **JobStep** クラスを使用します。  
  
