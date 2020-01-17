---
title: 初期構成 (PowerPivot for SharePoint) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: bc9b053b62a19cbe2c234f87010ae2a9652fb95c
ms.sourcegitcommit: 381595e990f2294dbf324ef31071e2dd2318b8dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74200433"
---
# <a name="initial-configuration-powerpivot-for-sharepoint"></a>初期構成 (PowerPivot for SharePoint)
  このトピックの手順を使用して、PowerPivot for SharePoint の最初のインストールを構成します。 最初のインストールを構成する最も簡単な方法は、PowerPivot 構成ツールを使用することです。 これによって、以下に説明したすべての構成手順が自動で行われます。  
  
 また、サーバーの構成方法を制御する場合には、サーバーの全体管理とこのトピックの情報を使用して各手順を個別に実行できます。  
  
 
  
## <a name="prerequisites"></a>前提条件  
 SharePoint サーバーは、SharePoint セットアップでサーバー ファーム インストール オプションを使用してインストールされたものである必要があります。 組み込みのデータベースを使用するスタンドアロン SharePoint サーバーはサポートされません。 詳細については、「 [SharePoint 2010 ファームで SQL SERVER BI 機能を使用するためのガイダンス](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)」を参照してください。  
  
> [!IMPORTANT]  
>  
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] データベース サーバーを使用する PowerPivot for SharePoint または SharePoint ファームを構成する前に、SharePoint 2010 SP1 をインストールする必要があります。 サービス パックをインストールしていない場合は、サーバーの構成を始める前にここでインストールしてください。  
  
 PowerPivot for SharePoint をインストールする必要があります。 少なくともファーム ソリューションを配置する必要があります。 PowerPivot 構成ツールまたは PowerShell スクリプトを使用してファーム ソリューションを配置します。 この手順はこのトピックで説明します。  
  
 コンピューターがドメインに参加する必要があります。 サービスに指定するアカウントは、ドメイン ユーザー アカウントである必要があります。 PowerPivot サービス アプリケーションには、少なくとも 1 つのドメイン アカウントが必要になります。 Excel Services などの他のサービスを構成している場合は、提供する各サービスに個別のアカウントを指定する必要があります。  
  
 PowerPivot for SharePoint をファームに追加するには、ファームの管理者である必要があります。 サーバーおよびアプリケーションをファームに追加するためのパスフレーズを把握しておく必要があります。  
  
##  <a name="deploywsp"></a>手順 1: PowerPivot ソリューションの配置  
 ファーム ソリューションおよび Web アプリケーション ソリューションという 2 つのソリューションをインストールして配置する必要があります。  
  
### <a name="install-and-deploy-the-farm-solution"></a>ファーム ソリューションのインストールおよび配置
  
 以前のリリースでは、SQL Server セットアップによってファーム ソリューションがインストールされ、配置されました。 このリリースでは、PowerPivot 構成ツールまたは PowerShell スクリプトを使用してファーム ソリューションを配置する必要があります。 サーバーの全体管理をファーム ソリューションの配置に使用することはできません。 これは、サーバーの全体管理で実行できない PowerPivot for SharePoint 構成の唯一の手順です。 ファーム ソリューションの配置後は、サーバーの全体管理とこのトピックの手順を使用して PowerPivot for SharePoint のインストールを構成できます。  
  
 この手順では、PowerShell を実行してファーム ソリューションをインストールおよび配置します。 詳細については、「 [Windows PowerShell を使用した PowerPivot の構成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)」を参照してください。  
  
1.  
  **[管理者として実行]** オプションを使用して SharePoint 2010 管理シェルを開きます。  
  
2.  最初のコマンドレットを実行します。  
  
    ```powershell
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\120\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     コマンドレットにより、ソリューション名、ソリューション ID、および Deployed=False が返されます。 次の手順では、ソリューションを配置します。  
  
3.  2 番目のコマンドレットを実行してソリューションを配置します。  
  
    ```powershell
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
### <a name="deploy-the-web-application-solution"></a>Web アプリケーションソリューションをデプロイする
  
1.  [スタート] ボタンをクリックし、[**すべてのプログラム**]、[ **Microsoft SharePoint 製品 2010**]、[ **Sharepoint 2010 サーバーの全体管理**] の順に選択します。  
  
