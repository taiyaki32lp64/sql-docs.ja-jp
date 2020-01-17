---
title: 手順 3:配置したパッケージのテスト | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9159da3f-c9ca-4015-9e85-3bf4373a1349
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ac260f2c3703260e5472d5be399333a93574f2c9
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283254"
---
# <a name="lesson-3-3---testing-the-deployed-packages"></a>レッスン 3-3 - 配置したパッケージのテスト

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このタスクでは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のインスタンスに配置したパッケージをテストします。  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] の他のチュートリアルでは、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)][デバッグ] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]メニューの **[デバッグ開始]** オプションを使用して、 **の配置環境である** でパッケージを実行しました。 今度は別の方法でパッケージを実行します。  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、テスト環境と運用環境でパッケージを実行するときに使用できるコマンド プロンプト ユーティリティ **dtexec** やパッケージ実行ユーティリティなどのツールが付属しています。 パッケージ実行ユーティリティは、 **dtexec**を基に構築されたグラフィカル ツールです。 この 2 つのツールはパッケージを即座に実行します。 さらに、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] には、SQL Server エージェントのジョブの一工程としてパッケージの実行をスケジュールするように設計された SQL Server エージェントのサブシステムがあります。  
  
パッケージ実行ユーティリティは、配置したパッケージを実行するために使用します。 パッケージはそのままの状態で使用されるため、ダイアログ ボックスのページで情報を更新する必要はありません。 パッケージ実行ユーティリティで最初に表示される [全般] ページからパッケージを実行します。 必要に応じて、他のページもクリックして、各パッケージに関する情報を表示できます。  
  
> [!NOTE]  
> このチュートリアル内でパッケージが正しく実行されるように、オプションは変更しないでください。  
  
