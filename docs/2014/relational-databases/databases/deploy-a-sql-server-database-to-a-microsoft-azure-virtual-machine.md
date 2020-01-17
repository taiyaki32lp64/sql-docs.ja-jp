---
title: Microsoft Azure Virtual Machine の SQL Server データベースの配置 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.deploymentwizard.deploymentsettings.f1
- sql12.swb.deploymentwizard.progress.f1
- sql11.swb.usevmdialog.f1
- sql11.swb.deploymentwizard.f1
- sql12.swb.deploymentwizard.azuresignin.f1
- sql11.swb.deploymentwizard.summary.f1
- sql11.swb.deploymentwizard.azuresignin.f1
- sql12.swb.deploymentwizard.f1
- sql12.swb.sqlvmdialog.f1
- sql11.swb.newvmdialog.f1
- sql12.swb.deploymentwizard.results.f1
- sql11.swb.deploymentwizard.progress.f1
- sql12.swb.newvmdialog.f1
- sql12.swb.deploymentwizard.sourcesettings.f1
- sql12.swb.usevmdialog.f1
- sql11.swb.deploymentwizard.sourcesettings.f1
- sql11.swb.deploymentwizard.results.f1
- sql12.swb.deploymentwizard.summary.f1
- sql11.swb.deploymentwizard.deploymentsettings.f1
helpviewer_keywords:
- Deploy a database
- Deploy to Azure VM
- Migrate to Azure
- Azure virtual machine
- Migrate to Azure VM
- Migrate to the cloud
- SQL Server Management Studio
- SSMS
- Deploy database wizard
- Deploy a SQL Server database to Azure
- Azure VM
ms.assetid: 5e82e66a-262e-4d4f-aa89-39cb62696d06
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c7d84fbe56d36bd91f2b7f8b49a3df73fb383c6e
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175741"
---
# <a name="deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine"></a>Microsoft Azure Virtual Machine の SQL Server データベースの配置
  Azure 仮想マシン (VM) 内の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスからデータベースをデプロイするには、 **AZURE VM への SQL Server データベースのデプロイ**ウィザードを使用します。 このウィザードはデータベースの完全バックアップ操作を活用し、SQL Server のユーザー データベースから常にデータベース スキーマ全体とデータ全体をコピーします。 また、このウィザードは Azure のすべての仮想マシンを自動的に構成するため、仮想マシンの事前構成は必要ありません。  
  
 このウィザードは同じデータベース名を持つ既存のデータベースを上書きしないため、このウィザードを使用して差分バックアップを実行することはできません。 仮想マシン上にある既存のデータベースを置き換えるには、まず既存のデータベースを削除するか、データベース名を変更する必要があります。 インフライト配置操作を実行しているときに、複数のデータベース名の間で名前の競合が発生し、既存のデータベースが仮想マシン上に存在している場合は、ウィザードはインフライト データベースに対して付加的なデータベース名を提示し、操作を完了できるようにします。  
  
##  <a name="before_you_begin"></a> はじめに  
 このウィザードを完了するには、次の情報を用意し、これらの構成設定を整える必要があります。  
  
-   Azure サブスクリプションに関連付けられている Microsoft アカウントの詳細。  
  