2.  SharePoint 2010 サーバーの全体管理で、[システム設定] の **[ファーム ソリューションの管理]** をクリックします。  
  
     owerpivotfarm.wsp および powerpivotwebapp.wsp の 2 つの個別のソリューション パッケージが表示されます。 最初のソリューション (powerpivotfarm.wsp) は既に配置されています。 これを配置した後は、再度配置する必要はありません。 2 つ目のソリューション (powerpivotwebapp.wsp) は、サーバーの全体管理に配置されるソリューションですが、PowerPivot データ アクセスをサポートする各 SharePoint Web アプリケーションに手動で配置する必要があります。  
  
3.  [ **Powerpivotwebapp.wsp**] をクリックします。  
  
4.  [**ソリューションの配置] をクリックします。**  
  
5.  [**配置先**] で、PowerPivot 機能のサポートを追加する SharePoint web アプリケーションを選択します。  
  
6.  [**OK**] をクリックすると、  
  
7.  PowerPivot データ アクセスをサポートする他の SharePoint Web アプリケーションに対して、この手順を繰り返します。  
  
##  <a name="Geneva"></a>手順 2: サーバーでサービスを開始する  
 PowerPivot for SharePoint の配置は、ファームに、Excel Calculation Services、Secure Store Service、Claims to Windows Token Service が含まれている必要があります。  
  
 Excel Services および PowerPivot for SharePoint には、Windows トークン サービスに対するクレームが必要です。 これは、現在の SharePoint ユーザーの Windows ID を使用して外部データ ソースとの接続を確立するために使用されるサービスです。 このサービスは、Excel Services または PowerPivot for SharePoint が有効になっている各 SharePoint サーバーで実行する必要があります。 このサービスが開始されていない場合は、Excel Services から PowerPivot System サービスに認証済みの要求を転送できるようにするために、ここで開始する必要があります。  
  
1.  サーバーの全体管理で、[システム設定] の [**サーバーのサービスの管理**] をクリックします。  
  
2.  Windows トークン サービスに対するクレームを開始します。  
  
3.  Excel Calculation Services を開始します。  
  
4.  Secure Store Service を開始します。  
  
5.  SQL Server Analysis Services と SQL Server PowerPivot System サービスの両方が開始されていることを確認します。  
  
##  <a name="createapp"></a>手順 3: PowerPivot サービスアプリケーションを作成する  
 次に、PowerPivot サービス アプリケーションを作成します。  
  
1.  サーバーの全体管理で、[アプリケーション構成の管理] の **[サービス アプリケーションの管理]** をクリックします。  
  
2.  
  **[サービス アプリケーション]** リボンで、 **[新規作成]** をクリックします。  
  
3.  [ **PowerPivot サービスアプリケーションの SQL Server**] を選択します。 この項目が一覧に表示されない場合は、PowerPivot for SharePoint がインストールされていないか、ソリューションが配置されていません。  
  
4.  [**新しい PowerPivot サービスアプリケーションの作成**] ページで、アプリケーションの名前を入力します。 既定値は Remove-powerpivotserviceapplication\<number> です。 複数の PowerPivot サービス アプリケーションを作成する場合は、それぞれの用途を明確に示す名前を付けると他の管理者にわかりやすくなります。  
  
5.  [アプリケーション プール] で、新しいアプリケーション プールを作成して、そのアプリケーション プールのセキュリティ アカウントを選択します。 ドメイン ユーザー アカウントが必要となります。  
  
6.  [**データベースサーバー**] で、サービスアプリケーションデータベースを作成するデータベースサーバーを選択します。 既定値は、ファーム構成データベースをホストする SQL Server データベース エンジン インスタンスです。  
  
7.  [**データベース名**] の既定値は PowerPivotServiceApplication1_\<guid> です。 既定のデータベース名は、既定のサービス アプリケーション名に対応しています。 独自のサービス アプリケーション名を入力した場合は、サービス アプリケーションとデータベースを一緒に管理できるように、データベース名に対しても同様の命名規則を使用してください。  
  
8.  
  **[データベース認証]** の既定値は、"Windows 認証" です。 
  **[SQL 認証]** を選択する場合は、SharePoint 管理者ガイドを参照して、SharePoint 配置でその認証の種類を使用するためのベスト プラクティスを確認してください。  
  
