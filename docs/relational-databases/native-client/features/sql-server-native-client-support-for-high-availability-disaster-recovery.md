---
title: Native Client、高可用性、復旧
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2b06186b-4090-4728-b96b-90d6ebd9f66f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b2cc984e4e519d9db0c0532ec5b1f917e18b4ec6
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247410"
---
# <a name="sql-server-native-client-support-for-high-availability-disaster-recovery"></a>SQL Server Native Client の HADR サポート
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  このトピックでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client のサポート ([!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] で追加) について説明します。 
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の詳細については、「[可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)」、「[可用性グループの作成と構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)」、「[フェールオーバー クラスタリングと AlwaysOn 可用性グループ &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)」、および「[アクティブなセカンダリ: 読み取り可能なセカンダリ レプリカ &#40;AlwaysOn 可用性グループ&#41;](~/database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
 接続文字列で、特定の可用性グループの可用性グループ リスナーを指定できます。 フェールオーバーする可用性グループ内のデータベースに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client アプリケーションが接続されている場合、元の接続が切断されるため、フェールオーバー後にアプリケーションが動作を継続するには新しい接続を開く必要があります。  
  
 可用性グループ リスナーに接続しておらず、ホスト名に複数の IP アドレスが関連付けられている場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は DNS エントリに関連付けられているすべての IP アドレスを順次繰り返し処理します。 DNS サーバーが最初に返した IP アドレスがネットワーク インターフェイス カード (NIC) にバインドされていない場合、この処理に時間がかかる可能性があります。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client が可用性グループ リスナーに接続するとき、すべての IP アドレスに対して並列で接続を試行します。1 つの接続試行が成功すると、保留中の接続試行はすべて破棄されます。  
  
> [!NOTE]  
>  接続タイムアウト値を大きくし、接続再試行ロジックを実装することにより、アプリケーションが可用性グループに接続する確立が高まります。 また、可用性グループのフェールオーバーにより接続が失敗する可能性があるため、接続再試行ロジックを実装して、再接続されるまで、失敗した接続の再接続を試行する必要があります。  
  
## <a name="connecting-with-multisubnetfailover"></a>MultiSubnetFailover を使用した接続  
 SQL Server 2012 可用性グループ リスナーまたは SQL Server 2012 フェールオーバー クラスター インスタンスに接続する際には、必ず **MultiSubnetFailover=Yes** を指定してください。 **MultiSubnetFailover**を使用すると SQL Server 2012 のすべての可用性グループとフェールオーバークラスターインスタンスの高速フェールオーバーが可能になり、シングルサブネット Always On トポロジのフェールオーバー時間が大幅に短縮されます。 マルチサブネット フェールオーバーの際には、クライアントは複数の接続を並列で試行します。 サブネット フェールオーバーの際には、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は積極的に TCP 接続を再試行します。  
  
 
  **MultiSubnetFailover** 接続プロパティを指定すると、アプリケーションが可用性グループまたはフェールオーバー クラスター インスタンスに配置され、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client がすべての IP アドレスに対して接続を試行することでプライマリ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス上のデータベースに接続を試みます。 接続に対して **MultiSubnetFailover=Yes** を指定した場合、オペレーティング システムの既定の TCP 再送信間隔より短い間隔で、クライアントにより TCP 接続が再試行されます。 これにより、Always On 可用性グループまたは Always On フェールオーバークラスターインスタンスのフェールオーバー後の再接続が高速化され、シングルサブネットとマルチサブネットの両方の可用性グループとフェールオーバークラスターインスタンスの両方に適用できます。  
  
 接続文字列キーワードの詳細については、「[SQL Server Native Client での接続文字列キーワードの使用](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
 可用性グループ リスナーまたはフェールオーバー クラスター インスタンス以外に接続するときに **MultiSubnetFailover=Yes** を指定するとパフォーマンスが低下する可能性があるため、このような指定はサポートされていません。  
  
 可用性グループまたはフェールオーバー クラスター インスタンス内のサーバーに接続する際には、次のガイドラインに従います。  
  
-   単一のサブネットまたはマルチサブネットに接続する場合は、 **MultiSubnetFailover**接続プロパティを使用します。これにより、両方のパフォーマンスが向上します。  
  
-   可用性グループに接続するには、接続文字列でサーバーとして、可用性グループの可用性グループ リスナーを指定します。  
  
-   64 個を超える数の IP アドレスが構成された [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに接続すると、接続エラーが発生します。  
  
-   **MultiSubnetFailover**接続プロパティを使用するアプリケーションの動作は、認証の種類 ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]認証、Kerberos 認証、または Windows 認証) によっては影響を受けません。  
  
-   
  **loginTimeout** の値を増やすことで、フェールオーバー時間に対応し、アプリケーションの接続試行回数を減らすことができます。  
  
-   分散トランザクションはサポートされません。  
  
 読み取り専用のルーティングが無効である場合、次の状況では可用性グループのセカンダリ レプリカの場所には接続できません。  
  
1.  セカンダリ レプリカの場所が、接続を許可するように構成されていない。  
  
2.  アプリケーションが**Applicationintent = ReadWrite** (後述) を使用していて、セカンダリレプリカの場所が読み取り専用アクセス用に構成されている場合。  
  
 プライマリ レプリカが読み取り専用ワークロードを拒否するように構成されているとき、接続文字列に **ApplicationIntent=ReadOnly** が含まれていると、接続は失敗します。  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>データベース ミラーリングの使用からマルチサブネット クラスターの使用へのアップグレード  
 接続文字列に **MultiSubnetFailover** および **Failover_Partner** の接続キーワードが存在する場合、接続エラーが発生します。 また、**MultiSubnetFailover** が使用されているとき、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] から、データベース ミラーリング ペアに属していることを示すフェールオーバー パートナー応答が返された場合にも、エラーが発生します。  
  
 データベース ミラーリングを現在使用している [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client アプリケーションをマルチサブネットのシナリオにアップグレードする場合、**Failover_Partner** 接続プロパティを削除して **MultiSubnetFailover** に置き換え、それを **Yes** に設定し、接続文字列内のサーバー名を可用性グループ リスナーの名前に置き換えます。 接続文字列で **Failover_Partner** および **MultiSubnetFailover=Yes** が使用されている場合、ドライバーでエラーが発生します。 ただし、接続文字列に **Failover_Partner** と **MultiSubnetFailover=No** (または **ApplicationIntent=ReadWrite**) が使用されている場合、アプリケーションはデータベース ミラーリングを使用します。  
  
 ドライバーは、可用性グループのプライマリ データベースでデータベース ミラーリングが使用されている場合、および可用性グループ リスナーではなくプライマリ データベースに接続する接続文字列内で **MultiSubnetFailover=Yes** が使用されている場合、エラーを返します。  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="odbc"></a>ODBC  
 
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] をサポートするために、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client には、次の 2 つの ODBC 接続文字列キーワードが追加されています。  
  
