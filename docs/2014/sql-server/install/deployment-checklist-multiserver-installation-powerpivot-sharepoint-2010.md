---
title: '展開チェックリスト: PowerPivot for SharePoint のマルチサーバーインストール 2010 |Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 4380040a-1368-4a47-8930-47c65a192e59
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ed0cd8bad3a99c7f1f59b5121aafb06ccdee63b2
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952240"
---
# <a name="deployment-checklist-multi-server-installation-of-powerpivot-for-sharepoint-2010"></a>配置のチェック リスト: PowerPivot for SharePoint 2010 のマルチサーバー インストール
  このチェックリストでは、最初から構築した3層の SharePoint 2010 ファームに SharePoint の [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] を追加する手順について説明します。 3 層ファームには、データベース層、アプリケーション層、および Web 層が含まれています。 このトポロジに [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] を追加するには SQL Server セットアップを実行してアプリケーション層に [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] をインストールする必要があります。 PowerPivot プログラムファイルは web 層に追加されますが、web アプリケーションソリューションを配置する場合は、インストール後のタスクとしてのみ追加されます。 配置手順は必要ですが、Web 層またはデータ層のいずれかで実行する必要のある個別のインストール手順はありません。 実行する必要があるインストール手順は、アプリケーションサーバーに [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] をインストールすることだけです。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2010|  
  
  
  
## <a name="prerequisites"></a>Prerequisites  
 SQL Server および SharePoint 2010 をインストールするには、ローカル管理者である必要があります。  
  
 SharePoint のインストール担当者は、ファームも構成する必要があります。 ファームを構成するには、データベース サーバーに対する SQL Server ログイン権限が必要です。 ログインは、`dbcreator`、`securityadmin`、および `public` のロールに割り当てる必要があります。  
  
 Enterprise Edition または Enterprise Evaluation Edition の SharePoint Server 2010 が必要です。  
  
 コンピューターがドメインに参加する必要があります。  
  
 データベース エンジン、ファーム内のサービス、および SharePoint 統合モードの Analysis Services を実行するために使用するアカウントを把握している必要があります。 これらのアカウントは後で変更できますが、インストール時に最初に指定します。  
  
 インストール時に指定するサービス アカウントは、ドメイン ユーザー アカウントである必要があります。  
  
 インストールを開始する前に、インターネット接続が有効であるかどうかをブラウザーの設定で確認してください。 必須コンポーネントのインストーラーにより、必要なソフトウェアをダウンロードするためにインターネットに接続されます。 必要なソフトウェアをすべて取得するために、次の変更を行ってください。  
  
-   サーバー マネージャーで、Internet Explorer セキュリティ強化の構成を一時的に無効にし、サーバーへのダウンロードを許可します。 必要なソフトウェアをダウンロードする目的でのみ、[IE ESC の構成] の [管理者グループ用] をオフにできます。  
  
-   また、Internet Explorer で、プロキシ サーバーをバイパスしてインターネット URL へのローカルホストのアクセスを許可するようにブラウザーを構成することが必要になる場合もあります。  
  
    1.  Internet Explorer で、[ツール] メニューの [インターネット オプション] をクリックします。  
  
    2.  [接続] タブで、[ローカル エリア ネットワーク (LAN) の設定] 領域にある [LAN の設定] をクリックします。  
  
    3.  [自動構成] 領域で、[設定を自動的に検出する] チェック ボックスをオフにします。  
  
    4.  [プロキシ サーバー] 領域で、[LAN にプロキシ サーバーを使用する] チェック ボックスをオンにします。  
  
    5.  プロキシ サーバーのアドレスを [アドレス] ボックスに入力します。  
  
    6.  プロキシ サーバーのポート番号を [ポート] ボックスに入力します。  
  
    7.  [ローカル アドレスにはプロキシ サーバーを使用しない] チェック ボックスをオンにします。  
  
    8.  [OK] をクリックして [ローカル エリア ネットワーク (LAN) の設定] ダイアログ ボックスを閉じます。  
  
    9. [OK] をクリックして [インターネット オプション] ダイアログ ボックスを閉じます。  
  