9. [**この PowerPivot サービスアプリケーションのプロキシを既定のプロキシグループに追加する**] チェックボックスをオンにします。 のチェック ボックスをオンにします。これにより、このサービス アプリケーション接続が既定のサービス接続のグループに追加されます。 既定の接続グループに少なくとも 1 つの PowerPivot サービス アプリケーションを追加する必要があります。  
  
     既定の接続グループの一覧に既に PowerPivot サービス アプリケーションが表示されている場合は、そのグループにサービス アプリケーションをそれ以上追加しないでください。 既定の接続グループに同じ型のサービス アプリケーションを 2 つ追加する構成はサポートされていません。 接続グループで追加のサービスアプリケーションを使用する方法の詳細については、「[サーバーの全体管理で PowerPivot サービスアプリケーションを SharePoint Web アプリケーションに接続](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca)する」を参照してください。  
  
10. [ **OK] をクリックします。** 作成したサービスが、他のマネージド サービスと共にファームのサービス アプリケーションの一覧に表示されます。  
  
##  <a name="ExcelServ"></a>手順 4: Excel Services を有効にする  
 PowerPivot for SharePoint でファーム内の PowerPivot データ アクセスをサポートするには、Excel Services が必要です。 Excel Services が既に有効になっているかどうかを確認するには、サーバーの全体管理のサービス アプリケーションの一覧に Excel Services アプリケーションが表示されているかどうかを確認します。 Excel Services が一覧に表示されていない場合は、次の手順に従ってここで有効にしてください。  
  
1.  サーバーの全体管理で、[アプリケーション構成の管理] の **[サービス アプリケーションの管理]** をクリックします。  
  
2.  [サービスアプリケーション] リボンの [作成] で、[**新規**] をクリックします。  
  
3.  [ **Excel Services アプリケーション**] を選択します。  
  
4.  [新しい Excel Services アプリケーションの作成] で、名前を指定します ("Excel Services アプリケーション" など)。  
  
5.  [アプリケーション プール] で、[新しいアプリケーション プールの作成] をクリックして、わかりやすい名前を指定します ("Excel Services アプリケーション プール" など)。  
  
6.  [構成可能] で、このアプリケーション プール ID の Windows ドメイン ユーザー アカウントを選択します。  
  
7.  チェック ボックスをオンのままにして、このサービス アプリケーション プロキシを既定のサービス接続リストに追加します。  
  
8.  [**OK**] をクリックすると、  
  
9. 作成した Excel Services アプリケーションをクリックします。  
  