パッケージ実行ユーティリティを使用して [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] でパッケージを実行する前に、Integration Services サービスが実行していることを確認してください。 Integration Services サービスは、パッケージの保管と実行のサポートを提供します。 このサービスが停止した場合は、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] に接続できず、実行するパッケージが [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] に表示されません。 また、パッケージを配置したインスタンスでパッケージを実行する権限も必要です。 詳細については、「[Integration Services のロール &#40;SSIS サービス&#41;](../integration-services/security/integration-services-roles-ssis-service.md)」を参照してください。  
  
[格納されたパッケージ] フォルダー内の最上位フォルダーは、Integration Services サービスが監視するユーザー定義フォルダーです。 MsDtsSrvr.ini.xml ファイルで指定できるフォルダー数に制限はありません。 このチュートリアルでは、既定の MsDtsSrvr.ini.xml ファイルを使用し、[格納されたパッケージ] 内の最上位フォルダーの名前は "File System" と "MSDB" であると想定しています。  
  
### <a name="to-connect-to-integration-services-in-sql-server-management-studio"></a>SQL Server Management Studio で Integration Services に接続するには  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[Microsoft SQL Server]** の順にポイントし、 **[SQL Server Management Studio]** をクリックします。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスで、 **[サーバーの種類]** ボックスの一覧から **[Integration Services]** を選択し、 **[サーバー名]** ボックスにサーバーの名前を入力して、 **[接続]** をクリックします。  
  
    > [!IMPORTANT]  
    > [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]に接続できない場合は、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスが実行されていない可能性があります。 このサービスの状態を調べるには、 **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[Microsoft SQL Server]** 、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。 左ペインで、 **[SQL Server のサービス]** をクリックします。 右ペインで、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスを見つけます。 サービスがまだ実行されていない場合は開始します。  
  
    [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] が開きます。 既定では [オブジェクト エクスプローラー] ウィンドウが開き、 の右上に表示されます。 オブジェクト エクスプローラーが開いていない場合は、 **[表示]** メニューの **[オブジェクト エクスプローラー]** をクリックします。  
  
### <a name="to-run-the-packages-using-the-execute-package-utility"></a>パッケージ実行ユーティリティを使用してパッケージを実行するには  
  
1.  オブジェクト エクスプローラーで、[格納されたパッケージ] フォルダーを展開します。  
  
2.  MSDB フォルダーを展開します。 パッケージを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に配置したため、配置したパッケージはすべて msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースに格納され、MSDB フォルダーに表示されます。 Deployment Tutorial 以外のファイル システムにパッケージを配置した場合を除き、[File System] フォルダーは空です。  
  
3.  パッケージ一覧の一番上から開始し、[DataTransfer] を右クリックして **[パッケージの実行]** をクリックします。  
  
4.  **[パッケージ実行ユーティリティ]** ダイアログ ボックスで **[実行]** をクリックします。  
  
5.  **[パッケージ実行ユーティリティ]** ダイアログ ボックスで、パッケージの進行状況と実行結果を表示します。 **[停止]** ボタンが無効の場合は、パッケージが完了したことを示すので、 **[閉じる]** をクリックします。  
  
    > [!IMPORTANT]  
    > パッケージの実行中に **[停止]** をクリックすると、パッケージは完了しません。  
  
6.  **[パッケージ実行ユーティリティ]** ダイアログ ボックスで **[閉じる]** をクリックします。  
  
7.  LoadXML パッケージに手順 3. ～ 6. を繰り返します。  
  
8.  **[ファイル]** メニューの **[終了]** をクリックします。  
  
### <a name="to-verify-the-results-of-the-datatransfer-package"></a>DataTransfer パッケージの結果を確認するには  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]のツール バーから **[新しいクエリ]** をクリックします。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスで、 **[サーバーの種類]** ボックスの一覧から **[データベース エンジン]** を選択し、チュートリアル パッケージをインストールしたサーバーの名前または種類 (local) を **[サーバー名]** ボックスに入力して、認証モードを選択します。 SQL Server 認証を使用する場合は、ユーザー名とパスワードを入力します。  
  
3.  **[接続]** をクリックします。  
  
4.  クエリ ウィンドウで、次の SQL ステートメントを入力するか貼り付けます。  
  
    `USE AdventureWorks`  
  
    `SELECT * FROM HighIncomeCustomers`  
  
5.  **F5** キーを押すか、ツール バーの実行アイコンをクリックします。  
  
    このクエリによって 31 行のデータが返されます。 返された結果には、YearlyIncome 列の値が 100,000 より大きい Customers.txt テキスト ファイルの行が含まれています。  
  
6.  DeploymentTutorial フォルダーを見つけ、ログ XML ファイル [Deployment Tutorial Log] を右クリックして、 **[開く]** をクリックします。 メモ帳やその他のテキスト エディターまたは XML エディターを使用してファイルを開くことができます。  
  
### <a name="to-verify-the-results-of-the-loadxmldata-package"></a>LoadXMLData パッケージの結果を確認するには  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]のツール バーから **[新しいクエリ]** をクリックします。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスで、 **[サーバーの種類]** ボックスの一覧から **[データベース エンジン]** を選択し、チュートリアル パッケージをインストールしたサーバーの名前または「(local)」を **[サーバー名]** ボックスに入力して、認証モードを選択します。 SQL Server 認証を使用する場合は、ユーザー名とパスワードを入力します。  
  
3.  **[接続]** をクリックします。  
  
4.  クエリ ウィンドウで、次の SQL ステートメントを入力するか貼り付けます。  
  
    `USE AdventureWorks`  
  
    `SELECT * FROM OrderDatesByCountryRegion`  
  
5.  **F5** キーを押すか、ツール バーの実行アイコンをクリックします。  
  
    このクエリによって 21 行のデータが返されます。 返された結果は、XML データ ファイル orders.xml の行で構成されています。 各行は国/地域別の要約であり、国名/地域名、国/地域ごとの注文数、および最新と最古の注文日が示されます。  
  
## <a name="see-also"></a>参照  
[dtexec ユーティリティ](../integration-services/packages/dtexec-utility.md)  
  
  
  