-   Azure 発行プロファイル。  
  
    > [!CAUTION]  
    >  SQL Server では現在、公開プロファイルのバージョン 2.0 がサポートされています。 公開プロファイルのサポート対象バージョンをダウンロードするには、「 [公開プロファイルのバージョン 2.0 のダウンロード](https://go.microsoft.com/fwlink/?LinkId=396421)」をご覧ください。  
  
-   Azure サブスクリプションにアップロードされた管理証明書。  
  
-   ウィザードを実行するコンピューターで個人証明書ストアに保存された管理証明書。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースをホストするコンピューターで使用できる一時格納場所が必要です。 この一時格納場所は、このウィザードを実行するコンピューターでも使用できる必要があります。  
  
-   既存の仮想マシンにデータベースを配置する場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを TCP/IP ポートでリッスンするように構成する必要があります。  
  
-   VM の作成に使用する予定の Azure VM またはギャラリーイメージには、SQL Server クラウドアダプター構成され、実行されている必要があります。  
  
-   プライベートポート11435を使用して、Azure ゲートウェイで SQL Server クラウドアダプターのオープンエンドポイントを構成する必要があります。  
  
 また、データベースを既存の Azure VM にデプロイする予定がある場合は、次の情報も提供できる必要があります。  
  
-   仮想マシンをホストするクラウド サービスの DNS 名。  
  
-   仮想マシンの管理者資格情報。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のソース インスタンスから配置を計画しているデータベースのバックアップ操作の特権資格情報。  
  
 Azure 仮想マシンでの SQL Server の実行の詳細については、「 [azure Virtual Machines で SQL Server に移行する](https://msdn.microsoft.com/library/dn133142.aspx)ための準備」を参照してください。  
  
 Windows Server オペレーティング システムを実行しているコンピューターでは、このウィザードを実行するために、次の構成設定を使用する必要があります。  
  
-   セキュリティ強化の構成の無効化。[サーバー マネージャー] > [ローカル サーバー] を使用し、[Internet Explorer セキュリティ強化の構成]\(ESC) を **[オフ]** に設定します。  
  
-   JavaScript の有効化。Internet Explorer > [インターネット オプション] > [セキュリティ] > [レベルのカスタマイズ] > [スクリプト] > [アクティブ スクリプト] を選択し、 **[有効にする]** に設定します。  
  
###  <a name="limitations"></a> 制限事項と制約事項  
 この操作に対応するデータベース サイズの上限は 1 TB です。  
  
 この配置機能は、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]用の SQL Server Management Studio で使用できます。  
  
 この配置機能は、ユーザー データベースを使用している場合にのみ有効です。システム データベースの配置はサポートされていません。  
  
 配置機能はアフィニティ グループに関連付けられているホストされたサービスをサポートしていません。 たとえば、アフィニティ グループに関連付けられたストレージ アカウントはこのウィザードの **配置の設定** ページで使用するためには選択できません。  
  
 VM での SQL Server のバージョンは、配置元の SQL Server のバージョンと同じまたはそれ以降である必要があります。 このウィザードを使用して Azure VM にデプロイできるデータベースのバージョン SQL Server:  
  
-   SQL Server 2008  
  
-   SQL Server 2008 R2  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 Azure VM データベースで実行されている SQL Server データベースのバージョンは、次のように配置できます。  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 インフライト配置操作を実行しているときに、複数のデータベース名の間で名前の競合が発生し、既存のデータベースが仮想マシン上に存在している場合は、ウィザードはインフライト データベースに対して付加的なデータベース名を提示し、操作を完了できるようにします。  
  
###  <a name="filestream"></a> FILESTREAM が有効なデータベースの Azure 仮想マシンへの配置に関する注意点  
 FILESTREAM オブジェクトに格納されている BLOBS があるデータベースを配置する場合は、次のガイドラインと制限事項に注意してください:  
  
-   配置機能は FILESTREAM が有効なデータベースを新しい仮想マシンに配置することはできません。 ウィザードを実行する前に FILESTREAM が仮想マシンで有効になっていない場合は、データベースの復元操作が失敗し、ウィザードの操作が正常に完了できません。 FILESTREAM を使用するデータベースを正常に配置するには、ウィザードを起動する前にホスト仮想マシンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで FILESTREAM を有効にします。 詳細については、「 [FILESTREAM (SQL Server)](https://msdn.microsoft.com/library/gg471497.aspx)」を参照してください。  
  
-   データベースがインメモリ OLTP を使用すると、データベースを変更せずに Azure 仮想マシンにデータベースを配置できます。 詳細については、「 [インメモリ OLTP (インメモリ最適化)](https://msdn.microsoft.com/library/dn133186\(SQL.120\).aspx)」を参照してください。  
  
###  <a name="geography"></a> 資産の地理的分散に関する注意点  
 次の資産が同じ地理的領域に存在する必要があることに注意してください:  
  
-   クラウド サービス  
  
-   仮想マシンの場所  
  
-   データ ディスク ストレージ サービス  
  
 上記の資産が同じ場所に配置されていない場合は、正常に完了できません。  
  
###  <a name="configuration_settings"></a> ウィザードの構成設定  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース配置の Azure 仮想マシンへの設定を変更するには、次の構成の詳細を使用します。  
  
-   **構成ファイルの既定のパス** - %LOCALAPPDATA%\SQL Server\Deploy to SQL in WA VM\DeploymentSettings.xml  
  
-   **構成ファイルの構造**  
  
    -   \<DeploymentSettings>  
  
        -   <OtherSettings  
  
            -   TraceLevel="Debug" \<!-- Logging level -->  
  
            -   BackupPath="\\\\[サーバー名]\\[ボリューム]\\" \<!-- バックアップの最後に使用されたパス。 ウィザードで既定値として使用されます。 -->  
  
            -   CleanupDisabled = False/> \<!--ウィザードでは、中間ファイルと Azure オブジェクト (VM、CS、SA) は削除されません。 -->  
  
        -   <PublishProfile \<! -- 最後に使用されたパブリッシュのプロファイル情報。 -->  
  
            -   Certificate="12A34B567890123ABCD4EF567A8" \<!-- ウィザードで使用する証明書。 -->  
  
            -   Subscription="1a2b34c5-67d8-90ef-ab12-xxxxxxxxxxxxx" \<!-- ウィザードで使用するサブスクリプション。 -->  
  
            -   Name="My Subscription" \<!-- サブスクリプションの名前。 -->  
  
            -   Publisher="" />  
  
    -   \</DeploymentSettings>  
  
 **構成ファイルの値**  
  
###  <a name="permissions"></a> アクセス許可  
 配置されるデータベースは標準状態でなければならず、このデータベースはウィザードを実行するユーザー アカウントからアクセスできる必要があり、ユーザー アカウントにはバックアップ操作を実行する権限が必要です。  
  
##  <a name="launch_wizard"></a>Azure 仮想マシンへのデータベースの配置ウィザードの使用  
 **ウィザードを起動するには、次の手順を実行します。**  
  
1.  SQL Server Management Studio を使用して、配置するデータベースがある [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続します。  
  
2.  **オブジェクト エクスプローラー**で、インスタンス名を展開してから、 **データベース** ノードを展開します。  
  
3.  配置するデータベースを右クリックし、 **[タスク]** をクリックして、 **[Azure VM にデータベースを配置]** を選択します。  
  

  
##  <a name="Introduction"></a> [説明] ページ  
 このページでは、 **AZURE VM への SQL Server データベースのデプロイ**ウィザードについて説明します。  
  
 **オプション**  
  
-   **[次回からこのページを表示しない]** - 今後 [説明] ページを表示しないようにするには、このチェック ボックスをオンにします。  
  
-   **[次へ]** - **[ソースの設定]** ページに進みます。  
  
-   **[キャンセル]** : 操作を取り消し、ウィザードを閉じます。  
  
-   **[ヘルプ]** : ウィザードの MSDN ヘルプトピックを起動します。  
  
##  <a name="Source_settings"></a> [ソース設定]  
 このページを使用して、Azure VM に配置するデータベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続します。 また、ファイルを Azure に転送する前に、ローカルコンピューターから保存するファイルの一時的な場所も指定します。 共有のネットワークの場所を指定できます。  
  
 **オプション**  
  
-   **[接続...]** をクリックし、配置するデータベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの接続詳細を指定します。  
  
-   **[データベースの選択]** ドロップダウン リストを使用して、展開するデータベースを指定します。  
  
-   **[その他の設定]** フィールドで、Azure VM サービスにアクセスできる共有フォルダーを指定します。  
  
##  <a name="Azure_sign-in"></a>Azure サインイン  
 このページを使用して、Azure に接続し、管理証明書または発行プロファイルの詳細を指定します。  
  
 **オプション**  
  
-   **[管理証明書]** -このオプションを使用して、Azure の管理証明書に一致するローカル証明書ストアの証明書を指定します。  
  
-   **[発行プロファイル]** : コンピューターにダウンロードした発行プロファイルがある場合に、このオプションを使用します。  
  
-   **サインイン**-このオプションを使用して、Live ID や Hotmail アカウントなどの Microsoft アカウントを使用して Azure にサインインし、新しい管理証明書を生成してダウンロードします。 サブスクリプションごとの証明書の数は制限されています。  
  
-   **[サブスクリプション]** -ローカルの証明書ストアまたは公開プロファイルと一致する、AZURE サブスクリプション ID を選択、入力、または貼り付けます。  
  
##  <a name="Deployment_settings"></a> [配置設定] ページ  
 このページを使用して、配置先サーバーと、新しいデータベースの詳細を指定します。  
  
 **オプション**  
  
-   **Azure 仮想マシン**-SQL Server データベースをホストする VM の詳細を指定します。  
  
-   **クラウドサービス名**-VM をホストするサービスの名前を指定します。 新しいクラウド サービスを作成するには、新しいクラウド サービスの名前を指定します。  
  
-   **仮想マシン名**-SQL Server データベースをホストする VM の名前を指定します。 新しい Azure VM を作成するには、新しい VM の名前を指定します。  
  
-   **設定**-[設定] ボタンを使用して、SQL Server データベースをホストする新しい VM を作成します。 既存の仮想マシンを使用している場合は、指定した情報を使用して資格情報の認証が行われます。  
  
-   **[ストレージアカウント]** -ドロップダウンリストからストレージアカウントを選択します。 新しいストレージ アカウントを作成するには、新しいアカウントの名前を指定します。 アフィニティ グループに関連付けられたストレージ アカウントは、ドロップダウン リストに使用できないことに注意してください。  
  
-   **ターゲットデータベース**-ターゲットデータベースの詳細を指定します。  
  
-   サーバー**接続**-サーバーの接続の詳細。  
  
-   **データベース**-新しいデータベースの名前を指定または確認します。 対象の SQL Server インスタンスにデータベース名が既にある場合は、変更したデータベース名を指定することをお勧めします。  
  
##  <a name="Summary"></a> [概要] ページ  
 このページを使用すると、操作について指定した設定を確認できます。 指定した設定で配置操作を実行するには、 **[完了]** をクリックします。 配置操作を取り消してウィザードを終了するには、 **[キャンセル]** をクリックします。  
  
 Azure VM の SQL Server データベースにデータベースの詳細をデプロイするには、手動の手順が必要になる場合があります。 これらの手順については概要を詳しく説明します。  
  
##  <a name="Results"></a> [結果] ページ  
 このページでは、配置操作の成功と失敗が報告され、各アクションの結果が示されます。 エラーが発生したアクションには、 **[結果]** 列に情報が表示されます。 そのアクションのエラーのレポートを表示するには、リンクをクリックします。  
  
 **[完了]** をクリックして、ウィザードを終了します。  
  
## <a name="see-also"></a>参照  
 [SQL Server 用のクラウド アダプター](../../database-engine/cloud-adapter-for-sql-server.md)   
 [データベースのライフサイクル管理](../database-lifecycle-management.md)   
 [データ層アプリケーションのエクスポート](../data-tier-applications/export-a-data-tier-application.md)   
 [BACPAC ファイルのインポートによる新しいユーザー データベースの作成](../data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)   
 [Azure SQL データベースのバックアップと復元](https://msdn.microsoft.com/library/azure/jj650016.aspx)   
 [Azure Virtual Machines  での SQL Server デプロイ](https://msdn.microsoft.com/library/dn133141.aspx)  
 [Azure Virtual Machines で SQL Server に移行するための準備](https://msdn.microsoft.com/library/dn133142.aspx)  
  
  
