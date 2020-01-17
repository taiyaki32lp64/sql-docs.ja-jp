---
title: 可用性グループに柔軟な自動フェールオーバー ポリシーを構成する
description: TRANSACT-SQL (T-SQL)、PowerShell、または SQL Server Management Studio を使用して Always On 可用性グループに柔軟なフェールオーバー ポリシーを構成する方法を説明します。
ms.date: 11/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 1ed564b4-9835-4245-ae35-9ba67419a4ce
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.custom: seo-lt-2019
ms.openlocfilehash: 39e6e14700fe7ad9d9c1c3ba71eca82b3855beb2
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056684"
---
# <a name="configure-a-flexible-automatic-failover-policy-for-an-always-on-availability-group"></a>Always On 可用性グループに柔軟な自動フェールオーバー ポリシーを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  このトピックでは、SQL Server で [!INCLUDE[tsql](../../../includes/tsql-md.md)] または PowerShell を使用して Always On 可用性グループの柔軟なフェールオーバー ポリシーを構成する方法について説明します。 柔軟なフェールオーバー ポリシーを使用すると、可用性グループの [自動フェールオーバー](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) を実行する条件をきめ細かく制御できます。 自動フェールオーバーを実行するエラー条件および正常性チェックの頻度を変更することで、自動フェールオーバーの確率値を増減して高可用性の SLA をサポートできます。  

   可用性グループの柔軟なフェールオーバー ポリシーは、そのエラー条件レベルと正常性チェックのタイムアウトしきい値によって定義されます。 可用性グループがエラー条件レベルまたはその正常性チェックのタイムアウトしきい値を超えていることを検出すると、可用性グループのリソース DLL が Windows Server フェールオーバー クラスタリング (WSFC) クラスターに応答を送り返します。 その後、WSFC クラスターは、セカンダリ レプリカに対する自動フェールオーバーを開始します。  
 
  > [!NOTE]  
  > 可用性グループの柔軟なフェールオーバー ポリシーは、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]を使用して構成できません。  
  
 
## <a name="Limitations"></a> 自動フェールオーバーの制限  
  
-   自動フェールオーバーが行われるには、現在のプライマリ レプリカおよび 1 つのセカンダリ レプリカが自動フェールオーバーを使用する同期コミット可用性モード用に構成され、セカンダリ レプリカがプライマリ レプリカと同期している必要があります。  
  
-   自動フェールオーバーでサポートされるレプリカは 3 つだけです。  
  
-   WSFC クラスターでは、可用性グループが WSFC のエラーしきい値を超えると、自動フェールオーバーはその可用性グループに対して実行されません。 また、クラスター管理者が失敗したリソース グループを手動でオンラインにするか、データベース管理者が可用性グループの手動フェールオーバーを実行するまで、可用性グループの WSFC リソース グループはエラー状態のままになります。 *WSFC のエラーしきい値* は、特定の期間に可用性グループに対して許容されるエラーの最大数として定義されています。 既定の期間は 6 時間であり、この期間のエラーの最大数の既定値は *n*-1 です ( *n* は WSFC ノードの数です)。 特定の可用性グループのエラーしきい値を変更するには、WSFC フェールオーバー マネージャー コンソールを使用します。  
  
##  <a name="Prerequisites"></a> 前提条件  
  
-   プライマリ レプリカをホストするサーバー インスタンスに接続されている必要があります。  
   
##  <a name="Permissions"></a> Permissions  
  
|タスク|アクセス許可|  
|----------|-----------------|  
|新しい可用性グループの柔軟なフェールオーバー ポリシーを構成する|**sysadmin** 固定サーバー ロールのメンバーシップと、CREATE AVAILABILITY GROUP サーバー権限、ALTER ANY AVAILABILITY GROUP 権限、CONTROL SERVER 権限のいずれかが必要です。|  
|既存の可用性グループのポリシーを変更する|可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。|  

##  <a name="HCtimeout"></a> 正常性チェックのタイムアウトしきい値  
 可用性グループの WSFC リソース DLL では、プライマリ レプリカをホストする SQL Server のインスタンスで *sp_server_diagnostics* ストアド プロシージャを呼び出して、プライマリ レプリカの [正常性チェック](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) を実行します。 **sp_server_diagnostics** は、可用性グループの正常性チェックのタイムアウトしきい値の 3 分の 1 の間隔で結果を返します。 既定の正常性チェックのタイムアウトしきい値は 30 秒であるので、 **sp_server_diagnostics** では 10 秒間隔で結果が返されます。 **sp_server_diagnostics** が低速であるか、情報を返さない場合、リソース DLL は正常性チェックのタイムアウトしきい値の間隔が完全に経過するのを待ってから、プライマリ レプリカが無応答であると判断します。 プライマリ レプリカが応答しない場合、自動フェールオーバー (現在サポートされている場合) が開始されます。  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** では、データベース レベルでの正常性チェックは実行されません。  
  
