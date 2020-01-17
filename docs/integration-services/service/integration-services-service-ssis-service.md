---
title: Integration Services サービス (SSIS サービス) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssiseditserverregistration.connectionproperties.f1
- sql13.swb.connecttodts.connectionproperties.f1
- sql13.swb.connection.login.dtsserver.f1
- sql13.swb.connecttodts.login.f1
- sql13.swb.connecttodtsserver.login.f1
helpviewer_keywords:
- Integration Services service, about Integration Services service
- SQL Server Integration Services service
- service [Integration Services],about Integration Services service
- service [Integration Services]
- SQL Server Integration Services, service
ms.assetid: 2c785b3b-4a0c-4df7-b5cd-23756dc87842
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 15da54550dd314a50d4c3235a77394292d23f1d9
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296946"
---
# <a name="integration-services-service-ssis-service"></a>Integration Services サービス (SSIS サービス)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  このセクションのトピックでは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを管理するための Windows サービスである [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスについて説明します。 Integration Service パッケージの作成、保存、および実行には、このサービスは不要です。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以前のリリースの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] との互換性を維持するために、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]サービスをサポートしています。  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] は、プロジェクト配置モデルを使用して **サーバーに配置したプロジェクトの**  SSISDB [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データベースにオブジェクト、設定、業務データを格納します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データベース エンジンのインスタンスである [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サーバーは、データベースをホストします。 データベースの詳細については、「 [SSIS カタログ](../../integration-services/catalog/ssis-catalog.md)」を参照してください。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーへのプロジェクトの配置の詳細については、「[Integration Services (SSIS) のプロジェクトとパッケージの配置](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。  
  
## <a name="management-capabilities"></a>管理機能  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを管理するための Windows サービスです。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でのみ使用できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを実行すると、以下の管理機能が使用できます。  
  
-   リモートまたはローカルに格納されたパッケージの開始  
  
-   リモートまたはローカルで実行中のパッケージの停止  
  
-   リモートまたはローカルで実行中のパッケージの監視  
  
-   パッケージのインポートおよびエクスポート  
  
-   パッケージ ストレージの管理  
  
-   ストレージ フォルダーのカスタマイズ  
  
-   サービス停止時の実行中のパッケージの停止  
  
-   Windows のイベント ログの表示  
  
-   複数の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーへの接続  
  
## <a name="startup-type"></a>スタートアップの種類
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]コンポーネントのインストール時にインストールされます。 既定では、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが起動され、スタートアップの種類が自動に設定されます。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストアに格納されているパッケージを監視するには、サービスが実行されている必要があります。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストアは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内の msdb データベース、またはファイル システム内の指定されたフォルダーのいずれかです。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの設計と実行だけを行う場合は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは必要ありません。 ただし、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してパッケージを一覧表示し、監視する場合はサービスが必要です。  

