---
title: データ マイニング サービスおよびデータ ソース |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b26fd6e3-7d87-4f66-ab47-5303b51b87da
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 048f737266e815a02058a51ebebce0b0f1ff46af
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66084914"
---
# <a name="data-mining-services-and-data-sources"></a>データ マイニング サービスおよびデータ ソース
  データ マイニングでは、SQL Server Analysis Services のインスタンスへの接続が必要になります。 キューブからのデータは、データ マイニングには必須ではなく、リレーショナル ソースの使用をお勧めします。ただし、データ マイニングでは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] エンジンによって提供されるコンポーネントが使用されます。  
  
 このトピックには、データ マイニング モデルの作成、処理、配置、またはクエリのために SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のインスタンスに接続する際に知っておく必要がある情報が含まれています。  
  
## <a name="data-mining-services"></a>データ マイニング サービス  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のサーバー コンポーネントは、msmdsrv.exe アプリケーションです。このアプリケーションは、通常、Windows サービスとして実行されます。 このアプリケーションは、セキュリティ コンポーネント、XML for Analysis (XMLA) リスナー コンポーネント、クエリ プロセッサ コンポーネント、および次の機能を実行するその他多くの内部コンポーネントで構成されています。  
  
-   クライアントから受信したステートメントの解析  
  
-   メタデータの管理  
  
-   トランザクションの処理  
  
-   計算の処理  
  
-   ディメンションおよびセル データの格納  
  
-   集計の作成  
  
-   クエリのスケジュール設定  
  
-   オブジェクトのキャッシュ  
  
-   サーバー リソースの管理  
  
### <a name="xmla-listener"></a>XMLA リスナー  
 XMLA リスナー コンポーネントでは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] とそのクライアントの間のすべての XMLA 通信が処理されます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] `Port`いるポートを指定する、msmdsrv.ini ファイルで構成設定を使用できます、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]インスタンスがリッスンします。 このファイルの 0 の値は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] が既定のポートをリッスンすることを示します。 特に指定がなければ、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では次の既定の TCP ポートが使用されます。  
  
|Port|説明|  
|----------|-----------------|  
|2383|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]の既定のインスタンスです。|  
|2382|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]の他のインスタンスのリダイレクターです。|  
|サーバーの起動時に動的に割り当てられます。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]の名前付きインスタンスです。|  
  
 このサービスが使用するポートを制御する方法の詳細については、「 [Analysis Services のアクセスを許可するための Windows ファイアウォールの構成](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)」を参照してください。  
  
## <a name="connecting-to-data-sources"></a>データ ソースへの接続  
 データ マイニング構造やデータ マイニング モデルを作成したり更新したりする際には、データ ソースで定義されているデータを使用します。 データ ソースには、Excel ブック、テキスト ファイル、SQL Server データベースなどのデータは含まれていません。接続情報が定義されているだけです。  データ ソース ビュー (DSV) は、そのソース上の抽象化レイヤーとして機能し、ソースから取得されるデータの変更やマップを行います。  
  
 これらの各ソースの接続要件については、このトピックでは説明していません。 詳細については、プロバイダーのマニュアルを参照してください。 ただし、一般には、プロバイダーとのやり取りで、Analysis Services の次の要件に注意してください。  
  
-   データ マイニングはサーバーによって提供されるサービスなので、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスはデータ ソースへのアクセスを許可されている必要があります。  アクセスには、場所とユーザー情報という、2 つの側面があります。  
  
     **場所** に関して問題になるのは、自分のコンピューターだけに格納されているデータを使用してモデルを作成し、それをサーバーに配置した場合、データ ソースが見つからないためにモデルの処理が失敗することです。 この問題を解決するには、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] が実行されている同じ SQL Server インスタンスにデータを転送するか、ファイルを共有の場所に移動することが必要になる場合があります。  
  
     **ユーザー情報** に関して問題になるのは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 上のサービスが適切な資格情報でデータ ファイルまたはデータ ソースを開くことができる必要があることです。 たとえば、モデルの作成者はデータを表示するための無制限の権限を持っているとしても、サーバー上のモデルを処理および更新するユーザーはデータへのアクセスが制限または禁止されている場合があるため、モデルのコンテンツの処理や変更が失敗することがあります。 少なくとも、リモート データ ソースへの接続に使用されるアカウントは、データの読み取り権限を持っている必要があります。  
  
