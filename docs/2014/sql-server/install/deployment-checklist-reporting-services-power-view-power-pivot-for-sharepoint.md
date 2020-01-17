---
title: '展開チェックリスト: Reporting Services、Power View、および PowerPivot for SharePoint |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 9a2575c8-06fc-4ef4-9f24-c19e52b1bbcf
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: f1eb0f6892192e5ed328386e6730ec3b1c41f05b
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952551"
---
# <a name="deployment-checklist-reporting-services-power-view-and-powerpivot-for-sharepoint"></a>配置のチェック リスト: Reporting Services、Power View、および PowerPivot for SharePoint
  PowerPivot for SharePoint、レポート ビルダー、[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] の各 BI 機能を同じ SharePoint ファームにインストールするときは、次のチェック リストを使用してください。 このチェック リストでは特定のインストール順序が推奨されていますが、実際には、ほぼどのような順序でもこれらの機能をインストールできます。 このチェック リストでは、次の製品または機能のインストールが想定されています。  
  
1.  SharePoint Server 2010 Service Pack 1 (SP1)  
  
2.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] データベースエンジン  
  
3.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Reporting Services および Reporting Services アドイン  
  
4.  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot for SharePoint  
  
 これらの機能をインストールすると、次のことができるようになります。  
  
-   SharePoint サイトから PowerPivot for Excel で作成した PowerPivot ブックにアクセスする。  
  
-   SharePoint で PowerPivot ブックに基づいて対話形式の [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] レポートを作成する。  
  
-   SharePoint でレポート ビルダーを起動するときにレポート ビルダー レポートを作成する。  
  
> [!NOTE]  
>  PowerPivot for SharePoint を使用するには、SharePoint 2010 Service Pack 1 (SP1) を SharePoint ファームにインストールする必要があります。 このソフトウェアを評価の目的でインストールする場合は、ファーム アップグレード手順のオーバーヘッドを避けるため、クリーン サーバーで開始することを検討してください。 ファームのアップグレードは SharePoint の動作に大きな影響を与え、通常は慎重な計画を必要とします。 できるだけ簡単に PowerPivot for SharePoint をインストールすることが目的の場合は、SharePoint 2010 をインストールし、SharePoint 2010 SP1 をインストールしてから、後の手順でファームを構成するという方法をとってください。 SharePoint 2010 SP1 のインストール時には、まだファームが構成されていないので、アップグレードは行われません。  
>   
>  このチェック リストでは、ファームの構成手順は PowerPivot for SharePoint の構成の間に PowerPivot 構成ツールを使用して行うことが想定されています。 必要に応じて、代わりに SharePoint 製品構成ウィザードを使用してもかまいません。 どちらの方法でも、PowerPivot for SharePoint をサポートする操作可能なファームが構成されます。  
  
## <a name="prerequisites"></a>Prerequisites  
 SQL Server セットアップを実行するには、ローカル管理者である必要があります。  
  
 PowerPivot for SharePoint には SharePoint Server 2010 Enterprise Edition が必要です。 評価版の Enterprise Edition を使用することもできます。  
  
 SharePoint Server 2010 SP1 をインストールする必要があります。 これがないと、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] の機能を使用するようにファームを構成できません。  
  
 コンピューターがドメインに参加する必要があります。  
  
 サービスを準備するためのドメイン ユーザー アカウントが 1 つ以上必要です。 ドメイン ユーザー アカウントは、SharePoint Web サービスおよび管理サービス、Reporting Services、Analysis Services、Excel Services、Secure Store Service、および PowerPivot System サービスで必要になります。 ドメイン アカウントは、SharePoint の管理アカウント機能で必要になります。 データベース エンジンは仮想アカウントを使用して準備できますが、他のすべてのサービスはドメイン ユーザーとして実行する必要があります。  
  
 PowerPivot インスタンスの名前を使用できる必要があります。 PowerPivot の名前のインスタンスが既に存在するコンピューターに、PowerPivot for SharePoint をインストールすることはできません。  
  
 既存のファームに PowerPivot for SharePoint をインストールする場合は、クラシック モード認証用に構成された SharePoint Web アプリケーションが 1 つ以上必要です。 PowerPivot データ アクセスは、Web アプリケーションがクラシック モード認証をサポートする場合にのみ機能します。 クラシックモードの要件の詳細については、「 [PowerPivot の認証と承認](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization)」を参照してください。  
  
 次の追加トピックを確認し、システムとバージョンの要件を理解してください。  
  