## <a name="manage-the-service"></a>サービスの管理
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]コンポーネントのインストール時に、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスもインストールされます。 既定では、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが起動され、スタートアップの種類が自動に設定されます。 ただし、サービスを使用して [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の格納されたパッケージおよび実行中のパッケージを管理するには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールする必要があります。  
  
> [!NOTE]
> レガシー Integration Services サービスに直接接続するには、Integration Services サービスが実行されている SQL Server のバージョンと合わせたバージョンの SQL Server Management Studio (SSMS) を使用する必要があります。 たとえば、SQL Server 2016 のインスタンスで実行されているレガシ Integration Services サービスに接続するには、SQL Server 2016 用にリリースされたバージョンの SSMS を使用する必要があります。 [SQL Server Management Studio (SSMS) をダウンロードします](../../ssms/download-sql-server-management-studio-ssms.md)。
>
>   SSMS の **[サーバーへの接続]** ダイアログ ボックスで、旧バージョンの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが実行されているサーバーの名前を入力することはできません。 ただし、リモート サーバーに格納されるパッケージを管理するために、そのリモート サーバー上の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスのインスタンスに接続する必要はありません。 代わりに、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成ファイルを編集し、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でリモート サーバーに格納されているパッケージが表示されるようにします。   
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスのインスタンスは 1 台のコンピューターに 1 つだけインストールできます。 このサービスは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の特定のインスタンスに固有ではありません。 サービスに接続するには、サービスが実行されているコンピューターの名前を使用します。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、次の Microsoft 管理コンソール (MMC) スナップインのいずれかを使用して管理できます: SQL Server 構成マネージャーまたはサービス。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパッケージを管理するには、事前にサービスを起動しておく必要があります。  
  
 既定では、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、[!INCLUDE[ssDE](../../includes/ssde-md.md)] と同時にインストールされる[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]のインスタンスの msdb データベース内にあるパッケージを管理するように構成されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスが同時にインストールされない場合、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、[!INCLUDE[ssDE](../../includes/ssde-md.md)]のローカルの既定インスタンスの msdb データベース内にあるパッケージを管理するように構成されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の名前付きインスタンスまたはリモート インスタンス、あるいは [!INCLUDE[ssDE](../../includes/ssde-md.md)]の複数のインスタンスに格納されているパッケージを管理するには、サービスの構成ファイルを変更する必要があります。
  
 既定では、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが停止すると、パッケージの実行も停止するように設定されています。 ただし、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスはパッケージが停止するまで待機しないため、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの停止後に実行を続けるパッケージもあります。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが停止した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザード、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナー、パッケージ実行ユーティリティ、および **dtexec** コマンド プロンプト ユーティリティ (dtexec.exe) を使用してパッケージを実行し続けることができます。 ただし、実行中のパッケージを監視することはできません。  
  
 既定では、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは NETWORK SERVICE アカウントのコンテキスト内で実行されます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは Windows のイベント ログに書き込みを行います。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でサービス イベントを表示できます。 Windows イベント ビューアーを使用してサービス イベントを表示することもできます。  
  
## <a name="set-the-properties-of-the-service"></a>サービスのプロパティの設定
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパッケージを管理および監視します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]を初めてインストールするときに、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが起動され、スタートアップの種類が自動に設定されます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスをインストールしたら、SQL Server 構成マネージャーまたはサービス MMC スナップインを使用してサービスのプロパティを設定できます。  
  
 パッケージを格納および管理する場所など、サービスのその他の重要な機能を構成するには、サービスの構成ファイルを変更する必要があります。
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-sql-server-configuration-manager"></a>SQL Server 構成マネージャーを使用して Integration Services サービスのプロパティを設定するには  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[Microsoft SQL Server]** 、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
2.  **[SQL Server 構成マネージャー]** スナップインで、サービスの一覧から **[SQL Server Integration Services]** を探します。次に、 **[SQL Server Integration Services]** を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[SQL Server Integration Services のプロパティ]** ダイアログ ボックスでは、次の操作を行うことができます。  
  
    -   **[ログオン]** タブをクリックして、アカウント名などのログオン情報を表示します。  
  
    -   **[サービス]** タブをクリックして、ホスト コンピューター名などのサービスに関する情報を表示し、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの開始モードを指定します。  
  
        > [!NOTE]  
        >  **[詳細設定]** タブに、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスに関する情報は表示されません。  
  
4.  **[OK]** をクリックします。  
  
5.  **[ファイル]** メニューの **[終了]** をクリックして **[SQL Server 構成マネージャー]** スナップインを終了します。  
  
### <a name="to-set-properties-of-the-integration-services-service-by-using-services"></a>[サービス] を使用して Integration Services サービスのプロパティを設定するには  
  
1.  **[コントロール パネル]** で、クラシック表示を使用している場合は **[管理ツール]** 、カテゴリの表示を使用している場合は **[パフォーマンスとメンテナンス]** をクリックしてから **[管理ツール]** をクリックします。  
  
2.  **[サービス]** をクリックします。  
  
