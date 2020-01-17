---
title: 可用性グループの読み取り専用ルーティングの構成 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- read-only routing
- Availability Groups [SQL Server], readable secondary replicas
- Availability Groups [SQL Server], read-only routing
- readable secondary replicas
- Availability Groups [SQL Server], client connectivity
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 7bd89ddd-0403-4930-a5eb-3c78718533d4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f50ff5cd5a3ecbc70aafb6da7cf5008f31bada0f
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797732"
---
# <a name="configure-read-only-routing-for-an-availability-group-sql-server"></a>可用性グループの読み取り専用ルーティングの構成 (SQL Server)
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]で読み取り専用ルーティングをサポートするように AlwaysOn 可用性グループを構成するには、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] または PowerShell を使用します。 *読み取り専用ルーティング* は、対象の読み取り専用接続要求を、AlwaysOn の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 読み取り可能なセカンダリ レプリカ [(セカンダリ ロールで実行されているときに、読み取り専用ワークロードを許可するように構成されているレプリカ) にルーティングする](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md) の機能です。 読み取り専用ルーティングをサポートするには、可用性グループに[可用性グループ リスナー](../../listeners-client-connectivity-application-failover.md)が存在する必要があります。 読み取り専用クライアントは、このリスナーに接続要求を送信する必要があります。クライアントの接続文字列では、アプリケーションの目的として "読み取り専用" を指定する必要があります。 つまり、 *読み取りを目的とした接続要求*であることが必要です。  
  
> [!NOTE]
>  読み取り可能なセカンダリ レプリカを構成する方法については、「[可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)」を参照してください。

> [!NOTE]
>  読み取り専用ルーティングの構成は [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ではサポートされていません。  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> の前提条件  
  
-   可用性グループに可用性グループ リスナーが存在している必要があります。 詳細については、「[可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)」を参照してください。  
  
-   1つまたは複数の可用性レプリカは、セカンダリロールで読み取り専用を受け入れるように構成する必要があります (つまり、読み取り[可能なセカンダリレプリカ](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)(AlwaysOn% 20availability% 20availability\)md))。 詳細については、「 [可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)が存在する必要があります。  
  
-   現在のプライマリ レプリカをホストするサーバー インスタンスに接続されている必要があります。  
  
###  <a name="RORReplicaProperties"></a> 読み取り専用ルーティングをサポートするために構成する必要があるレプリカのプロパティ  
  
-   読み取り専用ルーティングをサポートしようとしている読み取り可能なセカンダリ レプリカに対して、*読み取り専用ルーティングの URL* を指定する必要があります。 この URL は、ローカル レプリカがセカンダリ ロールで実行されている場合にのみ有効です。 読み取り専用ルーティングの URL は、必要に応じてレプリカごとに指定する必要があります。 各読み取り専用ルーティングの URL は、読み取りを目的とした接続要求を特定の読み取り可能なセカンダリ レプリカにルーティングする際に使用されます。 通常は、読み取り可能なすべてのセカンダリ レプリカに読み取り専用ルーティングの URL が割り当てられます。  
  
     可用性レプリカの読み取り専用ルーティングの URL の計算の詳細については、「 [AlwaysOn の read_only_routing_url の計算](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)」を参照してください。  
  
-   可用性レプリカがプライマリ レプリカである場合に読み取り専用ルーティングをサポートするには、その可用性レプリカに対して*読み取り専用ルーティング リスト*を指定する必要があります。 読み取り専用ルーティング リストは、ローカル レプリカがプライマリ ロールで実行されている場合にのみ有効です。 このリストは、必要に応じてレプリカごとに指定する必要があります。 通常、各読み取り専用ルーティング リストには、すべての読み取り専用ルーティングの URL が含まれており、リストの末尾にローカル レプリカの URL が示されています。  
  
    > [!NOTE]  
    >  読み取りを目的とした接続要求は、現在のプライマリ レプリカの読み取り専用ルーティング リスト内の最初に使用できる読み取り可能なセカンダリにルーティングされます。 負荷分散はありません。  
  
> [!NOTE]  
>  可用性グループ リスナーと読み取り専用ルーティングの詳細については、「[可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)」をご参照ください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> アクセス許可  
  
|タスク|アクセス許可|  
|----------|-----------------|  
|可用性グループの作成時にレプリカを構成する|**sysadmin** 固定サーバー ロールのメンバーシップと、CREATE AVAILABILITY GROUP サーバー権限、ALTER ANY AVAILABILITY GROUP 権限、CONTROL SERVER 権限のいずれかが必要です。|  
|可用性レプリカを変更する|可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。|  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **読み取り専用ルーティングを構成するには**  
  
