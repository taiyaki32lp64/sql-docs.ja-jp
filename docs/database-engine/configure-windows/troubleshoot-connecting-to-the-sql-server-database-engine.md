---
title: SQL Server データベース エンジンへの接続のトラブルシューティング | Microsoft Docs
ms.custom: sqlfreshmay19
ms.date: 11/25/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: troubleshooting
helpviewer_keywords:
- troubleshooting, connecting to Database Engine
- connecting to Database Engine, troubleshooting
ms.assetid: 474c365b-c451-4b07-b636-1653439f4b1f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b2394fc73483b78e5e90a4ccffa9ce45205dc237
ms.sourcegitcommit: 02449abde606892c060ec9e9e9a85a3f49c47c6c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74542314"
---
# <a name="troubleshoot-connecting-to-the-sql-server-database-engine"></a>SQL Server データベース エンジンへの接続のトラブルシューティング
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、シングル サーバーで SQL Server データベース エンジンのインスタンスに接続できないときに使用するトラブルシューティング技法を紹介しています。

>[!NOTE]
>他のシナリオについては、次を参照してください。
>- [可用性グループ リスナー](../availability-groups/windows/listeners-client-connectivity-application-failover.md)
>- [フェールオーバー クラスター インスタンス](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)

ここにある手順は、最も頻繁に発生する問題の順に並べられているわけではありません。 最も基本的な問題からより複雑な問題の順に並べられています。 TCP/IP プロトコルを利用し、別のコンピューターから SQL Server インスタンスに接続する場合を想定しています (それが最も一般的な状況です)。

これらの指示は、`Error Number: 11001 (or 53), Severity: 20, State: 0` のような "**サーバーに接続**" エラーをトラブルシューティングするときに役立ちます。 エラー メッセージの例を次に示します。

> `A network-related or instance-specific error occurred while establishing a connection to SQL Server. The server was not found or was not accessible. Verify that the instance name is correct and that SQL Server is configured to allow remote connections.`
>
> `(provider: Named Pipes Provider, error: 40 - Could not open a connection to SQL Server) (Microsoft SQL Server, Error: 53)`
>
> `(provider: TCP Provider, error: 0 - No such host is known.) (Microsoft SQL Server, Error: 11001)`

このエラーは通常、クライアントで SQL Server インスタンスを見つけることができないことを意味します。 これは通常、次の中で少なくとも 1 つに問題がある場合に発生します。

- SQL Server をホストするコンピューターの名前
- インスタンスによって正しい IP が解決されない
- TCP ポート番号が正しく指定されていない

> [!TIP]
> 対話型のトラブルシューティング ページは、「[Solving Connectivity errors to SQL Server](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server)」 (SQL Server への接続エラーの解決) の[!INCLUDE[msCoName_md](../../includes/msconame-md.md)] カスタマー サポート サービスから利用できます。

### <a name="not-included"></a>対象外の情報