##  <a name="FClevel"></a> エラー条件レベル  
 **sp_server_diagnostics** から返される診断データと正常性の情報によって自動フェールオーバーが保証されるかどうかは、可用性グループのエラー条件レベルによって異なります。 *エラー条件レベル* は、自動フェールオーバーを実行するエラー条件を指定します。 エラー条件レベルの範囲は、最も制限が緩いものから (レベル 1)、最も制限の厳しい指定 (レベル 5) まで 5 つあります。 任意のレベルは、それより制限が緩いすべてのレベルを含みます。 したがって、最も制限の厳しいレベル 5 にはそれより制限が緩い 4 つの条件が含まれます。以下同様です。  
  
> [!IMPORTANT]  
>  破損したデータベースおよび問題があると考えられるデータベースは、すべてのエラー条件レベルで検出されません。 そのため、破損したデータベースや問題があると考えられるデータベースによって、(その原因がハードウェア障害、データ破損、またはその他の問題であるかにかかわらず) 自動フェールオーバーがトリガーされることはありません。  
  
 次の表では、各レベルに対応するエラー条件について説明します。  
  
|Level|エラー状態|[!INCLUDE[tsql](../../../includes/tsql-md.md)] の値|PowerShell 値|  
|-----------|-----------------------|------------------------------|----------------------|  
|1|サーバーの停止。 次のいずれかが発生した場合に自動フェールオーバーを開始することを指定します。<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスがダウンした。<br /><br /> WSFC クラスターに接続するための可用性グループのリースが、サーバー インスタンスから ACK を受信しないために期限切れになった。 詳細については、「[How It Works:SQL Server Always On Lease Timeout](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)」 (動作方法: SQL Server Always On のリース タイムアウト) を参照してください。<br /><br /> <br /><br /> これは最も制限の緩いレベルです。|1|**OnServerDown**|  
|2|サーバーの応答停止。 次のいずれかが発生した場合に自動フェールオーバーを開始することを指定します。<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスがクラスターに接続していず、可用性グループのユーザー指定の正常性チェック タイムアウトしきい値を超えた。<br /><br /> 可用性レプリカがエラー状態である。|2|**OnServerUnresponsive**|  
|3|重大なサーバー エラー。 孤立したスピンロック、深刻な書き込みアクセス違反、ダンプが多すぎるなどの深刻な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部エラーが発生した場合に自動フェールオーバーを開始することを指定します。<br /><br /> これは既定のレベルです。|3|**OnCriticalServerError**|  
|4|中程度のサーバー エラー。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部リソース プールに永続的なメモリ不足の状態があるなど中程度の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部エラーが発生した場合に自動フェールオーバーを開始することを指定します。|4|**OnModerateServerError**|  
|5|任意の限定されたエラー条件。 以下のような任意の限定されたエラー条件に対して自動フェールオーバーを開始することを指定します。<br /><br /> スケジューラ デッドロックの検出。<br /><br /> 解決不可能なデッドロックが検出された。<br /><br /> <br /><br /> これは最も制限の厳しいレベルです。|5|**OnAnyQualifiedFailureConditions**|  
  
> [!NOTE]  
>  クライアント要求に対して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスが応答しないことは、可用性グループには関係ありません。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **柔軟なフェールオーバー ポリシーを構成するには**  
  
1.  プライマリ レプリカをホストするサーバー インスタンスに接続します。  
  
