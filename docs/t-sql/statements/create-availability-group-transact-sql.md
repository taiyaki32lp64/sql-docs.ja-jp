---
title: CREATE AVAILABILITY GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AVAILABILITY GROUP
- CREATE_AVAILABILITY_TSQL
- CREATE_AVAILABILITY_GROUP_TSQL
- CREATE AVAILABILITY GROUP
- CREATE AVAILABILITY
- AVAILABILITY_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- CREATE AVAILABILITY GROUP statement
- Availability Groups [SQL Server], creating
- Availability Groups [SQL Server], Transact-SQL statements
ms.assetid: a3d55df7-b4e4-43f3-a14b-056cba36ab98
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8266791ae6621dbf81f16b2eb5c83ef8c9a3c1b5
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244592"
---
# <a name="create-availability-group-transact-sql"></a>CREATE AVAILABILITY GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]機能に対して有効である場合、新しい可用性グループを作成します。  
  
> [!IMPORTANT]  
>  新しい可用性グループの初期プライマリ レプリカとして使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで CREATE AVAILABILITY GROUP を実行します。 このサーバー インスタンスは、Windows Server フェールオーバー クラスタリング (WSFC) ノードに存在している必要があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```SQL  
  
CREATE AVAILABILITY GROUP group_name  
   WITH (<with_option_spec> [ ,...n ] )  
   FOR [ DATABASE database_name [ ,...n ] ]  
   REPLICA ON <add_replica_spec> [ ,...n ]  
   AVAILABILITY GROUP ON <add_availability_group_spec> [ ,...2 ]  
   [ LISTENER 'dns_name' ( <listener_option> ) ]  
[ ; ]  
  
<with_option_spec>::=   
    AUTOMATED_BACKUP_PREFERENCE = { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
  | FAILURE_CONDITION_LEVEL  = { 1 | 2 | 3 | 4 | 5 }   
  | HEALTH_CHECK_TIMEOUT = milliseconds  
  | DB_FAILOVER  = { ON | OFF }   
  | DTC_SUPPORT  = { PER_DB | NONE }  
  | BASIC  
  | DISTRIBUTED
  | REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT = { integer }
  | CLUSTER_TYPE = { WSFC | EXTERNAL | NONE } 
  
<add_replica_spec>::=  
  <server_instance> WITH  
    (  
       ENDPOINT_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY },  
       FAILOVER_MODE = { AUTOMATIC | MANUAL | EXTERNAL }  
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
  
<add_availability_group_spec>::=  
 <ag_name> WITH  
    (  
       LISTENER_URL = 'TCP://system-address:port',  
       AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT },  
       FAILOVER_MODE = MANUAL,  
       SEEDING_MODE = { AUTOMATIC | MANUAL }  
    )  
  
<listener_option> ::=  
   {  
      WITH DHCP [ ON ( <network_subnet_option> ) ]  
    | WITH IP ( { ( <ip_address_option> ) } [ , ...n ] ) [ , PORT = listener_port ]  
   }  
  
  <network_subnet_option> ::=  
     'ip4_address', 'four_part_ipv4_mask'    
  
  <ip_address_option> ::=  
     {   
        'ip4_address', 'pv4_mask'  
      | 'ipv6_address'  
     }  
  
```  
  
## <a name="arguments"></a>引数  
 *group_name*  
 新しい可用性グループの名前を指定します。 *group_name* は有効な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の[識別子](../../relational-databases/databases/database-identifiers.md)であり、WSFC クラスター内のすべての可用性グループ間で一意である必要があります。 可用性グループ名の最大文字数は 128 文字です。  
  
 AUTOMATED_BACKUP_PREFERENCE **=** { PRIMARY | SECONDARY_ONLY| SECONDARY | NONE }  
 バックアップを実行する場所を選択する際の、バックアップ ジョブによるプライマリ レプリカの評価方法についての優先設定を指定します。 自動バックアップの優先設定を考慮して、特定のバックアップ ジョブのスクリプトを作成できます。 優先設定は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって適用されるものではないので、アドホック バックアップには影響がないことを理解しておくことが重要です。  
  
 サポートされる値は次のとおりです。  
  
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
>  既存の可用性グループの自動バックアップ設定を確認するには、[sys.availability_groups](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md) カタログ ビューの **automated_backup_preference** 列または **automated_backup_preference_desc** 列を選択します。 さらに、[sys.fn_hadr_backup_is_preferred_replica  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md) を使用して、優先されるバックアップ レプリカを決定することができます。  `AUTOMATED_BACKUP_PREFERENCE = NONE` の場合でも、この関数は少なくとも 1 つのレプリカに対して 1 を返します。  
  
 FAILURE_CONDITION_LEVEL **=** { 1 | 2 | **3** | 4 | 5 }  
 この可用性グループの自動フェールオーバーをトリガーするエラー状態を指定します。 FAILURE_CONDITION_LEVEL はグループ レベルで設定されますが、同期コミット可用性モードに構成されている (AVAILABILITY_MODE **=** SYNCHRONOUS_COMMIT) 可用性レプリカにのみ適用されます。 さらに、エラー状態が自動フェールオーバーをトリガーできるのは、プライマリとセカンダリの両方のレプリカが自動フェールオーバー モードに構成されていて (FAILOVER_MODE **=** AUTOMATIC)、セカンダリ レプリカが現在プライマリ レプリカと同期されている場合だけです。  
  
 エラー状態レベルの範囲は 1 ～ 5 で、レベル 1 が最も制限が緩く、レベル 5 が最も制限の厳しい指定です。 任意の状態レベルは、それより制限が緩いすべてのレベルを含みます。 したがって、最も厳しい状態レベル 5 にはそれより制限が緩い状態レベル (1 から 4) が含まれ、レベル 4 にはレベル 1 から 3 が含まれます。以下同様です。 次の表では、各レベルに対応するエラー状態について説明します。  
  
