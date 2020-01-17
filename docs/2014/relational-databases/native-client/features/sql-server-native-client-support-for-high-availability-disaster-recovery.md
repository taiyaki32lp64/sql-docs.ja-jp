---
title: 高可用性、ディザスター リカバリーのための SQL Server Native Client のサポート |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 08/31/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2b06186b-4090-4728-b96b-90d6ebd9f66f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4bd73d32a58e156a3ae8577d41bbdd4725f85656
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206642"
---
# <a name="sql-server-native-client-support-for-high-availability-disaster-recovery"></a>SQL Server Native Client の HADR サポート
  このトピックでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client のサポート ([!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] で追加) について説明します。 詳細については[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]を参照してください[可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../../database-engine/listeners-client-connectivity-application-failover.md)、[作成し、可用性グループの構成&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)、[フェールオーバー クラスタ リングと AlwaysOn 可用性グループ&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md)、および[アクティブなセカンダリ。読み取り可能なセカンダリ レプリカ (AlwaysOn 可用性グループ)](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)します。  
  
 接続文字列で、特定の可用性グループの可用性グループ リスナーを指定できます。 フェールオーバーする可用性グループ内のデータベースに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client アプリケーションが接続されている場合、元の接続が切断されるため、フェールオーバー後にアプリケーションが動作を継続するには新しい接続を開く必要があります。  
  
 可用性グループ リスナーに接続しておらず、ホスト名に複数の IP アドレスが関連付けられている場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は DNS エントリに関連付けられているすべての IP アドレスを順次繰り返し処理します。 DNS サーバーが最初に返した IP アドレスがネットワーク インターフェイス カード (NIC) にバインドされていない場合、この処理に時間がかかる可能性があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client が可用性グループ リスナーに接続するとき、すべての IP アドレスに対して並列で接続を試行します。1 つの接続試行が成功すると、保留中の接続試行はすべて破棄されます。  
  
> [!NOTE]  
>  接続タイムアウト値を大きくし、接続再試行ロジックを実装することにより、アプリケーションが可用性グループに接続する確立が高まります。 また、可用性グループのフェールオーバーにより接続が失敗する可能性があるため、接続再試行ロジックを実装して、再接続されるまで、失敗した接続の再接続を試行する必要があります。  
  