2.  新しい可用性グループの場合は、 [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用します。 既存の可用性グループを変更する場合は、 [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用します。  
  
    -   フェールオーバーの条件レベルを設定するには、FAILURE_CONDITION_LEVEL = *n* オプションを使用します。ここで、 *n* は 1 ～ 5 の整数です。  
  
         たとえば、次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントでは、既存の可用性グループ `AG1`のエラー条件レベルをレベル 1 に変更します。  
  
        ```  
  
        ALTER AVAILABILITY GROUP AG1 SET (FAILURE_CONDITION_LEVEL = 1);  
        ```  
  
         これらの整数値とエラー条件レベルの関係は次のとおりです。  
  
        |[!INCLUDE[tsql](../../../includes/tsql-md.md)] の値|Level|自動フェールオーバーが開始される条件|  
        |------------------------------|-----------|-------------------------------------------|  
        |1|1|サーバーの停止。 フェールオーバーまたは再起動のため、SQL Server サービスが停止した場合。|  
        |2|2|サーバーの応答停止。 下限値の任意の条件が満たされた場合、SQL Server サービスがクラスターに接続され正常性チェックのタイムアウトしきい値を超えた場合、または現在のプライマリ レプリカがエラー状態になった場合。|  
        |3|3|重大なサーバー エラー。 下限値の任意の条件が満たされるか、重大な内部サーバー エラーが発生した場合。<br /><br /> これは既定のレベルです。|  
        |4|4|中程度のサーバー エラー。 下限値の任意の条件が満たされるか、中程度のサーバー エラーが発生した場合。|  
        |5|5|任意の限定されたエラー条件。 下限値の任意の条件が満たされるか、限定されたエラー条件が発生した場合。|  
  
         詳細については、「[可用性グループの自動フェールオーバーのための柔軟なフェールオーバー ポリシー &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md)」を参照してください。  
  
    -   正常性チェックのタイムアウトしきい値を構成するには、HEALTH_CHECK_TIMEOUT = *n* オプションを使用します。ここで *n* は 15000 ミリ秒 (15 秒) ～ 4294967295 ミリ秒の整数です。 既定値は 30000 ミリ秒 (30 秒) です。  
  
         たとえば、次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントでは、既存の可用性グループ `AG1`の正常性チェックのタイムアウトしきい値が  60,000 ミリ秒 (1 分) に変更されます。  
  
        ```  
  
        ALTER AVAILABILITY GROUP AG1 SET (HEALTH_CHECK_TIMEOUT = 60000);  
        ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
 **柔軟なフェールオーバー ポリシーを構成するには**  
  
1.  既定 (**cd**) を、プライマリ レプリカをホストするサーバー インスタンスに設定します。  
  
2.  可用性グループに可用性レプリカを追加する場合は、 **New-SqlAvailabilityGroup** コマンドレットを使用します。 既存の可用性レプリカを変更する場合は、 **Set-SqlAvailabilityGroup** コマンドレットを使用します。  
  
    -   フェールオーバーの条件レベルを設定するには、 **FailureConditionLevel**_level_ パラメーターを使用します。この *level* は次の値のいずれかになります。  
  
        |[値]|Level|自動フェールオーバーが開始される条件|  
        |-----------|-----------|-------------------------------------------|  
        |**OnServerDown**|1|サーバーの停止。 フェールオーバーまたは再起動のため、SQL Server サービスが停止した場合。|  
        |**OnServerUnresponsive**|2|サーバーの応答停止。 下限値の任意の条件が満たされた場合、SQL Server サービスがクラスターに接続され正常性チェックのタイムアウトしきい値を超えた場合、または現在のプライマリ レプリカがエラー状態になった場合。|  
        |**OnCriticalServerError**|3|重大なサーバー エラー。 下限値の任意の条件が満たされるか、重大な内部サーバー エラーが発生した場合。<br /><br /> これは既定のレベルです。|  
        |**OnModerateServerError**|4|中程度のサーバー エラー。 下限値の任意の条件が満たされるか、中程度のサーバー エラーが発生した場合。|  
        |**OnAnyQualifiedFailureConditions**|5|任意の限定されたエラー条件。 下限値の任意の条件が満たされるか、限定されたエラー条件が発生した場合。|  
  
         詳細については、「[可用性グループの自動フェールオーバーのための柔軟なフェールオーバー ポリシー &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/flexible-automatic-failover-policy-availability-group.md)」を参照してください。  
  
         たとえば、次のコマンドでは、既存の可用性グループ `AG1` のエラー条件レベルをレベル 1 に変更します。  
  
        ```  
        Set-SqlAvailabilityGroup `   
        -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg `   
        -FailureConditionLevel OnServerDown  
        ```  
  
    -   正常性チェックのタイムアウトしきい値を設定するには、 **HealthCheckTimeout**_n_ パラメーターを使用します。ここで *n* は 15000 ミリ秒 (15 秒) ～ 4294967295 ミリ秒の整数です。 既定値は 30000 ミリ秒 (30 秒) です。  
  
         たとえば、次のコマンドでは、既存の可用性グループ `AG1`の正常性チェックのタイムアウトしきい値が 120,000 ミリ秒 (2 分) に変更されます。  
  
        ```  
        Set-SqlAvailabilityGroup `   
        -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAG `   
        -HealthCheckTimeout 120000  
        ```  
  
> [!NOTE]  
>  コマンドレットの構文を表示するには、 **PowerShell 環境で** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コマンドレットを使用します。 詳細については、「 [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)」を参照してください。  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md)  

##  <a name="RelatedTasks"></a> 関連タスク  
 **自動フェールオーバーを設定するには**  
  
-   [可用性レプリカの可用性モードの変更 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md) (自動フェールオーバーには同期コミット可用性モードが必要)  
  
-   [可用性レプリカのフェールオーバー モードの変更 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [自動フェールオーバーの条件を制御する柔軟なフェールオーバー ポリシーの構成 &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [動作方法: SQL Server Always On のリース タイムアウト](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [フェールオーバーとフェールオーバー モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)   
 [Windows Server フェールオーバー クラスタリング &#40;WSFC&#41; と SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [フェールオーバー クラスター インスタンスのフェールオーバー ポリシー](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)  
  
  
