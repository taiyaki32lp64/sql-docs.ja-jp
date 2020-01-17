---
title: パッケージに対する SQL Server エージェント ジョブ | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- jobs [Integration Services]
- automatic package execution
- scheduling packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 25a2d1fe5eba1f52fc9738b9191f9bdade40002d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295805"
---
# <a name="sql-server-agent-jobs-for-packages"></a>パッケージに対する SQL Server エージェント ジョブ

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの実行を自動化およびスケジュール設定できます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置されているパッケージ、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストア、ファイル システムに格納されているパッケージのスケジュールを設定できます。  
 
> [!NOTE]
> この記事では、SSIS パッケージのスケジュールを設定する方法 (全般) と、オンプレミスでパッケージのスケジュールを設定する方法について説明します。 次のプラットフォームで SSIS パッケージを実行し、スケジュールを設定することもできます。
> - **Microsoft Azure クラウド**。 詳細については、「[SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)」と [Azure で SSIS パッケージの実行スケジュールを設定する](../lift-shift/ssis-azure-schedule-packages.md)方法に関するページを参照してください。
> - **Linux**。 詳細については、[SSIS を利用し、Linux でデータを抽出し、変換し、読み込む](../../linux/sql-server-linux-migrate-ssis.md)方法に関するページと、[cron を利用し、Linux で SQL Server Integration Services パッケージの実行スケジュールを設定する](../../linux/sql-server-linux-schedule-ssis-packages.md)方法に関するページを参照してください。

## <a name="sections-in-this-topic"></a>このトピックのセクション  
 このトピックには、次のセクションが含まれます。  
  
