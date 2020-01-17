---
title: クライアント アプリケーション (Analysis Services) からの接続 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b1e0f1d4-0b87-4ad3-8172-f746fe2f16a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a646d152abaa3c352bf5ca1c576760e1715c3578
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080210"
---
# <a name="connect-from-client-applications-analysis-services"></a>クライアント アプリケーションからの接続 (Analysis Services)
  Analysis Services を初めて使用する場合は、このトピックの情報を参照し、一般的なツールとアプリケーションを使用して [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の既存のインスタンスに接続します。 このトピックでは、テスト目的で異なるユーザー ID を使用して接続する方法についても説明します。  
  
-   [SQL Server Management Studio (SSMS) による接続](#bkmk_SSMS)  
  
-   [Excel による接続](#bkmk_excel)  
  
-   [SQL Server Data Tools による接続](#bkmk_SSDT)  
  
-   [接続のテスト](#bkmk_tshoot)  
  
 接続文字列のリファレンス ドキュメントは個別に用意されています。 詳細については、「[接続文字列プロパティ &#40;Analysis Services&#41;](connection-string-properties-analysis-services.md)」を参照してください。  
  
 接続に成功するためには、ポート構成が有効であることと、適切なユーザー権限があることが必要です。 それぞれの要件の詳細については、次のリンクをクリックしてください。  
  
-   [Analysis Services のアクセスを許可するための Windows ファイアウォールの構成](configure-the-windows-firewall-to-allow-analysis-services-access.md)  
  
-   [オブジェクトと操作へのアクセスの承認 &#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
##  <a name="bkmk_SSMS"></a> SQL Server Management Studio (SSMS) による接続  
 サーバー インスタンスとデータベースを対話操作で管理するには、SSMS で Analysis Services に接続します。 また、XMLA クエリや MDX クエリを実行して、管理タスクの実行またはデータの取得を行うこともできます。 クエリの送信時にのみデータベースを読み込むツールやアプリケーションとは異なり、SSMS では、ユーザーがサーバーに接続すると、すべてのデータベースが読み込まれます (データベースを表示する権限がユーザーにある場合)。 これは、サーバー上に多数のテーブル データベースがある場合、SSMS を使用して接続するとすべてのデータベースがシステム メモリに読み込まれることを表します。  
  
 特定のユーザー ID で SSMS を実行し、そのユーザーとして Analysis Services に接続することで、権限をテストできます。  
  
 Shift キーを押したまま **[SQL Server Management Studio]** を右クリックして、 **[別のユーザーとして実行]** オプションにアクセスします。  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を起動します。 **[サーバーへの接続]** ダイアログ ボックスで、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバーの種類を選択します。  
  
2.  [ログイン] タブで、サーバーを実行しているコンピューターの名前を入力することによりサーバー名を指定します。 ネットワーク名または完全修飾ドメイン名を使用してサーバーを指定できます。  
  
     名前付きインスタンスの場合は、servername\instancename の形式でサーバー名を指定する必要があります。 たとえば、サーバーのネットワーク名が ADV-SRV062 で、Finance という名前付きインスタンスとして Analysis Services がインストールされている場合、「ADV-SRV062\Finance」と入力します。  
  
     フェールオーバー クラスター内に配置したサーバーの場合は、SSAS クラスターのネットワーク名を使用して接続します。 この名前は、SQL Server のセットアップ時に、 **[SQL Server のネットワーク名]** として指定されます。 Windows Server フェールオーバー クラスター (WSFC) に、名前付きインスタンスとして SSAS をインストールした場合、接続時にインスタンス名を追加することはできません。 これは SSAS 独自の処理です。これとは対照的に、クラスター化されたリレーショナル データベース エンジンの名前付きインスタンスには、インスタンス名が含まれています。 たとえば、SSAS とデータベース エンジンの両方を名前付きインスタンス (Contoso-Accounting) として、SQL-CLU という SQL Server のネットワーク名を使用してインストールした場合、"SQL-CLU" を使って SSAS に接続し、"SQL-CLU\Contoso-Accounting" というデータベース エンジンに接続することになります。 詳細と例については、「 [SQL Server Analysis Services をクラスター化する方法](https://go.microsoft.com/fwlink/p/?LinkId=396548) 」を参照してください。  
  
     ネットワーク負荷分散クラスター内に配置したサーバーの場合は、NLB の仮想サーバー名を使用して接続します。  
  
3.  認証方式は常に Windows 認証です。また、ユーザー ID として使用するユーザーは常に、Management Studio を介して接続する Windows ユーザーです。  
  
     接続に成功するためには、サーバー (またはサーバー上のデータベース) にアクセスするための権限が必要です。 Management Studio で実行するほとんどのタスクには管理権限が必要です。 接続に使用するアカウントがサーバー管理者ロールのメンバーであることを確認します。 詳細については、次を参照してください。[サーバーの管理者アクセス許可の付与&#40;Analysis Services&#41;](grant-server-admin-rights-to-an-analysis-services-instance.md)します。  
  
4.  **[接続プロパティ]** をクリックして、特定のデータベースを指定、タイムアウト値を設定、または暗号化のオプションを設定します。 省略可能な接続情報としては、現在の接続にしか使用されない接続プロパティがあります。  
  
5.  **[追加の接続パラメーター]** タブをクリックして、[サーバーへの接続] ダイアログ ボックスに用意されていない接続プロパティを設定します。 たとえば、テキスト ボックスに `Roles=Reader` を入力する場合があります。  
  
     より限られた権限のロールで接続すると、そのロールが有効なときにデータベースの動作をテストすることができます。  
  
    ```  
    Provider=MSOLAP; Data Source=SERVERNAME; Initial Catalog=AdventureWorks2012; Roles=READER  
    ```  
  
##  <a name="bkmk_excel"></a> Excel による接続  
 ビジネス データを分析するために Microsoft Excel を使用することがよくあります。 Office で Excel をインストールすると、ネットワーク サーバー上のデータをいつでもすぐに利用できるように、Analysis Services OLE DB プロバイダー (MSOLAP.dll)、ADOMD.NET、およびその他のデータ プロバイダーがインストールされます。 新しいバージョンの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を以前のバージョンの Excel と共に使用するときは、場合によっては、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]に接続する各ワークステーションに新しいデータ プロバイダーをインストールする必要があります。 詳細については、「 [Analysis Services 接続に使用するデータ プロバイダー](data-providers-used-for-analysis-services-connections.md) 」を参照してください。  
  
 Analysis Services キューブまたはテーブル モデル データベースに対する接続をセットアップすると、接続情報が、将来の使用に備えて .odc ファイルに保存されます。 接続は、現在の Windows ユーザーのセキュリティ コンテキストで確立されます。 接続が成功するためには、このユーザー アカウントに、データベースの読み取り権限が与えられている必要があります。  
  
 Excel ブックで [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データを使用するとき、その接続は、クエリ要求の間保持されます。 このため、Excel からクエリ ワークロードを監視する際に、各セッションに対して多くの接続が確認される場合があります。これらの接続が保持されるのは短期間です。  
  
 特定のユーザー ID で Excel を起動することにより、権限をテストできます。  
  
 Shift キーを押したまま **[Excel]** を右クリックして、 **[別のユーザーとして実行]** オプションにアクセスします。  
  
1.  Excel の [データ] タブで、 **[その他のデータ ソース]** をクリックし、 **[Analysis Services]** をクリックします。 サーバー名を入力し、クエリを実行するキューブまたはパースペクティブを選択します。  
  
     負荷分散クラスター内に配置するサーバーの場合は、クラスターに割り当てた仮想サーバー名を使用します。  
  
2.  Excel での接続を設定するときに、データ接続ウィザードの最後のページで、Excel Services の認証設定を指定できます。 Excel Services が存在する SharePoint サーバーにブックをアップロードするときには、これらの設定を使用してブックのプロパティが設定されます。 この設定は、データ更新操作で使用されます。 オプションとしては、 **[Windows 認証]** 、 **[Secure Store Service]** (SSS)、 **[なし]** があります。  
  
     **[なし]** を選択することは避けてください。 Analysis Services では、接続先のサーバーが HTTP アクセス用に構成されていないと、ユーザー名とパスワードを接続文字列に指定できません。 同様に、Analysis Services データベースに対するユーザー アクセス権を持った一連の Windows ユーザーの資格情報に SSS ターゲット アプリケーション ID がマップされていることがわかっている場合を除き、SSS は使用しないでください。 既定のオプションは Windows 認証であり、Excel から Analysis Services に接続するほとんどのシナリオに最適な選択肢です。  
  
 詳細については、「 [SQL Server Analysis Services のデータに接続する、または SQL Server Analysis Services のデータをインポートする](https://go.microsoft.com/fwlink/?linkID=215150)」を参照してください。  
  
##  <a name="bkmk_SSDT"></a> SQL Server Data Tools による接続  
 SQL Server Data Tools は、Analysis Services モデル、Reporting Services レポート、SSIS パッケージを含む BI ソリューションを構築するために使用します。 レポートまたはパッケージを構築する際に、Analysis Services への接続を指定する必要が生じる場合があります。  
  
 次のリンク先では、レポート サーバー プロジェクトまたは Integration Services プロジェクトから Analysis Services に接続する方法を説明しています。  
  
-   [MDX のための Analysis Services の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-mdx-ssrs.md)  
  
-   [Analysis Services 接続マネージャー](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
> [!NOTE]  
>  SQL Server Data Tools を使用して既存の Analysis Services プロジェクトで作業する場合、ローカル プロジェクトまたはバージョン管理されたプロジェクトを使用してオフラインで接続したり、オンライン モードで接続して、データベースの実行中に Analysis Services オブジェクトを更新することができます。 詳細については、「 [Analysis Services データベースへのオンライン モードでの接続](../multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md)」を参照してください。 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] からの接続はプロジェクト モードで行う方が一般的です。この場合は、明示的にプロジェクトを配置したときにのみ、変更がデータベースに反映されます。  
  
##  <a name="bkmk_tshoot"></a> 接続のテスト  
 SQL Server Profiler を使用すると、Analysis Services への接続を監視することができます。 Audit Login イベントおよび Audit Logout イベントは、接続の証拠を示します。 ID 列は、接続が確立されたセキュリティ コンテキストを示します。  
  
1.  Analysis Services インスタンスで **SQL Server Profiler** を開始し、新しいトレースを開始します。  
  
2.  [イベントの選択] で、[Security Audit] セクションの [`Audit Login`] および [`Audit Logout`] のチェック ボックスがオンになっていることを確認します。  
  
3.  リモート クライアント コンピューターから、アプリケーション サービス (SharePoint、Reporting Services など) を介して Analysis Services に接続します。 Audit Login イベントに、Analysis Services に接続しているユーザーの ID が表示されます。  
  
 接続エラーがトレースされると、多くの場合、不完全なサーバー構成や無効なサーバー構成であることがわかります。 必ずサーバー構成を最初に確認します。  
  
-   リモート コンピューターから ping を実行して、サーバーがリモート接続を許可することを確認します。  
  
-   **サーバー上のファイアウォール ルールでは、同じドメインのクライアントからの着信接続が許可されます。**  
  
     PowerPivot for SharePoint を除き、リモート サーバーに対するすべての接続は、ファイアウォールの構成 (Analysis Services がリッスンしているポートへのアクセスを許可) を必要とします。 接続エラーが発生した場合は、ポートにアクセスできるかどうかと、適切なデータベースに対しユーザー権限が付与されていることを確認してください。  
  
     テストするには、リモート コンピューターで Excel または SSMS を使用し、Analysis Services インスタンスが使用する IP アドレスとポートを指定します。 接続できる場合は、ファイアウォール ルールがインスタンスに対して有効であり、インスタンスはリモート接続を許可します。  
  
     また、TCP/IP を接続プロトコルに使用する場合、Analysis Services では、クライアント接続が同じドメインまたは信頼されたドメインからのものであることが必要です。 接続がセキュリティの境界をまたがっている場合は、HTTP アクセスを構成する必要性が最も高くなります。 詳細については、「[インターネット インフォメーション サービス &#40;IIS&#41; 8.0 上の Analysis Services への HTTP アクセスの構成](configure-http-access-to-analysis-services-on-iis-8-0.md)」を参照してください。  
  
-   一部のツールで接続できるが他のツールでは接続できないということはないでしょうか。 間違ったバージョンのクライアント ライブラリが問題である可能性があります。 クライアント ライブラリは、SQL Server Feature Pack のダウンロード ページから入手きます。  
  
 接続エラーの解決に役立つリソースは次のとおりです。  
  
 「[SQL Server 2005 Analysis Services の接続シナリオにおける一般的な接続の問題の解決](https://technet.microsoft.com/library/cc917670.aspx)」 このドキュメントは数年前のものですが、記載されている情報と手法はそのまま適用されます。  
  
## <a name="see-also"></a>参照  
 [Analysis Services への接続](connect-to-analysis-services.md)   
 [Analysis Services でサポートされる認証方法](authentication-methodologies-supported-by-analysis-services.md)   
 [権限借用 &#40;SSAS テーブル&#41;](../tabular-models/impersonation-ssas-tabular.md)   
 [データ ソースの作成 &#40;SSAS 多次元&#41;](../multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
  