## <a name="connecting-with-multisubnetfailover"></a>MultiSubnetFailover を使用した接続  
 SQL Server 2012 可用性グループ リスナーまたは SQL Server 2012 フェールオーバー クラスター インスタンスに接続する際には、必ず `MultiSubnetFailover=Yes` を指定してください。 `MultiSubnetFailover` を指定することで、SQL Server 2012 のすべての可用性グループおよびフェールオーバー クラスター インスタンスに対して高速フェールオーバーが有効化され、単一サブネットおよびマルチサブネットの AlwaysOn トポロジにおけるフェールオーバー時間が大幅に短縮されます。 マルチサブネット フェールオーバーの際には、クライアントは複数の接続を並列で試行します。 サブネット フェールオーバーの際には、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は積極的に TCP 接続を再試行します。  
  
 `MultiSubnetFailover` 接続プロパティを指定すると、アプリケーションが可用性グループまたはフェールオーバー クラスター インスタンスに配置され、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client がすべての IP アドレスに対して接続を試行することでプライマリ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス上のデータベースに接続を試みます。 ときに`MultiSubnetFailover=Yes`クライアントでは TCP 接続の試行をオペレーティング システムの既定の TCP 再送信間隔よりも高速で再試行します。 接続に対して指定します。 これにより、AlwaysOn 可用性グループまたは AlwaysOn フェールオーバー クラスター インスタンスのフェールオーバー後、再接続されるまでの時間を短縮することができます。単一サブネットとマルチサブネットの可用性グループ インスタンスおよびフェールオーバー クラスター インスタンスに適用することができます。  
  
 接続文字列キーワードの詳細については、「[SQL Server Native Client での接続文字列キーワードの使用](../applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
 接続先が可用性グループ リスナーでもフェールオーバー クラスター インスタンスでもないときに `MultiSubnetFailover=Yes` を指定すると、パフォーマンスが低下する可能性があるため、このような指定はサポートされません。  
  
 可用性グループまたはフェールオーバー クラスター インスタンス内のサーバーに接続する際には、次のガイドラインに従います。  
  
-   単一サブネットまたはマルチサブネットに接続する際には、`MultiSubnetFailover` 接続プロパティを使用します。これによって、どちらの場合にもパフォーマンスが向上します。  
  
-   可用性グループに接続するには、接続文字列でサーバーとして、可用性グループの可用性グループ リスナーを指定します。  
  
-   64 個を超える数の IP アドレスが構成された [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに接続すると、接続エラーが発生します。  
  
-   使用するアプリケーションの動作、`MultiSubnetFailover`接続プロパティが認証の種類に基づく影響を受けません。[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証、Kerberos 認証、または Windows 認証。  
  
-   `loginTimeout` の値を増やすことで、フェールオーバー時間に対応し、アプリケーションの接続試行回数を減らすことができます。  
  
-   分散トランザクションはサポートされていません。  
  
 読み取り専用のルーティングが無効である場合、次の状況では可用性グループのセカンダリ レプリカの場所には接続できません。  
  
1.  セカンダリ レプリカの場所が、接続を許可するように構成されていない。  
  
2.  アプリケーションに `ApplicationIntent=ReadWrite` (以降に解説します) が使用されているが、セカンダリ レプリカの場所が読み取り専用アクセスとして構成されている。  
  
 プライマリ レプリカが読み取り専用ワークロードを拒否するように構成されているとき、接続文字列に `ApplicationIntent=ReadOnly` が含まれていると、接続は失敗します。  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>データベース ミラーリングの使用からマルチサブネット クラスターの使用へのアップグレード  
 接続文字列に `MultiSubnetFailover` および `Failover_Partner` の接続キーワードが存在する場合、接続エラーが発生します。 また、`MultiSubnetFailover` が使用されているとき、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] から、データベース ミラーリング ペアに属していることを示すフェールオーバー パートナー応答が返された場合にも、エラーが発生します。  
  
 データベース ミラーリングを現在使用している [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client アプリケーションをマルチサブネットのシナリオにアップグレードする場合、`Failover_Partner` 接続プロパティを削除して `MultiSubnetFailover` に置き換え、それを `Yes` に設定し、接続文字列内のサーバー名を可用性グループ リスナーの名前に置き換えます。 接続文字列に `Failover_Partner` と `MultiSubnetFailover=Yes` が使用されている場合、ドライバーはエラーを生成します。 ただし、接続文字列で `Failover_Partner` および `MultiSubnetFailover=No` (または `ApplicationIntent=ReadWrite`) が使用されている場合、アプリケーションではデータベース ミラーリングが使用されます。  
  
 ドライバーは、可用性グループのプライマリ データベースでデータベース ミラーリングを使用する場合、エラーを返します`MultiSubnetFailover=Yes`は可用性グループ リスナーにはなく、プライマリ データベースに接続する接続文字列で使用します。  
  
## <a name="specifying-application-intent"></a>アプリケーション インテントの指定  
 `ApplicationIntent=ReadOnly` が指定されている場合、AlwaysOn が有効になっているデータベースにクライアントが接続するときに読み取りワークロードが要求されます。 サーバーは、接続時およびデータベース ステートメントの使用時にインテントを強制しますが、その対象は AlwaysOn 対応データベースのみです。  
  
 `ApplicationIntent` キーワードは、従来型の読み取り専用データベースに対しては動作しません。  
  
 対象の AlwaysOn データベースのワークロードの読み取りを許可または禁止することができます (これは、`ALLOW_CONNECTIONS`の句、`PRIMARY_ROLE`と`SECONDARY_ROLE`[!INCLUDE[tsql](../../../includes/tsql-md.md)]ステートメントです)。  
  
 `ApplicationIntent` キーワードを使用して、読み取り専用のルーティングを有効にします。  
  
## <a name="read-only-routing"></a>読み取り専用ルーティング  
 読み取り専用のルーティングは、データベースの読み取り専用レプリカを使用可能にする機能です。 読み取り専用のルーティングを有効にするには  
  
1.  AlwaysOn 可用性グループ リスナーに接続する必要があります。  
  
2.  `ApplicationIntent` 接続文字列キーワードは `ReadOnly` に設定する必要があります。  
  
3.  データベース管理者が可用性グループを構成し、読み取り専用のルーティングを有効にする必要があります。  
  
 読み取り専用のルーティングを使用した複数の接続が同じ読み取り専用レプリカに接続されるとは限りません。 データベース同期の変更やサーバーのルーティング構成の変更によって、クライアントが別の読み取り専用レプリカに接続される場合があります。 すべての読み取り専用要求を同じ読み取り専用レプリカに接続するには、可用性グループ リスナーを `Server` 接続文字列キーワードに渡さないでください。 代わりに、読み取り専用インスタンスの名前を指定します。  
  
 読み取り専用ルーティングでは、最初にプライマリに接続した後で読み取り可能の最適なセカンダリを探すため、プライマリに接続する場合よりも時間がかかる場合があります。 このため、ログイン タイムアウトを大きくする必要があります。  
  
## <a name="odbc"></a>ODBC  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] をサポートするために、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client には、次の 2 つの ODBC 接続文字列キーワードが追加されています。  
  
-   `ApplicationIntent`  
  
-   `MultiSubnetFailover`  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の ODBC 接続文字列キーワードの詳細については、「[SQL Server Native Client での接続文字列キーワードの使用](../applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
 対応する接続プロパティは次のとおりです。  
  
-   `SQL_COPT_SS_APPLICATION_INTENT`  
  
-   `SQL_COPT_SS_MULTISUBNET_FAILOVER`  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の ODBC 接続文字列プロパティの詳細については、「[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)」を参照してください。  
  
 `ApplicationIntent` キーワードと `MultiSubnetFailover` キーワードの機能は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ドライバーを使用する DSN の ODBC データ ソース アドミニストレーターで公開されます ([!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 以降)。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC アプリケーションは、次に示した 3 つの関数のいずれかを使用して、接続を行うことができます。  
  
|関数|説明|  
|--------------|-----------------|  
|[SQLBrowseConnect](../../native-client-odbc-api/sqlbrowseconnect.md)|`SQLBrowseConnect` から返されるサーバーの一覧に VNN は含まれません。 確認できるのはサーバーの一覧だけです。スタンドアロン サーバーであるのか、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が有効な 2 つ以上の [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] インスタンスが含まれる Windows Server フェールオーバー クラスタリング (WSFC) クラスターのうちのプライマリ サーバーまたはセカンダリ サーバーであるのかは示されません。 サーバーへの接続時にエラーが返された場合、接続先のサーバーの構成に `ApplicationIntent` 設定との互換性がないことが原因として考えられます。<br /><br /> `SQLBrowseConnect` は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が有効な 2 つ以上の [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] インスタンスが含まれる Windows Server フェールオーバー クラスタリング (WSFC) クラスター内のサーバーを認識しません。このため、`SQLBrowseConnect` 接続文字列キーワードは、`MultiSubnetFailover` では無視されます。|  
|[SQLConnect](../../native-client-odbc-api/sqlconnect.md)|`SQLConnect` は、データ ソース名 (DSN) または接続プロパティを介して、`ApplicationIntent` と `MultiSubnetFailover` の両方をサポートします。|  
|[SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md)|`SQLDriverConnect` は、接続文字列キーワード、接続プロパティ、または DSN を介して、`ApplicationIntent` と `MultiSubnetFailover` をサポートします。|  
  
## <a name="ole-db"></a>OLE DB (OLE DB)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の OLE DB では、`MultiSubnetFailover` キーワードはサポートされません。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の OLE DB では、アプリケーション インテントがサポートされます。 OLE DB アプリケーションにおけるアプリケーション インテントの動作は、ODBC アプリケーションの場合と同じです (上記を参照)。  
  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] をサポートするため、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client には、次の OLE DB 接続文字列キーワードが追加されています。  
  
-   `Application Intent`  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の接続文字列キーワードの詳細については、「[SQL Server Native Client での接続文字列キーワードの使用](../applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
 対応する接続プロパティは次のとおりです。  
  
-   `SSPROP_INIT_APPLICATIONINTENT`  
  
-   `DBPROP_INIT_PROVIDERSTRING`  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB アプリケーションは、次のいずれかの方法で、アプリケーション インテントを指定できます。  
  
 `IDBInitialize::Initialize`  
 `IDBInitialize::Initialize` は、あらかじめ構成された一連のプロパティを使用して、データ ソースを初期化し、データ ソース オブジェクトを作成します。 アプリケーション インテントは、プロバイダーのプロパティとして指定するか、拡張プロパティ文字列の一部として指定します。  
  
 `IDataInitialize::GetDataSource`  
 `IDataInitialize::GetDataSource` には、`Application Intent` キーワードを含んだ入力接続文字列を渡すことができます。  
  
 `IDBProperties::GetProperties`  
 `IDBProperties::GetProperties` は、現在データ ソースに設定されているプロパティの値を取得します。  `Application Intent` の値は、DBPROP_INIT_PROVIDERSTRING プロパティおよび SSPROP_INIT_APPLICATIONINTENT プロパティを通じて取得できます。  
  
 `IDBProperties::SetProperties`  
 `ApplicationIntent` プロパティの値を設定するには、`IDBProperties::SetProperties` を呼び出します。このとき、引数として、"`SSPROP_INIT_APPLICATIONINTENT`" または "`ReadWrite`" を値として持つ `ReadOnly` プロパティを指定するか、"`DBPROP_INIT_PROVIDERSTRING`" または "`ApplicationIntent=ReadOnly`" を値として持つ `ApplicationIntent=ReadWrite` プロパティを指定します。  
  
 アプリケーション インテントは、 **[データ リンク プロパティ]** ダイアログ ボックスの [すべて] タブの [アプリケーション インテントのプロパティ] フィールドで指定できます。  
  
 暗黙的な接続が確立された場合、その接続には、親の接続のアプリケーション インテント設定が使用されます。 同様に、同じデータ ソースから作成されたセッションはいずれも、そのデータ ソースのアプリケーション インテント設定を継承します。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Native Client の機能](sql-server-native-client-features.md)   
 [SQL Server Native Client での接続文字列キーワードの使用](../applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
  