- このトピックには、SSPI エラーに関する情報が含まれていません。 SSPI エラーについては、「 ["SSPI コンテキストを生成できません" エラー メッセージのトラブルシューティング方法](https://support.microsoft.com/kb/811889)」を参照してください。
- このトピックには、Kerberos エラーに関する情報が含まれていません。 ヘルプが必要な場合、「 [Microsoft® Kerberos Configuration Manager for SQL Server®](https://www.microsoft.com/download/details.aspx?id=39046)」をご覧ください。
- このトピックには、SQL Azure 接続に関する情報が含まれていません。 ヘルプについては、「[Troubleshooting connectivity issues with Microsoft Azure SQL Database](/azure/sql-database/troubleshoot-connectivity-issues-microsoft-azure-sql-database)」 (Microsoft Azure SQL Database の接続に関する問題のトラブルシューティング) を参照してください。

## <a name="get-instance-name-from-configuration-manger"></a>構成マネージャーからインスタンス名を取得する

SQL Server インスタンスをホストするサーバーで、インスタンス名を検証します。 [SQL Server 構成マネージャー](../../relational-databases/sql-server-configuration-manager.md)を使用します。

構成マネージャーは、SQL Server がインストールされているコンピューターに自動的にインストールされます。 構成マネージャーの起動に関する指示は、SQL Server と Windows のバージョンによって多少異なります。 バージョン固有の詳細については、「[SQL Server 構成マネージャー](../../relational-databases/sql-server-configuration-manager.md)」を参照してください。)

1. SQL Server のインスタンスをホストしているコンピューターにサインインします。
1. SQL Server 構成マネージャーを起動します。
1. 左側のウィンドウで、 **[SQL Server サービス]** を選択します。
1. 右側のウィンドウで、データベース エンジンのインスタンスの名前を確認します。

   - `SQL SERVER (MSSQLSERVER)` は、SQL Server の既定のインスタンスを示します。 既定のインスタンスの名前は `<computer name>` です。
   - `SQL SERVER (<instance name>)` は、SQL Server の名前付きインスタンスを示します。 名前インスタンスの名前は `<computer name>\<instance name>` です。

## <a name="verify---the-instance-is-running"></a>検証 - インスタンスが実行されている

インスタンスが実行されていることを確認するには、構成マネージャーで SQL Server インスタンスの横にある記号を見ます。

- 緑色の矢印は、インスタンスが実行されていることを示します。
- 赤色の四角形は、インスタンスが停止していることを示します。

インスタンスが停止している場合、インスタンスを右クリックし、 **[開始]** をクリックします。 サーバー インスタンスが起動し、インジケーターが緑の矢印になります。

## <a name = "startbrowser"></a> 検証 - SQL Server Browser サービスが実行されている

名前付きインスタンスに接続するには、SQL Server Browser サービスが実行されている必要があります。 構成マネージャーで、**SQL Server Browser** サービスを見つけ、それが実行されていることを確認します。 実行されていない場合、起動します。 既定のインスタンスの場合、SQL Server Browser サービスは必要ありません。

SQL Server の既定のインスタンスには、SQL Server Browser サービスは必要ありません。

## <a name="testing-a-local-connection"></a>ローカル接続をテストする

別のコンピューターから接続する場合の問題を解決する前に、SQL Server を実行しているコンピューターにローカル インストールされているクライアント コンピューターから接続できるか最初にテストします。 ローカル接続では、ネットワークやファイアウォールの問題が回避されます。 

この手順では、SQL Server Management Studio が使用されます。 Management Studio をインストールしていない場合、「[SQL Server Management Studio (SSMS) のダウンロード](../../ssms/download-sql-server-management-studio-ssms.md)」を参照してください。 Management Studio をインストールできない場合、`sqlcmd.exe` ユーティリティで接続をテストできます。 `sqlcmd.exe` はデータベース エンジンと共にインストールされています。 `sqlcmd.exe`の詳細については、「 [sqlcmd Utility](../../tools/sqlcmd-utility.md)」を参照してください。

1. SQL Server にアクセスする権限が与えられているログインを利用し、SQL Server がインストールされているコンピューターにサインインします。 (インストール中、SQL Server は、最低 1 つのログインが SQL Server 管理者として指定されることを必要とします。 管理者を知らない場合、「 [システム管理者がロックアウトされた場合の SQL Server への接続](connect-to-sql-server-when-system-administrators-are-locked-out.md)」を参照してください。)
1. [スタート] ページで、「 **SQL Server Management Studio**」と入力します。あるいは、以前のバージョンの Windows の場合、[スタート] メニューで、 **[すべてのプログラム]** をポイントし、 **[Microsoft SQL Server]** をポイントし、 **[SQL Server Management Studio]** をクリックします。
1. **[サーバーへの接続]** ダイアログ ボックスの **[サーバーの種類]** ボックスの一覧で、 **[データベース エンジン]** を選択します。 **[認証]** ボックスで、 **[Windows 認証]** を選択します。 **[サーバー名]** ボックスに、次の接続タイプのいずれかを入力します。

   |接続先|種類|例|
   |:-----------------|:---------------|:-----------------|
   |既定のインスタンス|`<computer name>`|`ACCNT27`|
   |名前付きインスタンス|`<computer name\instance name>`|`ACCNT27\PAYROLL`|

   > [!NOTE]
   > 同じコンピューターのクライアント コンピューターから SQL Server に接続するとき、共有メモリ プロトコルが使用されます。 共有メモリは一種のローカルの名前付きパイプであり、パイプに関するエラーに遭遇することがあります。

   この時点でエラーが発生する場合、続行する前に解決する必要があります。 問題にはさまざまな要因が考えられます。 ログインの接続が認証されないことがあります。 既定のデータベースがないことがあります。

   > [!NOTE]
   > クライアントに渡されるエラー メッセージの一部は、問題を解決するために十分な情報を意図的に与えません。 これはセキュリティ機能であり、SQL Server に関する情報を攻撃者に与えることを回避します。 エラーに関する完全な情報は、SQL Server エラー ログを調べてください。 そこに詳細があります。 

1. エラー `18456 Login failed for user` を受け取った場合、オンライン ブックのトピック、[MSSQLSERVER_18456](../../relational-databases/errors-events/mssqlserver-18456-database-engine-error.md) にエラー コードに関する追加情報があります。 また、Aaron Bertrand のブログで、非常に広範囲なエラー コード リストが紹介されています ( [エラー 18456 のトラブルシューティング](https://sqlblog.org/2011/01/14/troubleshooting-error-18456))。 オブジェクト エクスプローラーの管理セクションで、SSMS (接続できる場合) のエラー ログを見ることができます。 接続できない場合、Windows のメモ帳プログラムでエラー ログを表示できます。 既定の場所はバージョンによって異なり、セットアップ中に変更できます。 [!INCLUDE[ssSQL15_md](../../includes/sssqlv15-md.md)] の既定の場所は `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Log\ERRORLOG`です。 

1. 共有メモリで接続できない場合、TCP による接続をテストしてください。 名前の前に `tcp:` を指定すると、TCP 接続を強制できます。 次に例を示します。

   |接続先:|型:|例:|
   |-----------------|---------------|-----------------|
   |既定のインスタンス|`tcp:<computer name>`|`tcp:ACCNT27`|
   |名前付きインスタンス|`tcp:<computer name/instance name>`|`tcp:ACCNT27\PAYROLL`|

1. 共有メモリで接続できても、TCP で接続できない場合、TCP 問題を修正する必要があります。 TCP が有効になっていない可能性が高いです。 TCP を有効にするには、前述の「[プロトコルを有効にする](#enableprotocols)」の手順を参照してください。

1. 管理者アカウント以外のアカウントで接続する場合、管理者として接続できたら、(クライアント アプリケーションで使用される) Windows 認証ログインまたは SQL Server 認証ログインによる接続をもう一度試してください。

## <a name="get-the-ip-address-of-the-server"></a>サーバーの IP アドレスを取得する

SQL Server のインスタンスをホストしているコンピューターに IP アドレスを取得します。

1. [スタート] メニューの **[ファイル名を指定して実行]** をクリックします。 **[ファイル名を指定して実行]** ウィンドウで、「**cmd**」と入力し、 **[OK]** をクリックします。
1. コマンド プロンプト ウィンドウで「`ipconfig`」と入力し、Enter キーを押します。 **IPv4** アドレスと **IPv6** アドレスを書き留めます。

  >SQL Server では、IP バージョン 4 プロトコルまたは IP バージョン 6 プロトコルで接続できます。 ネットワークでは、一方または両方を許可できます。 ほとんどの人が **IPv4** アドレスのトラブルシューティングから始めます。 こちらの方が短く、入力が簡単です。

## <a name = "getTCP"></a>SQL Server インスタンス TCP ポートを取得する

ほとんどの場合、TCP プロトコルを使用して別のコンピューターからデータベース エンジンに接続します。

1. SQL Server を実行するコンピューターで SQL Server Management Studio を使用し、SQL Server のインスタンスに接続します。 オブジェクト エクスプローラーで、 **[管理]** を展開し、 **[SQL Server ログ]** を展開し、現在のログをダブルクリックします。
2. ログ ビューアーで、ツールパーの **[フィルター]** ボタンをクリックします。 **[テキストを含むメッセージ]** ボックスに「`server is listening on`」と入力し、 **[フィルターの適用]** をクリックし、 **[OK]** をクリックします。
3. `Server is listening on [ 'any' <ipv4> 1433]` のようなメッセージが表示されるはずです。 

このメッセージは、SQL Server のこのインスタンスがこのコンピューター (IP バージョン 4) ですべての IP アドレスを受け付け、TCP ポート 1433 で待機していることを示します。 (通常、TCP ポート 1433 は、データベース エンジンまたは SQL Server の既定のインスタンスで使用されるポートです。 ポートを使用できる SQL Server のインスタンスは 1 つだけです。そのため、SQL Server のインスタンスが複数インストールされている場合、一部のインスタンスは他のポート番号を使用する必要があります。)接続しようとしている [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] インスタンスに使用されているポート番号を記録しておきます。

  > [!NOTE]
  > `IP address 127.0.0.1` がおそらく表示されます。 これはループバック アダプター アドレスと呼ばれています。 同じコンピューター上のプロセスのみを接続に使用できます。 トラブルシューティングに役立ちますが、これを利用し、別のコンピューターから接続することはできません。

## <a name = "enableprotocols"></a>プロトコルを有効にする

SQL Server の一部のインストールでは、管理者が構成マネージャーを利用して有効にしない限り、別のコンピューターからデータベース エンジンへの接続が有効になりません。 別のコンピューターからの接続を有効にする:

1. 前述のように SQL Server 構成マネージャーを開きます。
1. 構成マネージャーを利用し、左ペインで、 **[SQL Server ネットワークの構成]** を展開し、接続先とする SQL Server インスタンスを選択します。 右ペインに、利用可能な接続プロトコルが一覧表示されます。 通常、共有メモリが有効になっています。 これは同じコンピューターからのみ利用できます。そのため、ほとんどのインストールで、共有メモリを有効にしたままにします。 別のコンピューターから SQL Server に接続するには、通常、TCP/IP を使用します。 TCP/IP が有効ではない場合、 **[TCP/IP]** を右クリックし、 **[有効化]** をクリックします。
1. プロトコルの有効化設定を変更した場合、データベース エンジンを再起動します。 左ペインで、 **[SQL Server のサービス]** を接続します。 右ペインで、データベース エンジンのインスタンスを右クリックし、 **[再起動]** をクリックします。

## <a name="testTCPIP"></a>TCP/IP 接続をテストする

TCP/IP を使用して SQL Server に接続するには、Windows が接続を確立できることが必須となります。 `ping` ツールを使用し、TCP をテストします。

1. [スタート] メニューの **[ファイル名を指定して実行]** をクリックします。 **[ファイル名を指定して実行]** ウィンドウで、「 **cmd**」と入力し、 **[OK]** をクリックします。 
1. コマンド プロンプト ウィンドウで、「 `ping <ip address>` 」と入力し、SQL Server を実行しているコンピューターの IP アドレスを入力します。 次に例を示します。

    - IPv4: `ping 192.168.1.101`
    - IPv6: `ping fe80::d51d:5ab5:6f09:8f48%11`

1. ネットワークが正しく構成されている場合、`ping` により `Reply from <IP address>` とそれに続くいくつかの追加情報が返されます。 `ping` で `Destination host unreachable` または `Request timed out` が返される場合、TCP/IP は正しく構成されていません。 この段階でのエラーは、クライアント コンピューター、サーバー コンピューター、ネットワーク (ルーターなど) に関する問題を示唆します。 ネットワークの問題のトラブルシューティングについては、「TCP/IP の問題に関する高度なトラブルシューティング」 (/windows/client-management/troubleshoot-tcpip) を参照してください。
1. 次に、IP アドレスによる ping テストに成功した場合、コンピューター名を TCP/IP アドレスに解決できることをテストします。 クライアント コンピューターのコマンド プロンプト ウィンドウで、「 `ping` 」と入力し、SQL Server を実行しているコンピューターのコンピューター名を入力します。 たとえば、`ping newofficepc` のように指定します。 
1. IP アドレスへの `ping` が成功したが、コンピューターへの `ping` で `Destination host unreachable` または `Request timed out` が返された場合、クライアント コンピューターにキャッシュされている名前解決情報が古くなっている可能性があります。 「 `ipconfig /flushdns` 」と入力し、DNS (動的な名前解決) キャッシュを消去します。 次に、もう一度、名前でコンピューターに ping を実行します。 DNS キャッシュが空の場合、クライアント コンピューターはサーバー コンピューターの IP アドレスに関する最新情報がないか確認します。 
1. ネットワークが正しく構成されている場合、`ping` により `Reply from <IP address>` とそれに続くいくつかの追加情報が返されます。 IP アドレスによるサーバー コンピューターへの ping に成功するが、コンピューター名で ping したとき、`Destination host unreachable.` や `Request timed out.` のようなエラーが発生した場合、名前解決が正しく構成されていません。 (詳細については、前述の 2006 年の記事、「[How to Troubleshoot Basic TCP/IP Problems](https://support.microsoft.com/kb/169790)」 (基本的 TCP/IP 問題のトラブルシューティング方法) を参照してください。)名前解決が成功しなくても、SQL Server に接続できますが、コンピューター名を IP アドレスに解決できない場合、IP アドレスを指定して接続を行う必要があります。 名前解決は後で修正できます。

## <a name = "openport"></a>ファイアウォールでポートを開く

既定では、Windows ファイアウォールが有効になっており、別のコンピューターからの接続がブロックされます。 別のコンピューターから TCP/IP で接続するには、SQL Server コンピューターで、データベース エンジンで使用される TCP ポートへの接続を許可するようにファイアウォールを構成する必要があります。 既定のインスタンスは、既定で TCP ポート 1433 で待ち受けます。 名前付きインスタンスを使用している場合、または既定のインスタンス ポートを変更した場合は、[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] の TCP ポートが別のポートでリッスンしている可能性があります。 「[SQL Server インスタンス TCP ポートを取得する](#getTCP)」を参照してください。

名前付きインスタンスまたは TCP ポート 1433 以外のポートに接続する場合、SQL Server Browser サービスの UDP ポート 1434 を開く必要もあります。 Windows ファイアウォールでポートを開くための詳細な手順については、「 [データベース エンジン アクセスを有効にするための Windows ファイアウォールを構成する](configure-a-windows-firewall-for-database-engine-access.md)」を参照してください。

## <a name="test-the-connection"></a>接続をテストする

同じコンピューターで TCP を利用して接続できたら、クライアント コンピューターからの接続を試します。 理論的にはあらゆるクライアント コンピューターを使用できますが、余計に複雑になることを避けるために、クライアントに SQL Server Management ツールをインストールし、SQL Server Management Studio の使用を試します。

1. クライアント コンピューターで、SQL Server Management Studio を利用し、IP アドレスと TCP ポート番号による接続を試します。<IP アドレス.ポート番号> の形式になります。 たとえば、「 `192.168.1.101,1433` 」のように入力します。 この接続に失敗する場合、次のいずれかの問題が想定されます。

   - IP アドレスの `ping` は失敗し、一般的な TCP 構成問題を示します。 「[TCP/IP 接続をテストする](#testTCPIP)」セクションに戻ってください。
   - SQL Server が TCP プロトコルで待機 (リスニング) していません。 「[プロトコルを有効にする](#enableprotocols)」セクションに戻ってください。
   - SQL Server が指定したポート以外で待機しています。 「[TCP ポート番号を取得する](#getTCP)」セクションに戻ってください。
   - SQL Server の TCP ポートがファイアウォールによりブロックされています。 「[ファイアウォールでポートを開く](#open-a-port-in-the-firewall)」セクションに戻ってください。

2. IP アドレスとポート番号で接続できたら、ポート番号なしで IP アドレスによる接続を試してください。 既定のインスタンスについては、IP アドレスだけを使用します。 名前付きインスタンスの場合、IP アドレスとインスタンス名を使用し、`192.168.1.101\<instance name>` のように「IP アドレス\インスタンス名」の形式にします。これでうまくいかない場合、次のいずれかの問題が考えられます。

   - 既定のインスタンスに接続している場合、TCP ポート 1433 以外のポートで待機している可能性があります。クライアントは、正しいポート番号への接続を試行していません。
   - 名前付きインスタンスに接続している場合、ポート番号がクライアントに返されていません。

   この 2 つの問題は SQL Server Browser サービスに関連します。SQL Server Browser サービスはポート番号をクライアントに与えます。 解決策は次のとおりです。

   - SQL Server Browser サービスを開始します。 SQL Server 構成マネージャーでブラウザーを起動する方法については、[こちら](#startbrowser)をご覧ください。
   - SQL Server Browser サービスがファイアウォールによりブロックされています。 ファイアウォールで UDP ポート 1434 を開きます。 「[ファイアウォールでポートを開く](#open-a-port-in-the-firewall)」セクションに戻ってください。 TCP ポートではなく UDP ポートを開いていることを確認します。
   - UDP ポート 1434 情報がルーターによりブロックされています。 UDP (ユーザー データグラム プロトコル) 通信は、ルーターを通過するように設計されていません。 それにより、ネットワークが優先度の低いトラフィックでいっぱいになることがありません。 UDP トラフィックを転送するようにルーターを構成できることがあります。あるいは、接続するとき、常にポート番号を指定するように設定できます。
   - クライアント コンピューターで Windows 7 または Windows Server 2008 (あるいは、もっと最近のオペレーティング システム) が使用されている場合、クライアントのオペレーティング システムが UDP トラフィックを破棄することがあります。サーバーからの応答が、クエリされたアドレスとは異なる IP アドレスから返されるためです。 これは "厳密でないソース マッピング" をブロックするセキュリティ機能です。 詳細については、「**複数のサーバー IP アドレス**」セクションを参照してください (ブックス オンライン トピック「[タイムアウト発生時のトラブルシューティング](https://msdn.microsoft.com/library/ms190181.aspx)」)。 これは SQL Server 2008 R2 の記事ですが、原則は同じです。 正しい IP アドレスを使用するようにクライアントを構成できることがあります。あるいは、接続するとき、常にポート番号を指定するように設定できます。

3. IP アドレス (あるいは、名前付きインスタンスの IP アドレスとインスタンス名) で接続できたら、コンピューター名 (あるいは、名前付きインスタンスのコンピューター名とインスタンス名) による接続を試してください。 TCP/IP 接続を強制するには、コンピューター名の前に `tcp:` を指定します。 たとえば、 `ACCNT27`という名前のコンピューターで既定のインスタンスを使用する場合、 `tcp:ACCNT27` を使用します。そのコンピューターで `PAYROLL`という名前のインスタンスを使用する場合、 `tcp:ACCNT27\PAYROLL` を使用します。IP アドレスで接続できてもコンピューター名で接続できない場合、名前解決の問題があります。 「**TCP/IP 接続をテストする**」セクションの 4 に戻ってください。

4. TCP を強制してコンピューター名で接続できたら、TCP を強制せずにコンピューター名による接続を試してください。 たとえば、既定のインスタンスの場合、`CCNT27` のような名前だけを使用します。名前付きインスタンスの場合、`ACCNT27\PAYROLL` のように、コンピューター名とインスタンス名を使用します。TCP を強制すると接続できるが、強制しないと接続できない場合、クライアントで別のプロトコルが使用されている可能性があります (名前付きパイプなど)。

    1. クライアント コンピューターで、SQL Server 構成マネージャーを使用し、左ペインで **[SQL Native Client** *<バージョン>* **の構成]** を展開し、 **[クライアント プロトコル]** を選択します。
    2. 右ペインで、TCP/IP が有効になっていることを確認します。 TCP/IP が無効になっている場合、 **[TCP/IP]** を右クリックし、 **[有効化]** をクリックします。
    3. TCP/IP のプロトコル順序が名前付きパイプ (または、古いバージョンでは VIA) プロトコルより小さい数値になっていることを確認します。 一般的に、共有メモリを 1 に、TCP/IP を 2 のままにしておきます。 共有メモリは、クライアントと SQL Server が同じコンピューターで実行されている場合にのみ使用されます。 有効なプロトコルはすべて、その中の 1 つが成功するまで試されます。ただし、同じコンピューターに接続するのでなければ、共有メモリはスキップされます。