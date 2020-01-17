---
title: チュートリアル:SSIS パッケージを SQL ビューとして公開する | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.packagepublishwizard.f1
ms.assetid: d32d9761-93fb-4020-bf82-231439c6f3ac
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 263f398e0c14c1b056185722a0662e031c9d7472
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297737"
---
# <a name="walkthrough-publish-an-ssis-package-as-a-sql-view"></a>チュートリアル:SQL ビューとして SSIS パッケージを公開する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  このチュートリアルでは、SSIS パッケージを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに SQL ビューとして公開する詳細な手順について説明します。  
  
## <a name="prerequisites"></a>Prerequisites  
 このチュートリアルを実行するには、コンピューターに次のソフトウェアがインストールされている必要があります。  
  
1.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 以降と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]を起動します。  
  
2.  [SQL Server Data Tools](../../ssdt/download-sql-server-data-tools-ssdt.md)  
  
## <a name="step-1-build-and-deploy-ssis-project-to-the-ssis-catalog"></a>手順 1:SSIS プロジェクトを構築して SSIS カタログに配置する  
 この手順では、SSIS 対応データ ソース ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースを使用します) からデータを抽出し、そのデータを Data Streaming Destination コンポーネントを使用して出力する SSIS パッケージを作成します。 その後、SSIS プロジェクトを構築して SSIS カタログに配置します。  
  
1.  **SQL Server Data Tools**を起動します。 **[スタート]** メニューで、 **[すべてのプログラム]** 、 **[Microsoft SQL Server]** の順にポイントし、 **[SQL Server Data Tools]** をクリックします。  
  