3.  **[サービス]** スナップインで、サービスの一覧から **[SQL Server Integration Services]** を探します。 **[SQL Server Integration Services]** を右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[SQL Server Integration Services のプロパティ]** ダイアログ ボックスでは、次の操作を行うことができます。  
  
    -   **[全般]** タブをクリックします。サービスを有効にするには、[スタートアップの種類] で [手動] または [自動] を選択します。 サービスを無効にするには、 **[スタートアップの種類]** ボックスで [無効] を選択します。 [無効] を選択しても、実行中のサービスは停止されません。  
  
         サービスが既に有効になっている場合は、 **[停止]** をクリックしてサービスを停止したり、 **[開始]** をクリックしてサービスを開始したりできます。  
  
    -   **[ログオン]** タブをクリックして、ログオン情報を表示または編集します。  
  
    -   **[復旧]** タブをクリックして、サービスが失敗した場合のコンピューターの既定の応答を表示します。 これらのオプションは、環境に合わせて変更できます。  
  
    -   **[依存関係]** タブをクリックして、依存サービスの一覧を表示します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、依存関係を持ちません。  
  
5.  **[OK]** をクリックします。  
  
6.  [スタートアップの種類] で [手動] または [自動] を選択している場合は、必要に応じて、 **[SQL Server Integration Services]** を右クリックし、 **[開始]、[停止]、または [再起動]** をクリックできます。  
  
7.  **[ファイル]** メニューの **[終了]** をクリックして **[サービス]** スナップインを終了します。  