|Level|エラー状態|  
|-----------|-----------------------|  
|1|次のいずれかが発生した場合に自動フェールオーバーを開始する必要があることを指定します。<br /><br /> -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスがダウンした。<br /><br /> -WSFC クラスターに接続するための可用性グループのリースが、サーバー インスタンスから ACK を受信しないために期限切れになった。 詳細については、「[How It Works:SQL Server Always On Lease Timeout](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-AlwaysOn-lease-timeout.aspx)」 (動作方法: SQL Server Always On のリース タイムアウト) を参照してください。|  
|2|次のいずれかが発生した場合に自動フェールオーバーを開始する必要があることを指定します。<br /><br /> -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスがクラスターに接続されておらず、可用性グループのユーザー指定の HEALTH_CHECK_TIMEOUT しきい値を超えている。<br /><br /> -可用性レプリカがエラー状態である。|  
|3|孤立したスピンロック、重大な書き込みアクセス違反、ダンプが多すぎるなどの重大な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部エラーが発生した場合に自動フェールオーバーを開始する必要があることを指定します。<br /><br /> これは既定の動作です。|  
|4|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部リソース プールに永続的なメモリ不足の状態があるなど、中程度の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部エラーが発生した場合に自動フェールオーバーを開始する必要があることを指定します。|  
|5|以下のような任意の修飾エラー状態に対して自動フェールオーバーを開始する必要があることを指定します。<br /><br /> -SQL エンジンのワーカー スレッドが枯渇している。<br /><br /> -解決不可能なデッドロックが検出された。|  
  
