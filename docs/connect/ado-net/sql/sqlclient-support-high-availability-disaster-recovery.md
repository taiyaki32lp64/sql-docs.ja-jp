---
title: 高可用性、ディザスター リカバリーのための SqlClient のサポート
description: 高可用性、ディザスターリカバリー (AlwaysOn) 可用性グループの SqlClient サポートについて説明します。
ms.date: 08/15/2019
ms.assetid: 61e0b396-09d7-4e13-9711-7dcbcbd103a0
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: c60ade4c949574b589bf1e1e660564775b394527
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451997"
---
# <a name="sqlclient-support-for-high-availability-disaster-recovery"></a>高可用性、ディザスター リカバリーのための SqlClient のサポート

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

このトピックでは、高可用性、ディザスターリカバリー、AlwaysOn 可用性グループの SQL Server サポートのための Microsoft SqlClient Data Provider について説明します。  AlwaysOn 可用性グループの機能は SQL Server 2012 に追加されています。 AlwaysOn 可用性グループの詳細については、SQL Server オンライン ブックを参照してください。  
  
現在は、接続プロパティで、(高可用性、障害回復) 可用性グループ (AG) の高可用性グループ リスナーまたは SQL Server 2012 フェールオーバー クラスター インスタンスを指定できます。 SqlClient アプリケーションを AlwaysOn データベースに接続しているときにフェールオーバーが発生した場合、元の接続は切断され、アプリケーションではフェールオーバー後に処理を続行するために新しい接続を開く必要があります。  
  
可用性グループ リスナーまたは SQL Server 2012 フェールオーバー クラスター インスタンスに接続していない場合、複数の IP アドレスがホスト名に関連付けられていると、SqlClient は、DNS エントリに関連付けられたすべての IP アドレスを順に反復処理します。 DNS サーバーが最初に返した IP アドレスがネットワーク インターフェイス カード (NIC) にバインドされていない場合、この処理に時間がかかる可能性があります。 可用性グループ リスナーまたは SQL Server 2012 フェールオーバー クラスター インスタンスに接続する場合、SqlClient ですべての IP アドレスへの接続確立を並列実行しようとして、接続試行が成功すると、ドライバーは保留状態の接続試行を破棄します。  
  
> [!NOTE]
>  接続タイムアウト値を大きくし、接続再試行ロジックを実装することにより、アプリケーションが可用性グループに接続する確立が高まります。 また、フェールオーバーにより接続が失敗する可能性があるため、接続再試行ロジックを実装して、再接続されるまで、失敗した接続の再接続を試行する必要があります。  
  
次の接続プロパティは、SQL Server 用の Microsoft SqlClient Data Provider でサポートされています。  
  
- `ApplicationIntent`  
  
- `MultiSubnetFailover`  
  
次のようにして、これらの接続文字列キーワードをプログラムで変更できます。  
  
- <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.ApplicationIntent%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A>  
  
## <a name="connecting-with-multisubnetfailover"></a>MultiSubnetFailover を使用した接続  
SQL Server 2012 可用性グループ リスナーまたは SQL Server 2012 フェールオーバー クラスター インスタンスに接続する際には、必ず `MultiSubnetFailover=True` を指定してください。 `MultiSubnetFailover` を指定することで、SQL Server 2012 のすべての可用性グループとフェールオーバー クラスター インスタンスに対して高速フェールオーバーが有効化され、単一サブネットおよびマルチサブネットの AlwaysOn トポロジにおけるフェールオーバー時間が大幅に短縮されます。 マルチサブネット フェールオーバーの際には、クライアントは複数の接続を並列で試行します。 サブネット フェールオーバーの際には、積極的に TCP 接続を再試行します。  
  
`MultiSubnetFailover` 接続プロパティは、アプリケーションが可用性グループまたは SQL Server 2012 フェールオーバー クラスター インスタンスで展開されていること、およびすべての IP アドレスへの接続を試行することで SqlClient がプライマリ SQL Server インスタンスのデータベースに接続を試行することを示します。 接続に対して `MultiSubnetFailover=True` を指定した場合、クライアントは、オペレーティング システムの既定の TCP 再送信間隔より短い間隔で TCP 接続を再試行します。 これにより、AlwaysOn 可用性グループまたは AlwaysOn フェールオーバー クラスター インスタンスのフェールオーバー後、再接続されるまでの時間を短縮することができます。単一サブネットとマルチサブネットの可用性グループ インスタンスおよびフェールオーバー クラスター インスタンスに適用することができます。  
  
SqlClient の接続文字列キーワードの詳細については、「<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>」を参照してください。  
  
可用性グループ リスナーまたは SQL Server 2012 フェールオーバー クラスター インスタンス以外の何かに接続する場合に `MultiSubnetFailover=True` を指定すると、パフォーマンスに負の影響が及ぶ可能性があるため、サポートされていません。  
  
可用性グループまたは SQL Server 2012 フェールオーバー クラスター インスタンス内のサーバーに接続する際には、次のガイドラインに従います。  
  
- 単一サブネットまたはマルチサブネットに接続する際には、`MultiSubnetFailover` 接続プロパティを使用します。これによって、どちらの場合にもパフォーマンスが向上します。  
  