> [!NOTE]  
>  コード例については、このセクションの後半の「 [例 (Transact-SQL)](#TsqlExample)」を参照してください。  
  
1.  プライマリ レプリカをホストするサーバー インスタンスに接続します。  
  
2.  新しい可用性グループのレプリカを指定する場合は、 [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用します。 既存の可用性グループのレプリカを追加または変更する場合は、 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用します。  
  
    -   セカンダリ ロールの読み取り専用ルーティングを構成するには、ADD REPLICA 句または MODIFY REPLICA WITH 句で、SECONDARY_ROLE オプションを次のように指定します。  
  
         SECONDARY_ROLE **(** READ_ONLY_ROUTING_URL **='** TCP **:// *`system-address`* : *`port`* ')**  
  
         読み取り専用ルーティング URL のパラメーターは次のとおりです。  
  
         *system-address*  
         システム名、完全修飾ドメイン名では、対象のコンピューター システムを明確に識別する、IP アドレスなどの文字列です。  
  
         *port*  
         [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのデータベース エンジンによって使用されるポート番号です。  
  
         例:   `SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433')`  
  
         レプリカが既に読み取り専用接続を許可するように構成されている場合、MODIFY REPLICA 句の ALLOW_CONNECTIONS は省略可能です。  
  
         詳細については、「 [AlwaysOn の read_only_routing_url の計算](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)」を参照してください。  
  
    -   プライマリ ロールの読み取り専用ルーティングを構成するには、ADD REPLICA 句または MODIFY REPLICA WITH 句で、PRIMARY_ROLE オプションを次のように指定します。  
  
         PRIMARY_ROLE **(** READ_ONLY_ROUTING_LIST **=(' *`server`* '** [ **,** ...*n* ] **))**  
  
         *server* は、可用性グループの読み取り専用セカンダリ レプリカをホストするサーバー インスタンスを識別します。  
  
         例:   `PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('Server1','Server2'))`  
  
        > [!NOTE]  
        >  読み取り専用ルーティング リストを構成する前に、読み取り専用ルーティング URL を設定する必要があります。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、既存の可用性グループ `AG1` の 2 つの可用性レプリカを、これらのレプリカのいずれかが現在プライマリ ロールを所有している場合に読み取り専用ルーティングをサポートするように変更します。 可用性レプリカをホストするサーバー インスタンスを識別するために、この例ではインスタンス名 `COMPUTER01` および `COMPUTER02` を指定します。  
  
```sql
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433'));  
  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER02.contoso.com:1433'));  
  
ALTER AVAILABILITY GROUP [AG1]   
MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER02','COMPUTER01')));  
  
ALTER AVAILABILITY GROUP [AG1]   
MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER01','COMPUTER02')));  
GO
```  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  

### <a name="to-configure-read-only-routing"></a>読み取り専用ルーティングを構成するには
  
> [!NOTE]  
>  コード例については、このセクションの後半の「[例 (PowerShell)](#PSExample)」を参照してください。  
  
1.  既定 (`cd`) を、プライマリ レプリカをホストするサーバー インスタンスに設定します。  
  
2.  可用性グループに可用性レプリカを追加する場合は、`New-SqlAvailabilityReplica` コマンドレットを使用します。 既存の可用性レプリカを変更する場合は、`Set-SqlAvailabilityReplica` コマンドレットを使用します。 関連するパラメーターは次のとおりです。  
  
    -   セカンダリロールの読み取り専用ルーティングを構成するには、 **ReadonlyRoutingConnectionUrl " *`url`* "** パラメーターを指定します。  
  
         *url* は、読み取り専用接続のためにレプリカにルーティングするときに使用する、接続の完全修飾ドメイン名 (FQDN) およびポートです。 例:  `-ReadonlyRoutingConnectionUrl "TCP://DBSERVER8.manufacturing.Adventure-Works.com:7024"`  
  
         詳細については、「 [AlwaysOn の read_only_routing_url の計算](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)」を参照してください。  
  
    -   プライマリロールの接続アクセスを構成するには、 **ReadonlyRoutingList " *`server`* "** [ **,** ... を指定します。*n* ]。ここで、*サーバー*は、可用性グループ内の読み取り専用セカンダリレプリカをホストするサーバーインスタンスを識別します。 例:  `-ReadOnlyRoutingList "SecondaryServer","PrimaryServer"`  
  
        > [!NOTE]  
        >  レプリカの読み取り専用ルーティング リストを構成する前に、レプリカの読み取り専用ルーティング URL を設定する必要があります。  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、`Get-Help` PowerShell 環境で [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)」を参照してください。  
  
SQL Server PowerShell プロバイダーを設定して使用するには、「 [SQL Server PowerShell プロバイダー](../../../powershell/sql-server-powershell-provider.md) 」と「[ヘルプの表示 SQL Server PowerShell](../../../powershell/sql-server-powershell.md)」を参照してください。
  
###  <a name="PSExample"></a> 例 (PowerShell)  
 次の例では、可用性グループ内のプライマリ レプリカと 1 つのセカンダリ レプリカを読み取り専用ルーティング用に構成します。 まず、読み取り専用ルーティングの URL が各レプリカに割り当てられます。 次に、プライマリ レプリカで読み取り専用ルーティング リストを設定します。 接続文字列で "ReadOnly" プロパティが設定された接続は、セカンダリ レプリカにリダイレクトされます。 このセカンダリ レプリカが読み取り不可である場合 (`ConnectionModeInSecondaryRole` 設定によって決まります)、接続はプライマリ レプリカに戻されます。  
  
```powershell
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  
$secondaryReplica = Get-Item "AvailabilityReplicas\SecondaryServer"  
  
Set-SqlAvailabilityReplica -ReadOnlyRoutingConnectionUrl "TCP://PrimaryServer.domain.com:1433" -InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ReadOnlyRoutingConnectionUrl "TCP://SecondaryServer.domain.com:1433" -InputObject $secondaryReplica  
Set-SqlAvailabilityReplica -ReadOnlyRoutingList "SecondaryServer","PrimaryServer" -InputObject $primaryReplica  
```  
  
##  <a name="FollowUp"></a> 補足情報: 読み取り専用ルーティングを構成した後  
 現在のプライマリ レプリカと読み取り可能なセカンダリ レプリカをそれぞれのロールで読み取り専用ルーティングをサポートするように設定すると、読み取り可能なセカンダリ レプリカは、可用性グループ リスナーを介して接続するクライアントからの読み取りを目的とした接続要求を受信できるようになります。  
  
> [!TIP]  
>  [Bcp ユーティリティ](../../../tools/bcp-utility.md)または[sqlcmd ユーティリティ](../../../tools/sqlcmd-utility.md)を使用する場合は、`-K ReadOnly` スイッチを指定することによって、読み取り専用アクセスが有効になっている任意のセカンダリレプリカへの読み取り専用アクセスを指定できます。  
  
###  <a name="ConnStringReqsRecs"></a> クライアント接続文字列の要件および推奨事項  
 クライアント アプリケーションで読み取り専用ルーティングを使用するには、クライアントの接続文字列が次の要件を満たしている必要があります。  
  
-   TCP プロトコルを使用する。  
  
-   アプリケーションの目的の属性またはプロパティを読み取り専用に設定する。  
  
-   読み取り専用ルーティングをサポートするように構成された可用性グループのリスナーを参照する。  
  
-   その可用性グループ内のデータベースを参照する。  
  
 さらに、接続文字列でマルチサブネット フェールオーバーを有効にすることをお勧めします。マルチサブネット フェールオーバーは、各サブネット上の各レプリカについて並行クライアント スレッドをサポートします。 これにより、フェールオーバー後のクライアント再接続時間が最小化されます。  
  
 接続文字列の構文は、アプリケーションが使用している SQL Server プロバイダーに依存します。 .NET Framework Data Provider 4.0.2 for SQL Server 用の次の接続文字列例は、読み取り専用ルーティング用に機能することが必須および推奨される接続文字列の一部を示しています。  
  
```  
Server=tcp:MyAgListener,1433;Database=Db1;IntegratedSecurity=SSPI;ApplicationIntent=ReadOnly;MultiSubnetFailover=True  
```  
  
 読み取り専用のアプリケーションの目的と読み取り専用のルーティングの詳細については、「 [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)が存在する必要があります。  
  
### <a name="if-read-only-routing-is-not-working-correctly"></a>読み取り専用ルーティングが正常に動作しない場合  
 読み取り専用ルーティング構成のトラブルシューティングの詳細については、「 [Read-Only Routing is Not Working Correctly](troubleshoot-always-on-availability-groups-configuration-sql-server.md)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  

### <a name="to-view-read-only-routing-configurations"></a>読み取り専用ルーティングの構成を表示するには
  
-   [sys.availability_read_only_routing_lists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)  
  
-   [sys.availability_replicas &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql) (**read_only_routing_url** 列)  
  
### <a name="to-configure-client-connection-access"></a>クライアント接続アクセスを構成するには
  
-   [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server&#41;](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
### <a name="to-use-connection-strings-in-applications"></a>アプリケーションで接続文字列を使用するには
  
-   [SQL Server Native Client の HADR サポート](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [SQL Server Native Client での接続文字列キーワードの使用](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   **ブログ:**  
  
     [AlwaysOn の read_only_routing_url を計算しています](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)  
  
     [AlwaysOn チームのブログの SQL Server: AlwaysOn チームの公式 SQL Server のブログ](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](https://blogs.msdn.com/b/psssql/)  
  
-   **ホワイト ペーパー:**  
  
     [SQL Server 2012 に関する Microsoft ホワイト ペーパー](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server ユーザー諮問チームのホワイト ペーパー](http://sqlcat.com/)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ&#40;SQL Server&#41;の概要](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ&#40;SQL Server&#41;の概要](overview-of-always-on-availability-groups-sql-server.md)   
 [アクティブなセカンダリ: 読み取り可能なセカンダリレプリカ (AlwaysOn 可用性グループ)](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [可用性レプリカに対するクライアント接続アクセスについて &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md)  