## <a name="grant-permissions-to-the-service"></a>サービスへのアクセス許可の付与
  以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールすると、既定で Users グループの全ユーザーが [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスにアクセスできました。 現在のリリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をインストールした場合、ユーザーは [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスにアクセスできません。 このサービスは既定で保護されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール後に、管理者はサービスに対するアクセスを許可する必要があります。  
  
### <a name="to-grant-access-to-the-integration-services-service"></a>Integration Services サービスへのアクセスを許可するには  
  
1.  Dcomcnfg.exe を実行します。 Dcomcnfg.exe には、レジストリ内の特定の設定を変更するためのユーザー インターフェイスが用意されています。  
  
2.  **[コンポーネント サービス]** ダイアログで、[コンポーネント サービス] > [コンピューター] > [マイ コンピューター] > [DCOM の構成] ノードの順に展開します。  
  
3.  **[Microsoft SQL Server Integration Services 13.0]** を右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[セキュリティ]** タブで、 **[起動とアクティブ化のアクセス許可]** 領域の **[編集]** をクリックします。  
  
5.  ユーザーを追加し、適切なアクセス許可を割り当てて、[OK] をクリックします。  
  
6.  アクセス許可で手順 4. と 5. を繰り返します。  
  
7.  SQL Server Management Studio を再起動します。  
  
8.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを再開します。  

### <a name="event-logged-when-permissions-are-missing"></a>アクセス許可が不足しているときに記録されるイベント

SQL Server エージェントのサービス アカウントに Integration Services DCOM **[起動とアクティブ化のアクセス許可]** が含まれていない場合は、SQL Server エージェントによって SSIS パッケージ ジョブが実行されたときに、次のイベントがシステム イベント ログに追加されます。

```
Log Name: System
Source: **Microsoft-Windows-DistributedCOM**
Date: 1/9/2019 5:42:13 PM
Event ID: **10016**
Task Category: None
Level: Error
Keywords: Classic
User: NT SERVICE\SQLSERVERAGENT
Computer: testmachine
Description:
The application-specific permission settings do not grant Local Activation permission for the COM Server application with CLSID
{xxxxxxxxxxxxxxxxxxxxxxxxxxxxx}
and APPID
{xxxxxxxxxxxxxxxxxxxxxxxxxxxxx}
to the user NT SERVICE\SQLSERVERAGENT SID (S-1-5-80-344959196-2060754871-2302487193-2804545603-1466107430) from address LocalHost (Using LRPC) running in the application container Unavailable SID (Unavailable). This security permission can be modified using the Component Services administrative tool.
```

## <a name="configure-the-service"></a>サービスの構成
 
[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]をインストールすると、セットアップ プロセスによって [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成ファイルが作成およびインストールされます。 この構成ファイルには、次の設定が含まれます。  
  
-   サービスが停止すると、パッケージに中止コマンドが送信されます。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のオブジェクト エクスプローラー内の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] に表示するルート フォルダーは、[MSDB] および [ファイル システム] フォルダーです。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが管理するファイル システム内のパッケージは、%ProgramFiles%\Microsoft SQL Server\130\DTS\Packages にあります。  
  
 この構成ファイルは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが管理するパッケージを含む msdb データベースも指定します。 既定では、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] と同時にインストールされる [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]のインスタンスの msdb データベース内にあるパッケージを管理するように構成されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスが同時にインストールされない場合、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のローカルの既定インスタンスの msdb データベース内にあるパッケージを管理するように構成されます。  
  
### <a name="default-configuration-file-example"></a>既定の構成ファイルの例  
 次の設定を含む既定の構成ファイルを以下の例に示します。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが停止すると、パッケージは実行を停止します。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 内のパッケージ ストレージのルート フォルダーは、[MSDB] および [ファイル システム] フォルダーです。  
  
-   このサービスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のローカルの既定インスタンスの msdb データベースに格納されるパッケージを管理します。  
  
-   このサービスは、ファイル システムの [パッケージ] フォルダーに格納されるパッケージを管理します。  
  
 **既定の構成ファイルの例**  
  
```xml
\<?xml version="1.0" encoding="utf-8"?>  
\<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    \<Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>.</ServerName>  
    </Folder>  
    \<Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
### <a name="modify-the-configuration-file"></a>構成ファイルの変更  
 構成ファイルを変更することによって、サービスが停止した場合にパッケージを継続して実行できるようにしたり、オブジェクト エクスプローラー内に別のルート フォルダーを表示したり、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが管理するファイル システム内に別のフォルダーまたは追加のフォルダーを指定することができます。 たとえば、 **SqlServerFolder**型の別のルート フォルダーを作成して、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の追加インスタンスの msdb データベースでパッケージを管理できます。  
  
> [!NOTE]  
>  一部の文字は、フォルダー名には無効です。 フォルダー名として有効な文字は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] クラスの **System.IO.Path** および **GetInvalidFilenameChars** フィールドによって決まります。 **GetInvalidFilenameChars** フィールドでは、 **Path** クラスのメンバーに渡されるパス文字列引数に指定できない、プラットフォーム固有の文字配列が指定されます。 無効な文字のセットは、ファイル システムによって異なる場合があります。 通常、無効な文字は、引用符 (")、小なり (<) 文字、およびパイプ (|) 文字です。  
  
 ただし、[!INCLUDE[ssDE](../../includes/ssde-md.md)]の名前付きインスタンスまたはリモート インスタンスに格納されているパッケージを管理するには、構成ファイルを変更する必要があります。 構成ファイルを更新しないと、 **で** オブジェクト エクスプローラー [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して名前付きインスタンスまたはリモート インスタンス上の msdb データベースに格納されているパッケージを表示することはできません。 **オブジェクト エクスプローラー** を使用してこのようなパッケージを表示しようとすると、次のエラー メッセージが返されます。  
  
 `Failed to retrieve data for this request. (Microsoft.SqlServer.SmoEnum)`  
  
 `The SQL Server specified in Integration Services service configuration is not present or is not available. This might occur when there is no default instance of SQL Server on the computer. For more information, see the topic "Configuring the Integration Services Service" in SQL Server 2008 Books Online.`  
  
 `Login Timeout Expired`  
  
 `An error has occurred while establishing a connection to the server. When connecting to SQL Server 2008, this failure may be caused by the fact that under the default settings SQL Server does not allow remote connections.`  
  
 `Named Pipes Provider: Could not open a connection to SQL Server [2]. (MsDtsSvr).`  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成ファイルを変更するには、テキスト エディターを使用します。  
  
> [!IMPORTANT]  
>  サービス構成ファイルを変更したら、更新されたサービス構成を使用するためにサービスを再起動する必要があります。  
  
### <a name="modified-configuration-file-example"></a>変更された構成ファイルの例  
 変更された [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]の構成ファイルの例を次に示します。 このファイルは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] という名前のサーバー上で、 `InstanceName` と呼ばれる `ServerName`の名前付きインスタンス用のファイルです。  
  
 **SQL Server の名前付きインスタンス用構成ファイルの変更例**  
  
```xml
\<?xml version="1.0" encoding="utf-8"?>  
\<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    \<Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>ServerName\InstanceName</ServerName>  
    </Folder>  
    \<Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
### <a name="modify-the-configuration-file-location"></a>構成ファイルの場所の変更  
 レジストリ キー **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS\ServiceConfigFile** には、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが使用する構成ファイルの場所と名前を指定します。 レジストリ キーの既定値は、**C:\Program Files\Microsoft SQL Server\130\DTS\Binn\MsDtsSrvr.ini.xml** です。 レジストリ キーの値を更新すると、構成ファイルに別の名前と場所を使用することができます。 パスのバージョン番号 (SQL Server [!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)] の場合は 120、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] の場合は 130 など) は、SQL Server のバージョンによって異なるので注意してください。
  
