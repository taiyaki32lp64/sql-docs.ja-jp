---
title: ALTER AVAILABILITY GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/02/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_AVAILABILITY_GROUP_TSQL
- ALTER_AVAILABILITY_TSQL
- ALTER AVAILABILITY GROUP
- ALTER AVAILABILITY
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- ALTER AVAILABILITY GROUP statement
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: f039d0de-ade7-4aaf-8b7b-d207deb3371a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1d3caeed2e7c57dfd4a3e993872034b066f56737
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874519"
---
# <a name="alter-availability-group-transact-sql"></a>ALTER AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既存の AlwaysOn 可用性グループを変更します。 ALTER AVAILABILITY GROUP のほとんどの引数は、現在のプライマリ レプリカでのみサポートされます。 ただし、JOIN、FAILOVER、FORCE_FAILOVER_ALLOW_DATA_LOSS の各引数は、セカンダリ レプリカでのみサポートされます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```SQL  
  
ALTER AVAILABILITY GROUP group_name   
  {  
     SET ( <set_option_spec> )   
   | ADD DATABASE database_name   
   | REMOVE DATABASE database_name  
   | ADD REPLICA ON <add_replica_spec>   
   | MODIFY REPLICA ON <modify_replica_spec>  
   | REMOVE REPLICA ON <server_instance>  
   | JOIN  
   | JOIN AVAILABILITY GROUP ON <add_availability_group_spec> [ ,...2 ]  
   | MODIFY AVAILABILITY GROUP ON <modify_availability_group_spec> [ ,...2 ]  
   | GRANT CREATE ANY DATABASE  
   | DENY CREATE ANY DATABASE  
   | FAILOVER  
   | FORCE_FAILOVER_ALLOW_DATA_LOSS   
   | ADD LISTENER 'dns_name' ( <add_listener_option> )  
   | MODIFY LISTENER 'dns_name' ( <modify_listener_option> )  
   | RESTART LISTENER 'dns_name'  
   | REMOVE LISTENER 'dns_name'  
   | OFFLINE  
  }  
[ ; ]  
  
<set_option_spec> ::=   
    AUTOMATED_BACKUP_PREFERENCE = { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
  | FAILURE_CONDITION_LEVEL  = { 1 | 2 | 3 | 4 | 5 }   
  | HEALTH_CHECK_TIMEOUT = milliseconds  
  | DB_FAILOVER  = { ON | OFF }   
  | DTC_SUPPORT  = { PER_DB | NONE }  
  | REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = { integer }
  
<server_instance> ::=   
 { 'system_name[\instance_name]' | 'FCI_network_name[\instance_name]' }  
  
<add_replica_spec>::=  
  <server_instance> WITH  
    (  
       ENDPOINT_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY },  
       FAILOVER_MODE = { AUTOMATIC | MANUAL }   
       [ , <add_replica_option> [ ,...n ] ]  
    )   
  
  <add_replica_option>::=  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
            [ ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL } ]   
        [,] [ READ_ONLY_ROUTING_URL = 'TCP://system-address:port' ]  
     } )  
     | PRIMARY_ROLE ( {   
            [ ALLOW_CONNECTIONS = { READ_WRITE | ALL } ]   
        [,] [ READ_ONLY_ROUTING_LIST = { ( '<server_instance>' [ ,...n ] ) | NONE } ]  
        [,] [ READ_WRITE_ROUTING_URL = { ( '<server_instance>' ) ] 
     } )  
     | SESSION_TIMEOUT = integer
  
<modify_replica_spec>::=  
  <server_instance> WITH  
    (    
       ENDPOINT_URL = 'TCP://system-address:port'   
     | AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }   
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }   
     | SEEDING_MODE = { AUTOMATIC | MANUAL }   
     | BACKUP_PRIORITY = n  
     | SECONDARY_ROLE ( {   
          ALLOW_CONNECTIONS = { NO | READ_ONLY | ALL }   
        | READ_ONLY_ROUTING_URL = 'TCP://system-address:port'   
          } )  
     | PRIMARY_ROLE ( {   
          ALLOW_CONNECTIONS = { READ_WRITE | ALL }   
        | READ_ONLY_ROUTING_LIST = { ( '<server_instance>' [ ,...n ] ) | NONE }   
          } )  
     | SESSION_TIMEOUT = seconds  
    )   
  
<add_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = MANUAL,  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<modify_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER = 'TCP://system-address:port'  
       | AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
       | SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<add_listener_option> ::=  
   {  
      WITH DHCP [ ON ( <network_subnet_option> ) ]  
    | WITH IP ( { ( <ip_address_option> ) } [ , ...n ] ) [ , PORT = listener_port ]  
   }  
  
  <network_subnet_option> ::=  
     'ipv4_address', 'ipv4_mask'    
  
  <ip_address_option> ::=  
     {   
        'four_part_ipv4_address', 'four_part_ipv4_mask'  
      | 'ipv6_address'  
     }  
  
<modify_listener_option>::=  
    {  
       ADD IP ( <ip_address_option> )   
     | PORT = listener_port  
    }  
  