2.  新しい [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを作成します。  
  
    1.  メニュー バーの **[ファイル]** をクリックし、 **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。  
  
    2.  左側のウィンドウで **[ビジネス インテリジェンス]** を展開し、ツリー ビューで **[Integration Services]** をクリックします。  
  
    3.  まだ選択していない場合は **[Integration Services プロジェクト]** を選択します。  
  
    4.  **[プロジェクト名]** に「 **SSISPackagePublishing**」を指定します。  
  
    5.  プロジェクトの場所を指定します。  
  
    6.  **[OK]** をクリックして、 **[新しいプロジェクト]** ダイアログ ボックスを閉じます。  
  
3.  **Data Flow** コンポーネントを、 **SSIS ツールボックス** から **[コントロール フロー]** タブのデザイン画面にドラッグします。  
  
4.  **コントロール フロー** の **Data Flow** コンポーネントをダブルクリックして **データ フロー デザイナー**を開きます。  
  
5.  **ソース コンポーネント** を、ツールボックスから **データ フロー デザイナー** にドラッグし、データ ソースからデータを抽出するように構成します。  
  
    1.  このチュートリアルを実行するために、次のものを作成します。テスト データベース: **TestDB**、テーブル: **Employee**。 **ID**、 **FirstName** 、 **LastName**という 3 つの列があるテーブルを作成します。  
  
    2.  **ID** を主キーとして設定します。  
  
    3.  次のデータを持つ 2 つのレコードを挿入します。  
  
        |ID|FirstName|LastName|  
        |--------|---------------|--------------|  
        |1|John|Doe|  
        |2|Jane|Doe|  
  
    4.  **OLE DB Source** コンポーネントを **SSIS ツールボックス** から **データ フロー デザイナー**にドラッグします。  
  
    5.  コンポーネントを、 **TestDB** データベースの **Employee** テーブルからデータを抽出するように構成します。 **[OLE DB 接続マネージャー]** で **[(local).TestDB]** を、 **[データ アクセス モード]** で **[テーブルまたはビュー]** を、 **[テーブルまたはビューの名前]** で **[[dbo].[Employee]]** を選択します。  
  
         ![Data Streaming Destination - OLE DB 接続](../../integration-services/data-flow/media/dsd-oledbconnectionmanager.jpg "Data Streaming Destination - OLE DB 接続")  
  
6.  次に、 **Data Streaming Destination** をツールボックスからデータフローにドラッグします。 このコンポーネントはツールボックスの [共通] セクションにあります。  
  
7.  データ フローの **OLE DB Source** コンポーネントを **Data Streaming Destination** コンポーネントに接続します。  
  
8.  SSIS プロジェクトを構築して SSIS カタログに配置します。  
  
    1.  メニュー バーの **[プロジェクト]** をクリックし、 **[配置]** をクリックします。  
  
    2.  ウィザードの指示に従って、プロジェクトをローカル データベース サーバーの SSIS カタログに配置します。 次の例では、 **Power BI** をフォルダー名として、 **SSISPackagePublishing** をSSIS カタログ内のプロジェクト名として使用します。  
  
## <a name="step-2-use-the-ssis-data-feed-publishing-wizard-to-publish-ssis-package-as-a-sql-view"></a>手順 2:SSIS データ フィード公開ウィザードを使用して SSIS パッケージを SQL ビューとして公開する  
 この手順では、SQL Server Integration Services (SSIS) データ フィード公開ウィザードを使用して、SSIS パッケージを SQL Server データベースにビューとして公開します。 パッケージの出力データは、このビューをクエリすることで使用できます。  
  
 SSIS データ フィード公開ウィザードにより、OLE DB Provider for SSIS (SSISOLEDB) を利用するリンク サーバーが作成され、リンク サーバーのクエリを構成する SQL ビューが作成されます。 このクエリには、SSIS カタログのフォルダー名、プロジェクト名、およびパッケージ名が含まれます。  
  
 実行時、このビューにより、作成したリンク サーバーを経由して OLE DB Provider for SSIS にクエリが送信されます。 OLE DB Provider for SSIS はクエリに指定されたパッケージを実行し、表形式の結果セットをクエリに返します。  
  
1.  C:\Program Files\Microsoft SQL Server\130\DTS\Binn から ISDataFeedPublishingWizard.exe を実行するか、[スタート] メニュー、[すべてのプログラム]、[Microsoft SQL Server 2016]、[SQL Server 2016 データ フィード発行ウィザード] をクリックして **SSIS データフィード発行ウィザード** を起動します。  
  
2.  **[概要]** ページで **[次へ]** をクリックします。  
  
     ![データフィード発行ウィザード - [概要] ページ](../../integration-services/data-flow/media/dsd-feedpublishingwizard-introductionpage.jpg "データフィード発行ウィザード - [概要] ページ")  
  
3.  **[パッケージの設定]** ページで、次のタスクを実行します。  
  
    1.  SSIS カタログを含む SQL Server インスタンスの **名前** を入力するか、 **[参照]** をクリックしてサーバーを選択します。  
  
         ![データフィード発行ウィザード - [パッケージの設定] ページ](../../integration-services/data-flow/media/dsd-feedpublishingwizard-packagesettingspage.jpg "データフィード発行ウィザード - [パッケージの設定] ページ")  
  
    2.  [パス] フィールドの横にある **[参照]** をクリックして SSIS カタログを参照し、公開する SSIS パッケージを選択し (例: **SSISDB**->**SSISPackagePublishing**->**Package.dtsx**)、 **[OK]** をクリックします。  
  
         ![データフィード発行ウィザード - パッケージの参照](../../integration-services/data-flow/media/dsd-feedpublishingwizard-browseforpackage.jpg "データフィード発行ウィザード - パッケージの参照")  
  
    3.  ページ下部の [パッケージ パラメーター]、[プロジェクト パラメーター]、[接続マネージャー] タブを使用して、パッケージのパッケージ パラメーター、プロジェクト パラメーター、または接続マネージャーの設定値を入力します。 パッケージを実行するために使用される環境参照を指定して、プロジェクト/パッケージ パラメーターを環境変数にバインドすることもできます。  
  
         環境変数には機密性のあるパラメーターをバインドすることをお勧めします。 これにより、機密性のあるパラメーターの値が、ウィザードによって作成される SQL ビューにプレーン テキスト形式で格納されないことが保証されます。  
  
    4.  **[次へ]** をクリックして、 **[公開の設定]** ページに切り替えます。  
  
4.  **[公開の設定]** ページで、次のタスクを実行します。  
  
    1.  ビューを作成する **データベース** を選択します。  
  
         ![データフィード発行ウィザード - [公開の設定] ページ](../../integration-services/data-flow/media/dsd-feedpublishingwizard-publishsettingspage.jpg "データフィード発行ウィザード - [公開の設定] ページ")  
  
    2.  **ビュー** の **名前**を入力します。 ボックスの一覧から既存のビューを選択することもできます。  
  
    3.  **[設定]** リストに、ビューと関連付ける **リンク サーバー** の **名前** を指定します。 リンク サーバーが存在しない場合、ウィザードは、ビューを作成する前にリンク サーバーを作成します。 **User32BitRuntime** と **Timeout** の値をここに設定することもできます。  
  
    4.  **[詳細設定]** をクリックします。 **[詳細設定]** ダイアログ ボックスが表示されます。  
  
    5.  **[詳細設定]** ダイアログ ボックスで、次の操作を行います。  
  
        1.  ビューを作成するデータベース スキーマを指定します ([スキーマ] フィールド) 。  
  
        2.  ネットワーク経由で送信する前にデータを暗号化するかどうかを指定します ([暗号化] フィールド)。 この設定と TrustServerCertificate 設定の詳細については、「 [検証を伴わない暗号化の使用](../../relational-databases/native-client/features/using-encryption-without-validation.md) 」トピックを参照してください。  
  
        3.  暗号化設定が有効な場合に自己署名サーバー証明書を使用できるかどうかを指定します ([**TrustServerCertificate]** フィールド)。  
  
        4.  **[OK]** をクリックして **[詳細設定]** ダイアログ ボックスを閉じます。  
  
    6.  **[次へ]** をクリックして **[検証]** ページに移動します。  
  
5.  **[検証]** ページで、すべての設定値の検証結果を確認します。 次の例では、選択した SQL Server インスタンスにリンク サーバーが存在しないために、リンクサーバーの存在に関する **警告** が表示されています。 **[結果]** に **[エラー]** が表示された場合は、 **[エラー]** の上にマウス カーソルを合わせると、エラーの詳細を確認できます。 たとえば、SSISOLEDB プロバイダーの [InProcess 許可] オプションを有効にしていなかった場合は、リンク サーバーの構成操作でエラーが発生します。  
  
     ![データフィード発行ウィザード - [検証] ページ](../../integration-services/data-flow/media/dsd-feedpublishingwizard-validationpage.jpg "データフィード発行ウィザード - [検証] ページ")  
  
6.  このレポートを XML ファイルとして保存するために [レポートの保存] をクリックします。  
  
7.  **[検証]** ページで **[次へ]** をクリックして **[概要]** ページに切り替えます。  
  
8.  **[概要]** ページで選択内容を確認し、 **[公開]** をクリックして公開プロセスを開始します。リンク サーバーがサーバー上に存在していない場合は、リンク サーバーの作成後にそのリンク サーバーを使用するビューが作成されます。  
  
     ![データフィード発行ウィザード - [概要] ページ](../../integration-services/data-flow/media/dsd-feedpublishingwizard-summarypage.jpg "データフィード発行ウィザード - [概要] ページ")  
  
     これで、次の SQL ステートメントを TestDB データベースに対して実行することで、パッケージの出力データをクエリできます: SELECT * FROM [SSISPackageView]。  
  
9. このレポートを XML ファイルとして保存するために **[レポートの保存]** をクリックします。  
  
10. 公開プロセスの結果を確認し、 **[完了]** をクリックしてウィザードを閉じます。  
  
    > [!NOTE]  
    >  次のデータ型はサポートされていません: text、ntext、image、nvarchar(max)、varchar(max)、varbinary(max)。  
  
## <a name="step-3-test-the-sql-view"></a>手順 3:SQL ビューをテストする  
 ここでは、SSIS データ フィード公開ウィザードによって作成された SQL ビューを実行します。  
  
1.  SQL Server Management Studio を起動します。  
  
2.  \<**コンピューター名**>、 **[データベース]** 、\<**ウィザードで選択したデータベース**>、 **[ビュー]** の順に展開します。  
  
3.  ウィザードで作成した \<**ウィザードで作成したビュー**> を右クリックし、 **[上位 1000 行を選択]** をクリックします。  
  
4.  SSIS パッケージの結果が表示されることを確認します。  
  
## <a name="step-4-verify-the-ssis-package-execution"></a>手順 4:SSIS パッケージの実行を確認する  
 この手順では、SSIS パッケージが実行されたことを確認します。  
  
1.  SQL Server Management Studio で、 **[Integration Services カタログ]** 、 **[SSISDB]** 、SSIS プロジェクトが存在する **フォルダー** 、 **[プロジェクト]** 、プロジェクト ノード、 **[パッケージ]** の順に展開します。  
  
2.  SSIS パッケージを右クリックし、 **[レポート]** 、 **[標準レポート]** の順にポイントし、 **[すべての実行]** をクリックします。  
  
3.  SSIS パッケージの実行がレポートに表示されます。  
  
    > [!NOTE]  
    >  Windows Vista Service Pack 2 コンピューターでは、2 種類の SSIS パッケージの実行 (成功した実行と失敗した実行) が表示される場合があります。 失敗した実行は今回のリリースの既知の問題によって発生しているため、無視してください。  
  
## <a name="more-info"></a>詳細  
 データ フィード公開ウィザードでは、次の重要な手順を実行します。  
  
1.  リンク サーバーを作成し、OLE DB Provider for SSIS を使用するように構成します。  
  
2.  SQL ビューを指定したデータベースに作成します。これは、選択したパッケージのカタログ情報があるリンク サーバーに対してクエリを実行します。  
  
 このセクションでは、データ フィード公開ウィザードを使用せずに、リンク サーバーと SQL ビューを作成するための手順について説明します。 OPENQUERY 関数を OLE DB Provider for SSIS で使用することに関する追加情報も記載されています。  
  
### <a name="create-a-linked-server-using-the-ole-db-provider-for-ssis"></a>OLE DB Provider for SSIS を使用してリンクサーバーを作成する  
 SQL Server Management Studio で次のクエリを実行して、OLE DB Provider for SSIS (SSISOLEDB) を使用するリンク サーバーを作成します。  
  
```sql 
  
USE [master]  
GO  
  
EXEC sp_addlinkedserver  
@server = N'SSISFeedServer',  
@srvproduct = N'Microsoft',  
@provider = N'SSISOLEDB',  
@datasrc = N'.'  
GO  
  
```  
  
### <a name="create-a-view-using-linked-server-and-ssis-catalog-information"></a>リンク サーバーと SSIS カタログ情報を使用するビューを作成する  
 この手順では、前のセクションで作成したリンク サーバーに対してクエリを実行する SQL ビューを作成します。 クエリには、SSIS カタログのフォルダー名、プロジェクト名、およびパッケージ名が含まれています。  
  
 実行時、ビューが実行されると、ビューに定義されたリンク サーバー クエリが、クエリに指定された SSIS パッケージを開始し、パッケージの出力を表形式の結果セットとして受信します。  
  
1.  ビューを作成する前に、新しいクエリ ウィンドウで次のクエリを入力して実行します。 OPENQUERY は、SQL Server でサポートされている行セット関数です。 それは、指定されたパススルー クエリを、リンク サーバーに関連付けられた OLE DB Provider を使用するリンク サーバーで実行します。 OPENQUERY は、テーブル名と同じように、クエリの FROM 句で参照できます。 詳細については、 [MSDN ライブラリの OPENQUERY ドキュメント](../../t-sql/functions/openquery-transact-sql.md) を参照してください。  
  
    ```sql
    SELECT * FROM OPENQUERY(SSISFeedServer,N'Folder=Eldorado;Project=SSISPackagePublishing;Package=Package.dtsx')   
    GO  
    ```  
  
    > [!IMPORTANT]  
    >  必要に応じて、フォルダー名、プロジェクト名、パッケージ名を更新します。 OPENQUERY が失敗した場合は、 **[SQL Server Management Studio]** 、 **[サーバー オブジェクト]** 、 **[リンク サーバー]** 、 **[プロバイダー]** の順に展開し、 **SSISOLEDB** プロバイダーをクリックし、 **[InProcess 許可]** オプションが有効であることを確認します。  
  
2.  次のクエリを実行して、このチュートリアル用のデータベース **TestDB** にビューを作成します。  
  
    ```sql
  
    USE [TestDB]   
    GO   
  
    CREATE VIEW SSISPackageView AS   
    SELECT * FROM OPENQUERY(SSISFeedServer, 'Folder=Eldorado;Project=SSISPackagePublishing;Package=Package.dtsx')   
    GO  
  
    ```  
  
3.  次のクエリを実行して、ビューをテストします。  
  
    ```sql
    SELECT * FROM SSISPackageView  
    ```  
  
### <a name="openquery-function"></a>OPENQUERY 関数  
 OPENQUERY 関数の構文は次のとおりです。  
  
```sql 
SELECT * FROM OPENQUERY(<LinkedServer Name>, N'Folder=<Folder Name from SSIS Catalog>; Project=<SSIS Project Name>; Package=<SSIS Package Name>; Use32BitRuntime=[True | False];Parameters="<parameter_name_1>=<value1>; parameter_name_2=<value2>";Timeout=<Number of Seconds>;')  
```  
  
 Folder、Project、Package パラメーターは必須です。 Use32BitRuntime、Timeout、Parameters は省略可能です。  
  
 Use32BitRuntime の値は、0、1、true、または false を指定できます。 これは、SQL Server のプラットフォームが 64 ビットの場合に、パッケージを 32 ビット ランタイムで実行するかどうかを示します (1 または true で実行)。  
  
 Timeout は、SSIS パッケージから新しいデータが到着するまで OLE DB provider for SSIS が待機できる秒数を示します。 既定のタイムアウトは 60 秒です。 Timeout には 20 ～ 32000 の範囲の整数値を指定できます。  
  
 Parameters には、パッケージ パラメーターとプロジェクト パラメーターの両方の値が含まれます。 パラメーターのルールは、 [DTExec](https://msdn.microsoft.com/library/hh231187.aspx)のパラメーターと同じです。  
  
 クエリ句で使用できる特殊文字を次に示します。  
  
-   単一引用符 (') - これは標準的な OPENQUERY によってサポートされています。 クエリ句で単一引用符を使用する場合は、2 つの単一引用符 (") を使用します。  
  
-   二重引用符 (") - クエリのパラメーター部分は二重引用符で囲みます。 パラメーターの値そのものに二重引用符が含まれる場合は、エスケープ文字を使用します。 例: \"」を参照してください。  
  
-   左右の角かっこ ([ と ]) - これらの文字は、前後のスペースを示すために使用されます。 たとえば、"[ some spaces ]" は、前に 1 つ、後ろに 1 つのスペースがある文字列 " some spaces " を示します。 これらの文字そのものをクエリ句で使用する場合は、エスケープする必要があります。 たとえば、 \\[ や \\] のように指定します。  
  
-   スラッシュ (\\) - クエリで使用するすべての \ では、エスケープ文字を使用する必要があります。 たとえば、クエリ句の \\\ は \ として評価されます。  
  
 スラッシュ (\\) - クエリで使用するすべての \ では、エスケープ文字を使用する必要があります。 たとえば、クエリ句の \\\ は \ として評価されます。  
  
## <a name="see-also"></a>参照  
 [Data Streaming Destination](../../integration-services/data-flow/data-streaming-destination.md)   
 [Data Streaming Destination を構成する](../../integration-services/data-flow/configure-data-streaming-destination.md)  
  
  