> [!CAUTION]  
>  レジストリの編集を誤ると、深刻な問題が発生し、オペレーティング システムの再インストールが必要になる場合があります。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] レジストリの誤った編集により発生した問題に関しては、一切責任を負わないものとします。 レジストリを編集する前に、重要なデータをすべてバックアップしてください。 レジストリのバックアップ、復元、および編集の方法については、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] サポート技術情報の記事「 [Microsoft Windows レジストリの説明](https://support.microsoft.com/kb/256986)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、サービスの開始時に構成ファイルを読み込みます。 レジストリ エントリを変更した場合、サービスを再起動する必要があります。  

## <a name="connect-to-the-local-service"></a>ローカル サービスへの接続
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスに接続する前に、管理者からこのサービスに対するアクセス権を付与してもらう必要があります。 
  
### <a name="to-connect-to-the-integration-services-service"></a>Integration Services サービスに接続するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を開きます。  
  
2.  **[表示]** メニューの **[オブジェクト エクスプローラー]** をクリックします。  
  
3.  [オブジェクト エクスプローラー] のツール バーの **[接続]** をクリックし、 **[Integration Services]** をクリックします。  
  
4.  **[サーバーへの接続]** ダイアログ ボックスで、サーバー名を指定します。 ピリオド (.)、(local)、または **localhost** を使用すると、ローカル サーバーを指定できます。  
  
5.  **[接続]** をクリックします。  

## <a name="connect-to-a-remote-ssis-server"></a>リモート SSIS サーバーへの接続
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] または他の管理アプリケーションからリモート サーバー上の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のインスタンスに接続するには、アプリケーションのユーザーがそのサーバーに対して特定の権限を持っている必要があります。  
  
> [!IMPORTANT]
> レガシ Integration Services サービスに直接接続するには、Integration Services サービスが実行されている SQL Server のバージョンと合わせたバージョンの SQL Server Management Studio (SSMS) を使用する必要があります。 たとえば、SQL Server 2016 のインスタンスで実行されているレガシ Integration Services サービスに接続するには、SQL Server 2016 用にリリースされたバージョンの SSMS を使用する必要があります。 [SQL Server Management Studio (SSMS) をダウンロードしてください](../../ssms/download-sql-server-management-studio-ssms.md)。
>
>  リモート サーバーに格納されるパッケージを管理するために、そのリモート サーバー上の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスのインスタンスに接続する必要はありません。 代わりに、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成ファイルを編集し、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でリモート サーバーに格納されているパッケージが表示されるようにします。
  
### <a name="connecting-to-integration-services-on-a-remote-server"></a>リモート サーバー上の Integration Services への接続  
  
#### <a name="to-connect-to-integration-services-on-a-remote-server"></a>リモート サーバー上の Integration Services に接続するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を開きます。  
  
