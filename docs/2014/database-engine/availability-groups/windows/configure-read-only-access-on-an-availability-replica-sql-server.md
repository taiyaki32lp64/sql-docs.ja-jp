---
title: 可用性レプリカでの読み取り専用アクセスの構成 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: d93f78c157d5551e805437f156b8972ca8616c2b
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797739"
---
# <a name="configure-read-only-access-on-an-availability-replica-sql-server"></a>可用性レプリカでの読み取り専用アクセスの構成 (SQL Server)
  既定では、プライマリ レプリカへの読み取り/書き込みアクセスと読み取りを目的としたアクセスの両方が許可され、AlwaysOn 可用性グループのセカンダリ レプリカへの接続は許可されません。 このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、または PowerShell を使用して、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]の AlwaysOn 可用性グループの可用性レプリカに対して接続アクセスを構成する方法について説明します。  
  
 セカンダリ レプリカに対して読み取り専用アクセスを有効にすることによる影響と、接続アクセスの概要については、「[可用性レプリカに対するクライアント接続アクセスについて &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)」および「[アクティブなセカンダリ: 読み取り可能なセカンダリ レプリカ &#40;AlwaysOn 可用性グループ&#41;](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件と制限  
  
-   別の接続アクセスを構成するには、プライマリ レプリカをホストするサーバー インスタンスに接続している必要があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> アクセス許可  
  
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
  
         **可**  
         読み取りアクセスに限り、このレプリカのセカンダリ データベースに対するすべての接続が許可されます。 セカンダリ データベースはすべて読み取りアクセスで利用できます。  
  
    -   プライマリ ロールの場合は、 **[プライマリ ロールの接続]** ボックスの一覧から新しい値を選択します。値は次のとおりです。  
  
         **[すべての接続を許可]**  
         プライマリ レプリカのデータベースに対するすべての接続が許可されます。 これが既定の設定です。  
  
         **[読み取り/書き込みの接続を許可]**  
         Application Intent プロパティが **ReadWrite** に設定されている場合、または Application Intent 接続プロパティが設定されていない場合は、接続が許可されます。 Application Intent 接続プロパティが **ReadOnly** に設定されている接続は許可されません。 これにより、読み取りを目的としたワークロードが誤ってプライマリ レプリカに接続されるのを防ぐことができます。 "アプリケーションの目的" 接続プロパティの詳細については、「 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **可用性レプリカに対してアクセスを構成するには**  
  
> [!NOTE]  
>  この手順の例については、このセクションの後半の「[例 (Transact-SQL)](#TsqlExample)」を参照してください。  
  
1.  プライマリ レプリカをホストするサーバー インスタンスに接続します。  
  
2.  新しい可用性グループのレプリカを指定する場合は、 [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用します。 既存の可用性グループのレプリカを追加または変更する場合は、 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用します。  
  
    -   セカンダリ ロールの接続アクセスを構成するには、ADD REPLICA 句または MODIFY REPLICA WITH 句で、SECONDARY_ROLE オプションを次のように指定します。  
  
         SECONDARY_ROLE **(** ALLOW_CONNECTIONS **=** { NO | READ_ONLY | ALL } **)**  
  
         パラメーターの説明  
  
         いいえ  
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
  
```sql
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

### <a name="to-configure-access-on-an-availability-replica"></a>可用性レプリカに対してアクセスを構成するには
  
> [!NOTE]  
>  コード例については、このセクションで後述する PowerShell の例を参照してください。  
  
1.  プライマリ レプリカをホストするサーバー インスタンスにディレクトリを変更 (`cd`) します。  
  
2.  可用性グループに可用性レプリカを追加する場合は、`New-SqlAvailabilityReplica` コマンドレットを使用します。 既存の可用性レプリカを変更する場合は、`Set-SqlAvailabilityReplica` コマンドレットを使用します。 関連するパラメーターは次のとおりです。  
  
    -   セカンダリロールの接続アクセスを構成するには、`ConnectionModeInSecondaryRole`*secondary_role_keyword*パラメーターを指定します。 *secondary_role_keyword*は次のいずれかの値になります。  
  
         `AllowNoConnections`  
         セカンダリ レプリカのデータベースに対する直接接続は許可されず、データベースに対して読み取りアクセスを実行できません。 これが既定の設定です。  
  
         `AllowReadIntentConnectionsOnly`  
         Application Intent プロパティが **ReadOnly**に設定されている場合に限り、セカンダリ レプリカのデータベースに対する接続が許可されます。 このプロパティの詳細については、「 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
         `AllowAllConnections`  
         読み取り専用アクセスに限り、セカンダリ レプリカのデータベースに対するすべての接続が許可されます。  
  
    -   プライマリロールの接続アクセスを構成するには、`ConnectionModeInPrimaryRole`*primary_role_keyword*を指定します。 *primary_role_keyword*は次のいずれかの値になります。  
  
         `AllowReadWriteConnections`  
         Application Intent 接続プロパティが ReadOnly に設定されている接続は許可されません。 Application Intent プロパティが ReadWrite に設定されている場合、または Application Intent 接続プロパティが設定されていない場合は、接続が許可されます。 "アプリケーションの目的" 接続プロパティの詳細については、「 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
         `AllowAllConnections`  
         プライマリ レプリカのデータベースに対するすべての接続が許可されます。 これが既定の設定です。  
  
    > [!NOTE]  
    >  コマンドレットの構文を表示するには、`Get-Help` PowerShell 環境で [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)」を参照してください。  
  
SQL Server PowerShell プロバイダーを設定して使用する方法については、「 [SQL Server PowerShell プロバイダー](../../../powershell/sql-server-powershell-provider.md)」を参照してください。
  
以下の例は、`ConnectionModeInSecondaryRole` パラメーターと `ConnectionModeInPrimaryRole` パラメーターの両方を `AllowAllConnections` に設定しています。  
  
```powershell
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  

Set-SqlAvailabilityReplica -ConnectionModeInSecondaryRole "AllowAllConnections" `
 -InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ConnectionModeInPrimaryRole "AllowAllConnections" `
-InputObject $primaryReplica
```  

##  <a name="FollowUp"></a> 補足情報: 可用性レプリカに対する読み取り専用アクセスの構成後  
 **読み取り可能なセカンダリ レプリカに対する読み取り専用アクセス**  
  
-   [Bcp ユーティリティ](../../../tools/bcp-utility.md)または[sqlcmd ユーティリティ](../../../tools/sqlcmd-utility.md)を使用する場合は、`-K ReadOnly` スイッチを指定することによって、読み取り専用アクセスが有効になっている任意のセカンダリレプリカへの読み取り専用アクセスを指定できます。  
  
-   読み取り可能なセカンダリ レプリカに接続するクライアント アプリケーションを有効にするには:  
  
    ||前提条件|リンク|  
    |-|------------------|----------|  
    |![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|可用性グループにリスナーがあることを確認する。|[可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)|  
    |![Checkbox](../../media/checkboxemptycenterxtraspacetopandright.gif "Checkbox")|可用性グループの読み取り専用ルーティングを構成する。|[可用性グループの読み取り専用ルーティングの構成 &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)|  
  
 **フェールオーバー後にトリガーとジョブに影響する可能性がある要因**  
  
 読み取り可能でないセカンダリ データベースまたは読み取り可能なセカンダリ データベースで実行されたときに失敗するトリガーとジョブがある場合は、トリガーとジョブをスクリプト化して、特定のレプリカに対して、データベースがプライマリ データベースか読み取り可能なセカンダリ データベースかを確認する必要があります。 この情報を入手するには、データベースの [Updatability](/sql/t-sql/functions/databasepropertyex-transact-sql) プロパティを返す **DATABASEPROPERTYEX** 関数を使用します。 読み取り専用データベースを識別するには、次のように、値として READ_ONLY を指定します。  
  
```  
DATABASEPROPERTYEX([db name],'Updatability') = N'READ_ONLY'  
```  
  
 読み取り/書き込みデータベースを識別するには、値として READ_WRITE を指定します。  
  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [可用性グループの読み取り専用ルーティングの構成 &#40;SQL Server&#41;](configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [AlwaysOn: 読み取り可能なセカンダリの価値提案](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-value-proposition-of-readable-secondary.aspx)  
  
-   [AlwaysOn: 読み取りワークロードのためにセカンダリレプリカを有効にするオプションが2つあるのはなぜですか。](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-why-there-are-two-options-to-enable-a-secondary-replica-for-read-workload.aspx)  
  
-   [AlwaysOn: 読み取り可能なセカンダリレプリカのセットアップ](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-setting-up-readable-seconary-replica.aspx)  
  
-   [AlwaysOn: 読み取り可能なセカンダリを有効にしましたが、クエリはブロックされていますか?](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-i-just-enabled-readble-secondary-but-my-query-is-blocked.aspx)  
  
-   [AlwaysOn: 読み取り可能なセカンダリ、読み取り専用のデータベース、データベースのスナップショットで最新の統計情報を使用できるようにする](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-making-upto-date-statistics-available-on-readable-secondary-read-only-database-and-database-snapshot.aspx)  
  
-   [AlwaysOn: 読み取り専用データベース、データベーススナップショット、およびセカンダリレプリカの統計に関する課題](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-challenges-with-statistics-on-readonly-database-database-snapshot-and-secondary-replica.aspx)  
  
-   [AlwaysOn: セカンダリレプリカでレポートワークロードを実行するときの主要なワークロードへの影響](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-impact-on-the-primary-workload-when-you-run-reporting-workload-on-the-secondary-replica.aspx)  
  
-   [AlwaysOn: 読み取り可能なセカンダリでのレポートワークロードのスナップショット分離への影響](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-impact-of-mapping-reporting-workload-to-snapshot-isolation-on-readable-secondary.aspx)  
  
-   [AlwaysOn: セカンダリレプリカでレポートワークロードを実行するときの再実行スレッドのブロックを最小化する](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson-minimizing-blocking-of-redo-thread-when-running-reporting-workload-on-secondary-replica.aspx)  
  
-   [AlwaysOn: 読み取り可能なセカンダリとデータ待機時間](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2011/12/22/alwayson.aspx)  
  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループ&#40;SQL Server&#41;の概要](overview-of-always-on-availability-groups-sql-server.md)   
 [アクティブなセカンダリ: 読み取り可能&#40;なセカンダリレプリカ AlwaysOn 可用性グループ&#41;](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)  
 [可用性レプリカに対するクライアント接続アクセスについて &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)  