10. [**信頼できるファイルの場所**] をクリックし、このページで信頼できる場所を選択します。 (通常、アドレス列には**http://** と表示されます)。Excel Services と PowerPivot サービスの両方にブックへのアクセス権があることを確認するには、SharePoint を Excel Services の信頼できる場所として含める必要があります。 PowerPivot System サービスは、SharePoint ファーム外に格納されたブックにはアクセスできません。  
  
11. [ブックのプロパティ] 領域で、[**ブックの最大サイズ**] を50に設定します。  
  
12. [外部データ] で、[**外部データ**を信頼できるデータ接続ライブラリに許可する]**および [埋め込み**] を設定します。 この設定は、ブックでの PowerPivot データ アクセスに必要です。  
  
13. PowerPivot ギャラリーで個々のワークシートのプレビューイメージを許可するには、[**データ更新時に警告**する] チェックボックスをオフにします。 警告とブックの設定で、ファイルを開くときに更新する動作が指定されていると、ブックのページではなく警告の単一のプレビュー イメージが表示されることがあります。  
  
14. [**OK**] をクリックすると、  
  
##  <a name="SSS"></a>手順 5: Secure Store Service の有効化とデータ更新の構成  
 PowerPivot for SharePoint で資格情報とデータ更新用の自動実行アカウントを格納するには、Secure Store Service が必要です。 Secure Store Service が既に有効になっているかどうかを確認するには、サービス アプリケーションの一覧に表示されているかどうかを確認します。  
  
> [!IMPORTANT]  
>  Secure Store Service が有効になっている場合でも、マスター キーが生成されていることを確認するようにしてください。 手順については、続く部分の「作業 2: マスター キーの生成」をご覧ください。  
  
 Secure Store Service が一覧に表示されていない場合は、次の手順に従ってここで有効にしてください。 Secure Store を有効にすると、ブックの作成者やドキュメントの所有者が、パブリッシュしたブックのデータ更新をスケジュールする際に、より多くのデータ ソース接続オプションを必要に応じて使用できるようになります。  
  
##### <a name="part-1-enable-secure-store-service"></a>作業 1: Secure Store Service の有効化  
  
1.  サーバーの全体管理で、[アプリケーション構成の管理] の **[サービス アプリケーションの管理]** をクリックします。  
  
2.  [サービスアプリケーション] リボンの [作成] で、[**新規**] をクリックします。  
  
3.  [ **Secure Store Service**] を選択します。  
  
4.  [ **Secure Store アプリケーションの作成**] ページで、アプリケーションの名前を入力します。  
  
5.  [**データベース**] で、このサービスアプリケーションのデータベースをホストする SQL Server インスタンスを指定します。 既定値は、ファーム構成データベースをホストする SQL Server データベース エンジン インスタンスです。  
  
6.  [**データベース名**] に、サービスアプリケーションデータベースの名前を入力します。 既定値は Secure_Store_Service_DB_\<guid> です。 既定の名前は、既定のサービス アプリケーション名に対応しています。 独自のサービス アプリケーション名を入力した場合は、サービス アプリケーションとデータベースを一緒に管理できるように、データベース名に対しても同様の命名規則を使用してください。  
  
7.  
  **[データベース認証]** の既定値は、"Windows 認証" です。 "SQL 認証" を選択する場合は、SharePoint 管理者ガイドを参照して、ファームでその認証の種類を使用する方法を確認してください。  
  
8.  [アプリケーションプール] で、[**新しいアプリケーションプールの作成**] を選択します。 他のサーバー管理者がアプリケーション プールの使用方法を理解できるように、わかりやすい名前を指定します。  
  
9. アプリケーション プールのセキュリティ アカウントを選択します。 ドメイン ユーザー アカウントを使用するマネージド アカウントを指定します。  
  
10. 残りの既定値をそのまま使用し、[OK] をクリックし**ます。** 作成したサービス アプリケーションが、他のマネージド サービスと共にファームのサービス アプリケーションの一覧に表示されます。  
  
##### <a name="part-2-generate-the-master-key"></a>作業 2: マスター キーの生成  
  
1.  一覧で、Secure Store Service アプリケーションをクリックします。  
  
2.  [サービスアプリケーション] リボンで、[**管理**] をクリックします。  
  
3.  [キー管理] で、[**新しいキーの生成**] をクリックします。  
  
4.  パス フレーズを入力し、そのパス フレーズを確認します。 パス フレーズは、Secure Store 共有サービス アプリケーションを追加するために使用されます。  
  
5.  [**OK**] をクリックすると、  
  
##### <a name="part-3-configure-the-unattended-powerpivot-data-refresh-account"></a>作業 3: 自動 PowerPivot データ更新アカウントの構成  
 データ更新時の外部データ アクセスのために、PowerPivot データ アクセスに対する自動データ更新アカウントの作成が必要になることがよくあります。 たとえば、Kerberos が有効になっていない場合、外部データ ソースに接続するには、PowerPivot サービスで使用できる自動アカウントを作成する必要があります。  
  
 データ更新で使用される自動 PowerPivot データ更新アカウントまたはその他の保存された資格情報を作成する方法については、「powerpivot[自動データ更新アカウントの構成 &#40;PowerPivot for SharePoint&#41;](../../analysis-services/configure-unattended-data-refresh-account-powerpivot-sharepoint.md)および[powerpivot データ更新用の保存された資格情報の構成 &#40;PowerPivot for SharePoint&#41;](../../../2014/analysis-services/configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)」を参照してください。  
  
##  <a name="Usage"></a>手順 6: 使用状況データ収集を有効にする  
 PowerPivot for SharePoint は、SharePoint の使用状況データ収集インフラストラクチャを使用して、PowerPivot の使用状況に関する情報をファーム全体で収集します。 使用状況データは常に SharePoint のインストールに含まれますが、使用する前に有効にする必要がある場合があります。 手順については、「 [&#40;PowerPivot for SharePoint の使用状況データ収集の構成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint)」を参照してください。  
  
##  <a name="Upload"></a>手順 7: SharePoint Web アプリケーションと Excel Services の最大アップロードサイズを増やす  
 PowerPivot ブックはサイズが大きくなる可能性があるため、最大ファイル サイズを増やしたい場合があります。 2 つのファイル サイズの設定として、Web アプリケーションには [アップロードの最大サイズ]、Excel Services には [ブックの最大サイズ] の設定を構成します。 最大ファイル サイズは、両方のアプリケーションで同じ値に設定してください。 手順については、「 [PowerPivot for SharePoint&#41;&#40;最大ファイルアップロードサイズを構成する](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint)」を参照してください。  
  
##  <a name="activatePP"></a>手順 8: サイトコレクションに対して PowerPivot 機能の統合をアクティブ化する  
 サイト コレクション レベルで機能をアクティブ化すると、サイトでアプリケーション ページやテンプレートを使用できるようになります。これには、定期データを更新するための構成ページや、PowerPivot ギャラリーとデータ フィード ライブラリのアプリケーション ページなどが含まれます。  
  
1.  SharePoint サイトで、 **[サイトの操作]** をクリックします。  
  
     既定では、SharePoint Web アプリケーションへのアクセスにはポート 80 が使用されます。 つまり、多くの場合、SharePoint サイトにアクセスするには\<、http://コンピューター名> を入力して、ルートサイトコレクションを開きます。  
  
2.  
  **[サイトの設定]** をクリックします。  
  
3.  [サイト コレクションの管理] で **[サイト コレクションの機能]** をクリックします。  
  
4.  [ **PowerPivot 統合サイトコレクション機能**] が表示されるまでページを下にスクロールします。  
  
5.  
  **[アクティブ化]** をクリックします。  
  
6.  各サイトを開き、[**サイトの操作**] をクリックして、追加のサイトコレクションに対してを繰り返します。  
  
 詳細については、「[サーバーの全体管理でサイトコレクションの PowerPivot 機能の統合をアクティブ化](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)する」を参照してください。  
  
##  <a name="bkmk_redist"></a>手順 9: SQL Server 2012 PowerPivot for SharePoint インスタンスに SQL Server 2008 R2 バージョンの OLE DB プロバイダーをインストールする  
 同じサーバーで古いバージョンと新しいバージョンの PowerPivot ブックを平行して実行するには、SQL Server 2008 R2 に付属の Analysis Services OLE DB プロバイダーを [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot for SharePoint サーバーにインストールする必要があります。  
  
 このプロバイダーをインストールすると、データ接続文字列の MSOLAP.4 を参照するブックが [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot サーバーで正常に機能するようになります。 以前のバージョンの PowerPivot for Excel で作成されたブックをアップグレードするには、SQL Server 2008 R2 OLE DB プロバイダーをインストールする方法があります。  
  
 [SQL Server 2008 R2 Feature Pack ページ](https://www.microsoft.com/download/details.aspx?id=16978)からプロバイダーをダウンロードできます。 Microsoft **® Analysis Services OLE DB Provider For microsoft® SQL Server® 2008 R2**を探し、 `SQLServer2008_ASOLEDB10.msi`インストールプログラムの x64 パッケージをダウンロードします。  
  
 検証手順を含め、プロバイダーのインストールの詳細については、「 [SharePoint サーバーに Analysis Services OLE DB Provider をインストール](../../../2014/sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md)する」を参照してください。  
  
##  <a name="verifyinstall"></a>手順 10: インストールの確認  
 ファームの PowerPivot クエリ処理は、ユーザーまたはアプリケーションが PowerPivot データを含む Excel ブックを開いたときに発生します。 PowerPivot 機能が使用可能になっているかどうかは、SharePoint サイトのページを調べれば確認できますが、 インストールを完全に確認するには、SharePoint にパブリッシュでき、ライブラリからアクセスできる PowerPivot ブックが必要になります。 テストの際には、既に PowerPivot データが含まれているサンプル ブックをパブリッシュし、それを使用して SharePoint 統合が正しく構成されているかどうかを確認できます。  
  
 PowerPivot の SharePoint サイトとの統合を確認するには、次の操作を行います。  
  
1.  ブラウザーで、作成した Web アプリケーションを開きます。 既定値を使用した場合は、URL\<アドレスに> コンピューター名を指定できます。  
  
2.  PowerPivot データ アクセス機能と PowerPivot データ処理機能がアプリケーションで使用可能になっていることを確認します。 そのためには、PowerPivot によって提供されるライブラリ テンプレートがあるかどうかを確認します。  
  
    1.  [サイトの操作] の [**その他のオプション**] をクリックします。  
  
    2.  ライブラリでは、[**データフィードライブラリ**] と [ **PowerPivot ギャラリー**] が表示されます。 これらのライブラリ テンプレートは PowerPivot 機能によって提供されるものであり、PowerPivot 機能が正しく統合されている場合に [ライブラリ] に表示されます。  
  
 サーバーで PowerPivot データ アクセスを確認するには、次の操作を行います。  
  
1.  PowerPivot ブックを PowerPivot ギャラリーまたは任意の SharePoint ライブラリにアップロードします。  
  
2.  ドキュメントをクリックしてライブラリから開きます。  
  
3.  スライサーをクリックするかデータをフィルター処理して PowerPivot クエリを開始します。 サーバーは PowerPivot データをバックグラウンドで読み込んで結果を返します。 次の手順で、サーバーに接続して、データの読み込みとキャッシュが行われたことを確認します。  
  
4.  [スタート] メニューの Microsoft SQL Server 2008 R2 プログラム グループから SQL Server Management Studio を起動します。 このツールがサーバーにインストールされていない場合は、最後の手順にスキップして、キャッシュされたファイルが存在することを確認できます。  
  
5.  [サーバーの種類] で **[Analysis Services]** を選択します。  
  
6.  [サーバー名] に、「 ** \<サーバー名>** を入力します。ここ** \<** で、サーバー名>は PowerPivot for SharePoint インストールされているコンピューターの名前です。  
  
7.  
  **[接続]** をクリックします。  
  
8.  オブジェクトエクスプローラーで、[**データベース**] をクリックして、読み込まれている PowerPivot データファイルの一覧を表示します。  
  
9. コンピューターのファイル システムのフォルダーで、ファイルがディスクにキャッシュされているかどうかを確認します。 キャッシュされたファイルが存在していれば、配置が機能していることの確認になります。 ファイル キャッシュを表示するには、\Program Files\Microsoft SQL Server\MSAS10_50.POWERPIVOT\OLAP\Backup フォルダーに移動します。  
  
##  <a name="nextsteps"></a>インストール後の手順  
 インストールの確認が完了したら、PowerPivot ギャラリーを作成するか個々の構成設定を調整してサービスの構成を終了します。 インストールしたサーバー コンポーネントを完全に利用するには、[!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] をダウンロードし、最初の PowerPivot ブックを作成してパブリッシュします。  
  
### <a name="install-data-providers-used-for-data-refresh"></a>データの更新に使用されるデータ プロバイダーのインストール  
 データの更新を有効にしている場合、サーバーでは、PowerPivot クライアント アプリケーションで元のデータをインポートするときに使用したのと同じデータ プロバイダーが、外部データ アクセス用に必要となります (たとえば、最初にデータが 32 ビット プロバイダーを使用してインポートされていた場合は、サーバー側のデータ更新で同じ外部データ ソースにアクセスするときに、32 ビット プロバイダーが必要です)。 詳細については、「 [SharePoint 2010 での PowerPivot データ更新](../../../2014/analysis-services/powerpivot-data-refresh-with-sharepoint-2010.md)」を参照してください。  
  
### <a name="install-adonet-data-services"></a>ADO.NET Data Services のインストール  
 SharePoint リストをデータ フィードとしてエクスポートする場合は、ADO.NET Data Services 3.5 SP1 をインストールする必要があります。 手順については、「 [SharePoint リストのデータフィードのエクスポートをサポートするための ADO.NET Data Services のインストール」を](../../../2014/sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md)参照してください。  
  
### <a name="create-a-powerpivot-gallery"></a>PowerPivot ギャラリーの作成  
 PowerPivot ギャラリーは、SharePoint サイトの PowerPivot ブックを表示するためのプレビュー オプションや表示オプションを備えたライブラリです。 プレビュー機能があるため、PowerPivot ブックをパブリッシュしたり表示したりする際には PowerPivot ギャラリーを使用することをお勧めします。 同じ SharePoint サーバーに Reporting Services も配置されている場合は、 PowerPivot ギャラリーからレポート ビルダーを起動して、パブリッシュされた PowerPivot ブックを新しいレポートのベースとして使用することもできます。 ライブラリの作成と使用の詳細については、「 [Powerpivot ギャラリーの作成とカスタマイズ](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery)」および「 [Powerpivot ギャラリーの使用](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/use-power-pivot-gallery)」を参照してください。  
  
### <a name="create-additional-trusted-sites-in-excel-services"></a>Excel Services に追加の信頼できるサイトの作成  
 Excel Services に信頼できるサイトを追加して、Excel ブックおよび PowerPivot のデータを提供するサイトの権限および構成設定を変更できます。 詳細については、「 [Create a trusted location for PowerPivot sites in Central Administration](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration)」を参照してください。  
  
### <a name="tune-configuration-settings"></a>構成設定の調整  
 PowerPivot サービス アプリケーションは、既定のプロパティと値を使用して作成されますが、 個々のサービス アプリケーションの構成設定を変更して、要求の割り当て方法を変更したり、サーバー タイムアウトを設定したり、クエリ応答レポート イベントのしきい値を変更したり、使用状況データを保持する期間を指定したりすることもできます。 サーバーの全体管理での構成、または SharePoint Web アプリケーションでの PowerPivot 機能の使用に関する詳細については、「[サーバーの全体管理での Powerpivot サーバーの管理と構成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)」を参照してください。  
  
### <a name="install-powerpivot-for-excel-and-build-a-powerpivot-workbook"></a>PowerPivot for Excel のインストールと PowerPivot ブックの作成  
 ファームにサーバー コンポーネントをインストールしたら、PowerPivot データが埋め込まれた最初の Excel 2010 ブックを作成して、Web アプリケーションの SharePoint ライブラリにパブリッシュすることができます。 PowerPivot データを含む Excel ブックを作成するには、まず Excel 2010 をインストールし、次に PowerPivot for Excel アドインをインストールする必要があります。このアドインは、PowerPivot データのインポートと高度な利用をサポートするように Excel を拡張します。  
  
### <a name="add-servers-or-applications"></a>サーバーまたはアプリケーションの追加  
 PowerPivot ソリューションを配置すると、web アプリケーション内のすべてのサイトコレクションについて、サイトコレクションレベルで機能の統合がアクティブ化されます。 後で新しい Web アプリケーションを作成した場合は、そのそれぞれに対して powerpivotwebapp ソリューションを配置する必要があります。 手順については、「 [SharePoint への PowerPivot ソリューションの配置](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint)」を参照してください。  
  
 PowerPivot サービス アプリケーションの構成方法によっては、PowerPivot System サービスが既定の接続グループに追加され、既定の接続を使用するすべての Web アプリケーションで使用できるようになります。 ただし、カスタム サービス アプリケーション接続リストを使用するように Web アプリケーションを構成した場合は、PowerPivot データ処理を有効にする各 SharePoint Web アプリケーションに PowerPivot サービス アプリケーションを追加する必要があります。 詳細については、「[サーバーの全体管理で PowerPivot サービスアプリケーションを SharePoint Web アプリケーションに接続する](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca)」を参照してください。  
  
 後でデータ ストレージや処理能力を追加する必要が生じた場合は、ファームに 2 つ目の PowerPivot for SharePoint サーバー インスタンスを追加することができます。 インストールの手順は、最初のサーバーを追加したときの手順とほとんど同じですが、インスタンス名とサービス アカウント情報の指定についての要件が異なります。 手順については、「[配置のチェックリスト: SharePoint 2010 ファームへの PowerPivot サーバーの追加によるスケールアウト](../../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2014 の各エディションがサポートする機能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [PowerPivot サービスアカウントの構成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts)   
 [サーバーの全体管理での PowerPivot サービスアプリケーションの作成と構成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca)   
 [SharePoint への PowerPivot ソリューションの配置](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint)   
 [サーバーの全体管理でサイトコレクションの PowerPivot 機能の統合をアクティブ化する](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca)   
 [PowerPivot for SharePoint 2010 のインストール](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