2.  **[ファイル]** メニューの **[オブジェクト エクスプローラーを接続]** をクリックして、 **[サーバーへの接続]** ダイアログ ボックスを表示します。  
  
3.  **[サーバーの種類]** ボックスの一覧で **[Integration Services]** を選択します。  
  
4.  **[サーバー名]** ボックスに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーの名前を入力します。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、そのインスタンスに固有のものではありません。 このサービスに接続するには、Integration Services サービスが実行されているコンピューターの名前を使用します。  
  
5.  **[接続]** をクリックします。  
  
> [!NOTE]  
>  **[サーバーの参照]** ダイアログ ボックスには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]のリモート インスタンスは表示されません。 また、 **[サーバーへの接続]** ダイアログ ボックスで **[オプション]** ボタンをクリックしたときに表示される **[接続プロパティ]** タブのオプションは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] への接続時には適用されません。  
  
### <a name="eliminating-the-access-is-denied-error"></a>"アクセスが拒否されました" エラーの回避  
 十分な権限を持っていないユーザーがリモート サーバー上の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] インスタンスに接続しようとすると、サーバーから "アクセスは拒否されました" というエラー メッセージが返されます。 必要な権限がユーザーに与えられていることを確認すれば、このエラー メッセージを回避できます。  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-server-2003-or-windows-xp"></a>Windows Server 2003 または Windows XP でリモート ユーザーの権限を構成するには  
  
1.  ユーザーがローカルの Administrators グループのメンバーでない場合、そのユーザーを Distributed COM Users グループに追加します。 この操作は、 **[管理ツール]** メニューからアクセスできるコンピューターの管理 MMC スナップインで実行できます。  
  
2.  コントロール パネルを開き、 **[管理ツール]** 、 **[コンポーネント サービス]** の順にダブルクリックして、コンポーネント サービス MMC スナップインを起動します。  
  
3.  コンソールの左ペインで **[コンポーネント サービス]** ノードを展開します。 **[コンピューター]** ノード、 **[マイ コンピューター]** の順に展開し、 **[DCOM の構成]** ノードをクリックします。  
  
4.  **[DCOM の構成]** ノードを選択し、構成できるアプリケーションの一覧から [SQL Server Integration Services 11.0] を選択します。  
  
5.  [SQL Server Integration Services 11.0] を右クリックし、 **[プロパティ]** を選択します。  
  
6.  **[SQL Server Integration Services 11.0 のプロパティ]** ダイアログ ボックスで、 **[セキュリティ]** タブをクリックします。  
  
7.  **[起動とアクティブ化のアクセス許可]** で **[カスタマイズ]** を選択し、 **[編集]** をクリックして **[起動許可]** ダイアログ ボックスを開きます。  
  
8.  **[起動許可]** ダイアログ ボックスで、ユーザーを追加または削除し、適切なアクセス許可を適切なユーザーとグループに割り当てます。 使用可能なアクセス許可は、[ローカルからの起動]、[リモートからの起動]、[ローカルからのアクティブ化]、[リモートからのアクティブ化] です。 起動権限ではサービスを開始および停止するアクセス許可を許可または拒否し、アクティブ化権限ではサービスに接続するアクセス許可を許可または拒否します。  
  
9. [OK] をクリックして、ダイアログ ボックスを閉じます。  
  
10. **[アクセス許可]** で手順 7. ～ 8. を繰り返し、適切なユーザーとグループに適切なアクセス許可を割り当てます。  
  
11. MMC スナップインを閉じます。  
  
12. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを再開します。  
  
#### <a name="to-configure-rights-for-remote-users-on-windows-2000-with-the-latest-service-packs"></a>最新の Service Pack が適用されている Windows 2000 でリモート ユーザーの権限を構成するには  
  
1.  コマンド プロンプトで **dcomcnfg.exe** を実行します。  
  
2.  **[分散 COM の構成のプロパティ]** ダイアログ ボックスの **[アプリケーション]** ページで、[SQL Server Integration Services 11.0] をクリックして **[プロパティ]** をクリックします。  
  
3.  **[セキュリティ]** ページをクリックします。  
  
