---
title: パッケージに対する SQL Server エージェント ジョブ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- jobs [Integration Services]
- automatic package execution
- scheduling packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7a4b9cd5eaad7b51f7cc3d2a0c73bea3f23fd542
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767184"
---
# <a name="sql-server-agent-jobs-for-packages"></a>パッケージに対する SQL Server エージェント ジョブ
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの実行を自動化およびスケジュール設定できます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置されているパッケージ、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストア、ファイル システムに格納されているパッケージのスケジュールを設定できます。  
  
## <a name="sections-in-this-topic"></a>このトピックのセクション  
 このトピックには、次のセクションが含まれます。  
  
-   [SQL Server エージェントでのジョブのスケジュール設定](#jobs)  
  
-   [Integration Services パッケージのスケジュール設定](#packages)  
  
-   [スケジュールされたパッケージのトラブルシューティング](#trouble)  
  
##  <a name="jobs"></a> Scheduling Jobs in SQL Server Agent  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントとは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを実行してタスクの自動化とスケジュール設定を可能にする、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってインストールされるサービスです。 ジョブを自動的に実行できるようにするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを実行している必要があります。 詳細については、「 [Configure SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md)」をご覧ください。  
  
 **のインスタンスに接続すると、** のオブジェクト エクスプローラーに [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [SQL Server エージェント] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ノードが表示されます。  
  
 定期的なタスクを自動化するには、 **[新しいジョブ]** ダイアログ ボックスを使用してジョブを作成します。 詳細については、 [「ジョブの実装」](../../ssms/agent/implement-jobs.md)を参照してください。  
  
 ジョブを作成した後は、少なくとも 1 つのステップを追加する必要があります。 1 つのジョブに複数のステップを含め、それぞれのステップで異なるタスクを実行できます。 詳細については、 [ジョブ ステップの管理](../../ssms/agent/manage-job-steps.md)を参照してください。  
  
 ジョブとジョブ ステップを作成した後は、ジョブを実行するためのスケジュールを作成できます。 また、手動で実行する、スケジュールされていないジョブも作成できます。 詳細については、「 [スケジュールの作成とジョブへのアタッチ](../../ssms/agent/create-and-attach-schedules-to-jobs.md)」を参照してください。  
  
 ジョブ完了時にオペレーターへ電子メール メッセージを送信する通知オプションなどの設定、警告の追加を行い、ジョブを拡張できます。 詳細については、「 [警告](../../ssms/agent/alerts.md)」を参照してください。  
  
##  <a name="packages"></a> Scheduling Integration Services Packages  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを作成して [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのスケジュールを設定する場合は、少なくとも 1 つのステップを追加し、ステップの種類を **[SQL Server Integration Services パッケージ]** に設定する必要があります。 1 つのジョブに複数のステップを含め、それぞれのステップで異なるパッケージを実行できます。  
  
 ジョブ ステップからの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの実行は、 **dtexec** ユーティリティ (dtexec.exe) および **DTExecUI** (dtexecui.exe) を使用したパッケージの実行に似ています。 コマンド ライン オプションまたは **[パッケージ実行ユーティリティ]** ダイアログ ボックスを使用してパッケージの実行時オプションを設定する代わりに、 **[新しいジョブ ステップ]** ダイアログ ボックスで実行時オプションを設定します。 パッケージを実行するためのオプションの詳細については、「 [dtexec ユーティリティ](dtexec-utility.md)」を参照してください。  
  
 詳しくは、「 [SQL Server エージェントを使用してパッケージのスケジュールを設定する](../schedule-a-package-by-using-sql-server-agent.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用してパッケージを実行する方法を示しているビデオについては、MSDN ライブラリのビデオのホームページの「[SQL Server エージェントを使用してパッケージ実行を自動化する方法 (SQL Server ビデオ)](https://go.microsoft.com/fwlink/?LinkId=141771)」をご覧ください。  
  
##  <a name="trouble"></a> トラブルシューティング  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ ステップは、パッケージを [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] およびコマンド ラインで正常に実行できる場合でも、パッケージの開始に失敗することがあります。 この問題には、いくつかの一般的な原因と、推奨されるソリューションがあります。 詳細については、次のリソースを参照してください。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポート技術情報の記事「 [SQL Server エージェントのジョブ ステップから SSIS パッケージを呼び出したときに SSIS パッケージが実行されません](https://support.microsoft.com/kb/918760)  
  
-   MSDN ライブラリのビデオ「[トラブルシューティング: SQL Server エージェントを使用した SSIS パッケージ実行 (SQL Server ビデオ)](https://go.microsoft.com/fwlink/?LinkId=141772)」  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ ステップがパッケージを開始した後、パッケージの実行が失敗したり、正常に実行されても予期しない結果になる場合があります。 これらの問題のトラブルシューティングには、次のツールを使用できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] MSDB データベース、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストア、またはローカル コンピューターのフォルダーに格納されているパッケージでは、 **[ログ ファイルの表示]** と、パッケージの実行中に生成されたログおよびデバッグ ダンプ ファイルを使用できます。  
  
     **[ログ ファイルの表示] を使用するには、次の操作を実行します。**  
  
    1.  オブジェクト エクスプローラーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを右クリックし、 **[履歴の表示]** をクリックします。  
  
    2.  **[ログ ファイルの概要]** ボックスで、 **[メッセージ]** 列に **"ジョブが失敗しました"** というメッセージが含まれているジョブ実行を探します。  
  
    3.  ジョブ ノードを展開し、ジョブ ステップをクリックして、メッセージの詳細を **[ログ ファイルの概要]** ボックスの下の領域に表示します。  
  
-   SSISDB データベースに格納されているパッケージでも、 **[ログ ファイルの表示]** と、パッケージの実行中に生成されたログおよびデバッグ ダンプ ファイルを使用できます。 また、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーのレポートを使用できます。  
  
     **レポートでジョブ実行に関連するパッケージ実行の情報を探すには、次の操作を行います。**  
  
    1.  上記の手順に従って、ジョブ ステップのメッセージの詳細を表示します。  
  
    2.  メッセージに記載されている実行 ID を探します。  
  
    3.  オブジェクト エクスプローラーで、[Integration Services カタログ] ノードを展開します。  
  
    4.  SSISDB を右クリックし、[レポート]、[標準レポート] の順にポイントして、[すべての実行] をクリックします。  
  
    5.  **[すべての実行]** レポートの **[ID]** 列で、実行 ID を探します。 **[概要]** 、 **[すべてのメッセージ]** 、または **[実行のパフォーマンス]** をクリックして、このパッケージ実行についての情報を表示します。  
  
         "概要"、"すべてのメッセージ"、および "実行のパフォーマンス" の各レポートの詳細については、「 [Integration Services サーバーのレポート](../reports-for-the-integration-services-server.md)」を参照してください。  
  
## <a name="external-resources"></a>外部リソース  
  
-   [Web サイトのサポート技術情報の記事「](https://support.microsoft.com/kb/918760)SQL Server エージェントのジョブ ステップから SSIS パッケージを呼び出したときに SSIS パッケージが実行されません [!INCLUDE[msCoName](../../includes/msconame-md.md)] 」  
  
-   MSDN ライブラリのビデオ「[トラブルシューティング: SQL Server エージェントを使用した SSIS パッケージ実行 (SQL Server ビデオ)](https://go.microsoft.com/fwlink/?LinkId=141772)」  
  
-   MSDN ライブラリのビデオ「[SQL Server エージェントを使用してパッケージ実行を自動化する方法 (SQL Server ビデオ)](https://go.microsoft.com/fwlink/?LinkId=141771)」  
  
-   mssqltips.com の技術記事「 [Windows PowerShell を使用した SQL Server エージェント ジョブの確認](https://go.microsoft.com/fwlink/?LinkId=165675)」  
  
-   mssqltips.com の技術記事「 [SQL エージェント ジョブを有効または無効にしたときの自動警告](https://go.microsoft.com/fwlink/?LinkId=165676)」  
  
-   mssqltips.com のブログ「 [Windows イベント ログに書き込むための SQL エージェント ジョブの構成](https://go.microsoft.com/fwlink/?LinkId=220745)」  
  
  