- 可用性グループに接続するには、接続文字列でサーバーとして、可用性グループの可用性グループ リスナーを指定します。  
  
- 64 個を超える数の IP アドレスが構成された SQL Server インスタンスに接続すると、接続エラーが発生します。  
  
- `MultiSubnetFailover` 接続プロパティを使用するアプリケーションの動作は、認証の種類 (SQL Server 認証、Kerberos 認証、または Windows 認証) の影響を受けません。  
  
- フェールオーバー時間に合わせて、アプリケーションの接続再試行回数を減らすには、`Connect Timeout` の値を大きくします。  
  
- 分散トランザクションはサポートされていません。  
  
 読み取り専用のルーティングが無効である場合、次の状況ではセカンダリ レプリカの場所には接続できません。  
  
- セカンダリ レプリカの場所が、接続を許可するように構成されていない。  
  
- アプリケーションに `ApplicationIntent=ReadWrite` (以降に解説します) が使用されているが、セカンダリ レプリカの場所が読み取り専用アクセスとして構成されている。  
  
<xref:Microsoft.Data.SqlClient.SqlDependency> は、読み取り専用のセカンダリレプリカではサポートされていません。  
  
プライマリ レプリカが読み取り専用ワークロードを拒否するように構成されているとき、接続文字列に `ApplicationIntent=ReadOnly` が含まれていると、接続は失敗します。  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>データベース ミラーリングからマルチサブネット クラスターの使用へのアップグレード  
接続文字列に `MultiSubnetFailover` と `Failover Partner` の接続キーワードが存在する場合、または `MultiSubnetFailover=True` と TCP 以外のプロトコルが使用されている場合は、接続エラー (<xref:System.ArgumentException>) が発生します。 また、`MultiSubnetFailover` が使用されているとき、SQL Server から、データベース ミラーリング ペアに属していることを示すフェールオーバー パートナー応答が返された場合にも、エラー (<xref:Microsoft.Data.SqlClient.SqlException>) が発生します。  
  
データベース ミラーリングを現在使用している SqlClient アプリケーションをマルチサブネットのシナリオにアップグレードする場合、`Failover Partner` 接続プロパティを削除して `MultiSubnetFailover` に置き換え、それを `True` に設定し、接続文字列内のサーバー名を可用性グループ リスナーの名前に置き換えます。 接続文字列に `Failover Partner` と `MultiSubnetFailover=True` が使用されている場合、ドライバーはエラーを生成します。 ただし、接続文字列で `Failover Partner` および `MultiSubnetFailover=False` (または `ApplicationIntent=ReadWrite`) が使用されている場合、アプリケーションではデータベース ミラーリングが使用されます。  
  
AG のプライマリ データベースでデータベース ミラーリングが使用されている場合、また、可用性グループ リスナーの代わりにプライマリ データベースに接続されている接続文字列で `MultiSubnetFailover=True` が使用されている場合、ドライバーからエラーが返されます。  
  
## <a name="specifying-application-intent"></a>アプリケーションの意図を指定する  
`ApplicationIntent=ReadOnly` が指定されている場合、AlwaysOn が有効になっているデータベースにクライアントが接続するときに読み取りワークロードが要求されます。 サーバーは、接続時およびデータベース ステートメントの使用時にインテントを強制しますが、その対象は AlwaysOn 対応データベースのみです。  
  
`ApplicationIntent` キーワードは、従来型の読み取り専用データベースに対しては動作しません。  
  
対象の AlwaysOn データベースのワークロードの読み取りを許可または禁止することができます (これは、`PRIMARY_ROLE` と `SECONDARY_ROLE`Transact SQL ステートメントの `ALLOW_CONNECTIONS` 句を使用して行います)。  
  
`ApplicationIntent` キーワードを使用して、読み取り専用のルーティングを有効にします。  
  
## <a name="read-only-routing"></a>読み取り専用ルーティング  
読み取り専用のルーティングは、データベースの読み取り専用レプリカを使用可能にする機能です。 読み取り専用のルーティングを有効にするには  
  
- AlwaysOn 可用性グループ リスナーに接続する必要があります。  
  
- `ApplicationIntent` 接続文字列キーワードは `ReadOnly` に設定する必要があります。  
  
- データベース管理者が可用性グループを構成し、読み取り専用のルーティングを有効にする必要があります。  
  
読み取り専用のルーティングを使用した複数の接続が同じ読み取り専用レプリカに接続されるとは限りません。 データベース同期の変更やサーバーのルーティング構成の変更によって、クライアントが別の読み取り専用レプリカに接続される場合があります。 すべての読み取り専用要求を同じ読み取り専用レプリカに接続するには、可用性グループ リスナーを `Data Source` 接続文字列キーワードに渡さないでください。 代わりに、読み取り専用インスタンスの名前を指定します。  
  
読み取り専用ルーティングでは、最初にプライマリに接続した後で読み取り可能の最適なセカンダリを探すため、プライマリに接続する場合よりも時間がかかる場合があります。 このため、ログイン タイムアウトを大きくする必要があります。  
  
## <a name="next-steps"></a>次の手順
- [SQL Server の機能と ADO.NET](sql-server-features-adonet.md)