4.  2 つのダイアログ ボックスを使用して、 **[アクセスの許可]** と **[起動の許可]** を構成します。 リモートとローカルのアクセスは区別できません。アクセスの許可にはローカルとリモートのアクセス権が含まれており、起動の権限にはローカルとリモートの起動権限が含まれています。  
  
5.  ダイアログ ボックスを閉じ、 **dcomcnfg.exe**を閉じます。  
  
6.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスを再開します。  
  
### <a name="connecting-by-using-a-local-account"></a>ローカル アカウントを使用した接続  
 クライアント コンピューターのローカル Windows アカウントで作業している場合、リモート コンピューターの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスに接続できるのは、同じ名前、同じパスワード、および十分な権限が設定されたローカル アカウントがリモート コンピューター上に存在する場合だけです。  
  
### <a name="by-default-the-ssis-service-does-not-support-delegation"></a>既定では SSIS サービスは委任をサポートしない  
既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは資格情報を委任できません。資格情報の委任はダブル ホップとも呼ばれます。 たとえば、ユーザーがクライアント コンピューターで作業しており、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] が別のコンピューターで実行されているとします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はさらに別のコンピューターで実行されています。 まず、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] がクライアント コンピューターから [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが実行されている 2 番目のコンピューターに資格情報を渡します。 ただし、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは 2 番目のコンピューターから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されている 3 番目のコンピューターに資格情報を委任できません。

資格情報の委任は、 **[任意のサービスへの委任でこのユーザーを信頼する (Kerberos のみ)]** の権限を SQL Server のサービス アカウントで有効にできます。これにより、子プロセスとして Integration Services サービス (ISServerExec.exe) が起動します。 この権限を付与する前に、組織のセキュリティ要件を満たしているかどうかを検討してください。

詳細については、「 [Getting Cross Domain Kerberos and Delegation working with SSIS Package](https://blogs.msdn.microsoft.com/psssql/2014/06/26/getting-cross-domain-kerberos-and-delegation-working-with-ssis-package/)」(SSIS パッケージで機能するクロス ドメイン Kerberos の取得) を参照してください。
 
## <a name="configure-the-firewall"></a>ファイアウォールの構成
  
 Windows ファイアウォール システムは、ネットワーク接続経由でコンピューター リソースに不正なアクセスが行われるのを防ぐのに役立ちます。 このファイアウォールを経由して [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] にアクセスするには、アクセスを有効にするようにファイアウォールを構成する必要があります。  
  
> [!IMPORTANT]  
>  リモート サーバーに格納されるパッケージを管理するために、そのリモート サーバー上の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスのインスタンスに接続する必要はありません。 代わりに、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの構成ファイルを編集し、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でリモート サーバーに格納されているパッケージが表示されるようにします。
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは、DCOM プロトコルを使用しています。
  
 多くのファイアウォール システムが市販されています。 Windows ファイアウォール以外のファイアウォールを実行している場合、使用しているシステム固有の情報については、そのファイアウォールのマニュアルを参照してください。  
  
 ファイアウォールでアプリケーション レベルのフィルター処理がサポートされている場合は、Windows によって提供されるユーザー インターフェイスを使用して、プログラムやサービスなどの例外を指定し、ファイアウォールを通過することを許可できます。 それ以外の場合は、限定された TCP ポートのセットを使用するように DCOM を構成する必要があります。 上記の Microsoft Web サイト リンクには、使用する TCP ポートを指定する方法が紹介されています。  
  
 Integration Services サービスでは、ポート 135 を使用します。このポートは変更できません。 サービス コントロール マネージャー (SCM) のアクセスのためには、TCP ポート 135 を開く必要があります。 SCM は、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスの起動と停止、実行中のサービスに対する制御要求の転送などのタスクを実行します。  
  
 以下のセクションに記載されている情報は、Windows ファイアウォールに固有の情報です。 Windows ファイアウォール システムを構成する方法には、コマンド プロンプトでコマンドを実行する方法と、[Windows ファイアウォール] ダイアログ ボックスでプロパティを設定する方法があります。  
  
 Windows ファイアウォールの既定の設定の詳細と、データベース エンジン、Analysis Services、Reporting Services、および Integration Services に影響する TCP ポートの説明については、「 [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」をご覧ください。  
  
### <a name="configuring-a-windows-firewall"></a>Windows ファイアウォールの構成  
 次のコマンドを使用すると、TCP ポート 135 を開き、MsDtsSrvr.exe を例外リストに追加し、ファイアウォールのブロックを解除するスコープを指定できます。  
  
#### <a name="to-configure-a-windows-firewall-using-the-command-prompt-window"></a>コマンド プロンプト ウィンドウを使用して Windows ファイアウォールを構成するには  
  
1.  次のコマンドを実行します。

    ```dos
    netsh firewall add portopening protocol=TCP port=135 name="RPC (TCP/135)" mode=ENABLE scope=SUBNET
    ```
  
2.  次のコマンドを実行します。

    ```dos
    netsh firewall add allowedprogram program="%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.exe" name="SSIS Service" scope=SUBNET
    ```
  
    > [!NOTE]  
    >  すべてのコンピューターおよびインターネット上のコンピューターに対してファイアウォールを開くには、scope=SUBNET を scope=ALL に変更します。  
  
 次の手順では、Windows のユーザー インターフェイスを使用して、TCP ポート 135 を開き、MsDtsSrvr.exe を例外リストに追加して、ファイアウォールのブロックを解除するスコープを指定する方法について説明します。  
  
#### <a name="to-configure-a-firewall-using-the-windows-firewall-dialog-box"></a>[Windows ファイアウォール] ダイアログ ボックスを使用してファイアウォールを構成するには  
  
1.  コントロール パネルの **[Windows ファイアウォール]** をダブルクリックします。  
  
2.  **[Windows ファイアウォール]** ダイアログ ボックスで、 **[例外]** タブをクリックし、 **[プログラムの追加]** をクリックします。  
  
3.  **[プログラムの追加]** ダイアログ ボックスで、 **[参照]** をクリックし、Program Files\Microsoft SQL Server\100\DTS\Binn フォルダーに移動します。次に MsDtsSrvr.exe をクリックし、 **[開く]** をクリックします。 **[OK]** をクリックして、 **[プログラムの追加]** ダイアログ ボックスを閉じます。  
  
4.  **[例外]** タブで、 **[ポートの追加]** をクリックします。  
  
5.  **[ポートの追加]** ダイアログ ボックスの **[名前]** ボックスに、「 **RPC(TCP/135)** 」またはその他のわかりやすい名前を入力します。次に、 **[ポート番号]** ボックスに「 **135** 」と入力し、 **[TCP]** をクリックにします。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスは常にポート 135 を使用します。 別のポートを指定することはできません。  
  
6.  **[ポートの追加]** ダイアログ ボックスで、必要に応じて **[スコープの変更]** をクリックし、既定のスコープを変更できます。  
  
7.  **[スコープの変更]** ダイアログ ボックスで、 **[ユーザーのネットワーク (サブネット) のみ]** を選択するか、カスタムの一覧を入力し、 **[OK]** をクリックします。  
  
8.  **[OK]** をクリックして **[ポートの追加]** ダイアログ ボックスを閉じます。  
  
9. **[OK]** をクリックして **[Windows ファイアウォール]** ダイアログ ボックスを閉じます。  
  
    > [!NOTE]  
    >  Windows ファイアウォールを構成するために、この手順では、コントロール パネルの **[Windows ファイアウォール]** を使用します。 **[Windows ファイアウォール]** では、現在のネットワークの場所のプロファイルに対してのみファイアウォールを構成できます。 ただし、Windows ファイアウォールは、 **netsh** コマンド ライン ツール、またはセキュリティが強化された Windows ファイアウォールの [!INCLUDE[msCoName](../../includes/msconame-md.md)] 管理コンソール (MMC) スナップインを使用して構成することもできます。 これらのツールの詳細については、「 [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」を参照してください。  