-   モデルを移動するときには、同じ要件が適用されます。元のデータ ソースの場所への適切なアクセスをセットアップするか、データ ソースをコピーするか、新しいデータ ソースを構成する必要があります。 また、ログインおよびロールを転送するか、データ マイニング オブジェクトを新しい場所で処理および更新できるように権限をセットアップする必要があります。  
  
## <a name="configuring-permissions-and-server-properties"></a>権限とサーバー プロパティの構成  
 データ マイニングには、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに対する追加の権限が必要です。 ほとんどのデータ マイニング プロパティは、[[分析サーバーのプロパティ] ダイアログ ボックス &#40;Analysis Services&#41;](../analysis-server-properties-dialog-box-analysis-services.md) を使用して設定できます。  
  
 構成できるプロパティの詳細については、次を参照してください。 [Configure Server Properties in Analysis Services](../server-properties/server-properties-in-analysis-services.md)します。  
  
 データ マイニングに関連するサーバー プロパティを以下に示します。  
  
-   `AllowAdHocOpenRowsetQueries` サーバーのメモリ領域に直接読み込まれる OLE DB プロバイダーへのアドホック アクセスを制御します。  
  
    > [!IMPORTANT]  
    >  セキュリティを強化するため、このプロパティは `false` に設定することをお勧めします。 既定値は `false` です。 このプロパティが `false` に設定されていても、ユーザーは単一クエリを作成したり、許可されているデータ ソースに対して OPENQUERY を使用したりできます。  
  
-   **AllowedProvidersInOpenRowset** アドホック アクセスが有効な場合にプロバイダーを指定します。 ProgID のコンマ区切りのリストを入力することにより、複数のプロバイダーを指定できます。  
  
-   **MaxConcurrentPredictionQueries** 予測によるサーバーの負荷を制御します。 既定値は 0 で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise ではクエリが制限されず、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard では同時実行クエリが 5 つまで許可されます。 制限を超えたクエリはシリアル化され、タイムアウトすることがあります。  
  
 サーバーにはこの他に、使用できるデータ マイニング アルゴリズム (およびアルゴリズムに対する制限) や、すべてのデータ マイニング サービスの既定値を制御するプロパティもあります。 ただし、データ マイニング ストアド プロシージャへのアクセスを制御できる設定はありません。 詳細については、「 [データ マイニング プロパティ](../server-properties/data-mining-properties.md)」を参照してください。  
  
 そのほか、サーバーをチューニングしたりクライアントの利用に関するセキュリティを制御したりするためのプロパティを設定することもできます。 詳細については、「 [機能プロパティ](../server-properties/feature-properties.md)」を参照してください。  
  
> [!NOTE]  
>  各エディションによるプラグイン アルゴリズムのサポートの詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2012 の各エディションでサポートされている](https://go.microsoft.com/fwlink/?linkid=232473)(https://go.microsoft.com/fwlink/?linkid=232473) します。  
  
## <a name="programmatic-access-to-data-mining-objects"></a>データ マイニング オブジェクトへのプログラムによるアクセス  
 以下のオブジェクト モデルを使用して、Analysis Services データベースへの接続を作成し、データ マイニング オブジェクトを操作できます。  
  
 **ADO** OLE DB を使用して Analysis Services サーバーに接続します。 ADO を使用する場合は、クライアントがスキーマ行セットのクエリと DMX ステートメントのみに制限されます。  
  
 **ADO.NET** 特に SQL Server プロバイダーとのやり取りに適しています。 データ アダプターを使用して動的な行セットを格納したり、 データセット オブジェクトを使用したりできます。データセット オブジェクトは、XML として更新したり保存したりできるデータ テーブルとして格納されるサーバー データのキャッシュです。  
  
 **ADOMD.NET** データ マイニングと OLAP の操作に最適化されたマネージド データ プロバイダーです。 ADOMD.NET は ADO.NET より高速で、メモリ効率も ADO.NET より優れています。 サーバー オブジェクトに関するメタデータを取得することもできます。 クライアント アプリケーションでは、.NET が使用できない場合以外は ADOMD.NET を使用することをお勧めします。  
  
 **Server ADOMD** サーバー上で直接 Analysis Services オブジェクトにアクセスするためのオブジェクト モデルです。 Analysis Services ストアド プロシージャで使用されます。クライアントでは使用しません。  
  
 **AMO** Decision Support オブジェクト (DSO) に代わる Analysis Services 用の管理インターフェイスです。 オブジェクトの繰り返し処理などの操作では、他のインターフェイスを使用する場合に比べて高い権限が必要になります。 これは、AMO が直接メタデータにアクセスするためです。ADOMD.NET などの他のインターフェイスがアクセスするのはデータベース スキーマだけです。  
  
### <a name="browse-and-query-access-to-servers"></a>サーバーへの参照およびクエリ アクセス  
 OLAP/データ マイニング モードの Analysis Services のインスタンスを使用して、すべての種類の予測を実行できます。ただし、次の制限があります。  
  
-   Server ADOMD を使用する場合は、接続を作成せずに DMX を使用してサーバーにアクセスし、 結果を直接データ テーブルにコピーできます。 ただし、リモート インスタンスでは Server ADOMD は使用できません。クエリを実行できるのはローカル サーバーだけです。  
  
-   ADO.NET は、データ マイニングの名前付きパラメーターをサポートしません。 ADOMD.NET を使用する必要があります。  
  
-   ADOMD.NET では、テーブル全体をパラメーターとして渡すことができます。したがって、クライアント側のデータ (サーバーからは使用できないデータ) を使用することができます。 形が指定されたテーブルを予測の入力として使用することもできます。  
  
### <a name="using-data-mining-stored-procedures"></a>データ マイニング ストアド プロシージャの使用  
 ストアド プロシージャは、クエリを再利用に向けてカプセル化するために使用されるのが一般的です。 クライアントでは、CALL を使用してストアド プロシージャ ( [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のシステム ストアド プロシージャを含む) を実行できます。  
  
 プロシージャがデータセットを返した場合、クライアントは、行を含む入れ子になったテーブルを持つデータセットまたはデータ テーブルを受け取ります。 たとえば、モデル コンテンツに対するクエリを作成すると、そのクエリではモデル全体が返されます。 あまり多くの行が返されないようにするには、ADOMD+ オブジェクト モデルを使用してストアド プロシージャを作成します。  
  
 サーバー ストアド プロシージャを記述するには、Microsoft.AnalysisServices.AdomdServer 名前空間を参照する必要があります。 ストアド プロシージャを作成および使用する方法の詳細については、「 [ユーザー定義関数およびストアド プロシージャ](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-server/user-defined-functions-and-stored-procedures)」を参照してください。  
  
> [!NOTE]  
>  ストアド プロシージャを使用してデータ サーバー オブジェクトのセキュリティを変更することはできません。 ストアド プロシージャの実行時には、ユーザーの現在のコンテキストを使用してすべてのサーバー オブジェクトへのアクセスが決定されます。 したがって、ユーザーは、アクセスするすべてのデータベース オブジェクトに対する適切な権限を持っている必要があります。  
  
## <a name="see-also"></a>参照  
 [物理アーキテクチャ &#40;Analysis Services - 多次元データ&#41;](../multidimensional-models/olap-physical/understanding-microsoft-olap-physical-architecture.md)   
 [物理アーキテクチャ &#40;Analysis Services - データ マイニング&#41;](physical-architecture-analysis-services-data-mining.md)   
 [データ マイニング ソリューションおよびオブジェクトの管理](management-of-data-mining-solutions-and-objects.md)  
  
  