-   **ApplicationIntent**  
  
-   **MultiSubnetFailover**  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の ODBC 接続文字列キーワードの詳細については、「[SQL Server Native Client での接続文字列キーワードの使用](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
 対応する接続プロパティは次のとおりです。  
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の ODBC 接続文字列プロパティの詳細については、「[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)」を参照してください。  
  
 
  **ApplicationIntent** キーワードと **MultiSubnetFailover** キーワードの機能は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ドライバー ([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 以降) を使用する DSN の ODBC データ ソース アドミニストレーターで公開されます。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC アプリケーションは、次に示した 3 つの関数のいずれかを使用して、接続を行うことができます。  
  
|機能|説明|  
|--------------|-----------------|  
|[SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)|
  **SQLBrowseConnect** から返されるサーバーの一覧に VNN は含まれません。 確認できるのはサーバーの一覧だけです。スタンドアロン サーバーであるのか、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が有効な 2 つ以上の [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] インスタンスが含まれる Windows Server フェールオーバー クラスタリング (WSFC) クラスターのうちのプライマリ サーバーまたはセカンダリ サーバーであるのかは示されません。 サーバーへの接続時にエラーが返された場合、接続先のサーバーの構成に **ApplicationIntent** 設定との互換性がないことが原因として考えられます。<br /><br /> 
  **SQLBrowseConnect** は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が有効な 2 つ以上の [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] インスタンスが含まれる Windows Server フェールオーバー クラスタリング (WSFC) クラスター内のサーバーを認識しません。このため、**MultiSubnetFailover** 接続文字列キーワードは、**SQLBrowseConnect** では無視されます。|  
|[SQLConnect](../../../relational-databases/native-client-odbc-api/sqlconnect.md)|**SQLConnect**は、データソース名 (DSN) または接続プロパティを介して**Applicationintent**と**MultiSubnetFailover**の両方をサポートします。|  
|[SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)|**SQLDriverConnect**では、接続文字列キーワード、接続プロパティ、または DSN を使用して**Applicationintent**と**MultiSubnetFailover**をサポートしています。|  
  
## <a name="ole-db"></a>OLE DB  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の OLE DB では、**MultiSubnetFailover** キーワードはサポートされません。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の OLE DB では、アプリケーション インテントがサポートされます。 OLE DB アプリケーションにおけるアプリケーション インテントの動作は、ODBC アプリケーションの場合と同じです (上記を参照)。  
  
 
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] をサポートするため、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client には、次の OLE DB 接続文字列キーワードが追加されています。  
  
-   **アプリケーションの目的**  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の接続文字列キーワードの詳細については、「[SQL Server Native Client での接続文字列キーワードの使用](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
 対応する接続プロパティは次のとおりです。  
  
-   **SSPROP_INIT_APPLICATIONINTENT**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB アプリケーションは、次のいずれかの方法で、アプリケーション インテントを指定できます。  
  
 **IDBInitialize:: Initialize**  
 **IDBInitialize:: initialize**は、以前に構成されたプロパティのセットを使用して、データソースを初期化し、データソースオブジェクトを作成します。 アプリケーション インテントは、プロバイダーのプロパティとして指定するか、拡張プロパティ文字列の一部として指定します。  
  
 **IDataInitialize:: GetDataSource**  
 **IDataInitialize:: GetDataSource**は、**アプリケーションインテント**キーワードを含むことができる入力接続文字列を受け取ります。  
  
 **IDBProperties::GetProperties**  
 **IDBProperties:: GetProperties**は、データソースに現在設定されているプロパティの値を取得します。  
  **Application Intent** の値は、DBPROP_INIT_PROVIDERSTRING プロパティおよび SSPROP_INIT_APPLICATIONINTENT プロパティを通じて取得できます。  
  
 **IDBProperties:: SetProperties**  
 
  **ApplicationIntent** プロパティ値を設定するには、**IDBProperties::SetProperties** を呼び出して、"**ReadWrite**" または "**ReadOnly**" の値で **SSPROP_INIT_APPLICATIONINTENT** プロパティを渡すか、または "**ApplicationIntent=ReadOnly**" または "**ApplicationIntent=ReadWrite**" を含む値で **DBPROP_INIT_PROVIDERSTRING** プロパティを渡します。  
  
 アプリケーション インテントは、**[データ リンク プロパティ]** ダイアログ ボックスの [すべて] タブの [アプリケーション インテントのプロパティ] フィールドで指定できます。  
  
 暗黙的な接続が確立された場合、その接続には、親の接続のアプリケーション インテント設定が使用されます。 同様に、同じデータ ソースから作成されたセッションはいずれも、そのデータ ソースのアプリケーション インテント設定を継承します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client 機能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [SQL Server Native Client での接続文字列キーワードの使用](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
  