-   [SQL Server エージェントでのジョブのスケジュール設定](#jobs)  
  
-   [Integration Services パッケージのスケジュール設定](#packages)  
  
-   [スケジュールされたパッケージのトラブルシューティング](#trouble)  
  
##  <a name="jobs"></a> Scheduling Jobs in SQL Server Agent  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントとは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを実行してタスクの自動化とスケジュール設定を可能にする、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってインストールされるサービスです。 ジョブを自動的に実行できるようにするには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを実行している必要があります。 詳細については、「 [Configure SQL Server Agent](https://docs.microsoft.com/sql/ssms/agent/configure-sql-server-agent)」をご覧ください。  
  
 **のインスタンスに接続すると、** のオブジェクト エクスプローラーに [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [SQL Server エージェント] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ノードが表示されます。  
  
 定期的なタスクを自動化するには、 **[新しいジョブ]** ダイアログ ボックスを使用してジョブを作成します。 詳細については、 [「ジョブの実装」](https://docs.microsoft.com/sql/ssms/agent/implement-jobs)を参照してください。  
  
 ジョブを作成した後は、少なくとも 1 つのステップを追加する必要があります。 1 つのジョブに複数のステップを含め、それぞれのステップで異なるタスクを実行できます。 詳細については、 [ジョブ ステップの管理](https://docs.microsoft.com/sql/ssms/agent/manage-job-steps)を参照してください。  
  
 ジョブとジョブ ステップを作成した後は、ジョブを実行するためのスケジュールを作成できます。 また、手動で実行する、スケジュールされていないジョブも作成できます。 詳細については、「 [スケジュールの作成とジョブへのアタッチ](https://docs.microsoft.com/sql/ssms/agent/create-and-attach-schedules-to-jobs)」を参照してください。  
  
 ジョブ完了時にオペレーターへ電子メール メッセージを送信する通知オプションなどの設定、警告の追加を行い、ジョブを拡張できます。 詳細については、「 [警告](https://docs.microsoft.com/sql/ssms/agent/alerts)」を参照してください。  
  
##  <a name="packages"></a> Scheduling Integration Services Packages  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを作成して [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのスケジュールを設定する場合は、少なくとも 1 つのステップを追加し、ステップの種類を **[SQL Server Integration Services パッケージ]** に設定する必要があります。 1 つのジョブに複数のステップを含め、それぞれのステップで異なるパッケージを実行できます。  
  
 ジョブ ステップからの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの実行は、 **dtexec** ユーティリティ (dtexec.exe) および **DTExecUI** (dtexecui.exe) を使用したパッケージの実行に似ています。 コマンド ライン オプションまたは **[パッケージ実行ユーティリティ]** ダイアログ ボックスを使用してパッケージの実行時オプションを設定する代わりに、 **[新しいジョブ ステップ]** ダイアログ ボックスで実行時オプションを設定します。 パッケージを実行するためのオプションの詳細については、「 [dtexec ユーティリティ](../../integration-services/packages/dtexec-utility.md)」を参照してください。  
  
 詳しくは、「 [SQL Server エージェントを使用してパッケージのスケジュールを設定する](#schedule)」を参照してください。  
  
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
  
    "概要"、"すべてのメッセージ"、および "実行のパフォーマンス" の各レポートの詳細については、「 [Integration Services サーバーのレポート](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)」を参照してください。  

## <a name="schedule"></a> SQL Server エージェントを使用してパッケージのスケジュールを設定する
  以下の手順は、パッケージを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ ステップを使用して、パッケージの実行を自動化する方法を示しています。  
  
### <a name="to-automate-package-execution-by-using-sql-server-agent"></a>SQL Server エージェントを使用してパッケージの実行を自動化するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、ジョブを作成する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続するか、ステップを追加するジョブを含むインスタンスに接続します。  
  
2.  オブジェクト エクスプローラーで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのノードを展開し、次のいずれかの操作を実行します。  
  
    -   新しいジョブを作成するには、 **[ジョブ]** を右クリックして **[新しいジョブ]** をクリックします。  
  
    -   既存のジョブにステップを追加するには、 **[ジョブ]** を展開して該当するジョブを右クリックしてから、 **[プロパティ]** をクリックします。  
  
3.  新しいジョブを作成する場合は、 **[全般]** ページで、ジョブの名前を入力し、所有者およびジョブ カテゴリを選択し、必要に応じてジョブの説明も入力します。  
  
4.  ジョブをスケジュールできるようにするには、 **[有効]** を選択します。  
  
5.  スケジュールするパッケージのジョブ ステップを作成するには、 **[ステップ]** をクリックし、 **[新規作成]** をクリックします。  
  
6.  ジョブ ステップの種類として **[Integration Services パッケージ]** をクリックします。  
  
7.  **[実行するアカウント名]** ボックスの一覧で、 **[SQL Server エージェント サービスのアカウント]** をクリックするか、ジョブ ステップで使用する資格情報を備えたプロキシ アカウントをクリックします。 プロキシ アカウントの作成方法の詳細については、「 [Create a SQL Server Agent Proxy](../../ssms/agent/create-a-sql-server-agent-proxy.md)」を参照してください。  
  
     **[SQL Server エージェント サービスのアカウント]** の代わりにプロキシ アカウントを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用してパッケージを実行する場合に発生する一般的な問題を解決できる場合があります。 それらの問題の詳細については、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポート技術情報の記事「 [SQL Server エージェント ジョブ ステップから SSIS パッケージを呼び出したときに、SSIS パッケージが実行されない](https://support.microsoft.com/kb/918760)」を参照してください。 
     
  7.1 プロキシを使用してジョブを実行する場合、ジョブを正常に実行するには、次のセキュリティ項目が配置されている必要があります。

      プロキシによって使用される資格情報でのログインでは、SQL Server エージェントを実行するアカウントと SQL Server サービスを実行するアカウントに、次のアクセス許可が必要です。ローカル セキュリティ ポリシー属性:%SYSTEMROOT%\Temp に対するプロセス レベルのトークンのフル コントロールを置き換えます。 

セキュリティ項目が配置されていない場合、ジョブは失敗し、次のようなエラー メッセージが表示されます。ジョブは失敗しました。  クライアントには必要な特権がありません。
     
  
    > **NOTE:** If the password changes for the credential that the proxy account uses, you need to update the credential password. Otherwise, the job step will fail.  
  
     For information about configuring the SQL Server Agent service account, see [Set the Service Startup Account for SQL Server Agent &#40;SQL Server Configuration Manager&#41;](https://msdn.microsoft.com/library/46ffe818-ebb5-43a0-840b-923f219a2472).  
  
8.  **[パッケージ ソース]** ボックスの一覧でパッケージのソースをクリックし、ジョブ ステップのオプションを構成します。  
  
     **次の表は、使用できるパッケージ ソースを示しています。**  
  
    |[パッケージ ソース]|[説明]|  
    |--------------------|-----------------|  
    |**SSIS カタログ**|SSISDB データベースに格納されるパッケージ。 パッケージは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置される [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトに含まれています。|  
    |**SQL Server**|MSDB データベースに格納されるパッケージ。 これらのパッケージを管理するには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを使用します。|  
    |**[SSIS パッケージ ストア]**|コンピューターの既定のフォルダーに格納されるパッケージ。 既定のフォルダーは、 *\<ドライブ>* :\Program Files\Microsoft SQL Server\110\DTS\Packages です。 これらのパッケージを管理するには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを使用します。<br /><br /> 注:[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の構成ファイルを変更することで、別のフォルダーを指定したり、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスによって管理されるファイル システムの追加のフォルダーを指定したりすることができます。 詳細については、「[Integration Services サービス (SSIS サービス)](../../integration-services/service/integration-services-service-ssis-service.md)」を参照してください。|  
    |**[ファイル システム]**|ローカル コンピューターの任意のフォルダーに格納されるパッケージ。|  
  
     **次の表では、選択したパッケージ ソースに応じてジョブ ステップで使用できる構成オプションについて説明しています。**  
  
    > **重要:** パッケージがパスワードで保護されている場合、 **[新しいジョブ ステップ]** ダイアログ ボックスの **[全般]** ページのいずれかのタブ ( **[パッケージ]** タブを除く) をクリックすると、 **[パッケージ パスワード]** ダイアログ ボックスが表示されるので、パスワードを入力する必要があります。 入力しないと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブはパッケージの実行に失敗します。  
  
     **パッケージ ソース:** SSIS カタログ  
  
    |タブ|オプション|  
    |---------|-------------|  
    |**[パッケージ]**|**[サーバー]**<br /><br /> SSISDB カタログをホストしているデータベース サーバー インスタンスの名前を入力または選択します。<br /><br /> **[SSIS カタログ]** がパッケージ ソースである場合、サーバーへのログオンに使用できるのは Microsoft Windows ユーザー アカウントだけです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証は使用できません。|  
    ||**[パッケージ]**<br /><br /> 参照ボタンをクリックして、パッケージを選択します。<br /><br /> **オブジェクト エクスプローラー** の **[Integration Services カタログ]** ノードの下にあるフォルダー内のパッケージを選択します。|  
    |**パラメーター**<br /><br /> **[構成]** タブにあります。|**Integration Services プロジェクト変換ウィザード** を使用すると、パッケージ構成をパラメーターに置き換えることができます。<br /><br /> **[パラメーター]** タブには、たとえば [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]を使用してパッケージをデザインしたときに追加したパラメーターが表示されます。 タブには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトをパッケージ配置モデルからプロジェクト配置モデルに変換したときにパッケージに追加されたパラメーターも表示されます。 パッケージに含まれているパラメーターの新しい値を入力します。 リテラル値を入力するか、既にパラメーターにマップしてあるサーバー環境変数に含まれている値を使用することができます。<br /><br /> リテラル値を入力するには、パラメーターの横にある参照ボタンをクリックします。 **[実行用のリテラル値を編集]** ダイアログ ボックスが表示されます。<br /><br /> 環境変数を使用するには、 **[環境]** をクリックし、使用する変数を含む環境を選択します。<br /><br /> **\*\* 重要 \*\*** 複数のパラメーターや接続マネージャー プロパティを複数の環境に含まれている変数にマップしている場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによってエラー メッセージが表示されます。 特定の実行で、パッケージは単一のサーバー環境に含まれている値だけで実行できます。<br /><br /> サーバー環境を作成し、変数をパラメーターにマップする方法については、「[Integration Services (SSIS) プロジェクトとパッケージの配置](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。|  
    |**接続マネージャー**<br /><br /> **[構成]** タブにあります。|接続マネージャー プロパティの値を変更します。 たとえば、サーバー名を変更できます。 パラメーターは、SSIS サーバー上で接続マネージャー プロパティ用に自動的に生成されます。 プロパティの値を変更するには、リテラル値を入力するか、既に接続マネージャー プロパティにマップしてあるサーバー環境変数に含まれている値を使用することができます。<br /><br /> リテラル値を入力するには、パラメーターの横にある参照ボタンをクリックします。 **[実行用のリテラル値を編集]** ダイアログ ボックスが表示されます。<br /><br /> 環境変数を使用するには、 **[環境]** をクリックし、使用する変数を含む環境を選択します。<br /><br /> **\*\* 重要 \*\*** 複数のパラメーターや接続マネージャー プロパティを複数の環境に含まれている変数にマップしている場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによってエラー メッセージが表示されます。 特定の実行で、パッケージは単一のサーバー環境に含まれている値だけで実行できます。<br /><br /> サーバー環境を作成し、変数を接続マネージャーのプロパティにマップする方法については、「[Integration Services (SSIS) プロジェクトとパッケージの配置](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。|  
    |**詳細設定**<br /><br /> **[構成]** タブにあります。|パッケージ実行用の次の追加の設定を構成します。|  
    ||**プロパティのオーバーライド**:<br /><br /> **[追加]** をクリックして、パッケージ プロパティの新しい値の入力、プロパティ パスの指定、およびプロパティ値が機微なデータであるかどうかの指定を行います。 機微なデータは [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーによって暗号化されます。 プロパティの設定を編集または削除するには、 **[プロパティのオーバーライド]** ボックスの行をクリックし、 **[編集]** または **[削除]** をクリックします。 プロパティ パスを見つけるには、次のいずれかの操作を行います。<br /><br /> \- XML 構成ファイル (\*.dtsconfig) からプロパティ パスをコピーします。 パスは、ファイルの Configuration セクションに PATH 属性の値として記述されています。 MaximumErrorCount プロパティのパスの例: \Package.Properties[MaximumErrorCount]<br /><br /> \- **パッケージ構成ウィザード** を実行し、最後の **[ウィザードの完了]** ページからプロパティ パスをコピーします。 その後、ウィザードの実行を取り消すことができます。<br /><br /> <br /><br /> 注: **[プロパティのオーバーライド]** オプションは、以前のリリースの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] からアップグレードされた構成を持つパッケージに対して適用されます。 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] を使用して作成し、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置するパッケージは、構成の代わりにパラメーターを使用します。|  
    ||**ログ記録レベル**<br /><br /> パッケージ実行のために、次のいずれかのログ記録レベルを選択します。 **[パフォーマンス]** または **[詳細]** ログ記録レベルを選択すると、パッケージ実行のパフォーマンスに影響を及ぼす可能性があります。<br /><br /> **[なし]** :<br />                          ログ記録をオフにします。 パッケージの実行状態のみがログに記録されます。<br /><br /> **[基本]** :<br />                          カスタム イベントと診断イベントを除く、すべてのイベントをログに記録します。 これがログ記録レベルの既定値です。<br /><br /> **[パフォーマンス]** :<br />                          パフォーマンス統計、および OnError イベントと OnWarning のイベントのみをログに記録します。<br /><br /> **[詳細]** :<br />                          カスタム イベントと診断イベントを含む、すべてのイベントをログに記録されます。<br /><br /> 選択したログ記録レベルによって、SSISDB ビューや [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーのレポートに表示される情報が決まります。 詳細については、「 [Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」を参照してください。|  
    ||**エラー時にダンプする**<br /><br /> パッケージの実行中にエラーが発生した場合に、デバッグ ダンプ ファイルを生成するかどうかを指定します。 ファイルには、問題のトラブルシューティングに役立つ、パッケージの実行に関する情報が含まれます。 このオプションを選択した場合、実行中にエラーが発生すると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によって .mdmp ファイル (バイナリ ファイル) および .tmp ファイル (テキスト ファイル) が作成されます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の既定では、これらのファイルは *\<ドライブ>:* \Program Files\Microsoft SQL Server\110\Shared\ErrorDumps フォルダーに格納されます。|  
    ||**32 ビット ランタイム**<br /><br /> 64 ビット バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがインストールされている 64 ビット コンピューター上で、32 ビット バージョンの dtexec ユーティリティを使用してパッケージを実行するかどうかを示します。<br /><br /> たとえば、パッケージが 64 ビット バージョンでは使用できないネイティブ OLE DB プロバイダーを使用している場合に、32 ビット バージョンの dtexec を使用してパッケージを実行する必要がある場合があります。 詳細については、「 [64 ビット コンピューター上の Integration Services に関する注意点](https://msdn.microsoft.com/library/ms141766\(SQL.105\).aspx)」を参照してください。<br /><br /> 既定では、ジョブ ステップの種類として **[SQL Server Integration Services パッケージ]** を選択した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントはシステムによって自動的に呼び出されるバージョンの dtexec ユーティリティを使用してパッケージを実行します。 システムは、コンピューター プロセッサと、コンピューター上で実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのバージョンに応じて、32 ビットまたは 64 ビット バージョンのユーティリティを呼び出します。|  
  
     **パッケージ ソース:** SQL Server、SSIS パッケージ ストア、またはファイル システム  
  
     SQL Server、SSIS パッケージ ストア、またはファイル システムに格納されるパッケージに設定できるオプションの多くは、 **dtexec** コマンド プロンプト ユーティリティのコマンド ライン オプションに対応しています。 ユーティリティとコマンド ライン オプションの詳細については、「 [dtexec ユーティリティ](../../integration-services/packages/dtexec-utility.md)」を参照してください。  
  
    |タブ|オプション|  
    |---------|-------------|  
    |**[パッケージ]**<br /><br /> これらは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストアに格納されるパッケージのタブ オプションです。|**[サーバー]**<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスのデータベース サーバー インスタンスの名前を入力または選択します。|  
    ||**[Windows 認証を使用する]**<br /><br /> Microsoft Windows ユーザー アカウントを使用してサーバーにログオンする場合に、このオプションを選択します。|  
    ||**[SQL Server 認証を使用する]**<br /><br /> 指定されたログイン名とパスワードを使用して、信頼関係の低い接続から接続した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン アカウントが設定されているかどうか、指定されたパスワードが以前に記録されたパスワードと一致しているかどうかを確認することで認証を行います。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のログイン アカウントが見つからない場合、認証は失敗し、エラー メッセージが返されます。|  
    ||**[ユーザー名]**|  
    ||**パスワード**|  
    ||**[パッケージ]**<br /><br /> 参照ボタンをクリックして、パッケージを選択します。<br /><br /> **オブジェクト エクスプローラー** の **[格納されたパッケージ]** ノードの下にあるフォルダー内のパッケージを選択します。|  
    |**[パッケージ]**<br /><br /> これらは、ファイル システムに格納されるパッケージのタブ オプションです。|**[パッケージ]**<br /><br /> パッケージ ファイルのフル パスを入力するか、参照ボタンをクリックしてパッケージを選択します。|  
    |**構成**|特定の構成でパッケージを実行するための XML 構成ファイルを追加します。 パッケージのプロパティの値を実行時に更新するために、パッケージ構成を使用します。<br /><br /> このオプションは、 **dtexec** の **/ConfigFile**オプションに対応しています。<br /><br /> パッケージ構成が適用されるしくみについては、「 [Package Configurations](../../integration-services/packages/package-configurations.md)」を参照してください。 パッケージ構成を作成する方法の詳細については、「 [Create Package Configurations](../../integration-services/packages/create-package-configurations.md)」を参照してください。|  
    |**[コマンド ファイル]**|**dtexec**と共に実行する追加のオプションを、別のファイル内に指定します。<br /><br /> たとえば、/Dump *errorcode* オプションが記述されたファイルを含めると、パッケージの実行中に 1 つ以上の指定されたイベントが発生した場合に、デバッグ ダンプ ファイルを生成することができます。<br /><br /> 複数のファイルを作成し、 **[コマンド ファイル]** オプションを使用して適切なファイルを指定することで、異なるオプションのセットでパッケージを実行できます。<br /><br /> **[コマンド ファイル]** オプションは、 **dtexec** の **/CommandFile**オプションに対応しています。|  
    |**データ ソース**|パッケージに含まれている接続マネージャーを表示します。 接続文字列を変更するには、接続マネージャーをクリックして、接続文字列をクリックします。<br /><br /> このオプションは、 **dtexec** の **/Connection**オプションに対応しています。|  
    |**実行オプション**|**検証時に警告が発生したらパッケージを失敗とする**<br /> 警告メッセージをエラーと見なすかどうかを示します。 このオプションを選択した場合、検証中に警告が発生すると、パッケージは失敗します。 このオプションは、 **dtexec** の **/WarnAsError**オプションに対応しています。<br /><br /> **[パッケージを実行せずに検証する]**<br /> 検証フェーズ後にパッケージの実行を停止して、実際にはパッケージを実行しないかどうかを示します。 このオプションは、 **dtexec** の **/Validate**オプションに対応しています。<br /><br /> **MacConcurrentExecutables プロパティをオーバーライドする**<br /> パッケージが同時に実行できる実行可能ファイルの数を指定します。 値を -1 にすると、パッケージが実行できる実行可能ファイルの最大数が、パッケージを実行しているコンピューターのプロセッサの合計数に 2 を加えた数と等しくなることを意味します。 このオプションは、 **dtexec** の **/MaxConcurrent**オプションに対応しています。<br /><br /> **[パッケージのチェックポイントを有効にする]**<br /> パッケージの実行中にパッケージがチェックポイントを使用するかどうかを示します。 詳細については、「 [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md)」を参照してください。<br /><br /> このオプションは、 **dtexec** の **/CheckPointing**オプションに対応しています。<br /><br /> **[再開オプションをオーバーライドする]**<br /> パッケージの **CheckpointUsage** プロパティに新しい値が設定されるかどうかを示します。 **[再開オプション]** ボックスの一覧から値を選択します。<br /><br /> このオプションは、 **dtexec** の **/Restart**オプションに対応しています。<br /><br /> **32 ビット ランタイムを使用する**<br /> 64 ビット バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがインストールされている 64 ビット コンピューター上で、32 ビット バージョンの dtexec ユーティリティを使用してパッケージを実行するかどうかを示します。<br /><br /> たとえば、パッケージが 64 ビット バージョンでは使用できないネイティブ OLE DB プロバイダーを使用している場合に、32 ビット バージョンの dtexec を使用してパッケージを実行する必要がある場合があります。 詳細については、「 [64 ビット コンピューター上の Integration Services に関する注意点](https://msdn.microsoft.com/library/ms141766\(SQL.105\).aspx)」を参照してください。<br /><br /> 既定では、ジョブ ステップの種類として **[SQL Server Integration Services パッケージ]** を選択した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントはシステムによって自動的に呼び出されるバージョンの dtexec ユーティリティを使用してパッケージを実行します。 システムは、コンピューター プロセッサと、コンピューター上で実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのバージョンに応じて、32 ビットまたは 64 ビット バージョンのユーティリティを呼び出します。|  
    |**ログ記録**|ログ プロバイダーをパッケージの実行に関連付けます。<br /><br /> **テキスト ファイルの SSIS ログ プロバイダー**<br /> ログ エントリを ASCII テキスト ファイルに書き込みます。<br /><br /> **SQL Server の SSIS ログ プロバイダー**<br /> ログ エントリを MSDB データベースの sysssislog テーブルに書き込みます。<br /><br /> **SQL Server Profiler の SSIS ログ プロバイダー**<br /> SQL Server Profiler を使用して表示できるトレースを書き込みます。<br /><br /> **Windows イベント ログの SSIS ログ プロバイダー**<br /> ログ エントリを Windows イベント ログのアプリケーション ログに書き込みます。<br /><br /> **XML ファイルの SSIS ログ プロバイダー**<br /> ログ ファイルを XML ファイルに書き込みます。<br /><br /> テキスト ファイル、XML ファイル、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler のログ プロバイダーには、パッケージに含まれているファイル接続マネージャーを選択しています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログ プロバイダーには、パッケージに含まれている OLE DB 接続マネージャーを選択しています。<br /><br /> このオプションは、 **dtexec** の **/Logger**オプションに対応しています。|  
    |**値の設定**|パッケージのプロパティ設定をオーバーライドします。 **[プロパティ]** ボックスで、 **[プロパティのパス]** および **[値]** 列に値を入力します。 1 つのプロパティに値を入力すると、 **[プロパティ]** ボックスに空の行が表示され、他のプロパティの値を入力できるようになります。<br /><br /> [プロパティ] ボックスからプロパティを削除するには、行をクリックし、 **[削除]** をクリックします。<br /><br /> プロパティ パスを見つけるには、次のいずれかの操作を行います。<br /><br /> \- XML 構成ファイル (\*.dtsconfig) からプロパティ パスをコピーします。 パスは、ファイルの Configuration セクションに PATH 属性の値として記述されています。 MaximumErrorCount プロパティのパスの例: \Package.Properties[MaximumErrorCount]<br /><br /> \- **パッケージ構成ウィザード** を実行し、最後の **[ウィザードの完了]** ページからプロパティ パスをコピーします。 その後、ウィザードの実行を取り消すことができます。|  
    |**検証**|**[署名付きパッケージのみ実行する]**<br /> パッケージの署名が確認されるかどうかを示します。 パッケージが署名されていないか、署名が有効でない場合、パッケージは失敗します。 このオプションは、 **dtexec** の **/VerifySigned**オプションに対応しています。<br /><br /> **パッケージのビルドを検証する**<br /> パッケージのビルド番号を、このオプションの横にある **[ビルド]** ボックスに入力されたビルド番号と比較して検証するかどうかを示します。 不一致が発生した場合、パッケージは実行されません。 このオプションは、 **dtexec** の **/VerifyBuild**オプションに対応しています。<br /><br /> **[パッケージ ID を確認する]**<br /> パッケージの GUID を、このオプションの横にある **[パッケージ ID]** ボックスに入力されたパッケージ ID と比較して検証するかどうかを示します。 このオプションは、 **dtexec** の **/VerifyPackageID**オプションに対応しています。<br /><br /> **[バージョン ID を確認する]**<br /> パッケージのバージョン GUID を、このオプションの横にある **[バージョン ID]** ボックスに入力されたバージョン ID と比較して検証するかどうかを示します。 このオプションは、 **dtexec** の **/VerifyVersionID**オプションに対応しています。|  
    |**コマンド ライン**|dtexec のコマンド ライン オプションを変更します。 オプションの詳細については、「 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)」を参照してください。<br /><br /> **[元のオプションを復元する]**<br /> **[ジョブ ステップのプロパティ]** ダイアログ ボックスの **[パッケージ]** 、 **[構成]** 、 **[コマンド ファイル]** 、 **[データ ソース]** 、 **[実行オプション]** 、 **[ログ記録]** 、 **[値の設定]** 、 **[検証]** の各タブで設定したコマンド ライン オプションを使用します。<br /><br /> **コマンド ラインを手動で編集する**<br /> **[コマンド ライン]** ボックスに追加のコマンド ライン オプションを入力します。<br /><br /> **[OK]** をクリックして変更をジョブ ステップに保存する前に、 **[元のオプションを復元する]** をクリックすると、 **[コマンド ライン]** ボックスに入力したすべての追加のオプションを削除できます。<br /><br /> **\*\* ヒント \*\*** コマンド ラインをコマンド プロンプト ウィンドウにコピーし、 `dtexec`を追加して、コマンド ラインからパッケージを実行できます。 これは、コマンド ライン テキストを生成する簡単な方法です。|  
  
9. **[OK]** をクリックして設定を保存し、 **[新しいジョブ ステップ]** ダイアログ ボックスを閉じます。  
  
    > **注:** **SSIS カタログ**に格納されるパッケージの場合、未解決のパラメーターまたは接続マネージャーのプロパティ設定があると、 **[OK]** ボタンが無効になります。 設定が未解決になるのは、パラメーターまたはプロパティを設定するためにサーバー環境変数に含まれている値を使用し、次のいずれかの条件が満たされる場合です。  
    >   
    >  **[構成]** タブの **[環境]** チェック ボックスがオフになっている。  
    >   
    >  変数を含むサーバー環境が、 **[構成]** タブのリスト ボックスで選択されていない。  
  
10. ジョブ ステップのスケジュールを作成するには、 **[ページの選択]** ペインの **[スケジュール]** をクリックします。 スケジュールを構成する方法の詳細については、「 [Schedule a Job](../../ssms/agent/schedule-a-job.md)」を参照してください。  
  
    > [!TIP]  
    >  スケジュールに名前を付けるときには、他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのスケジュールとの区別がより簡単にできるように、一意でわかりやすい名前を使用してください。  

## <a name="see-also"></a>参照  
 [プロジェクトとパッケージの実行](deploy-integration-services-ssis-projects-and-packages.md)  

## <a name="external-resources"></a>外部リソース  
  
-   [Web サイトのサポート技術情報の記事「](https://support.microsoft.com/kb/918760)SQL Server エージェントのジョブ ステップから SSIS パッケージを呼び出したときに SSIS パッケージが実行されません [!INCLUDE[msCoName](../../includes/msconame-md.md)] 」  
  
-   MSDN ライブラリのビデオ「[トラブルシューティング: SQL Server エージェントを使用した SSIS パッケージ実行 (SQL Server ビデオ)](https://go.microsoft.com/fwlink/?LinkId=141772)」  
  
-   MSDN ライブラリのビデオ「[SQL Server エージェントを使用してパッケージ実行を自動化する方法 (SQL Server ビデオ)](https://go.microsoft.com/fwlink/?LinkId=141771)」  
  
-   mssqltips.com の技術記事「 [Windows PowerShell を使用した SQL Server エージェント ジョブの確認](https://go.microsoft.com/fwlink/?LinkId=165675)」  
  
-   mssqltips.com の技術記事「 [SQL エージェント ジョブを有効または無効にしたときの自動警告](https://go.microsoft.com/fwlink/?LinkId=165676)」  
  
-   mssqltips.com のブログ「 [Windows イベント ログに書き込むための SQL エージェント ジョブの構成](https://go.microsoft.com/fwlink/?LinkId=220745)」  
  
  