> [!NOTE]  
>  クライアント要求に対して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが応答しないことは、可用性グループには関係ありません。  
  
 FAILURE_CONDITION_LEVEL 値と HEALTH_CHECK_TIMEOUT 値は、特定のグループに対する*柔軟なフェールオーバー ポリシー*を定義します。 この柔軟なフェールオーバー ポリシーを使用すると、自動フェールオーバーを引き起こす条件をきめ細かく制御できます。 詳細については、「[可用性グループの自動フェールオーバーのための柔軟なフェールオーバー ポリシー &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md)」を参照してください。  
  
 HEALTH_CHECK_TIMEOUT **=** *milliseconds*  
 [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) システム ストアド プロシージャによってサーバーの状態情報が返されるのを待機する時間 (ミリ秒単位) を指定します。この時間が経過すると、WSFC クラスターはサーバー インスタンスが速度低下またはハングしているものと見なします。 HEALTH_CHECK_TIMEOUT はグループ レベルで設定されますが、自動フェールオーバーで同期コミット可用性モードが構成されている (AVAILABILITY_MODE **=** SYNCHRONOUS_COMMIT) 可用性レプリカにのみ適用されます。  さらに、正常性チェック タイムアウトが自動フェールオーバーをトリガーできるのは、プライマリとセカンダリの両方のレプリカが自動フェールオーバー モードに構成されていて (FAILOVER_MODE **=** AUTOMATIC)、セカンダリ レプリカが現在プライマリ レプリカと同期されている場合だけです。  
  
 HEALTH_CHECK_TIMEOUT の既定値は 30000 ミリ秒 (30 秒) です。 最小値は 15,000 ミリ秒 (15 秒)、最大値は 4,294,967,295 ミリ秒です。  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** では、データベース レベルでの正常性チェックは実行されません。  
  
 DB_FAILOVER  **=** { ON | OFF }  
 プライマリ レプリカ上のデータベースがオフラインのときに実行する応答を指定します。 ON に設定すると、可用性グループ内のデータベースがオンライン以外のすべての状態で、自動フェールオーバーがトリガーされます。 このオプションが OFF に設定されている場合は、インスタンスの正常性だけが自動フェールオーバーのトリガーに使用されます。  
  
  この設定の詳細については、「[データベース レベルの正常性検出オプション](../../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md)」を参照してください。 
  
 DTC_SUPPORT  **=** { PER_DB | NONE }  
 データベースをまたがるトランザクションが分散トランザクション コーディネーター (DTC) でサポートされるかどうかを指定します。 データベースにまたがるトランザクションは、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降でのみサポートされます。 PER_DB では、これらのトランザクションをサポートする可用性グループが作成されます。 詳細については、「[Always On 可用性グループとデータベース ミラーリングでの複数データベースにまたがるトランザクションと分散トランザクション &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)」を参照してください。  
  
 BASIC  
 基本的な可用性グループを作成するために使用します。 基本的な可用性グループは、1 つのデータベースと 2 つのレプリカ (プライマリ レプリカとセカンダリ レプリカ) に制限されます。 このオプションは、SQL Server Standard Edition の非推奨のデータベース ミラーリング機能に代わるものです。 詳細については、「[基本的な可用性グループ &#40;AlwaysOn 可用性グループ&#41;](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)」を参照してください。 基本的な可用性グループは、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降でサポートされています。  

 DISTRIBUTED  
 分散型可用性グループを作成するために使用します。 このオプションは、個別の Windows Server フェールオーバー クラスター内の 2 つの可用性グループを接続するために AVAILABILITY GROUP ON パラメーターと共に使用されます。  詳細については、「[Distributed Availability Groups &#40;Always On Availability Groups&#41; (分散型可用性グループ (Always On 可用性グループ))](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md)」を参照してください。 分散型可用性グループは、[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降でサポートされています。 

 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT   
 SQL Server 2017 で導入されました。 コミットに必要な同期セカンダリ レプリカの最小数を設定するために使用します。この数を超えると、プライマリがトランザクションをコミットします。 セカンダリ レプリカの最小数についてトランザクション ログが更新されるまで、SQL Server トランザクションが確実に待機するようになります。 既定値は 0 であり、SQL Server 2016 と同じように動作します。 最小値は 0 です。 最大値はレプリカの数から 1 を引いた値になります。 このオプションは、同期コミット モードのレプリカに関連しています。 レプリカが同期コミット モードのとき、セカンダリ同期レプリカに対する書き込みがレプリカ データベース トランザクション ログにコミットされるまで、プライマリ レプリカへの書き込みは待機します。 セカンダリ同期レプリカをホストする SQL Server が応答を停止した場合、プライマリ レプリカをホストする SQL Server はそのセカンダリ レプリカを同期未実行としてマークし、続行します。 応答のないデータベースがオンラインに復帰すると、"未同期" 状態になります。プライマリが再度同期可能になるまで、レプリカに異常のマークが付きます。 この設定により、レプリカの最小数で各トランザクションがコミットされるまで、プライマリ レプリカは確実に待機するようになります。 レプリカの最小数が使用できない場合、プライマリのコミットは失敗します。 クラスター タイプ `EXTERNAL` の場合、可用性グループがクラスター リソースに追加されると、設定が変更されます。 「[可用性グループの構成の高可用性とデータの保護](../../linux/sql-server-linux-availability-group-ha.md)」を参照してください。

 CLUSTER_TYPE  
 SQL Server 2017 で導入されました。 可用性グループが Windows Server フェールオーバー クラスター (WSFC) にあるかどうかを識別するために使用します。  可用性グループが Windows Server フェールオーバー クラスターのフェールオーバー クラスター インスタンスにある場合は、WSFC に設定します。 クラスターが、Linux Pacemaker などの、Windows Server フェールオーバー クラスターではないクラスター マネージャーで管理されている場合は、EXTERNAL に設定します。 可用性グループがクラスターの調整で WSFC を使用していない場合は、NONE に設定します。 たとえば、可用性グループに、クラスター マネージャーがない Linux サーバーが含まれている場合です。 

 DATABASE *database_name*  
 ローカル [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス (つまり可用性グループを作成するサーバー インスタンス) 上の 1 つ以上のユーザー データベースのリストを指定します。 1 つの可用性グループに対して複数のデータベースを指定できますが、各データベースが所属できる可用性グループは 1 つだけです。 可用性グループでサポートできるデータベースの種類については、「[Always On 可用性グループの前提条件、制限事項、推奨事項 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。 可用性グループに既に属しているローカル データベースを確認する場合は、[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) カタログ ビューで **replica_id** 列を参照してください。  
  
 DATABASE 句は省略可能です。 これを省略した場合、新しい可用性グループは空になります。  
  
 可用性グループを作成したら、セカンダリ レプリカをホストする各サーバー インスタンスに接続して、各セカンダリ データベースを準備し、可用性グループに参加させます。 詳細については、「 [AlwaysOn セカンダリ データベース上のデータ移動の開始 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  後で、現在のプライマリ レプリカをホストするサーバー インスタンス上の適格なデータベースを可用性グループに追加できます。 また、データベースを可用性グループから削除することもできます。 詳細については、「 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)、または PowerShell を使用して、既存の AlwaysOn 可用性グループにセカンダリ レプリカを追加する方法について説明します。  
  
 REPLICA ON  
 新しい可用性グループの可用性レプリカをホストする 1 ～ 5 個の SQL Server インスタンスを指定します。  各レプリカを指定する際には、サーバー インスタンスのアドレスに続けて WITH (...) 句を入力します。 少なくとも、初期プライマリ レプリカとなる、ローカル サーバー インスタンスを指定する必要があります。 必要に応じて、セカンダリ レプリカを 4 つまで指定することもできます。  
  
 すべてのセカンダリ レプリカを可用性グループに参加させる必要があります。 詳細については、「 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)、または PowerShell を使用して、既存の AlwaysOn 可用性グループにセカンダリ レプリカを追加する方法について説明します。  
  
> [!NOTE]  
>  可用性グループの作成時に 4 つ未満のセカンダリ レプリカを指定した場合は、[ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用して、いつでもセカンダリ レプリカを追加作成できます。 このステートメントを使用すると、既存の可用性グループから任意のセカンダリ レプリカを削除することもできます。  
  
 \<server_instance> レプリカのホストである [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのアドレスを指定します。 アドレスの形式は、インスタンスが既定のインスタンスか名前付きインスタンスか、またスタンドアロン インスタンスかフェールオーバー クラスター インスタンス (FCI) かによって、次のように異なります。  
  
 { '*system_name*[\\*instance_name*]' | '*FCI_network_name*[\\*instance_name*]' }  
  
 このアドレスの構成要素は次のとおりです。  
  
 *system_name*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のターゲット インスタンスが存在するコンピューター システムの NetBIOS 名です。 このコンピューターは WSFC ノードである必要があります。  
  
 *FCI_network_name*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターにアクセスするために使用されるネットワーク名です。 サーバー インスタンスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー パートナーとして参加している場合に使用します。 FCI サーバー インスタンスで SELECT [@@SERVERNAME](../../t-sql/functions/servername-transact-sql.md) を実行すると、'*FCI_network_name*[\\*instance_name*]' という文字列全体 (完全なレプリカ名) が返されます。  
  
 *instance_name*  
 *system_name* または *FCI_network_name* によってホストされ、HADR サービスが有効になっている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの名前です。 既定のサーバー インスタンスの場合、 *instance_name* は省略可能です。 インスタンス名では大文字と小文字が区別されません。 名前付きインスタンスでは、この名前の値は `select ServerProperty(N'InstanceName');` を実行したときに返される値と同じです。  
  
 \  
 *system_name* または *FCI_network_name* と区別するために、*instance_name* を指定するときにのみ使用される区切り記号です。  
  
 WSFC ノードとサーバーのインスタンスの前提条件については、「[AlwaysOn 可用性グループの前提条件、制限事項、推奨事項 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。  
  
 ENDPOINT_URL **='** TCP **://** _system-address_ **:** _port_ **'**  
 現在の REPLICA ON 句で定義している可用性レプリカをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス上の[データベース ミラーリング エンドポイント](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)の URL パスを指定します。  
  
 ENDPOINT_URL 句は必須です。 詳細については、「 [可用性レプリカを追加または変更する場合のエンドポイント URL の指定 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)の構成に関する一般的な問題のトラブルシューティングに役立つ情報を提供します。  
  
 **'** TCP **://** _system-address_ **:** _port_ **'**  
 エンドポイントの URL または読み取り専用ルーティングの URL を指定するための URL を指定します。 URL のパラメーターは次のとおりです。  
  
 *system-address*  
 システム名、完全修飾ドメイン名では、対象のコンピューター システムを明確に識別する、IP アドレスなどの文字列です。  
  
 *port*  
 パートナー サーバー インスタンスのミラーリング エンドポイントと関連付けられているポート番号 (ENDPOINT_URL オプションの場合)、またはサーバー インスタンスの[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって使用されるポート番号 (READ_ONLY_ROUTING_URL オプションの場合) です。  
  
 AVAILABILITY_MODE **=** { {SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY }  
 SYNCHRONOUS_COMMIT または ASYNCHRONOUS_COMMIT では、プライマリ レプリカが特定のプライマリ データベースでトランザクションをコミットする前に、ディスクへのログ レコードの書き込みがセカンダリ レプリカで確認されるのを待機する必要があるかどうかを指定します。 同じプライマリ レプリカに対する異なるデータベースでのトランザクションは個別にコミットできます。 SQL Server 2017 CU 1 では CONFIGURATION_ONLY が導入されています。 CONFIGURATION_ONLY レプリカは、CLUSTER_TYPE = EXTERNAL または CLUSTER_TYPE = NONE の可用性グループにのみ適用されます。 
  
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
  
 AVAILABILITY_MODE 句は必須です。 詳細については、「[可用性モード &#40;Always On 可用性グループ&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)」を参照してください。  
  
 FAILOVER_MODE **=** { AUTOMATIC | MANUAL }  
 定義している可用性レプリカのフェールオーバー モードを指定します。  
  
 AUTOMATIC  
 自動フェールオーバーを有効にします。 このオプションは、AVAILABILITY_MODE = SYNCHRONOUS_COMMIT も指定した場合にのみサポートされます。 AUTOMATIC は、プライマリ レプリカを含む 2 つの可用性レプリカに対して指定できます。  
  
> [!NOTE]  
>  SQL Server フェールオーバー クラスター インスタンス (FCI) は可用性グループによる自動フェールオーバーをサポートしないため、FCI によってホストされる可用性レプリカは手動フェールオーバー用にのみ構成できます。  
  
 MANUAL  
 データベース管理者による計画的な手動フェールオーバーまたは強制手動フェールオーバー (通常は*強制フェールオーバー*と呼ばれる) を有効にします。  
  
 FAILOVER_MODE 句は必須です。 データ損失のない手動フェールオーバーと強制フェールオーバー (データ損失の可能性あり) という 2 種類の手動フェールオーバーは、異なる条件の下でサポートされます。 詳細については、「 [フェールオーバーとフェールオーバー モード &#40;AlwaysOn 可用性グループ&#41;](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)、または PowerShell を使用して、AlwaysOn 可用性グループ上で計画的な手動フェールオーバーまたは強制手動フェールオーバー (強制フェールオーバー) を実行する方法について説明します。  
  
 SEEDING_MODE **=** { AUTOMATIC | MANUAL }  
 セカンダリ レプリカの初回シード処理方法を指定します。  
  
 AUTOMATIC  
 直接シード処理を有効にします。 この方法では、ネットワーク上でセカンダリ レプリカがシード処理されます。 この方法では、レプリカでプライマリ データベースのコピーをバックアップしたり、復元したりする必要がありません。  
  
> [!NOTE]  
>  直接シード処理の場合、セカンダリ レプリカごとにデータベース作成を許可する必要があります。**GRANT CREATE ANY DATABASE** オプションを指定し、**ALTER AVAILABILITY GROUP** を呼び出してください。  
  
 MANUAL  
 手動シード処理を指定します (既定)。 この方法では、プライマリ レプリカでデータベースのバックアップを作成し、セカンダリ レプリカでそのバックアップを手動で復元する必要があります。  
  
 BACKUP_PRIORITY **=** *n*  
 同じ可用性グループ内の他のレプリカと比較して、このレプリカでバックアップを実行する優先順位を指定します。 値は 0 ～ 100 の範囲の整数です。 これらの値には次の意味があります。  
  
-   1 から 100 は、その可用性レプリカがバックアップの実行に向けて選択される可能性があることを示します。 1 は最も低い優先順位を示し、100 は最も高い優先順位を示します。 BACKUP_PRIORITY = 1 の場合、現在使用可能な可用性レプリカにそれより高い優先順位のものがない場合にのみ、その可用性レプリカがバックアップの実行に向けて選択されます。  
  
-   0 は、この可用性レプリカがバックアップの実行対象でないことを示します。 これは、たとえば、バックアップをフェールオーバーすることがないリモート可用性レプリカのような場合に便利です。  
  
 詳細については、「[アクティブなセカンダリ:セカンダリ レプリカでのバックアップ &#40;Always On 可用性グループ&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
 SECONDARY_ROLE **(** ... **)**  
 この可用性レプリカが現在セカンダリ ロールを所有している場合に (つまり、セカンダリ レプリカである場合は常に) 有効であるロール固有の設定を指定します。 かっこの中では、いずれか一方または両方のセカンダリ ロール オプションを指定します。 両方を指定する場合は、コンマ区切りのリストを使用します。  
  
 セカンダリ ロール オプションは次のとおりです。  
  
 ALLOW_CONNECTIONS **=** { NO | READ_ONLY | ALL }  
 セカンダリ ロールを実行している (つまりセカンダリ レプリカとして機能している) 特定の可用性レプリカのデータベースがクライアントから接続を受け入れることができるかどうかを指定します。以下のいずれかになります。  
  
 NO  
 このレプリカのセカンダリ データベースに対するユーザー接続は禁止されます。 読み取りアクセスで利用することはできません。 これは既定の動作です。  
  
 READ_ONLY  
 Application Intent プロパティが **ReadOnly** に設定されている場合に限り、セカンダリ レプリカのデータベースに対する接続が許可されます。 このプロパティの詳細については、「 [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
 ALL  
 読み取り専用アクセスに限り、セカンダリ レプリカのデータベースに対するすべての接続が許可されます。  
  
 詳細については、「[アクティブなセカンダリ:読み取り可能なセカンダリ レプリカ &#40;Always On 可用性グループ&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
 READ_ONLY_ROUTING_URL **='** TCP **://** _system-address_ **:** _port_ **'**  
 読み取りを目的とした接続要求をこの可用性レプリカにルーティングするために使用する URL を指定します。 これは、SQL Server データベース エンジンがリッスンしている URL です。 通常、SQL Server データベース エンジンの既定のインスタンスは、TCP ポート 1433 でリッスンします。  
  
 名前付きインスタンスの場合は、[sys.dm_tcp_listener_states](../../relational-databases/system-dynamic-management-views/sys-dm-tcp-listener-states-transact-sql.md) 動的管理ビューの **port** 列と **type_desc** 列をクエリすることで、ポート番号を取得できます。 サーバー インスタンスでは Transact-SQL リスナーを使用します (**type_desc='TSQL'** )。  
  
 レプリカの読み取り専用ルーティング URL の計算の詳細については、「[AlwaysOn の read_only_routing_url の計算](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-AlwaysOn.aspx)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前付きインスタンスの場合は、特定のポートを使用するように Transact-SQL リスナーを構成する必要があります。 詳細については、「[特定の TCP ポートで受信待ちするようにサーバーを構成する方法 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)」を参照してください。  
  
 PRIMARY_ROLE **(** ... **)**  
 この可用性レプリカが現在プライマリ ロールを所有している場合に (つまり、プライマリ レプリカである場合は常に) 有効であるロール固有の設定を指定します。 かっこの中では、いずれか一方または両方のプライマリ ロール オプションを指定します。 両方を指定する場合は、コンマ区切りのリストを使用します。  
  
 プライマリ ロール オプションは次のとおりです。  
  
 ALLOW_CONNECTIONS **=** { READ_WRITE | ALL }  
 プライマリ ロールを実行している (つまりプライマリ レプリカとして機能している) 特定の可用性レプリカのデータベースが受け入れることのできるクライアントからの接続の種類を指定します。以下のいずれかになります。  
  
 READ_WRITE  
 Application Intent 接続プロパティが **ReadOnly** に設定されている接続は許可されません。  Application Intent プロパティが **ReadWrite** に設定されている場合、または Application Intent 接続プロパティが設定されていない場合は、接続が許可されます。 "アプリケーションの目的" 接続プロパティの詳細については、「 [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)」を参照してください。  
  
 ALL  
 プライマリ レプリカのデータベースに対するすべての接続が許可されます。 これは既定の動作です。  
  
 READ_ONLY_ROUTING_LIST **=** { **('** \<server_instance> **'** [ **,** ...*n* ] **)** | NONE } セカンダリ ロールで実行されている場合は、次の要件を満たしている、この可用性グループの可用性レプリカをホストするサーバー インスタンスのコンマ区切りリストを指定します。  
  
-   すべての接続または読み取り専用の接続を許可するように構成されていること (前に示した SECONDARY_ROLE オプションの ALLOW_CONNECTIONS 引数を参照)。  
  
-   読み取り専用ルーティングの URL が定義されていること (前に示した SECONDARY_ROLE オプションの READ_ONLY_ROUTING_URL 引数を参照)。  
  
 READ_ONLY_ROUTING_LIST の値は次のとおりです。  
  
 \<server_instance> セカンダリ ロールで実行するときに読み取り可能なセカンダリ レプリカであるレプリカのホストである [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのアドレスを指定します。  
  
 読み取り可能なセカンダリ レプリカをホストする可能性があるすべてのサーバー インスタンスを指定するには、コンマ区切りリストを使用します。 読み取り専用のルーティングは、リストで指定されているサーバー インスタンスの順序に従います。 レプリカの読み取り専用ルーティング リストにレプリカのホスト サーバー インスタンスを含める場合、通常は一覧の最後にこのサーバー インスタンスを配置することをお勧めします。読み取りを目的とした接続が使用できる場合に、これがセカンダリ レプリカに移動するためです。  
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、読み取り可能なセカンダリ レプリカ間で読み取りを目的とした要求の負荷を分散することができます。 読み取り専用ルーティング リスト内のかっこの入れ子になったセットにレプリカを配置することで、これを指定します。 詳細と例については、「[読み取り専用レプリカ間の負荷分散の構成](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md#loadbalancing)」を参照してください。  
  
 NONE  
 この可用性レプリカがプライマリ レプリカの場合は、読み取り専用のルーティングをサポートしないことを指定します。 これは既定の動作です。  
  
 SESSION_TIMEOUT **=** *integer*  
 セッション タイムアウト期間を秒単位で指定します。 このオプションを指定しない場合、この時間は既定で 10 秒に設定されます。 最小値は 5 秒です。  
  
> [!IMPORTANT]  
>  タイムアウト期間を 10 秒以上にしておくことをお勧めします。  
  
 セッション タイムアウト期間の詳細については、「[AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)」を参照してください。  
  
 AVAILABILITY GROUP ON  
 *分散型可用性グループ* を構成する 2 つの可用性グループを指定します。 各可用性グループは、独自の Windows Server フェールオーバー クラスター (WSFC) の一部です。 分散型可用性グループを作成すると、現在の SQL Server インスタンスの可用性グループがプライマリ可用性グループになります。 2 つ目の可用性グループはセカンダリ可用性グループになります。  
  
 セカンダリ可用性グループを分散型可用性グループに参加させる必要があります。 詳細については、「 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)、または PowerShell を使用して、既存の AlwaysOn 可用性グループにセカンダリ レプリカを追加する方法について説明します。  
  
 \<ag_name> 分散可用性グループの半分を占める可用性グループの名前を指定します。  
  
 LISTENER **='** TCP **://** _system-address_ **:** _port_ **'**  
 可用性グループに関連付けられているリスナーの URL パスを指定します。  
  
 LISTENER 句は必須です。  
  
 **'** TCP **://** _system-address_ **:** _port_ **'**  
 可用性グループに関連付けられているリスナーの URL を指定します。 URL のパラメーターは次のとおりです。  
  
 *system-address*  
 システム名、完全修飾ドメイン名、IP アドレスなど、リスナーを明確に識別する文字列です。  
  
 *port*  
 可用性グループのミラーリング エンドポイントに関連付けられているポート番号です。 これはリスナーのポートではないことに注意してください。  
  
 AVAILABILITY_MODE **=** { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT | CONFIGURATION_ONLY }  
 プライマリ レプリカが特定のプライマリ データベースでトランザクションをコミットする前に、ディスクへのログ レコードの書き込みがセカンダリ可用性グループで確認されるのを待機する必要があるかどうかを指定します。  
  
 SYNCHRONOUS_COMMIT  
 セカンダリ可用性グループでトランザクションが書き込まれるまで、プライマリ レプリカがトランザクションのコミットを待機するように指定します。 SYNCHRONOUS_COMMIT は、プライマリ可用性グループを含む、最大 2 つの可用性グループに指定できます。  
  
 ASYNCHRONOUS_COMMIT  
 このセカンダリ可用性グループがログを書き込むのを待たず、プライマリ レプリカがトランザクションをコミットするように指定します。 ASYNCHRONOUS_COMMIT は、プライマリ可用性グループを含む、最大 2 つの可用性グループに指定できます。  
  
 AVAILABILITY_MODE 句は必須です。  
  
 FAILOVER_MODE **=** { MANUAL }  
 分散型可用性グループのフェールオーバー モードを指定します。  
  
 MANUAL  
 データベース管理者による計画的な手動フェールオーバーまたは強制手動フェールオーバー (通常は*強制フェールオーバー*と呼ばれる) を有効にします。  
  
 FAILOVER_MODE 句は必須であり、唯一のオプションは MANUAL です。 セカンダリ可用性グループへの自動フェールオーバーはサポートされていません。  
  
 SEEDING_MODE **=** { AUTOMATIC | MANUAL }  
 セカンダリ可用性グループの初回シード処理方法を指定します。  
  
 AUTOMATIC  
 直接シード処理を有効にします。 この方法では、ネットワーク上でセカンダリ可用性グループがシード処理されます。 この方法では、セカンダリ可用性グループのレプリカでプライマリ データベースのコピーをバックアップしたり、復元したりする必要がありません。  
  
 MANUAL  
 手動シード処理を指定します (既定)。 この方法では、プライマリ レプリカでデータベースのバックアップを作成し、セカンダリ可用性グループのレプリカでそのバックアップを手動で復元する必要があります。  
  
 LISTENER **'** _dns\_name_ **'(** \<listener_option\> **)** この可用性グループの新しい可用性グループ リスナーを定義します。 LISTENER は省略可能な引数です。  
  
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
>  NetBIOS では、dns_name の最初の 15 文字のみが認識されます。 同じ Active Directory で制御されている 2 つの WSFC クラスターがあり、両方のクラスターで可用性グループ リスナーを作成しようとする場合、15 文字より長い名前を使用して、15 文字のプレフィックスが同一であると、エラーが表示され、仮想ネットワーク名リソースをオンラインにできなかったことがレポートされます。 DNS 名のプレフィックスに対する名前付け規則の詳細については、「 [ドメイン名を割り当てる](https://technet.microsoft.com/library/cc731265\(WS.10\).aspx)」を参照してください。  
  
 \<listener_option> LISTENER は次のいずれかの \<listener_option> オプションを受け取ります。 
  
 WITH DHCP [ ON { **('** _four\_part\_ipv4\_address_ **','** _four\_part\_ipv4\_mask_ **')** } ]  
 可用性グループ リスナーが動的ホスト構成プロトコル (DHCP) を使用することを指定します。  必要に応じて、ON 句を使用して、このリスナーが作成されるネットワークを識別します。 DHCP は、可用性グループのレプリカをホストする各サーバー インスタンスに使用される単一のサブネットに限定されます。  
  
> [!IMPORTANT]  
>  運用環境での DHCP の使用はお勧めしません。 ダウンタイムが発生して DHCP IP のリース期限が切れると、リスナーの DNS 名に関連付けられている新しい DHCP のネットワーク IP アドレスの登録に余分な時間がかかり、クライアント接続に影響が及びます。 ただし、開発環境とテスト環境を設定して可用性グループの基本機能を確認する場合や、アプリケーションとの統合の場合には DHCP が適しています。  
  
 次に例を示します。  
  
 `WITH DHCP ON ('10.120.19.0','255.255.254.0')`  
  
 WITH IP **(** { **('** _four\_part\_ipv4\_address_ **','** _four\_part\_ipv4\_mask_ **')**  |  **('** _ipv6\_address_ **')** } [ **,** ...*n* ] **)** [ **,** PORT **=** _listener\_port_ ]  
 可用性グループ リスナーが、DHCP を使用する代わりに、1 つ以上の静的 IP アドレスを使用することを指定します。 複数のサブネットにわたる可用性グループを作成するには、各サブネットのリスナー構成に静的 IP アドレスが 1 つ必要です。 サブネットの静的 IP アドレスには、IPv4 アドレスまたは IPv6 アドレスを使用できます。 ネットワーク管理者に連絡し、新しい可用性グループのレプリカをホストする各サブネットの静的 IP アドレスを入手してください。  
  
 次に例を示します。  
  
 `WITH IP ( ('10.120.19.155','255.255.254.0') )`  
  
 *ip4_address*  
 可用性グループ リスナーに対する IPv4 の 4 つの部分から成るアドレスを指定します。 たとえば、「 `10.120.19.155` 」のように入力します。  
  
 *ipv4_mask*  
 可用性グループ リスナーに対する IPv4 の 4 つの部分から成るマスクを指定します。 たとえば、「 `255.255.254.0` 」のように入力します。  
  
 *ipv6_address*  
 可用性グループ リスナーに対する IPv6 アドレスを指定します。 たとえば、「 `2001::4898:23:1002:20f:1fff:feff:b3a3` 」のように入力します。  
  
 PORT **=** *listener_port*  
 WITH IP 句で指定されている可用性グループ リスナーが使用するポート番号 *listener_port* を指定します。 PORT は省略できます。  
  
 既定のポート番号 1433 がサポートされます。 ただし、セキュリティ上の問題がある場合は、別のポート番号を使用することをお勧めします。  
  
 例: `WITH IP ( ('2001::4898:23:1002:20f:1fff:feff:b3a3') ) , PORT = 7777`  
  
## <a name="prerequisites-and-restrictions"></a>前提条件と制限  
 可用性グループを作成するための前提条件については、「[AlwaysOn 可用性グループの前提条件、制限事項、推奨事項 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」を参照してください。  
  
 AVAILABILITY GROUP Transact-SQL ステートメントの制限については、「[AlwaysOn 可用性グループの Transact-SQL ステートメントの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/transact-sql-statements-for-always-on-availability-groups.md)」を参照してください。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 **sysadmin** 固定サーバー ロールのメンバーシップと、CREATE AVAILABILITY GROUP サーバー権限、ALTER ANY AVAILABILITY GROUP 権限、CONTROL SERVER 権限のいずれかが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-configuring-backup-on-secondary-replicas-flexible-failover-policy-and-connection-access"></a>A. セカンダリ レプリカ上のバックアップ、柔軟なフェールオーバー ポリシー、および接続アクセスを構成する  
 次の例では、2 つのユーザー データベース (`ThisDatabase` および `ThatDatabase`) に対して、`MyAg` という名前の可用性グループを作成します。 次の表は、可用性グループ全体を対象に設定されるオプションの指定値をまとめたものです。  
  
|グループ オプション|設定|[説明]|  
|------------------|-------------|-----------------|  
|AUTOMATED_BACKUP_PREFERENCE|SECONDARY|この自動バックアップの設定によって、プライマリ レプリカがオンラインの唯一のレプリカである場合を除いて、バックアップがセカンダリ レプリカで発生することが示されます (これが既定の動作です)。 AUTOMATED_BACKUP_PREFERENCE 設定が作用するためには、自動バックアップの設定が考慮されるようにバックアップ ジョブのスクリプトを可用性データベースに作成する必要があります。|  
|FAILURE_CONDITION_LEVEL|3|このエラー条件レベル設定は、孤立したスピンロック、深刻な書き込みアクセス違反、ダンプが多すぎるなど、SQL Server 内部の深刻なエラーが発生した場合に自動フェールオーバーを開始する必要があることを指定します。|  
|HEALTH_CHECK_TIMEOUT|600000|正常性チェックのタイムアウト値を 60 秒に設定します。同期コミット レプリカ (自動フェールオーバー有効) をホストしているサーバー インスタンスについての状態情報が [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) システム ストアド プロシージャから返されるまで、WSFC クラスターは 60000 ミリ秒待機します。その時間を経過すると、ホスト サーバー インスタンスは速度低下またはハングしているものと見なされます (既定値は 30000 ミリ秒です)。|  
  
 3 つの可用性レプリカは、`COMPUTER01`、`COMPUTER02`、および `COMPUTER03` という名前のコンピューター上の既定のサーバー インスタンスによってホストされます。 次の表は、レプリカ オプションの指定値をレプリカごとにまとめたものです。  
  
|レプリカ オプション|`COMPUTER01` 上の設定|`COMPUTER02` 上の設定|`COMPUTER03` 上の設定|[説明]|  
|--------------------|-----------------------------|-----------------------------|-----------------------------|-----------------|  
|ENDPOINT_URL|TCP://*COMPUTER01:5022*|TCP://*COMPUTER02:5022*|TCP://*COMPUTER03:5022*|この例では、いずれのシステムも同じドメインに存在するため、エンドポイントの URL には、コンピューター システムの名前をシステム アドレスとして使用できます。|  
|AVAILABILITY_MODE|SYNCHRONOUS_COMMIT|SYNCHRONOUS_COMMIT|ASYNCHRONOUS_COMMIT|2 つのレプリカが同期コミット モードを使用します。 同期されているレプリカは、データ損失のないフェールオーバーをサポートします。 3 番目のレプリカには、非同期コミットの可用性モードが使用されます。|  
|FAILOVER_MODE|AUTOMATIC|AUTOMATIC|MANUAL|同期コミット レプリカは、自動フェールオーバーおよび計画的な手動フェールオーバーをサポートします。 同期コミット可用性モードのレプリカは、強制手動フェールオーバーのみサポートします。|  
|BACKUP_PRIORITY|30|30|90|非同期コミット レプリカには、同期コミット レプリカよりも高い優先度 (90) が割り当てられます。 バックアップの頻度は、非同期コミット レプリカをホストするサーバー インスタンスのほうが高くなります。|  
|SECONDARY_ROLE|( ALLOW_CONNECTIONS = NO,<br /><br /> READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01:1433' )|( ALLOW_CONNECTIONS = NO,<br /><br /> READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02:1433' )|( ALLOW_CONNECTIONS = READ_ONLY, <br />READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03:1433' )|非同期コミット レプリカだけが、読み取り可能なセカンダリ レプリカとして機能します。<br /><br /> コンピューターの名前と、データベース エンジンの既定のポート番号 (1433) を指定します。<br /><br /> この引数は省略可能です。|  
|PRIMARY_ROLE|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = (COMPUTER03) )|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = (COMPUTER03) )|( ALLOW_CONNECTIONS = READ_WRITE, <br />READ_ONLY_ROUTING_LIST = NONE )|プライマリ ロールでは、読み取りを目的とした接続試行は、すべてのレプリカで拒否されます。<br /><br /> ローカル レプリカがセカンダリ ロールで実行されている場合、読み取りを目的とした接続要求は COMPUTER03 にルーティングされます。 そのレプリカがプライマリ ロールで実行していると、読み取り専用のルーティングは無効になります。<br /><br /> この引数は省略可能です。|  
|SESSION_TIMEOUT|10|10|10|この例では、既定のセッション タイムアウト値 (10) を指定します。 この引数は省略可能です。|  
  
 最後に、新しい可用性グループの可用性グループ リスナーを作成するための省略可能な LISTENER 句を指定します。 このリスナーには、一意の DNS 名 `MyAgListenerIvP6`を指定します。 2 つのレプリカが異なるサブネット上に存在するため、リスナーは静的 IP アドレスを使用する必要があります。 WITH IP 句には、2 つの可用性レプリカについて、それぞれ IPv6 形式の静的 IP アドレス (`2001:4898:f0:f00f::cf3c` および `2001:4898:e0:f213::4ce2`) を指定します。 また、この例では、オプションの PORT 引数を使用して、 `60173` をリスナー ポートとして指定しています。  
  
```SQL
CREATE AVAILABILITY GROUP MyAg   
   WITH (  
      AUTOMATED_BACKUP_PREFERENCE = SECONDARY,  
      FAILURE_CONDITION_LEVEL  =  3,   
      HEALTH_CHECK_TIMEOUT = 600000  
       )  
  
   FOR   
      DATABASE  ThisDatabase, ThatDatabase   
   REPLICA ON   
      'COMPUTER01' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER01:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC,  
         BACKUP_PRIORITY = 30,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = NO,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01:1433' ),
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER03) ),  
         SESSION_TIMEOUT = 10  
         ),   
  
      'COMPUTER02' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER02:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = AUTOMATIC,  
         BACKUP_PRIORITY = 30,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = NO,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER03) ),  
         SESSION_TIMEOUT = 10  
         ),   
  
      'COMPUTER03' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03:5022',  
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
         FAILOVER_MODE =  MANUAL,  
         BACKUP_PRIORITY = 90,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = NONE ),  
         SESSION_TIMEOUT = 10  
         );
GO  
ALTER AVAILABILITY GROUP [MyAg]
  ADD LISTENER 'MyAgListenerIvP6' ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173 );   
GO  
```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [可用性グループの作成 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [可用性グループ ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [可用性グループ ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>参照  
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-availability-group-transact-sql.md)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)   
 [DROP AVAILABILITY GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-availability-group-transact-sql.md)   
 [AlwaysOn 可用性グループの構成のトラブルシューティング &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)   
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
  

