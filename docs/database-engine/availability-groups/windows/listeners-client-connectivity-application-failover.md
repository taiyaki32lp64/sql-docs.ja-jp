---
title: 可用性グループ リスナーに接続する
description: フェールオーバー前後の、Always On 可用性グループ リスナーへの接続に関する情報が含まれています。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- read-only routing
- read-intent connections [AlwaysOn Availability Groups]
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 76fb3eca-6b08-4610-8d79-64019dd56c44
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e2116c0a587b82f289f5dba17968f3eb42e47c05
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228242"
---
# <a name="connect-to-an-always-on-availability-group-listener"></a>Always On 可用性グループ リスナーに接続する 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  この記事では、[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] クライアント接続とアプリケーションのフェールオーバー機能に関する考慮事項について説明します。  
  
> [!NOTE]  
>  通常のリスナー構成では、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントまたは PowerShell コマンドレットを使用して最初の可用性グループ リスナーを簡単に作成できます。 詳細については、このトピックの「 [関連タスク](#RelatedTasks)」を参照してください。  
  
  
##  <a name="AGlisteners"></a> 可用性グループ リスナー  
 可用性グループ リスナーを作成することによって、特定の可用性グループのデータベースへのクライアント接続が可能になります。 可用性グループ リスナーは、Always On 可用性グループのプライマリ レプリカまたはセカンダリ レプリカ内のデータベースにアクセスするためにクライアントが接続できる仮想ネットワーク名 (VNN) です。 可用性グループ リスナーによって、クライアントは、接続先の SQL Server の物理インスタンス名が不明な場合でも、可用性レプリカに接続できます。  現在のプライマリ レプリカの現在の場所に接続するために、クライアント接続文字列を変更する必要はありません。  
  
 可用性グループ リスナーには、ドメイン ネーム システム (DNS) のリスナー名、リスナー ポート指定、および 1 つ以上の IP アドレスが含まれます。 可用性グループ リスナーでは、TCP プロトコルのみがサポートされています。  リスナーの DNS 名も、ドメインおよび NetBIOS 内で固有であることが必要です。  作成された新しい可用性グループ リスナーは、関連付けられた仮装ネットワーク名 (VNN)、仮想 IP (VIP)、可用性グループの依存関係と共に、クラスター内のリソースになります。 クライアントは、DNS を使用して VNN を複数の IP アドレスに解決した後、接続要求が成功するかタイムアウトするまで、それぞれのアドレスに接続を試みます。  
  
 1 つ以上の[読み取り可能なセカンダリ レプリカ](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)に対して読み取り専用のルーティングが構成されている場合、プライマリ レプリカに対する読み取りを目的としたクライアント接続は読み取り可能なセカンダリ レプリカにリダイレクトされます。 さらに、SQL Server の 1 つのインスタンスでプライマリ レプリカがオフラインになり、SQL Server の他のインスタンスで新しいプライマリ レプリカがオンラインになると、可用性グループ リスナーによって、クライアントは新しいプライマリ レプリカに接続できます。  
  
 可用性グループ リスナーに関する必須情報については、「 [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)」を参照してください。  
  
  
##  <a name="AGlConfig"></a> 可用性グループ リスナーの構成  
 可用性グループ リスナーは、以下のものによって定義されます。  
  
 一意の DNS 名  
 これは仮想ネットワーク名 (VNN) とも呼ばれています。 DNS ホスト名に対する Active Directory の名前付け規則が適用されます。 詳細については、サポート技術情報の「 [Active Directory でのコンピューター、ドメイン、サイト、および OU の名前付け規則](https://support.microsoft.com/kb/909264) 」を参照してください。  
  
 1 つ以上の仮想 IP アドレス (VIP)  
 VIP は、可用性グループがフェールオーバーする 1 つ以上のサブネットに対して構成されます。  
  
 IP アドレスの構成  
 特定の可用性グループ リスナーの IP アドレスには、動的ホスト構成プロトコル (DHCP) または 1 つ以上の静的 IP アドレスを使用します。  
  
-   動的ホスト構成プロトコル (DHCP)  
  
     可用性グループが 1 つのサブネット上にある場合、DHCP を使用するようにすべての可用性グループ リスナーの IP アドレスを構成できます。 実稼動前の環境では、DHCP を使用すると、別のサブネット上のリモート サイトに対するディザスター リカバリーを必要としない可用性グループを簡単にセットアップできます。 ただし、実稼働環境では DHCP と可用性グループ リスナーを組み合わせて使用しないでください。 これは、ダウンタイムが発生した場合に DHCP の IP リース期限が切れると、リスナーの DNS 名に関連付けられている新しい DHCP IP アドレスの再登録に余分な時間がかかるためです。 余分な時間がかかると、クライアント接続に失敗します。  
  
-   静的 IP アドレス  
  
     実稼働環境では、可用性グループ リスナーで静的 IP アドレスを使用することをお勧めします。 また、可用性グループがマルチサブネット ドメインのサブネットにまたがっている場合、可用性グループ リスナーで静的 IP アドレスを使用する必要があります。  
  
 ハイブリッド ネットワーク構成とサブネットにまたがる DHCP は、可用性グループ リスナーではサポートされていません。 これは、フェールオーバーが発生すると動的 IP アドレスの期限が切れたり、解放されたりする場合があり、全体的な可用性が低下するおそれがあるためです。  
  
##  <a name="SelectListenerPort"></a> 可用性グループ リスナー ポートの選択  
 可用性グループ リスナーを構成する場合は、ポートを指定する必要があります。  既定のポートを 1433 に構成すると、クライアント接続文字列をシンプルにできます。 1433 を使用する場合は、接続文字列でポート番号を指定する必要がありません。   また、各可用性グループ リスナーに個別の仮想ネットワーク名があるため、1 つの WSFC で構成された各可用性グループ リスナーが同じ既定のポート 1433 を参照するように構成できます。  
  
 標準ではないリスナー ポートを指定することもできます。ただし、その場合、可用性グループ リスナーに接続するたびに、接続文字列で接続先ポートを明示的に指定する必要があります。  また、標準以外のポートに対して、ファイアウォールのアクセス許可を有効にする必要があります。  
  
 可用性グループ リスナー VNN で既定のポート 1433 を使用する場合、クラスター ノード上の他のサービスがそのポートを使用していないことを確認する必要があります。確認しない場合、ポートの競合が発生する可能性があります。  
  
 SQL Server のインスタンスの 1 つが、インスタンス リスナーを通じて TCP ポート 1433 を既にリッスンしていて、コンピューター上の他のサービス (SQL Server の別のインスタンスを含む) がポート 1433 をリッスンしていない場合は、可用性グループ リスナーでポートの競合は発生しません。  これは、可用性グループ リスナーが同じサービス プロセス内で同じ TCP ポートを共有できるためです。  ただし、同じポートをリッスンするように、SQL Server の複数のインスタンス (サイド バイ サイド) を構成しないでください。  
  
##  <a name="ConnectToPrimary"></a> リスナーを使用したプライマリ レプリカへの接続  
 可用性グループ リスナーを使用して読み取り/書き込みアクセスでプライマリ レプリカに接続するには、可用性グループ リスナーの DNS 名を接続文字列で指定します。  可用性グループ プライマリ レプリカが新しいレプリカに変更された場合、可用性グループ リスナーのネットワーク名を使用している既存の接続は解除されます。  その後、可用性グループ リスナーへの新しい接続によって、新しいプライマリ レプリカにダイレクトされます。 ADO.NET プロバイダー (System.Data.SqlClient) の基本的な接続文字列の例を次に示します。  
  
```  
Server=tcp: AGListener,1433;Database=MyDB;Integrated Security=SSPI  
```  
  
 可用性グループ リスナーのサーバー名を使用する代わりに、プライマリ レプリカまたはセカンダリ レプリカの SQL Server 名のインスタンスを直接参照することもできます。ただし、その場合、新しい接続が現在のプライマリ レプリカに自動的にダイレクトされるという利点がなくなります。  また、読み取り専用ルーティングの利点もなくなります。  
  
##  <a name="ConnectToSecondary"></a> リスナーを使用した読み取り専用セカンダリ レプリカ (読み取り専用ルーティング) への接続  
 *読み取り専用ルーティング[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]は、可用性グループ リスナーへの着信接続を、読み取り専用ワークロードを許可するように構成されたセカンダリ レプリカへルーティングする、* の機能です。 次の条件が満たされる場合、可用性グループ リスナー名を参照する着信接続を、読み取り専用レプリカに自動的にルーティングできます。  
  
-   少なくとも 1 つのセカンダリ レプリカが読み取り専用アクセスに設定され、各読み取り専用セカンダリ レプリカとプライマリ レプリカが読み取り専用ルーティングをサポートするように構成されている。 詳細については、このセクションの後の「 [読み取り専用ルーティングの可用性レプリカを構成するには](#ConfigureARsForROR)」を参照してください。  

-   接続文字列は、可用性グループに含まれるデータベースを参照します。 これに代わる方法は、接続に使うログインで、データベースを既定のデータベースとして構成することです。 詳しくは、[読み取り専用ルーティングでのアルゴリズムの動作に関するこちらの記事](https://blogs.msdn.microsoft.com/mattn/2012/04/25/calculating-read_only_routing_url-for-alwayson/)をご覧ください。

-   接続文字列は可用性グループ リスナーを参照し、着信接続のアプリケーションの目的が読み取り専用に設定されている (たとえば、ODBC または OLEDB の接続文字列、接続属性、またはプロパティで **Application Intent=ReadOnly** キーワードを使用している)。 詳細については、このセクションの後の「 [読み取り専用アプリケーションの目的および読み取り専用ルーティング](#ReadOnlyAppIntent)」を参照してください。  
  
##  <a name="ConfigureARsForROR"></a> 読み取り専用ルーティングの可用性レプリカを構成するには  
 データベース管理者は、可用性レプリカを次のように構成する必要があります。  
  
1.  読み取り可能なセカンダリ レプリカとして構成する可用性レプリカごとに、データベース管理者はセカンダリ ロールにのみ影響する次の設定を構成する必要があります。  
  
    -   接続アクセスを「すべて」または「読み取り専用」に設定する必要があります。  
  
    -   読み取り専用ルーティングの URL を指定する必要があります。  
  
2.  これらのレプリカごとに、プライマリ ロールに対して読み取り専用ルーティング リストを指定する必要があります。 1 つ以上のサーバー名をルーティング ターゲットとして指定します。  
  
####  <a name="RelatedTasksROR"></a> 関連タスク  
  
-   [可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [可用性グループの読み取り専用ルーティングの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
##  <a name="ReadOnlyAppIntent"></a> 読み取り専用アプリケーションの目的および読み取り専用ルーティング  
 アプリケーションの目的の接続文字列プロパティは、読み取り/書き込み用または読み取り専用のどちらかの可用性グループ データベースにダイレクトされる、クライアント アプリケーションの要求を表します。 読み取り専用ルーティングを使用するには、可用性グループ リスナーに接続するときに、クライアントが接続文字列内で読み取り専用のアプリケーションの目的を使用する必要があります。 読み取り専用のアプリケーションの目的がないと、可用性グループ リスナーへの接続は、プライマリ レプリカ上のデータベースに送られます。  
  
 アプリケーションの目的の属性は、ログイン中にクライアントのセッションに格納されます。その後、SQL Server のインスタンスがこの目的を処理し、可用性グループの構成およびセカンダリ レプリカ内のターゲット データベースの現在の読み取り/書き込み状態に基づいて、実行する操作を決定します。  
  
 読み取り専用のアプリケーションの目的を指定する ADO.NET プロバイダー (System.Data.SqlClient) の接続文字列の例を次に示します。  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;Integrated Security=SSPI;ApplicationIntent=ReadOnly  
```  
  
 この接続文字列の例では、クライアントはポート 1433 で `AGListener` という名前の可用性グループ リスナーを介して AdventureWorks データベースへの接続を試みます (可用性グループ リスナーが 1433 でリッスンしている場合、このポートの指定を省略できます)。  この接続文字列は、 **ApplicationIntent** プロパティが **ReadOnly**に設定されているため、 *読み取りを目的とした接続文字列*となります。  この設定がない場合、サーバーは接続の読み取り専用へのルーティングを試行しません。  
  
 可用性グループのプライマリ データベースは、読み取り専用の受信ルーティング要求を処理し、プライマリ レプリカに参加していて読み取り専用ルーティング用に構成されているオンラインの読み取り専用レプリカを特定します。  クライアントは、プライマリ レプリカ サーバーから接続情報を受け取り、特定された読み取り専用レプリカに接続します。  
  
 アプリケーションの目的は、クライアント ドライバーから下位の SQLServer インスタンスに送信できます。  この場合、読み取り専用のアプリケーションの目的は無視され、接続は通常どおり続行されます。  
  
 読み取り専用ルーティングをバイパスする場合、または、可用性グループ リスナー名を使用せずに SQL Server のプライマリ レプリカ インスタンスに直接接続する場合は、"アプリケーションの目的" 接続プロパティを **ReadOnly** に設定しません (指定しない場合、既定では、ログイン中は **ReadWrite** )。  読み取り専用レプリカに直接接続する場合は、読み取り専用ルーティングも実行されません。  
  
####  <a name="RelatedTasksApps"></a> 関連タスク  
  
-   [SQL Server Native Client の HADR サポート](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [SQL Server Native Client での接続文字列キーワードの使用](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
##  <a name="BypassAGl"></a> 可用性グループ リスナーのバイパス  
 可用性グループ リスナーでフェールオーバー リダイレクトと読み取り専用ルーティングが有効にされている場合、クライアント接続でこれらを使用する必要はありません。 また、クライアント接続は、可用性グループ リスナーに接続する代わりに、SQLServer のインスタンスを直接参照できます。  
  
 SQL Server のインスタンスにとって、接続のログインで、可用性グループ リスナーまたは他のインスタンス エンドポイントのどちらを使用するかは関係ありません。  SQL Server のインスタンスは、接続先データベースの状態を確認し、可用性グループの構成およびインスタンス上のデータベースの現在の状態に基づいて、接続を許可または禁止します。  たとえば、クライアント アプリケーションが SQL Server ポートのインスタンスに直接接続し、可用性グループでホストされているターゲット データベースに接続する場合、ターゲット データベースがプライマリ状態でオンラインであれば接続は成功します。  ターゲット データベースがオフラインまたは移行状態の場合は、データベースへの接続が失敗します。  
  
 データベース ミラーリングを [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]に移行している間、セカンダリ レプリカが 1 つしか存在せず、これにユーザーが接続できない場合は、アプリケーションでデータベース ミラーリング接続文字列を指定できます。 詳細については、このセクションの後の「 [データベース ミラーリング接続文字列と可用性グループの使用](#DbmConnectionString)」を参照してください。  
  
##  <a name="DbmConnectionString"></a> データベース ミラーリング接続文字列と可用性グループの使用  
 可用性グループに 1 つしかセカンダリ レプリカが存在せず、さらに、その可用性グループが、セカンダリ レプリカに ALLOW_CONNECTIONS = READ_ONLY または ALLOW_CONNECTIONS = NONE が構成されている場合、クライアントは、データベース ミラーリングの接続文字列を使用してプライマリ レプリカに接続できます。 可用性グループに存在する可用性レプリカが 2 つだけ (プライマリ レプリカおよび 1 つのセカンダリ レプリカ) であれば、既存のアプリケーションをデータベース ミラーリングから可用性グループに移行する際にこの方法を用いることができます。 セカンダリ レプリカをさらに追加する場合は、可用性グループの可用性グループ リスナーを作成し、その可用性グループ リスナー DNS 名を使用するようにアプリケーションを更新する必要があります。  
  
 データベース ミラーリングの接続文字列を使用する際、クライアントは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client または .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を使用できます。 クライアントが指定する接続文字列には、最低限、1 つのサーバー インスタンスの名前 ( *イニシャル パートナー名*) が指定されている必要があります。接続先の可用性レプリカを初期状態でホストするサーバー インスタンスは、この名前によって識別されます。 接続文字列には、必要に応じて、別のサーバー インスタンスの名前を指定することもできます。これを *フェールオーバー パートナー名*といい、初期状態でセカンダリ レプリカをホストするサーバー インスタンスは、フェールオーバー パートナー名として識別されます。  
  
 データベース ミラーリングの接続文字列の詳細については、「 [データベース ミラーリング セッションへのクライアントの接続 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)」を参照してください。  
  
##  <a name="CCBehaviorOnFailover"></a> フェールオーバー時のクライアント接続動作  
 可用性グループのフェールオーバーが発生すると、可用性グループへの既存の永続的な接続は終了します。このため、クライアントが、同じプライマリ データベースまたは読み取り専用セカンダリ データベースとの連携を保つには、新しい接続を確立する必要があります。  フェールオーバーがサーバー側で発生している間は、可用性グループへの接続が失敗することがあります。この場合、プライマリが完全にオンラインになるまで、クライアント アプリケーションは接続を再試行します。  
  
 クライアント アプリケーションの接続の試行中、接続のタイムアウト期間が経過する前に可用性グループがオンラインに戻ると、クライアント ドライバーによる内部での再試行のいずれかが正常に接続できる場合があります。このとき、アプリケーションでエラーは発生しません。  
  
##  <a name="SupportAgMultiSubnetFailover"></a> 可用性グループ マルチサブネット フェールオーバーのサポート  
 接続文字列で MultiSubnetFailover 接続オプションをサポートするクライアント ライブラリを使用している場合、MultiSubnetFailover を "True" または "Yes" に設定して (使用しているプロバイダーの構文によって異なります)、別のサブネットへの可用性グループのフェールオーバーを最適化できます。  
  
> [!NOTE]  
>  可用性グループ リスナーおよび SQL Server フェールオーバー クラスター インスタンス名への単一サブネット接続およびマルチサブネット接続の両方に対して、この設定を推奨します。  このオプションを有効にすると、単一サブネットのシナリオでも、さらに最適化されます。  
  
 **MultiSubnetFailover** 接続オプションは TCP ネットワーク プロトコルのみで機能します。また、可用性グループ リスナーに接続する場合、および [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]に接続している仮想ネットワーク名を使用する場合にのみサポートされます。  
  
 マルチサブネット フェールオーバーを有効にする ADO.NET プロバイダー (System.Data.SqlClient) の接続文字列の例を次に示します。  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;Integrated Security=SSPI; MultiSubnetFailover=True  
```  
  
 **MultiSubnetFailover** 接続オプションは、可用性グループが単一のサブネットのみにある場合でも、 **True** に設定することをお勧めします。  これにより、今後、クライアント接続文字列を変更することなく、複数のサブネットをサポートするように新しいクライアントをあらかじめ構成することができ、単一サブネットのフェールオーバーのパフォーマンスも最適化できます。  **MultiSubnetFailover** 接続オプションは必須ではありませんが、サブネットのフェールオーバーが速くなるという利点があります。  これは、クライアント ドライバーが、可用性グループに関連付けられている各 IP アドレスの TCP ソケットを同時に開こうとするためです。  クライアント ドライバーは、最初の IP が正常に応答するのを待ち、応答した場合は、その IP を接続に使用します。  
  
##  <a name="SSLcertificates"></a> 可用性グループ リスナーと SSL 証明書  
 可用性グループ リスナーへの接続時に、参加している SQL Server のインスタンスがセッションの暗号化と共に SSL 証明書を使用していることがあります。この場合、強制的に暗号化するために、接続クライアント ドライバーが SSL 証明書のサブジェクト代替名をサポートする必要があります。  SQL Server ドライバーでの証明書のサブジェクト代替名のサポートは、ADO.NET (SqlClient)、Microsoft JDBC、および SQL Native Client (SNAC) に対して計画されています。  
  
 X.509 証明書は、すべての可用性グループ リスナー セットのリストを証明書のサブジェクト代替名に設定して、フェールオーバー クラスターに参加している各サーバー ノードに対して構成する必要があります。  
  
 たとえば、WSFC に `AG1_listener.Adventure-Works.com`、 `AG2_listener.Adventure-Works.com`、 `AG3_listener.Adventure-Works.com`という 3 つの可用性グループ リスナーがある場合、証明書のサブジェクト代替名を次のように設定する必要があります。  
  
```  
CN = ServerFQDN  
SAN = ServerFQDN,AG1_listener.Adventure-Works.com, AG2_listener.Adventure-Works.com, AG3_listener.Adventure-Works.com  
```  
  
##  <a name="SPNs"></a> 可用性グループ リスナーとサーバー プリンシパル名 (SPN)  
 可用性グループ リスナーへのクライアント接続で Kerberos を有効にするには、各可用性グループ リスナー名のドメイン管理者が、Active Directory 内にサーバー プリンシパル名 (SPN) を構成する必要があります。 SPN が登録されている場合、可用性レプリカをホストするサーバー インスタンスのサービス アカウントを使用する必要があります。  SPN がすべてのレプリカで機能するためには、可用性グループをホストする WSFC クラスター内のすべてのインスタンスで同じサービス アカウントを使用する必要があります。  
  
 SPN は、Windows コマンド ライン ツールの **setspn** を使用して構成します。  たとえば、 `AG1listener.Adventure-Works.com` というドメイン アカウントで実行されるように構成された、一連の SQL Server インスタンスでホストされている `corp/svclogin2`という名前の可用性グループの SPN を構成する場合は、次のようになります。  
  
```  
setspn -A MSSQLSvc/AG1listener.Adventure-Works.com:1433 corp/svclogin2  
```  
  
 SQL Server の SPN の手動登録の詳細については、「 [Kerberos 接続用のサービス プリンシパル名の登録](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [Always On クライアント接続 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)  
  
-   [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [可用性グループ リスナーのプロパティの表示 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
-   [可用性グループ リスナーの削除 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [可用性グループの読み取り専用ルーティングの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [高可用性と災害復旧のための Microsoft SQL Server AlwaysOn ソリューション ガイド](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Introduction to the Availability Group Listener (可用性グループ リスナーの概要)](https://blogs.msdn.microsoft.com/sqlalwayson/2012/01/16/introduction-to-the-availability-group-listener/) (SQL Server Always On チームのブログ)  
  
-   [SQL Server Always On チーム ブログ:SQL Server Always On チームのオフィシャル ブログ](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn クライアントの接続 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)   
 [可用性レプリカに対するクライアント接続アクセスについて &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [アクティブなセカンダリ:読み取り可能なセカンダリ レプリカ &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [データベース ミラーリング セッションへのクライアントの接続 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)  
  
  