-   [SharePoint 2010 ファームで SQL Server BI 機能を使用するためのガイド](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
## <a name="steps"></a>手順  
 次の手順では、管理者がサーバーをインストールして構成すると想定しています。 SharePoint のセットアップ ユーザーはファーム管理者でもあり、通常は、既定のサイト コレクションのプライマリ サイト管理者です。 以下の手順を複数のユーザーで行う場合は、追加の権限が必要になることがあります。  
  
|手順|リンク|  
|----------|----------|  
|SharePoint 2010 製品準備ツールを実行します。|SharePoint 2010 のインストール メディアが必要です。 準備ツールはインストール メディアの PrerequisiteInstaller.exe です。|  
|SharePoint Server 2010 Enterprise Edition または Enterprise Evaluation Edition をインストールします。|SharePoint をインストールするときは、セットアップが終了した後で SharePoint 2010 製品構成ウィザードを実行しないでおき、ファームの構成を後で行うこともできます。 ファームの構成を待機すると、ファームのデータベースサーバーとして、後の手順でインストールされる [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] データベースエンジンインスタンスを使用できるようになります。 ファームを構成するには、PowerPivot 構成ツールを使用します。 このツールには、ファームがまだ構成されていない場合にファームを準備する処理が含まれます。|  
|SharePoint Server 2010 SP1 をインストールします。|[https://support.microsoft.com/kb/2460045](https://go.microsoft.com/fwlink/p/?linkID=219697)から SP1 をダウンロードします。|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] セットアップを実行して、データベース エンジンと PowerPivot for SharePoint をインストールします。|[PowerPivot for SharePoint 2010 をインストールする](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)<br /><br /> 手順 1 では、PowerPivot for SharePoint のインストール方法を説明します。 この手順では、ロールにデータベース エンジンを追加する [セットアップ ロール] ページのチェック ボックスをオンにします。 これにより、データベースエンジンがインストールに追加され、次の手順でファームを構成するときにファームのデータベースサーバーとして使用できるようになります。 ただし、既にファームが構成されている場合は、この手順をスキップできます。<br /><br /> 手順 2. では、サーバーを構成します。 ここでは、PowerPivot 構成ツールを選択します。 複数の方法を利用できますが、スタンドアロン インストールの場合は構成ツールを使用するのが最も効率的な方法です。<br /><br /> SharePoint 2010 がインストールされていて、構成されていない場合、ツールでは、ファーム、既定の Web アプリケーション、およびルート サイト コレクションを作成する処理があらかじめ選択されます。 これらのオプションを選択したままにして、ファームが作成されるようにする必要があります。 ファームを既に構成してある場合、ツールではこれらの処理は省略されて、PowerPivot for SharePoint の構成に必要な処理だけが提供されます。<br /><br /> 手順 3. では、Analysis Services OLE DB プロバイダーの SQL Server 2008 R2 バージョンをインストールします。 この手順は、2008 R2 バージョンの PowerPivot for Excel で作成されたブックのバージョンをサポートするために重要です。|  
|ファームが動作することを確認します。|最初に、サーバーの全体管理を起動して、使用できることを確認します。 次に、 http://localhostを入力して、チームサイトを開きます。  SharePoint チーム サイトが表示されます。|  
|PowerPivot for SharePoint が動作することを確認します。|[PowerPivot for SharePoint インストールの確認](https://docs.microsoft.com/analysis-services/instances/install-windows/verify-a-power-pivot-for-sharepoint-installation)<br /><br /> このタスクでは、アップロードするサンプルのブックを使用して、PowerPivot データのアクセスを確認します。|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] セットアップを実行し、Reporting Services および Reporting Services アドインをインストールして構成します。|[SharePoint 2010 用 Reporting Services の SharePoint モードのインストール](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)<br /><br /> 表形式のデータをホストするために第 2 のリソースが必要な場合は、Reporting Services をインストールするときに、必要に応じて、追加の Analysis Services インスタンスをセットアップの機能ツリーに追加できます。 追加の Analysis Services インスタンスは、[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] で作成する表形式のモデル データベースをホストするために使用されます。 表形式のデータベースは、[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] レポートに有効なデータ ソースです。<br /><br /> [表形式モードでの Analysis Services のインストール](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services)|  
|Reporting Services が動作することを確認します。|[Verify a Reporting Services Installation](../../reporting-services/install-windows/verify-a-reporting-services-installation.md)|  
|(サイト管理者) SharePoint 権限を構成します。|SharePoint ライブラリのアイテムを追加、編集、削除するには、投稿権限が必要です。 レポートおよび埋め込みデータを表す PowerPivot ブックへの読み取りアクセスには、表示権限レベルで十分です。<br /><br /> 外部データ ソースとしてアクセスされる PowerPivot ブック (ブックの URL が別のブックまたはレポート内の接続文字列である場合) には、表示権限より高い読み取り権限が必要です。<br /><br /> BI セマンティック モデル接続にも読み取り権限が必要です。 正しい権限を適用するには、新しい権限レベルまたは SharePoint グループの作成が必要な場合があります。|  
|(サイト管理者) ドキュメント ライブラリを拡張します。|BI コンテンツの種類、BI セマンティック モデル接続、Reporting Services 共有データ ソース、レポート ビルダー レポートを使用できるようにドキュメント ライブラリを拡張します。<br /><br /> 1 <br />                    **コンテンツの種類の管理を有効に**します。 共有ドキュメントまたは別のドキュメントライブラリの ライブラリ タブで、**ライブラリの設定** をクリックします。 全般設定 の **詳細設定** をクリックします。 コンテンツの種類 で、**はい** を選択してコンテンツの種類の管理を許可し、**OK** をクリックします。<br /><br /> 3 <br />                    **BI コンテンツの種類を選択**します。 ライブラリ タブで、**ライブラリの設定** をクリックします。 コンテンツタイプ の **既存のサイトコンテンツタイプから追加** をクリックします。 [ビジネスインテリジェンスのコンテンツの種類] グループの [ **BI セマンティックモデル接続ファイル**および**レポートデータソース**] を追加します。 必要であれば、その他の Reporting Services コンテンツ (レポート モデルなど) を追加して、追加のレポート作成シナリオを有効化することもできます。<br /><br /> <br /><br /> 詳細については、「 [BI セマンティックモデル接続のコンテンツタイプをライブラリ&#40;PowerPivot for SharePoint&#41;に追加](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library)する」および「 [SharePoint 統合モード&#40;&#41;のライブラリ Reporting Services にレポートサーバーのコンテンツの種類を追加する」を](../../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md)参照してください。|  
|(サイト管理者) [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] の起動に使用されるデータ接続ファイルを作成します。|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] に対するデータ ソースとして、BI セマンティック モデル接続 (.bism) または Reporting Services 共有データ ソース (.rsds) を作成する必要があります。 データ接続ファイルを作成した後は、データ接続をデータ ソースとして使用して [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] を起動できます。<br /><br /> [PowerPivot ブックへの BI セマンティック モデル接続の作成](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-power-pivot-workbook)<br /><br /> [Create a BI Semantic Model Connection to a Tabular Model Database](../../relational-databases/databases/model-database.md)<br /><br /> 注: [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] は、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] バージョンの Reporting Services をインストールし、サーバーを共有サービスとして構成したことによって使用可能になります。 Reporting Services をインストールし、SQL Server 2008 レベルの統合用に構成した場合は、[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] を使用できません。|  
  
## <a name="see-also"></a>参照  
 [SQL Server 2012 の各エディションがサポートする機能](https://go.microsoft.com/fwlink/?linkid=232473)  
  
  
