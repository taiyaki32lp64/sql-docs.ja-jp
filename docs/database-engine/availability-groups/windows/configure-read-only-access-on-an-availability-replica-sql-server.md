---
title: セカンダリ可用性グループ レプリカへの読み取り専用アクセスの構成
description: 'Always On 可用性グループでセカンダリ レプリカに読み取りアクセスのみが許可されるように構成します。 '
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- connection access to availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 22387419-22c4-43fa-851c-5fecec4b049b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: aaeef70fe81699d0cbb00ba3d7e5a6dfcf1b6aa7
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241731"
---
# <a name="configure-read-only-access-to-a-secondary-replica-of-an-always-on-availability-group"></a>Always On 可用性グループのセカンダリ レプリカへの読み取り専用アクセスの構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  既定では、プライマリ レプリカへの読み取り/書き込みアクセスと読み取りを目的としたアクセスの両方が許可され、AlwaysOn 可用性グループのセカンダリ レプリカへの接続は許可されません。 このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、または PowerShell を使用して、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]の AlwaysOn 可用性グループの可用性レプリカに対して接続アクセスを構成する方法について説明します。  
  
 セカンダリ レプリカに対して読み取り専用アクセスを有効にすることによる影響と、接続アクセスの概要については、「[可用性レプリカに対するクライアント接続アクセスについて &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)」および「[アクティブなセカンダリ:読み取り可能なセカンダリ レプリカ &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
 
##  <a name="Prerequisites"></a> 前提条件と制限  
  
-   別の接続アクセスを構成するには、プライマリ レプリカをホストするサーバー インスタンスに接続している必要があります。  
  
##  <a name="Permissions"></a> Permissions  
  
|タスク|アクセス許可|  
|----------|-----------------|  
|可用性グループの作成時にレプリカを構成する|**sysadmin** 固定サーバー ロールのメンバーシップと、CREATE AVAILABILITY GROUP サーバー権限、ALTER ANY AVAILABILITY GROUP 権限、CONTROL SERVER 権限のいずれかが必要です。|  
|可用性レプリカを変更する|可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。|  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **可用性レプリカに対してアクセスを構成するには**  
  
1.  オブジェクト エクスプローラーで、プライマリ レプリカをホストするサーバー インスタンスに接続し、サーバー ツリーを展開します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  変更するレプリカが含まれる可用性グループをクリックします。  
  
4.  可用性レプリカを右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[可用性レプリカ プロパティ]** ダイアログ ボックスで、プライマリ ロールおよびセカンダリ ロールの接続アクセスを、次のように変更できます。  
  
    -   セカンダリ ロールの場合は、 **[読み取り可能セカンダリ]** ボックスの一覧から新しい値を選択します。値は次のとおりです。  
  
         **いいえ**  
         このレプリカのセカンダリ データベースに対するユーザー接続は禁止されます。 読み取りアクセスで利用することはできません。 これが既定の設定です。  
  
         **[読み取り目的のみ]**  
         このレプリカのセカンダリ データベースに対する接続は、読み取り専用でのみ許可されます。 セカンダリ データベースはすべて読み取りアクセスで利用できます。  
  
         **はい**  
         読み取りアクセスに限り、このレプリカのセカンダリ データベースに対するすべての接続が許可されます。 セカンダリ データベースはすべて読み取りアクセスで利用できます。  
  
    -   プライマリ ロールの場合は、 **[プライマリ ロールの接続]** ボックスの一覧から新しい値を選択します。値は次のとおりです。  
  
         **[すべての接続を許可]**  
         プライマリ レプリカのデータベースに対するすべての接続が許可されます。 これが既定の設定です。  
  
         **[読み取り/書き込みの接続を許可]**  
         Application Intent プロパティが **ReadWrite** に設定されている場合、または Application Intent 接続プロパティが設定されていない場合は、接続が許可されます。 Application Intent 接続プロパティが **ReadOnly** に設定されている接続は許可されません。 これにより、読み取りを目的としたワークロードが誤ってプライマリ レプリカに接続されるのを防ぐことができます。 "アプリケーションの目的" 接続プロパティの詳細については、「 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **可用性レプリカに対してアクセスを構成するには**  
  
> [!NOTE]  
>  この手順の例については、このセクションの後半の「 [例 (Transact-SQL)](#TsqlExample)」を参照してください。  
  
1.  プライマリ レプリカをホストするサーバー インスタンスに接続します。  
  
2.  新しい可用性グループのレプリカを指定する場合は、 [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用します。 既存の可用性グループのレプリカを追加または変更する場合は、 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用します。  
  
    -   セカンダリ ロールの接続アクセスを構成するには、ADD REPLICA 句または MODIFY REPLICA WITH 句で、SECONDARY_ROLE オプションを次のように指定します。  
  
         SECONDARY_ROLE **(** ALLOW_CONNECTIONS **=** { NO | READ_ONLY | ALL } **)**  
  
         パラメーターの説明  
  
         NO  
         このレプリカのセカンダリ データベースに対する直接接続は禁止されます。 読み取りアクセスで利用することはできません。 これが既定の設定です。  
  
         READ_ONLY  
         このレプリカのセカンダリ データベースに対する接続は、読み取り専用でのみ許可されます。 セカンダリ データベースはすべて読み取りアクセスで利用できます。  
  
         ALL  
         読み取りアクセスに限り、このレプリカのセカンダリ データベースに対するすべての接続が許可されます。 セカンダリ データベースはすべて読み取りアクセスで利用できます。  
  
3.  プライマリ ロールの接続アクセスを構成するには、ADD REPLICA 句または MODIFY REPLICA WITH 句で、PRIMARY_ROLE オプションを次のように指定します。  
  
     PRIMARY_ROLE **(** ALLOW_CONNECTIONS **=** { READ_WRITE | ALL } **)**  
  
     パラメーターの説明  
  
     READ_WRITE  
     Application Intent 接続プロパティが **ReadOnly** に設定されている接続は許可されません。  Application Intent プロパティが **ReadWrite** に設定されている場合、または Application Intent 接続プロパティが設定されていない場合は、接続が許可されます。 "アプリケーションの目的" 接続プロパティの詳細については、「 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
     ALL  
     プライマリ レプリカのデータベースに対するすべての接続が許可されます。 これが既定の設定です。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、セカンダリ レプリカを *AG2*という名前の可用性グループに追加します。 新しい可用性レプリカをホストするため、スタンドアロン サーバー インスタンスの *COMPUTER03\HADR_INSTANCE*が指定されています。 このレプリカは、プライマリ ロールに対してのみ読み取り/書き込み接続を許可し、セカンダリ ロールに対しては読み取りを目的とした接続のみを許可するように構成されています。  
  
```  
ALTER AVAILABILITY GROUP AG2   
   ADD REPLICA ON   
      'COMPUTER03\HADR_INSTANCE' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03:7022',  
         PRIMARY_ROLE ( ALLOW_CONNECTIONS = READ_WRITE ),  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY )  
         );   
GO  
```  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
 **可用性レプリカに対してアクセスを構成するには**  
  
> [!NOTE]  
>  コード例については、このセクションの後半の「 [例 (PowerShell)](#PSExample)」を参照してください。  
  
1.  プライマリ レプリカをホストするサーバー インスタンスにディレクトリを変更 (**cd**) します 。  
  
2.  可用性グループに可用性レプリカを追加する場合は、 **New-SqlAvailabilityReplica** コマンドレットを使用します。 既存の可用性レプリカを変更する場合は、 **Set-SqlAvailabilityReplica** コマンドレットを使用します。 関連するパラメーターは次のとおりです。  
  
    -   セカンダリ ロールの接続アクセスを構成するには、 **ConnectionModeInSecondaryRole**_secondary_role_keyword_ パラメーターを指定します。 *secondary_role_keyword* は次のいずれかの値になります。  
  
         **AllowNoConnections**  
         セカンダリ レプリカのデータベースに対する直接接続は許可されず、データベースに対して読み取りアクセスを実行できません。 これが既定の設定です。  
  
         **AllowReadIntentConnectionsOnly**  
         Application Intent プロパティが **ReadOnly**に設定されている場合に限り、セカンダリ レプリカのデータベースに対する接続が許可されます。 このプロパティの詳細については、「 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
         **AllowAllConnections**  
         読み取り専用アクセスに限り、セカンダリ レプリカのデータベースに対するすべての接続が許可されます。  
  
    -   プライマリ ロールの接続アクセスを構成するには、 **ConnectionModeInPrimaryRole**_primary_role_keyword_を指定します。 *primary_role_keyword* は次のいずれかの値になります。  
  
         **AllowReadWriteConnections**  
         Application Intent 接続プロパティが ReadOnly に設定されている接続は許可されません。 Application Intent プロパティが ReadWrite に設定されている場合、または Application Intent 接続プロパティが設定されていない場合は、接続が許可されます。 "アプリケーションの目的" 接続プロパティの詳細については、「 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
         **AllowAllConnections**  
         プライマリ レプリカのデータベースに対するすべての接続が許可されます。 これが既定の設定です。  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
###  <a name="PSExample"></a> 例 (PowerShell)  
 以下の例は、 **ConnectionModeInSecondaryRole** パラメーターと **ConnectionModeInPrimaryRole** パラメーターの両方を **AllowAllConnections**に設定しています。  
  
```  
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  
Set-SqlAvailabilityReplica -ConnectionModeInSecondaryRole "AllowAllConnections" `   
-InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ConnectionModeInPrimaryRole "AllowAllConnections" `   
-InputObject $primaryReplica  
  
```  
  
##  <a name="FollowUp"></a>補足情報: 可用性レプリカに対する読み取り専用アクセスの構成後  
 **読み取り可能なセカンダリ レプリカに対する読み取り専用アクセス**  
  
-   [bcp ユーティリティ](../../../tools/bcp-utility.md) または [sqlcmd ユーティリティ](../../../tools/sqlcmd-utility.md)を使用する場合、 **-K ReadOnly** スイッチを指定することによって、読み取り専用アクセスが有効になっている任意のセカンダリ レプリカへの読み取り専用アクセスを指定できます。  
  
-   読み取り可能なセカンダリ レプリカに接続するクライアント アプリケーションを有効にするには:  
  
    ||前提条件|Link|  
    |-|------------------|----------|  
    |![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|可用性グループにリスナーがあることを確認する。|[可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)|  
    |![Checkbox](../../../database-engine/availability-groups/windows/media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|可用性グループの読み取り専用ルーティングを構成する。|[可用性グループの読み取り専用ルーティングの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)|  
  
 **フェールオーバー後にトリガーとジョブに影響する可能性がある要因**  
  
 読み取り可能でないセカンダリ データベースまたは読み取り可能なセカンダリ データベースで実行されたときに失敗するトリガーとジョブがある場合は、トリガーとジョブをスクリプト化して、特定のレプリカに対して、データベースがプライマリ データベースか読み取り可能なセカンダリ データベースかを確認する必要があります。 この情報を入手するには、データベースの [Updateability](../../../t-sql/functions/databasepropertyex-transact-sql.md) プロパティを返す **DATABASEPROPERTYEX** 関数を使用します。 読み取り専用データベースを識別するには、次のように、値として READ_ONLY を指定します。  
  
```  
DATABASEPROPERTYEX([db name],'UpdateAbility') = N'READ_ONLY'  
```  
  
 読み取り/書き込みデータベースを識別するには、値として READ_WRITE を指定します。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [可用性グループの読み取り専用ルーティングの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [Always On:読み取り可能なセカンダリの価格提案](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-value-proposition-of-readable-secondary.aspx)  
  
-   [Always On:読み取りワークロードのセカンダリ レプリカを有効にするオプションが 2 つ存在する理由](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-why-there-are-two-options-to-enable-a-secondary-replica-for-read-workload.aspx)  
  
-   [Always On:読み取り可能なセカンダリ レプリカのセットアップ](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-setting-up-readable-seconary-replica.aspx)  
  
-   [Always On:読み取り可能なセカンダリを有効にしたばかりだが、クエリがブロックされる](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-i-just-enabled-readble-secondary-but-my-query-is-blocked.aspx)  
  
-   [Always On:読み取り可能なセカンダリ、読み取り専用のデータベース、データベースのスナップショットで最新の統計情報を取得できるようにする](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-making-upto-date-statistics-available-on-readable-secondary-read-only-database-and-database-snapshot.aspx)  
  
-   [Always On:読み取り専用のデータベース、データベースのスナップショット、セカンダリ レプリカでの統計に関する課題](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-challenges-with-statistics-on-readonly-database-database-snapshot-and-secondary-replica.aspx)  
  
-   [Always On:セカンダリ レプリカでレポート ワークロードを実行した場合にプライマリ ワークロードに及ぶ影響](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-impact-on-the-primary-workload-when-you-run-reporting-workload-on-the-secondary-replica.aspx)  
  
-   [Always On:読み取り可能なセカンダリのレポート ワークロードをスナップショット分離にマップした場合の影響](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-impact-of-mapping-reporting-workload-to-snapshot-isolation-on-readable-secondary.aspx)  
  
-   [Always On:セカンダリ レプリカでレポート ワークロードを実行する場合に再実行スレッドのブロッキングを最小限に抑える](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On-minimizing-blocking-of-redo-thread-when-running-reporting-workload-on-secondary-replica.aspx)  
  
-   [Always On:読み取り可能なセカンダリとデータ待機時間](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/Always%20On.aspx)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [アクティブなセカンダリ:読み取り可能なセカンダリ レプリカ &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [可用性レプリカに対するクライアント接続アクセスについて &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)  
  
  