##  <a name="installdb"></a>データベースサーバーのインストール  
 このトピックでは、ファームトポロジが、「 [3 層ファームの複数サーバー](https://go.microsoft.com/fwlink/?LinkId=182771)」で説明されているものに基づいていることを前提としています。 操作可能なファームが既にある場合は、「 [PowerPivot for SharePoint のインストール](#installppapp)」に進んでください。  
  
 トポロジを初めて設定する場合は、SQL Server データベース エンジンのインストールから始めます。 以下の手順を実行すると、ファーム内の SharePoint サーバーがアクセスできるデータベース サーバーがインストールされます。  
  
1.  データベースサーバーに使用しているコンピューターで、SQL Server セットアップを実行して SQL Server データベースエンジンをインストールします ([インストールウィザード&#40;のセットアップ&#41;から SQL Server 2014 をインストール](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)してください)。  
  
     インストールする機能として、以下を選択します。  
  
    -   データベース エンジン サービス  
  
    -   クライアント ツール接続  
  
    -   管理ツール - 完全 (基本機能は自動的に含まれます)  
  
2.  データベース エンジンをインストールした後、リモート接続用の TCP/IP を有効にし、サービスを再起動します。  
  
    1.  SQL Server 構成マネージャーを起動します。  
  
    2.  [SQL Server ネットワークの構成] を開きます。  
  
    3.  **[MSSQLSERVER のプロトコル]** を選択します。  
  
    4.  **[Tcp/ip]** を右クリックし、 **[有効]** を選択します。  
  
    5.  **[SQL Server Services]** をクリックします。  
  
    6.  **[SQL Server (MSSQLSERVER)]** を右クリックし、 **[再起動]** をクリックします。  
  
3.  Windows ファイアウォールを経由したデータベース サーバーへの入力方向のアクセスを有効にします。 これにより、ファーム内の SharePoint サーバーが SharePoint データベースに接続できるようになります。 詳細については、「 [Analysis Services のアクセスを許可するための Windows ファイアウォールの構成](../../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」をご参照ください。  
  
    1.  Windows のコントロールパネルの 管理ツール で、**セキュリティが強化された Windows ファイアウォール** をクリックします。  
  
    2.  **[受信の規則]** をクリックします。  
  
    3.  **[新しいルール]** をクリックします。  
  
    4.  ルールの種類 で、**カスタム** をクリックします。  
  
    5.  **[次へ]** をクリックします。  
  
    6.  プログラム の サービス セクションで、**カスタマイズ** をクリックします。  
  
    7.  [**このサービスに適用する] を**クリックします。  
  
    8.  SQL Server を既定のインスタンスとしてインストールした場合は、 **[SQL Server (MSSQLSERVER)]** を選択し、 **[OK]** をクリックします。  
  
    9. **[次へ]** をクリックします。  
  
    10. プロトコルおよびポート で、既定の設定をそのまま使用し、**次へ** をクリックします。  
  
    11. スコープ で、既定の設定をそのまま使用し、**次へ** をクリックします。  
  
    12. アクション で、既定の設定をそのまま使用し、**次へ** をクリックします。  
  
    13. プロファイル で、**プライベート** および **パブリック** のチェックボックスをオフにし、**次へ** をクリックします。  
  
    14. [名前] に、受信規則のわかりやすい名前 (たとえば、 **SQL Server**) を入力します。  
  
    15. **[完了]** をクリックします。  
  
##  <a name="installsp"></a>3層の SharePoint 2010 ファームをインストールして構成する  
 SharePoint サーバーとして使用しているコンピューターで、SharePoint の必須コンポーネントのインストーラー プログラムを実行してから、SharePoint Server セットアップを実行します。  
  
 SharePoint 2010 ドキュメントに記載されている次の手順に従って、2 台の Web サーバーと 1 台のアプリケーション サーバーを含む SharePoint 2010 ファームをインストールし、構成します。  
  
 [3層ファーム用の複数サーバー (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=182771)  
  
 データベース サーバーを指定するように求められたら、以前インストールしたデータベース サーバーを指定します。  
  
 以後の手順では、3 層ファームのセットアップ手順を使用してファームが構成されていることが前提となります。 ファームには次のサービスと機能が含まれている必要があります。  
  
-   Excel Services、Search Service、および Secure Store Service  
  
-   Web アプリケーションおよびサイト コレクション  
  
-   使用状況および正常性のデータ収集  
  
-   診断ログ  
  
##  <a name="installppapp"></a>アプリケーションサーバーへの PowerPivot for SharePoint のインストール  
 SQL Server セットアップを実行して SharePoint ファームに PowerPivot for SharePoint を追加します。 ファームが複数の SharePoint サーバーで構成されている場合は、既にファームに参加しているアプリケーション サーバーで SQL Server セットアップを実行する必要があります。  
  
 アプリケーション サーバーには常に PowerPivot for SharePoint をインストールします。 PowerPivot for SharePoint サーバー コンポーネントは Web フロントエンド サーバーでも実行されますが、Web フロントエンドで実行されるコンポーネントは、PowerPivot for SharePoint の構成手順で、ファームにソリューションを配置するときにインストールされます。 セットアップの詳細については、「 [Install PowerPivot for SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)」を参照してください。  
  
 配置トポロジに 2 つの PowerPivot for SharePoint インスタンスが必要な場合は、各アプリケーション サーバーで SQL Server セットアップを実行します。 1 台のコンピューターには PowerPivot for SharePoint のインスタンスを 1 つだけインストールできます。 複数のインスタンスが必要な場合は、追加のサーバーを使用する必要があります。 複数の PowerPivot for SharePoint サーバーを同じファームに追加する方法の詳細については、「[配置チェックリスト: SharePoint 2010 ファームへの PowerPivot サーバーの追加によるスケールアウト](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)」を参照してください。  
  
##  <a name="installclientlib"></a>PowerPivot for SharePoint がインストールされていない SharePoint アプリケーションサーバーに Analysis Services クライアントライブラリをインストールする  
 同じコンピューターに PowerPivot for SharePoint がインストールされておらず、次のアプリケーションを実行している Web フロントエンドまたはアプリケーション サーバーを含むファーム トポロジには、PowerPivot データ アクセスおよび機能をサポートするための追加ソフトウェアが必要になります。  
  
-   Excel Services または PerformancePoint Services  
  
-   自身のサーバーでスタンドアロン アプリケーションとして実行される、サーバーの全体管理  
  
 Excel Services と PerformancePoint Services には、PowerPivot データ アクセスをサポートするための新しいバージョンの Analysis Services OLE DB プロバイダーが必要です。 最新の OLE DB プロバイダーがインストールされていないコンピューターでいずれかのアプリケーションを実行する場合、プロバイダーを手動でインストールする必要があります。 詳細については、「 [SharePoint サーバーに Analysis Services OLE DB Provider をインストールする](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)」を参照してください。  
  
 同様に、サーバーの全体管理だけがインストールされていて、PowerPivot for SharePoint がインストールされていないコンピューターは、ADOMD.NET クライアント ライブラリが必要になります。 PowerPivot 管理ダッシュボードはこのライブラリを使用して内部データにアクセスし、このデータを使ってダッシュボードを設定します。 詳細については、「 [Install ADOMD.NET on Web Front-End Servers Running Central Administration](../../../2014/sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md)」を参照してください。  
  
##  <a name="configsrvr"></a>サーバーを構成する  
 PowerPivot 構成ツールを使用して PowerPivot for SharePoint を構成します。 このツールは、ファームの既存の構成をスキャンし、PowerPivot for SharePoint に必要な SharePoint 機能をインストールまたはアクティブ化するためのオプションを提供します。 このステップで、Claims to Windows Token Service が開始されます。 さらに、その他の必要な SharePoint 機能がまだ有効になっていない場合は、構成ツールによってそれらが一覧に追加され、機能を有効にするためのアクションが組み込まれます。  
  
 詳細については、「 [PowerPivot for SharePoint 2010 &#40;PowerPivot 構成ツール&#41;の構成または修復](../../../2014/analysis-services/configure-repair-powerpivot-sharepoint-2010.md)」を参照してください。  
  
##  <a name="AAM"></a>Web フロントエンドサーバーの代替アクセスマッピングを構成する  
 PowerPivot のデータ アクセスまたはデータ更新に対する要求を各 Web フロントエンド サーバーによって処理するには、各サーバーの異なる URL を同じ Web アプリケーションにマップする必要があります。  
  
1.  サーバーの全体管理で、アプリケーション構成の管理 の **代替アクセスマッピングの構成** をクリックします。  
  
2.  [代替アクセス マッピング コレクション] で、Web アプリケーションを選択します。  
  
3.  **[内部 URL の追加]** をクリックします。  
  
4.  最初の Web フロントエンド サーバーの URL を指定します。  
  
5.  前の手順を繰り返し、2 番目の Web フロントエンド サーバーの URL を追加します。  
  
##  <a name="activatePP"></a>サイトコレクションの PowerPivot 機能の統合のアクティブ化  
 サイト コレクション レベルで機能をアクティブ化すると、サイトでアプリケーション ページやテンプレートを使用できるようになります。これには、定期データを更新するための構成ページや、PowerPivot ギャラリーとデータ フィード ライブラリのアプリケーション ページなどが含まれます。  
  
 PowerPivot 構成ツールでは、指定したサイト コレクションに対して機能の統合がアクティブ化されます。 ツールを複数回実行すると追加のサイト コレクションを選択できます。 または、サイト管理者が SharePoint 内から機能のアクティブ化を構成することもできます。 詳細については、「[サーバーの全体管理でサイトコレクションの PowerPivot 機能の統合をアクティブ化](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)する」を参照してください。  
  
##  <a name="verify"></a>統合とサーバーの可用性を確認する  
 ファームの PowerPivot クエリ処理は、ユーザーまたはアプリケーションが PowerPivot データを含む Excel ブックを開いたときに発生します。 PowerPivot 機能が使用可能になっているかどうかは、SharePoint サイトのページを調べれば確認できますが、 インストールを完全に確認するには、SharePoint にパブリッシュでき、ライブラリからアクセスできる PowerPivot ブックが必要になります。 テストの際には、既に PowerPivot データが含まれているサンプル ブックをパブリッシュし、それを使用して SharePoint 統合が正しく構成されているかどうかを確認できます。  
  
 PowerPivot の SharePoint サイトとの統合を確認するには、次の操作を行います。  
  
1.  ブラウザーで、作成した Web アプリケーションを開きます。 既定値を使用した場合は、URL アドレスで > コンピューター名\<http://を指定できます。  
  
2.  PowerPivot データ アクセス機能と PowerPivot データ処理機能がアプリケーションで使用可能になっていることを確認します。 そのためには、PowerPivot によって提供されるライブラリ テンプレートがあるかどうかを確認します。  
  
    1.  サイトの操作をクリックします**オプション**。  
  
    2.  ライブラリでは、 **[データフィードライブラリ]** と **[PowerPivot ギャラリー]** が表示されます。 これらのライブラリ テンプレートは PowerPivot 機能によって提供されるものであり、PowerPivot 機能が正しく統合されている場合に [ライブラリ] に表示されます。  
  
 サーバーで PowerPivot データ アクセスを確認するには、次の操作を行います。  
  
1.  Reporting Services のチュートリアルにある Picnic のデータ サンプルを[ダウンロード](https://go.microsoft.com/fwlink/?LinkID=219108) します。 このダウンロードに含まれるサンプル ブックを使用して、PowerPivot データのアクセスを確認します。 ファイルを抽出します。  
  
2.  PowerPivot ブックを PowerPivot ギャラリーまたは任意の SharePoint ライブラリにアップロードします。  
  
3.  ドキュメントをクリックしてライブラリから開きます。  
  
4.  スライサーをクリックするかデータをフィルター処理して PowerPivot クエリを開始します。 サーバーは PowerPivot データをバックグラウンドで読み込んで結果を返します。 次の手順で、サーバーに接続して、データの読み込みとキャッシュが行われたことを確認します。  
  
5.  [スタート] メニューの Microsoft SQL Server 2008 R2 プログラム グループから SQL Server Management Studio を起動します。 このツールがサーバーにインストールされていない場合は、最後の手順にスキップして、キャッシュされたファイルが存在することを確認できます。  
  
6.  [サーバーの種類] で **[Analysis Services]** を選択します。  
  
7.  [サーバー名] に、 **\<サーバー名 >** を入力します。ここで **\<サーバー名 >** は、PowerPivot for SharePoint がインストールされているコンピューターの名前です。  
  
8.  **[接続]** をクリックします。  
  
9. オブジェクトエクスプローラーで、 **[データベース]** をクリックして、読み込まれている PowerPivot データファイルの一覧を表示します。  
  
10. コンピューターのファイル システムのフォルダーで、ファイルがディスクにキャッシュされているかどうかを確認します。 キャッシュされたファイルが存在していれば、配置が機能していることの確認になります。 ファイル キャッシュを表示するには、\Program Files\Microsoft SQL Server\MSAS10_50.POWERPIVOT\OLAP\Backup フォルダーに移動します。  
  
##  <a name="nextsteps"></a>インストール後の手順  
 インストールの確認が完了したら、PowerPivot ギャラリーを作成するか個々の構成設定を調整してサービスの構成を終了します。 インストールしたサーバー コンポーネントを完全に利用するには、[!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] をダウンロードし、最初の PowerPivot ブックを作成してパブリッシュします。  
  
####  <a name="bkmk_disk"></a>ディスク領域の使用率の上限を設定する  
 ディスクにキャッシュされる PowerPivot データ ファイルに使用されるディスク容量の最大制限を設定できます。 既定では、使用可能なすべてのディスク領域が使用されます。 ディスク領域の使用量を制限する方法については、「 [ &#40;PowerPivot for SharePoint&#41;のディスク領域使用量の構成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-disk-space-usage-power-pivot-for-sharepoint)」を参照してください。  
  
####  <a name="Upload"></a>SharePoint Web アプリケーションのファイルの最大アップロードサイズを増やす  
 PowerPivot ブックはサイズが大きくなる可能性があるため、ファイルの最大アップロード サイズを増やしたい場合があります。 2 つのファイル サイズの設定として、Web アプリケーションには [アップロードの最大サイズ]、Excel Services には [ブックの最大サイズ] の設定を構成します。 最大ファイル サイズは、両方のアプリケーションで同じ値に設定してください。 手順については、「 [PowerPivot for SharePoint&#41;最大&#40;ファイルアップロードサイズの構成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint)」を参照してください。  
  
#### <a name="grant-sharepoint-permissions-to-workbook-users"></a>ブックのユーザーへの SharePoint 権限の付与  
 ユーザーがブックをパブリッシュまたは表示するには、SharePoint 権限が必要です。 パブリッシュされたブックを表示する必要があるユーザーには**表示**権限を付与し、ブックをパブリッシュまたは管理するユーザーには**投稿**権限を与えるようにしてください。 権限を付与するには、サイト コレクションの管理者である必要があります。  
  
1.  サイトで、 **[サイトの操作]** をクリックします。  
  
2.  **[サイトの権限]** をクリックします。  
  
3.  [サイトコレクション**メンバー** ] グループのチェックボックスをオンにします。  
  
4.  リボンで、 **[アクセス許可の付与]** をクリックします。  
  
5.  ドキュメントを追加または削除する権限を必要とする Windows ドメインのユーザー アカウントまたはグループ アカウントを入力します。  
  
6.  クリックして **OK**です。  
  
7.  サイトコレクションの**閲覧**者グループのチェックボックスをオンにします。  
  
8.  リボンで、 **[アクセス許可の付与]** をクリックします。  
  
9. ドキュメントを表示する権限を必要とする Windows ドメインのユーザー アカウントまたはグループ アカウントを入力します。 上で説明した手順と同様に、アプリケーションで従来の認証が構成されている場合は、電子メール アドレスまたは配布グループを使用しないでください。  
  
10. クリックして **OK**です。  
  
#### <a name="install-adonet-data-services-35-sp1"></a>ADO.NET Data Services 3.5 SP1 のインストール  
 ADO.NET Data Services は、SharePoint リストのデータ フィードのエクスポートに必要です。 SharePoint 2010 では、このコンポーネントは PrerequisiteInstaller プログラムに含まれていないため、手動でインストールする必要があります。 ADO.NET Data Services のインストール方法の詳細については、「 [SharePoint リストのデータフィードのエクスポートをサポートするための ADO.NET Data Services のインストール](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md)」を参照してください。  
  
#### <a name="install-data-providers-used-in-data-refresh-and-check-user-permissions"></a>データ更新で使用するデータ プロバイダーのインストールとユーザー権限の確認  
 サーバー側のデータ更新により、ユーザーは更新されたデータをブックに自動モードで再インポートできます。 データ更新を正常に行うためには、最初にデータをインポートするために使用したものと同じデータ プロバイダーがサーバーに必要になります。 さらに、通常は、データ更新を実行するユーザー アカウントに外部データ ソースに対する読み取り権限が必要です。 データ更新を正常に実行できるように、データ更新の有効化と構成の要件をご確認ください。 詳細については、「 [SharePoint 2010 での PowerPivot データ更新](../../../2014/analysis-services/powerpivot-data-refresh-with-sharepoint-2010.md)」を参照してください。  
  
#### <a name="create-a-powerpivot-gallery"></a>PowerPivot ギャラリーの作成  
 PowerPivot ギャラリーは、SharePoint サイトの PowerPivot ブックを表示するためのプレビュー オプションや表示オプションを備えたライブラリです。 プレビュー機能があるため、PowerPivot ブックをパブリッシュしたり表示したりする際には PowerPivot ギャラリーを使用することをお勧めします。 同じ SharePoint サーバーに Reporting Services も配置されている場合は、 PowerPivot ギャラリーからレポート ビルダーを起動して、パブリッシュされた PowerPivot ブックを新しいレポートのベースとして使用することもできます。 ライブラリの作成と使用の詳細については、「 [Powerpivot ギャラリーの作成とカスタマイズ](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery)」および「 [Powerpivot ギャラリーの使用](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/use-power-pivot-gallery)」を参照してください。  
  
#### <a name="tune-configuration-settings"></a>構成設定の調整  
 PowerPivot サービス アプリケーションは、既定のプロパティと値を使用して作成されますが、 個々のサービス アプリケーションの構成設定を変更して、要求の割り当て方法を変更したり、サーバー タイムアウトを設定したり、クエリ応答レポート イベントのしきい値を変更したり、使用状況データを保持する期間を指定したりすることもできます。 サーバーの全体管理での構成、または SharePoint Web アプリケーションでの PowerPivot 機能の使用に関する詳細については、「[サーバーの全体管理での Powerpivot サーバーの管理と構成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2012  の各エディションがサポートする機能](https://go.microsoft.com/fwlink/?linkid=232473)  
 [PowerPivot for SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)  のインストール  
 [配置のチェックリスト: SharePoint 2010 ファームへの PowerPivot サーバーの追加によるスケールアウト](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)  
  
  