```  
  
## <a name="arguments"></a>引数  
 *group_name*  
 新しい可用性グループの名前を指定します。 *group_name* は有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別子、およびその必要がありますで一意である、WSFC クラスター内のすべての可用性グループです。  
  
 AUTOMATED_BACKUP_PREFERENCE **=** { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
 バックアップを実行する場所を選択する際の、バックアップ ジョブによるプライマリ レプリカの評価方法についての優先設定を指定します。 自動バックアップの優先設定を考慮して、特定のバックアップ ジョブのスクリプトを作成できます。 優先設定は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって適用されるものではないので、アドホック バックアップには影響がないことを理解しておくことが重要です。  
  
 プライマリ レプリカでのみサポートされます。  
  
 値は次のとおりです。  
  
 PRIMARY  
 バックアップを常にプライマリ レプリカで実行することを指定します。 このオプションは、差分バックアップの作成など、バックアップがセカンダリ レプリカで実行されたときにはサポートされないバックアップ機能が必要な場合に役に立ちます。  
  
> [!IMPORTANT]  
>  ログ配布を使用して可用性グループのセカンダリ データベースを準備する場合は、すべてのセカンダリ データベースの準備が完了し、それらを可用性グループに参加させるまで、自動バックアップ設定を **[プライマリ]** に設定します。  
  
 SECONDARY_ONLY  
 バックアップをプライマリ レプリカでは実行しないことを指定します。 オンラインのレプリカがプライマリ レプリカだけの場合、バックアップは実行されません。  
  
 SECONDARY  
 オンラインのレプリカがプライマリ レプリカのみである場合を除き、セカンダリ レプリカでバックアップを実行することを指定します。 オンラインのレプリカがプライマリ レプリカのみである場合は、プライマリ レプリカでバックアップを実行する必要があります。 これは既定の動作です。  
  
 NONE  
 バックアップを実行するレプリカを選択するときにバックアップ ジョブが可用性レプリカのロールを無視するように指定します。 バックアップ ジョブは、動作状態および接続状態と組み合わせて、各可用性レプリカのバックアップ優先順位などの他の要素を評価する場合があります。  
  
> [!IMPORTANT]  
>  AUTOMATED_BACKUP_PREFERENCE 設定の適用はありません。 この優先設定の解釈は、特定の可用性グループのデータベースに対するバックアップ ジョブのスクリプトでのロジックに依存します (ある場合)。 自動バックアップ設定はアドホック バックアップには影響しません。 詳細については、「[可用性レプリカでのバックアップの構成 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  既存の可用性グループの自動バックアップ設定を確認するには、[sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) カタログ ビューの **automated_backup_preference** 列または **automated_backup_preference_desc** 列を選択します。 また、[sys.fn_hadr_backup_is_preferred_replica  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md) を使用し、優先バックアップ レプリカを決定できます。  `AUTOMATED_BACKUP_PREFERENCE = NONE` の場合でも、この関数は常に、少なくとも 1 つのレプリカに対して 1 を返します。  
  
 FAILURE_CONDITION_LEVEL **=** { 1 | 2 | **3** | 4 | 5 }  
 この可用性グループの自動フェールオーバーをトリガーするエラー状態を指定します。 FAILURE_CONDITION_LEVEL はグループ レベルで設定されますが、同期コミット可用性モードに構成されている (AVAILABILITY_MODE **=** SYNCHRONOUS_COMMIT) 可用性レプリカにのみ適用されます。 さらに、エラー状態が自動フェールオーバーをトリガーできるのは、プライマリとセカンダリの両方のレプリカが自動フェールオーバー モードに構成されていて (FAILOVER_MODE **=** AUTOMATIC)、セカンダリ レプリカが現在プライマリ レプリカと同期されている場合だけです。  
  
 プライマリ レプリカでのみサポートされます。  
  
 エラー状態レベルの範囲は 1 ～ 5 で、レベル 1 が最も制限が緩く、レベル 5 が最も制限の厳しい指定です。 任意の状態レベルは、それより制限が緩いすべてのレベルを含みます。 したがって、最も厳しい状態レベル 5 にはそれより制限が緩い状態レベル (1 から 4) が含まれ、レベル 4 にはレベル 1 から 3 が含まれます。以下同様です。 次の表では、各レベルに対応するエラー状態について説明します。  
  
|Level|エラー状態|  
|-----------|-----------------------|  
|1|次のいずれかが発生した場合に自動フェールオーバーを開始する必要があることを指定します。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスがダウンした。<br /><br /> WSFC クラスターに接続するための可用性グループのリースが、サーバー インスタンスから ACK を受信しないために期限切れになった。 詳細については、「[How It Works:SQL Server Always On Lease Timeout (動作方法: SQL Server AlwaysOn のリース タイムアウト)](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)」を参照してください。|  
|2|次のいずれかが発生した場合に自動フェールオーバーを開始する必要があることを指定します。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスがクラスターに接続しておらず、可用性グループのユーザー指定の HEALTH_CHECK_TIMEOUT しきい値を超えた。<br /><br /> 可用性レプリカがエラー状態である。|  
|3|孤立したスピンロック、重大な書き込みアクセス違反、ダンプが多すぎるなどの重大な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部エラーが発生した場合に自動フェールオーバーを開始する必要があることを指定します。<br /><br /> これは既定の動作です。|  
|4|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部リソース プールに永続的なメモリ不足の状態があるなど、中程度の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部エラーが発生した場合に自動フェールオーバーを開始する必要があることを指定します。|  
|5|以下のような任意の修飾エラー状態に対して自動フェールオーバーを開始する必要があることを指定します。<br /><br /> SQL エンジンのワーカー スレッドが枯渇している。<br /><br /> 解決不可能なデッドロックが検出された。|  
  
> [!NOTE]  
>  クライアント要求に対して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが応答しないことは、可用性グループには関係ありません。  
  
 FAILURE_CONDITION_LEVEL 値と HEALTH_CHECK_TIMEOUT 値は、特定のグループに対する*柔軟なフェールオーバー ポリシー*を定義します。 この柔軟なフェールオーバー ポリシーを使用すると、自動フェールオーバーを引き起こす条件をきめ細かく制御できます。 詳細については、「[可用性グループの自動フェールオーバーのための柔軟なフェールオーバー ポリシー &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md)」を参照してください。  
  
 HEALTH_CHECK_TIMEOUT **=** *milliseconds*  
 [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) システム ストアド プロシージャによってサーバーの状態情報が返されるのを待機する時間 (ミリ秒単位) を指定します。この時間が経過すると、WSFC クラスターはサーバー インスタンスが速度低下または応答停止しているものと見なします。 HEALTH_CHECK_TIMEOUT はグループ レベルで設定されますが、自動フェールオーバーで同期コミット可用性モードが構成されている (AVAILABILITY_MODE **=** SYNCHRONOUS_COMMIT) 可用性レプリカにのみ適用されます。  さらに、正常性チェック タイムアウトが自動フェールオーバーをトリガーできるのは、プライマリとセカンダリの両方のレプリカが自動フェールオーバー モードに構成されていて (FAILOVER_MODE **=** AUTOMATIC)、セカンダリ レプリカが現在プライマリ レプリカと同期されている場合だけです。  
  
 HEALTH_CHECK_TIMEOUT の既定値は 30000 ミリ秒 (30 秒) です。 最小値は 15,000 ミリ秒 (15 秒)、最大値は 4,294,967,295 ミリ秒です。  
  
 プライマリ レプリカでのみサポートされます。  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** では、データベース レベルでの正常性チェックは実行されません。  
  
 DB_FAILOVER  **=** { ON | OFF }  
 プライマリ レプリカ上のデータベースがオフラインのときに実行する応答を指定します。 ON に設定すると、可用性グループ内のデータベースがオンライン以外のすべての状態で、自動フェールオーバーがトリガーされます。 このオプションが OFF に設定されている場合は、インスタンスの正常性だけが自動フェールオーバーのトリガーに使用されます。  
 
 この設定の詳細については、「[データベース レベルの正常性検出オプション](../../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md)」を参照してください。 

DTC_SUPPORT  **=** { PER_DB | NONE }  
この可用性グループの分散トランザクションが有効かどうかを指定します。 分散トランザクションは [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降の可用性グループ データベースに対してのみサポートされ、複数データベースにまたがるトランザクションは [!INCLUDE[ssSQL16](../../includes/sssql15-md.md)] SP2 以降に対してのみサポートされます。 `PER_DB` では、これらのトランザクションをサポートする可用性グループが作成され、可用性グループ内のデータベースを含む複数データベースにまたがるトランザクションが分散トランザクションに自動的に昇格されます。 `NONE` では、複数データベースにまたがるトランザクションは分散トランザクションに自動昇格されず、データベースは DTC の安定した RMID に登録されません。 `NONE` の設定を使用しても分散トランザクションは妨げられませんが、状況によってはデータベースのフェールオーバーと自動復旧が失敗する場合があります。 詳細については、「[Always On 可用性グループとデータベース ミラーリングでの複数データベースにまたがるトランザクションと分散トランザクション &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)」を参照してください。 
 
> [!NOTE]
> 可用性グループの設定 DTC_SUPPORT の変更のサポートは、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Service Pack 2 で導入されました。 それより前のバージョンでは、このオプションは使用できません。 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] の以前のバージョンでこの設定を変更するには、可用性グループをいったん削除してから、再度作成する必要があります。
 
 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT   
 SQL Server 2017 で導入されました。 コミットに必要な同期セカンダリ レプリカの最小数を設定します。この数を超えると、プライマリがトランザクションをコミットします。 SQL Server トランザクションは、セカンダリ レプリカの最小数の最新情報がトランザクション ログに与えられるまで待機することになります。 既定値は 0 であり、SQL Server 2016 と同じように動作します。 最小値は 0 です。 最大値はレプリカの数から 1 を引いた値になります。 このオプションは、同期コミット モードのレプリカに関連しています。 レプリカが同期コミット モードのとき、セカンダリ同期レプリカに対する書き込みがレプリカ データベース トランザクション ログにコミットされるまで、プライマリ レプリカへの書き込みは待機します。 セカンダリ同期レプリカをホストする SQL Server が応答を停止した場合、プライマリ レプリカをホストする SQL Server はそのセカンダリ レプリカを同期未実行としてマークし、続行します。 応答のないデータベースがオンラインに復帰すると、"未同期" 状態になります。プライマリが再度同期可能になるまで、レプリカに異常のマークが付きます。 この設定により、レプリカの最小数で各トランザクションがコミットされるまで、プライマリ レプリカは続行しません。 レプリカの最小数が利用できない場合、プライマリのコミットは失敗します。 クラスター タイプ `EXTERNAL` の場合、可用性グループがクラスター リソースに追加されると、設定が変更されます。 「[High availability and data protection for availability group configurations](../../linux/sql-server-linux-availability-group-ha.md)」 (可用性グループ構成の高可用性とデータ保護) を参照してください。
  
 ADD DATABASE *database_name*  
 可用性グループに追加する 1 つ以上のユーザー データベースのリストを指定します。 これらのデータベースは、現在のプライマリ レプリカをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス上にある必要があります。 1 つの可用性グループに対して複数のデータベースを指定できますが、各データベースが所属できる可用性グループは 1 つだけです。 可用性グループでサポートできるデータベースの種類については、「[Always On 可用性グループの前提条件、制限事項、推奨事項 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。 可用性グループに既に属しているローカル データベースを確認する場合は、[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) カタログ ビューで **replica_id** 列を参照してください。  
  
 プライマリ レプリカでのみサポートされます。  
  
> [!NOTE]  
>  可用性グループを作成した後、セカンダリ レプリカをホストする各サーバー インスタンスに接続して、各セカンダリ データベースを準備し、可用性グループに参加させる必要があります。 詳細については、「 [AlwaysOn セカンダリ データベース上のデータ移動の開始 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)」を参照してください。  
  
 REMOVE DATABASE *database_name*  
 指定したプライマリ データベースと、対応するセカンダリ データベースを可用性グループから削除します。 プライマリ レプリカでのみサポートされます。  
  
 可用性グループから可用性データベースを削除した後の推奨するフォロー アップの詳細については、「[可用性グループからのプライマリ データベースの削除 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)」を参照してください。  
  
 ADD REPLICA ON  
 可用性グループのセカンダリ レプリカをホストする 1 ～ 8 個の SQL Server インスタンスを指定します。  各レプリカを指定する際には、サーバー インスタンスのアドレスに続けて WITH (...) 句を入力します。  
  
 プライマリ レプリカでのみサポートされます。  
  
 すべての新しいセカンダリ レプリカを可用性グループに参加させる必要があります。 詳細については、後述する JOIN オプションの説明を参照してください。  
  
 \<server_instance>  
 レプリカのホストである [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのアドレスを指定します。 アドレスの形式は、インスタンスが既定のインスタンスか名前付きインスタンスか、およびスタンドアロン インスタンスかフェールオーバー クラスター インスタンス (FCI) かによって異なります。 構文は次のとおりです。  
  
 { '*system_name*[\\*instance_name*]' | '*FCI_network_name*[\\*instance_name*]' }  
  
 このアドレスの構成要素は次のとおりです。  
  
 *system_name*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のターゲット インスタンスが存在するコンピューター システムの NetBIOS 名です。 このコンピューターは WSFC ノードである必要があります。  
  
 *FCI_network_name*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターにアクセスするために使用されるネットワーク名です。 サーバー インスタンスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー パートナーとして参加している場合に使用します。 FCI サーバー インスタンスで SELECT [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md) を実行すると、'*FCI_network_name*[\\*instance_name*]' という文字列全体 (完全なレプリカ名) が返されます。  
  
 *instance_name*  
 *system_name* または *FCI_network_name* によってホストされ、AlwaysOn が有効になっている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前です。 既定のサーバー インスタンスの場合、 *instance_name* は省略可能です。 インスタンス名では大文字と小文字が区別されません。 スタンドアロン サーバー インスタンスでは、この名前の値は SELECT [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md) を実行したときに返される値と同じです。  
  
 \  
 *system_name* または *FCI_network_name* と区別するために、*instance_name* を指定するときにのみ使用される区切り記号です。  
  
 WSFC ノードとサーバーのインスタンスの前提条件の詳細については、「[AlwaysOn 可用性グループの前提条件、制限事項、推奨事項 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。  
  
 ENDPOINT_URL ='TCP://*system-address*:*port*'  
 追加または変更している可用性レプリカをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス上の[データベース ミラーリング エンドポイント](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)の URL パスを指定します。  
  
 ENDPOINT_URL は、ADD REPLICA ON 句では必須で、MODIFY REPLICA ON 句では省略可能です。  詳細については、「 [可用性レプリカを追加または変更する場合のエンドポイント URL の指定 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)の構成に関する一般的な問題のトラブルシューティングに役立つ情報を提供します。  
  
 **'** TCP **://** _system-address_ **:** _port_ **'**  
 エンドポイントの URL または読み取り専用ルーティングの URL を指定するための URL を指定します。 URL のパラメーターは次のとおりです。  
  
 *system-address*  
 システム名、完全修飾ドメイン名では、対象のコンピューター システムを明確に識別する、IP アドレスなどの文字列です。  
  
 *port*  
 サーバー インスタンスのミラーリング エンドポイントと関連付けられているポート番号 (ENDPOINT_URL オプションの場合)、またはサーバー インスタンスの [!INCLUDE[ssDE](../../includes/ssde-md.md)]によって使用されるポート番号 (READ_ONLY_ROUTING_URL オプションの場合) です。  
  
 AVAILABILITY_MODE **=** { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY }  
 プライマリ レプリカによって特定のプライマリ データベースでのトランザクションがコミットされる前に、セカンダリ レプリカによるディスクへのログ レコードの固定 (書き込み) の確認応答を待機する必要があるかどうかを指定します。 同じプライマリ レプリカに対する異なるデータベースでのトランザクションは個別にコミットできます。  
  
 SYNCHRONOUS_COMMIT  
 このセカンダリ レプリカでトランザクションが書き込まれるまで、プライマリ レプリカがトランザクションのコミットを待機することを指定します (同期コミット モード)。 SYNCHRONOUS_COMMIT は、プライマリ レプリカを含む最大 3 つのレプリカに対して指定できます。  
  
 ASYNCHRONOUS_COMMIT  
 このセカンダリ レプリカでログが書き込まれるのを待たずに、プライマリ レプリカによってトランザクションがコミットされるよう指定します (同期コミット可用性モード)。 ASYNCHRONOUS_COMMIT は、プライマリ レプリカを含む最大 5 つの可用性レプリカに対して指定できます。  

 CONFIGURATION_ONLY プライマリ レプリカがこのレプリカの master データベースに可用性グループ構成メタデータを同期コミットするように指定します。 このレプリカにはユーザー データは含まれません。 このオプションの特徴:

- Express Edition など、SQL Server のあらゆるエディションでホストできます。
- CONFIGURATION_ONLY レプリカのデータ ミラーリング エンドポイントの型を `WITNESS` にする必要があります。
- 変更できません。
- `CLUSTER_TYPE = WSFC` の場合は無効です。 

   詳細については、[構成のみのレプリカ](../../linux/sql-server-linux-availability-group-ha.md)に関するページを参照してください。
    
 AVAILABILITY_MODE は、ADD REPLICA ON 句では必須で、MODIFY REPLICA ON 句では省略可能です。 詳細については、「[可用性モード &#40;Always On 可用性グループ&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)」を参照してください。  
  
 FAILOVER_MODE **=** { AUTOMATIC | MANUAL }  
 定義している可用性レプリカのフェールオーバー モードを指定します。  
  
 AUTOMATIC  
 自動フェールオーバーを有効にします。 AUTOMATIC は、AVAILABILITY_MODE = SYNCHRONOUS_COMMIT も指定した場合にのみサポートされます。 AUTOMATIC は、プライマリ レプリカを含む 3 つの可用性レプリカに対して指定できます。  
  
> [!NOTE]  
>  SQL Server 2016 より前は、プライマリ レプリカを含めて 2 つの自動フェールオーバー レプリカに制限されていました
  
> [!NOTE]  
>  SQL Server フェールオーバー クラスター インスタンス (FCI) は可用性グループによる自動フェールオーバーをサポートしないため、FCI によってホストされる可用性レプリカは手動フェールオーバー用にのみ構成できます。  
  
 MANUAL  
 データベース管理者による手動フェールオーバーまたは強制手動フェールオーバー (*強制フェールオーバー*) を有効にします。  
  
 FAILOVER_MODE は、ADD REPLICA ON 句では必須で、MODIFY REPLICA ON 句では省略可能です。 手動フェールオーバーにはデータ損失のない手動フェールオーバーと強制フェールオーバー (データ損失の可能性あり) の 2 種類があり、異なる条件の下でサポートされます。  詳細については、「 [フェールオーバーとフェールオーバー モード &#40;AlwaysOn 可用性グループ&#41;](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)、または PowerShell を使用して、AlwaysOn 可用性グループ上で計画的な手動フェールオーバーまたは強制手動フェールオーバー (強制フェールオーバー) を実行する方法について説明します。  
  
 SEEDING_MODE **=** { AUTOMATIC | MANUAL }  
 セカンダリ レプリカの初回シード処理方法を指定します。  
  
 AUTOMATIC  
 直接シード処理を有効にします。 この方法では、ネットワーク全体でセカンダリ レプリカがシード処理されます。 この方法では、レプリカでプライマリ データベースのコピーをバックアップしたり、復元したりする必要がありません。  
  
> [!NOTE]  
>  直接シード処理の場合、セカンダリ レプリカごとにデータベース作成を許可する必要があります。**GRANT CREATE ANY DATABASE** オプションを指定し、**ALTER AVAILABILITY GROUP** を呼び出してください。  
  
 MANUAL  
 手動シード処理を指定します (既定)。 この方法では、プライマリ レプリカでデータベースのバックアップを作成し、セカンダリ レプリカでそのバックアップを手動で復元する必要があります。  
  
 BACKUP_PRIORITY **=** _n_  
 同じ可用性グループ内の他のレプリカと比較して、このレプリカでバックアップを実行する優先順位を指定します。 値は 0 ～ 100 の範囲の整数です。 これらの値には次の意味があります。  
  
-   1 から 100 は、その可用性レプリカがバックアップの実行に向けて選択される可能性があることを示します。 1 は最も低い優先順位を示し、100 は最も高い優先順位を示します。 BACKUP_PRIORITY = 1 の場合、現在使用可能な可用性レプリカにそれより高い優先順位のものがない場合にのみ、その可用性レプリカがバックアップの実行に向けて選択されます。  
  
-   0 は、その可用性レプリカがバックアップの実行に対して選択されないことを示します。 これは、たとえば、バックアップをフェールオーバーすることがないリモート可用性レプリカのような場合に便利です。  
  
 詳細については、「[アクティブなセカンダリ:セカンダリ レプリカでのバックアップ &#40;Always On 可用性グループ&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
 SECONDARY_ROLE **(** ... **)**  
 この可用性レプリカによって現在セカンダリ ロールが所有されている場合に (つまり、セカンダリ レプリカである場合は常に) 有効な、ロール固有の設定を指定します。 かっこの中では、いずれか一方または両方のセカンダリ ロール オプションを指定します。 両方を指定する場合は、コンマ区切りのリストを使用します。  
  
 セカンダリ ロール オプションは次のとおりです。  
  
 ALLOW_CONNECTIONS **=** { NO | READ_ONLY | ALL }  
 セカンダリ ロールを実行している (つまりセカンダリ レプリカとして機能している) 特定の可用性レプリカのデータベースがクライアントから接続を受け入れることができるかどうかを指定します。以下のいずれかになります。  
  
 NO  
 このレプリカのセカンダリ データベースに対するユーザー接続は禁止されます。 読み取りアクセスで利用することはできません。 これは既定の動作です。  
  
 READ_ONLY  
 Application Intent プロパティが **ReadOnly** に設定されている場合に限り、セカンダリ レプリカのデータベースに対する接続が許可されます。 このプロパティの詳細については、「 [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
 ALL  
 読み取り専用アクセスに限り、セカンダリ レプリカのデータベースに対するすべての接続が許可されます。  
  
 詳細については、「[アクティブなセカンダリ:読み取り可能なセカンダリ レプリカ &#40;AlwaysOn 可用性グループ&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
 READ_ONLY_ROUTING_URL **='** TCP **://** _system-address_ **:** _port_ **'**  
 読み取りを目的とした接続要求をこの可用性レプリカにルーティングするために使用する URL を指定します。 これは、SQL Server データベース エンジンがリッスンしている URL です。 通常、SQL Server データベース エンジンの既定のインスタンスは、TCP ポート 1433 でリッスンします。  
  
 名前付きインスタンスの場合は、[sys.dm_tcp_listener_states](../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md) 動的管理ビューの **port** 列と **type_desc** 列をクエリすることで、ポート番号を取得できます。 サーバー インスタンスは Transact-SQL リスナーを使用します (**type_desc='TSQL'** )。  
  
 可用性レプリカの読み取り専用ルーティングの URL の計算の詳細については、「[AlwaysOn の read_only_routing_url の計算](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-Always%20On.aspx)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前付きインスタンスの場合は、特定のポートを使用するように Transact-SQL リスナーを構成する必要があります。 詳細については、「[特定の TCP ポートで受信待ちするようにサーバーを構成する方法 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)」を参照してください。  
  
 PRIMARY_ROLE **(** ... **)**  
 この可用性レプリカによって現在セカンダリ ロールが所有されている場合に (つまり、プライマリ レプリカである場合は常に) 有効な、ロール固有の設定を指定します。 かっこの中では、いずれか一方または両方のプライマリ ロール オプションを指定します。 両方を指定する場合は、コンマ区切りのリストを使用します。  
  
 プライマリ ロール オプションは次のとおりです。  
  
 ALLOW_CONNECTIONS **=** { READ_WRITE | ALL }  
 プライマリ ロールを実行している (つまりプライマリ レプリカとして機能している) 特定の可用性レプリカのデータベースが受け入れることのできるクライアントからの接続の種類を指定します。以下のいずれかになります。  
  
 READ_WRITE  
 Application Intent 接続プロパティが **ReadOnly** に設定されている接続は許可されません。  Application Intent プロパティが **ReadWrite** に設定されている場合、または Application Intent 接続プロパティが設定されていない場合は、接続が許可されます。 "アプリケーションの目的" 接続プロパティの詳細については、「 [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
 ALL  
 プライマリ レプリカのデータベースに対するすべての接続が許可されます。 これは既定の動作です。  
  
 READ_ONLY_ROUTING_LIST **=** { **('** \<server_instance> **'** [ **,** ...*n* ] **)** | NONE }  
 セカンダリ ロールの下で実行するときに次の要件を満たす、この可用性グループの可用性レプリカをホストするサーバー インスタンスのコンマ区切りリストを指定します。  
  
-   すべての接続または読み取り専用の接続を許可するように構成されていること (前に示した SECONDARY_ROLE オプションの ALLOW_CONNECTIONS 引数を参照)。  
  
-   読み取り専用ルーティングの URL が定義されていること (前に示した SECONDARY_ROLE オプションの READ_ONLY_ROUTING_URL 引数を参照)。  
  
 READ_ONLY_ROUTING_LIST の値は次のとおりです。  
  
 \<server_instance>  
 セカンダリ ロールで実行するときに読み取り可能なセカンダリ レプリカである可用性レプリカをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのアドレスを指定します。  
  
 読み取り可能なセカンダリ レプリカをホストする可能性があるすべてのサーバー インスタンスを指定するには、コンマ区切りのリストを使用します。 読み取り専用のルーティングは、リストで指定されているサーバー インスタンスの順序に従います。 レプリカの読み取り専用ルーティング リストにレプリカのホスト サーバー インスタンスを含める場合、通常は一覧の最後にこのサーバー インスタンスを配置することをお勧めします。読み取りを目的とした接続が使用できる場合に、これがセカンダリ レプリカに移動するためです。  
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、読み取り可能なセカンダリ レプリカ間で読み取りを目的とした要求の負荷を分散することができます。 読み取り専用ルーティング リスト内のかっこの入れ子になったセットにレプリカを配置することで、これを指定します。 詳細と例については、「[読み取り専用レプリカ間の負荷分散の構成](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing)」を参照してください。  
  
 NONE  
 この可用性レプリカがプライマリ レプリカの場合は、読み取り専用のルーティングをサポートしないことを指定します。 これは既定の動作です。 MODIFY REPLICA ON と併せて使用すると、この値は既存のリスト (ある場合) を無効にします。  
  
 SESSION_TIMEOUT **=** _seconds_  
 セッション タイムアウト期間を秒単位で指定します。 このオプションを指定しない場合、この時間は既定で 10 秒に設定されます。 最小値は 5 秒です。  
  
> [!IMPORTANT]  
>  タイムアウト期間を 10 秒以上にしておくことをお勧めします。  
  
 セッション タイムアウト期間の詳細については、「[AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)」を参照してください。  
  
 MODIFY REPLICA ON  
 可用性グループの任意のレプリカを変更します。 変更対象のレプリカの一覧には、サーバー インスタンスのアドレスと、各レプリカに対する WITH (...) 句が含まれます。  
  
 プライマリ レプリカでのみサポートされます。  
  
 REMOVE REPLICA ON  
 指定したセカンダリ レプリカを可用性グループから削除します。 現在のプライマリ レプリカを可用性グループから削除することはできません。 レプリカが削除されると、データの受信が停止します。 セカンダリ データベースが可用性グループから削除され、RESTORING 状態に移行します。  
  
 プライマリ レプリカでのみサポートされます。  
  
> [!NOTE]  
>  使用不可中または障害発生中のレプリカを削除した場合、オンラインに戻ったレプリカでは、可用性グループに属していないことが検出されます。  
  
 JOIN  
 ローカル サーバー インスタンスにより、指定した可用性グループ内のセカンダリ レプリカがホストされるようになります。  
  
 可用性グループにまだ参加していないセカンダリ レプリカでのみサポートされます。  
  
 詳細については、「 [可用性グループへのセカンダリ レプリカの参加 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)、または PowerShell を使用して、既存の AlwaysOn 可用性グループにセカンダリ レプリカを追加する方法について説明します。  
  
 FAILOVER  
接続されているセカンダリ レプリカへの可用性グループのデータ損失のない手動フェールオーバーを開始します。 プライマリ レプリカをホストするレプリカは*フェールオーバー ターゲット*です。  フェールオーバー ターゲットによってプライマリ ロールが引き継がれ、各データベースのコピーが復旧されて、新しいプライマリ データベースとしてオンラインになります。 元のプライマリ レプリカは同時にセカンダリ ロールに移行し、そのデータベースがセカンダリ データベースになって、直ちに中断されます。 これらのロールは、連続する障害によって繰り返し切り替えられる可能性があります。  
  
 現在プライマリ レプリカと同期されている同期コミット モードのセカンダリ レプリカでのみサポートされます。 セカンダリ レプリカを同期する場合、プライマリ レプリカも同期コミット可用性モードで実行されている必要があります。  
  
> [!NOTE]  
>  フェールオーバー コマンドは、フェールオーバー ターゲットがコマンドを受け入れた直後に戻ります。 ただし、データベースの復旧は、可用性グループがフェールオーバーを完了した後に非同期で行われます。  
  
 計画的な手動フェールオーバーを実行する場合の制限、前提条件、推奨事項については、「[可用性グループの計画的な手動フェールオーバーの実行 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)」を参照してください。  
  
 FORCE_FAILOVER_ALLOW_DATA_LOSS  
 > [!CAUTION]  
>  データの損失を伴う可能性があるフェールオーバーの強制は、厳密にはディザスター リカバリー手段です。 したがって、プライマリ レプリカが動作しなくなった状況で、データの損失を許容でき、可用性グループに直ちにサービスを復元する必要がある場合のみ、強制フェールオーバーを実行することを強くお勧めします。  
  
 ロールが SECONDARY 状態または RESOLVING 状態であるレプリカでのみサポートされます。 --フェールオーバー コマンドを入力する対象のレプリカは、*フェールオーバー ターゲット*と呼ばれます。  
  
 フェールオーバー ターゲットへの可用性グループのフェールオーバーを強制します (データ損失の可能性あり)。 フェールオーバー ターゲットによってプライマリ ロールが引き継がれ、各データベースのコピーが復旧されて、新しいプライマリ データベースとしてオンラインになります。 残りのセカンダリ レプリカのすべてのセカンダリ データベースは手動で再開するまで中断されます。 元のプライマリ レプリカが使用可能になった場合はセカンダリ ロールに切り替わり、そのデータベースは中断されたセカンダリ データベースになります。  
  
> [!NOTE]  
>  フェールオーバー コマンドは、フェールオーバー ターゲットがコマンドを受け入れた直後に戻ります。 ただし、データベースの復旧は、可用性グループがフェールオーバーを完了した後に非同期で行われます。  
  
 強制フェールオーバーの制限、前提条件、推奨事項について、およびフェールオーバー グループ内の以前のプライマリ データベースに対する強制フェールオーバーの影響については、「[可用性グループの強制手動フェールオーバーの実行 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)」を参照してください。  
  
 ADD LISTENER **'** _dns\_name_ **'(** \<add_listener_option> **)**  
 この可用性グループの新しい可用性グループ リスナーを定義します。 プライマリ レプリカでのみサポートされます。  
  
> [!IMPORTANT]
>  最初のリスナーを作成する前に、「[可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)」をお読みになることを強くお勧めします。  
> 
>  可用性グループのリスナーを作成した後は、次のことを行うことを強くお勧めします。  
> 
>  -   リスナーの IP アドレスが排他的に使用されるように確保することを、ネットワーク管理者に依頼します。  
> -   この可用性グループへのクライアント接続を要求するときの接続文字列で使用できるよう、リスナーの DNS ホスト名をアプリケーション開発者に通知します。  
  
 *dns_name*  
 可用性グループ リスナーの DNS ホスト名を指定します。 リスナーの DNS 名が、ドメインおよび NetBIOS 内で一意である必要があります。  
  
 *dns_name* は文字列値です。 この名前には、英数字、ダッシュ (-)、およびハイフン (_) のみを任意の順序で含めることができます。 DNS ホスト名では大文字と小文字は区別されません。 最大長は 63 文字です。  
  
 意味のある文字列を指定することをお勧めします。 たとえば、可用性グループの名前が `AG1`の場合は、 `ag1-listener`のような意味のある DNS ホスト名にします。  
  
> [!IMPORTANT]  
>  NetBIOS では、dns_name の最初の 15 文字のみが認識されます。 同じ Active Directory で制御されている 2 つの WSFC クラスターがあり、両方のクラスターで可用性グループ リスナーを作成しようとする場合、15 文字より長い名前を使用して、15 文字のプレフィックスが同一であると、仮想ネットワーク名リソースをオンラインにできなかったことを示すエラーが表示されます。 DNS 名のプレフィックスに対する名前付け規則の詳細については、「 [ドメイン名を割り当てる](https://technet.microsoft.com/library/cc731265\(WS.10\).aspx)」を参照してください。  
  
 JOIN AVAILABILITY GROUP ON  
 *分散可用性グループ*に参加します。 分散可用性グループを作成すると、それが作成されたクラスターの可用性グループがプライマリの可用性グループになります。 分散可用性グループに参加する可用性グループがセカンダリ可用性グループになります。  
  
 \<ag_name>  
 分散可用性グループの半分を占める可用性グループの名前を指定します。  
  
 LISTENER **='** TCP **://** _system-address_ **:** _port_ **'**  
 可用性グループに関連付けられているリスナーの URL パスを指定します。  
  
 LISTENER 句は必須です。  
  
 **'** TCP **://** _system-address_ **:** _port_ **'**  
 可用性グループに関連付けられているリスナーの URL を指定します。 URL のパラメーターは次のとおりです。  
  
 *system-address*  
 システム名、完全修飾ドメイン名、IP アドレスなど、リスナーを明確に識別する文字列です。  
  
 *port*  
 可用性グループのミラーリング エンドポイントに関連付けられているポート番号です。 これはリスナーのポートではないことにご注意ください。  
  
 AVAILABILITY_MODE **=** { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
 プライマリ レプリカが特定のプライマリ データベースでトランザクションをコミットする前に、ディスクへのログ レコードの書き込みがセカンダリ可用性グループで確認されるのを待機する必要があるかどうかを指定します。  
  
 SYNCHRONOUS_COMMIT  
 セカンダリ可用性グループでトランザクションが書き込まれるまで、プライマリはトランザクションのコミットを延期するように指定します。 SYNCHRONOUS_COMMIT は、プライマリ可用性グループを含む、最大 2 つの可用性グループに指定できます。  
  
 ASYNCHRONOUS_COMMIT  
 このセカンダリ可用性グループがログを書き込むのを待たず、プライマリ レプリカがトランザクションをコミットするように指定します。 ASYNCHRONOUS_COMMIT は、プライマリ可用性グループを含む、最大 2 つの可用性グループに指定できます。  
  
 AVAILABILITY_MODE 句は必須です。  
  
 FAILOVER_MODE **=** { MANUAL }  
 分散型可用性グループのフェールオーバー モードを指定します。  
  
 MANUAL  
 データベース管理者による計画的な手動フェールオーバーまたは強制手動フェールオーバー (通常は*強制フェールオーバー*と呼ばれる) を有効にします。  
  
 セカンダリ可用性グループへの自動フェールオーバーはサポートされていません。  
  
 SEEDING_MODE **=** { AUTOMATIC | MANUAL }  
 セカンダリ可用性グループの初回シード処理方法を指定します。  
  
 AUTOMATIC  
 自動シード処理を有効にします。 この方法では、ネットワーク全体でセカンダリ可用性グループがシード処理されます。 この方法では、セカンダリ可用性グループのレプリカでプライマリ データベースのコピーをバックアップしたり、復元したりする必要がありません。  
  
 MANUAL  
 手動シード処理を指定します。 この方法では、プライマリ レプリカでデータベースのバックアップを作成し、セカンダリ可用性グループのレプリカでそのバックアップを手動で復元する必要があります。  
  
 MODIFY AVAILABILITY GROUP ON  
 分散可用性グループの可用性グループ設定を変更します。 変更する可用性グループの一覧には、可用性グループの名前と可用性グループ別の WITH (...) 句が含まれています。  
  
> [!IMPORTANT]  
>  このコマンドはプライマリの可用性グループ インスタンスとセカンダリ可用性グループ インスタンスの両方で繰り返す必要があります。  
  
 GRANT CREATE ANY DATABASE  
 直接シード処理をサポートするプライマリ レプリカの代わりにデータベースを作成することを可用性グループに許可します (SEEDING_MODE = AUTOMATIC)。 このパラメーターは直接シード処理をサポートするすべてのセカンダリ レプリカで、そのセカンダリが可用性グループに参加した後に実行する必要があります。  CREATE ANY DATABASE 権限が必要です。  
  
 DENY CREATE ANY DATABASE  
 プライマリ レプリカの代わりにデータベースを作成する可用性グループの機能を削除します。  
  
 \<add_listener_option>  
 ADD LISTENER には、次のいずれかのオプションを指定できます。  
  
 WITH DHCP [ ON { **('** _four\_part\_ipv4\_address_ **','** _four\_part\_ipv4\_mask_ **')** } ]  
 可用性グループ リスナーによって動的ホスト構成プロトコル (DHCP) が使用されるよう指定します。  必要に応じて、ON 句を使用して、このリスナーを作成するネットワークを識別します。 DHCP は、可用性グループの可用性レプリカをホストする各サーバー インスタンスに使用される単一のサブネットに限定されます。  
  
> [!IMPORTANT]  
>  運用環境での DHCP の使用はお勧めしません。 ダウンタイムが発生して DHCP IP のリース期限が切れると、リスナーの DNS 名に関連付けられている新しい DHCP のネットワーク IP アドレスの登録に余分な時間がかかり、クライアント接続に影響が及びます。 ただし、開発環境とテスト環境を設定して可用性グループの基本機能を確認する場合や、アプリケーションとの統合の場合には DHCP が適しています。  
  
 例:  
  
 `WITH DHCP ON ('10.120.19.0','255.255.254.0')`  
  
 WITH IP **(** { **('** _four\_part\_ipv4\_address_ **','** _four\_part\_ipv4\_mask_ **')**  |  **('** _ipv6\_address_ **')** } [ **,** ..._n_ ] **)** [ **,** PORT **=** _listener\_port_ ]  
 可用性グループ リスナーが、DHCP を使用する代わりに、1 つ以上の静的 IP アドレスを使用することを指定します。 複数のサブネットにわたる可用性グループを作成するには、各サブネットのリスナー構成に静的 IP アドレスが 1 つ必要です。 サブネットの静的 IP アドレスには、IPv4 アドレスまたは IPv6 アドレスを使用できます。 ネットワーク管理者に連絡し、新しい可用性グループの可用性レプリカをホストする各サブネットの静的 IP アドレスを入手してください。  
  
 例:  
  
 `WITH IP ( ('10.120.19.155','255.255.254.0') )`  
  
 *ipv4_address*  
 可用性グループ リスナーに対する IPv4 の 4 つの部分から成るアドレスを指定します。 たとえば、`10.120.19.155` のようになります。  
  
 *ipv4_mask*  
 可用性グループ リスナーに対する IPv4 の 4 つの部分から成るマスクを指定します。 たとえば、`255.255.254.0` のようになります。  
  
 *ipv6_address*  
 可用性グループ リスナーに対する IPv6 アドレスを指定します。 たとえば、`2001::4898:23:1002:20f:1fff:feff:b3a3` のようになります。  
  
 PORT **=** *listener_port*  
 WITH IP 句で指定されている可用性グループ リスナーが使用するポート番号 *listener_port* を指定します。 PORT は省略できます。  
  
 既定のポート番号 1433 がサポートされます。 ただし、セキュリティ上の問題がある場合は、別のポート番号を使用することをお勧めします。  
  
 例: `WITH IP ( ('2001::4898:23:1002:20f:1fff:feff:b3a3') ) , PORT = 7777`  
  
 MODIFY LISTENER **'** _dns\_name_ **'(** \<modify\_listener\_option\> **)**  
 この可用性グループに対する既存の可用性グループ リスナーを変更します。 プライマリ レプリカでのみサポートされます。  
  
 \<modify\_listener\_option\>  
 MODIFY LISTENER には、次のいずれかのオプションを指定できます。  
  
 ADD IP { **('** _four\_part\_ipv4\_address_ **','** _four\_part\_ipv4_mask_ **')** \| <b>('</b>dns\_name*ipv6\_address* __')__ }  
 指定した IP アドレスを *dns\_name* で指定されている可用性グループ リスナーに追加します。  
  
 PORT **=** *listener_port*  
 このセクションで既に説明したこの引数に関する説明を参照してください。  
  
 RESTART LISTENER **'** _dns\_name_ **'**  
 指定した DNS 名に関連付けられたリスナーを再起動します。 プライマリ レプリカでのみサポートされます。  
  
 REMOVE LISTENER **'** _dns\_name_ **'**  
 指定した DNS 名に関連付けられたリスナーを削除します。 プライマリ レプリカでのみサポートされます。  
  
 OFFLINE  
 オンラインの可用性グループをオフラインにする 同期コミット データベースのデータ損失はありません。  
  
 可用性グループがオフラインになると、クライアントはそのデータベースを使用できなくなりますが、可用性グループをオンラインに戻すことはできません。 したがって、OFFLINE オプションは、可用性グループのリソースを新しい WSFC クラスターに移行するときに、クラスター間での [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]の移行中に限って使用してください。  
  
 詳細については、「[可用性グループをオフラインにする &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/take-an-availability-group-offline-sql-server.md)」を参照してください。  
  
## <a name="prerequisites-and-restrictions"></a>前提条件と制限  
 可用性レプリカ、そのホスト サーバー インスタンス、そのコンピューターに関する前提条件と制限については、「[Always On 可用性グループの前提条件、制限事項、推奨事項 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。  
  
 AVAILABILITY GROUP Transact-SQL ステートメントの制限については、「[AlwaysOn 可用性グループの Transact-SQL ステートメントの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md)」を参照してください。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。  ALTER ANY DATABASE 権限も必要です。   
  
## <a name="examples"></a>使用例  
  
###  <a name="Join_Secondary_Replica"></a> A. セカンダリ レプリカを可用性グループに参加させる  
 次の例では、接続しているセカンダリ レプリカを `AccountsAG` 可用性グループに参加させます。  
  
```SQL  
ALTER AVAILABILITY GROUP AccountsAG JOIN;  
GO  
```  
  
###  <a name="Force_Failover"></a> B. 可用性グループを強制的にフェールオーバーする  
 次の例では、`AccountsAG` 可用性グループを、接続されているセカンダリ レプリカに強制的にフェールオーバーします。  
  
```SQL
ALTER AVAILABILITY GROUP AccountsAG FORCE_FAILOVER_ALLOW_DATA_LOSS;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [DROP AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-availability-group-transact-sql.md)   
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [AlwaysOn 可用性グループの構成のトラブルシューティング &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)   
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
  
