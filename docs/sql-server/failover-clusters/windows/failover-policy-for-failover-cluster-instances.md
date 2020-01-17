---
title: フェールオーバー クラスター インスタンスのフェールオーバー ポリシー | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- flexible failover policy
ms.assetid: 39ceaac5-42fa-4b5d-bfb6-54403d7f0dc9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8e2fae9bbc5f0f601f4d455204df6c9d18383458
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044751"
---
# <a name="failover-policy-for-failover-cluster-instances"></a>Failover Policy for Failover Cluster Instances
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンス (FCI) において、特定の時点で Windows Server フェールオーバー クラスター (WSFC) クラスター リソース グループを所有できるノードは 1 つだけです。 FCI のこのノードを通じて、クライアント要求が処理されます。 万一障害が発生した場合や再起動が失敗した場合、グループの所有権が、FCI 内の別の WSFC ノードに移ります。 この処理はフェールオーバーと呼ばれます。 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] では、障害検出の信頼性が向上し、柔軟なフェールオーバー ポリシーが提供されます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] FCI は、基になる WSFC サービスにフェールオーバー検出を依存します。 したがって、FCI のフェールオーバー動作は、ネイティブ WSFC 機能と、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップによって追加される機能の 2 つのメカニズムによって決定されます。  
  
-   WSFC クラスターはクォーラム構成を保持するため、自動フェールオーバーにおいて一意のフェールオーバー ターゲットが保証されます。 WSFC サービスは、クラスターが常に最適なクォーラム状態であるかどうかを判定したうえで、リソース グループをオンラインまたはオフラインにします。  
  
-   アクティブな [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスは、専用接続を介して、コンポーネント診断のセットを WSFC リソース グループに定期的に報告します。 WSFC リソース グループは、再起動およびフェールオーバーをトリガーする障害条件を定義するフェールオーバー ポリシーを保持します。  
  
 このトピックでは、上記の 2 番目のメカニズムについて説明します。 クォーラム構成および正常性状態の検出のための WSFC 動作の詳細については、「[WSFC クォーラム モードと投票の構成 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)」を参照してください。  
  
> [!IMPORTANT]  
>  FCI との間の自動フェールオーバーは AlwaysOn 可用性グループでは許可されません。 ただし、FCI との間の手動フェールオーバーは AlwaysOn 可用性グループで許可されます。  
  
##  <a name="Concepts"></a> フェールオーバー ポリシーの概要  
 フェールオーバー プロセスは、次の手順に分けることができます。  
  
1.  [正常性状態の監視](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#monitor)  
  
2.  [エラーの特定](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#determine)  
  
3.  [エラーへの対応](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#respond)  
  
###  <a name="monitor"></a> 正常性状態の監視  
 FCI に対して監視される正常性状態には、次の 3 種類があります。  
  
-   [SQL Server サービスの状態](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#service)  
  
-   [SQL Server インスタンスの応答時間](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#instance)  
  
-   [SQL Server コンポーネント診断](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md#component)  
  
####  <a name="service"></a> SQL Server サービスの状態  
 WSFC サービスは、アクティブな FCI ノード上の SQL Server サービスの開始状態を監視して、SQL Server サービスの停止を検出します。  
  
####  <a name="instance"></a> SQL Server インスタンスの応答時間  
 SQL Server の起動時、WSFC サービスは、SQL Server データベース エンジン リソース DLL を使用して、正常性状態の監視にのみ使用される新しい接続を別個のスレッド上に作成します。 これにより、負荷があるときの正常性状態を SQL インスタンスがレポートするために必要なリソースが確保されます。 この専用の接続を使用して、SQL Server は [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) システム ストアド プロシージャを繰り返しモードで実行し、SQL Server コンポーネントの正常性状態をリソース DLL に定期的に報告します。  
  
 リソース DLL は、正常性チェックのタイムアウトを使用して SQL インスタンスの応答時間を判定します。 HealthCheckTimeout プロパティは、リソース DLL が sp_server_diagnostics ストアド プロシージャを待機する時間を定義します。この待機時間を経過すると、SQL インスタンスは応答不能と見なされ、その旨が WSFC サービスに報告されます。 このプロパティは、フェールオーバー クラスター マネージャー スナップインに加え、T-SQL を使用して構成できます。 詳細については、「 [HealthCheckTimeout プロパティ設定の構成](../../../sql-server/failover-clusters/windows/configure-healthchecktimeout-property-settings.md)」を参照してください。 次に、このプロパティがタイムアウトに与える影響、およびリピート間隔設定について説明します。  
  
-   リソース DLL によって sp_server_diagnostics ストアド プロシージャが呼び出され、リピート間隔が HealthCheckTimeout 設定の 1/3 に設定されます。  
  
-   sp_server_diagnostics ストアド プロシージャの処理が遅いか、情報が返されない場合、リソース DDL は HealthCheckTimeout によって指定された時間待機した後、SQL インスタンスが応答していないことを WSFC サービスに通知します。  
  
-   専用の接続が失われた場合、リソース DLL は、HealthCheckTimeout によって指定された時間にわたって SQL インスタンスへの接続を再試行した後、SQL インスタンスが応答していないことを WSFC サービスに通知します。  
  
####  <a name="component"></a> SQL Server コンポーネント診断  
 システム ストアド プロシージャ sp_server_diagnostics は、SQL インスタンスで定期的にコンポーネント診断を収集します。 収集された診断情報は、次の各コンポーネント用の行として表され、呼び出し側スレッドに渡されます。  
  
1.  システム  
  
2.  resource  
  
3.  query process  
  
4.  io_subsystem  
  
5.  イベント  
  
 system、resource、および query process コンポーネントはエラー検出に使用されます。 io_subsytem および events コンポーネントは、診断目的でのみ使用されます。  
  
 それぞれの情報の行セットは、SQL Server クラスター診断ログに書き込まれます。 詳細については、「 [フェールオーバー クラスター インスタンスの診断ログを表示して読む方法](../../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md)」を参照してください。  
  
> [!TIP]  
>  sp_server_diagnostic ストアド プロシージャは SQL Server AlwaysOn テクノロジによって使用されるほか、問題の検出とトラブルシューティングを行うために任意の SQL Server インスタンスで使用できます。  
  
####  <a name="determine"></a> エラーの特定  
 SQL Server データベース エンジン リソース DLL は、FailureConditionLevel プロパティを使用して、検出された正常性状態がエラー条件に該当するかどうかを判定します。 FailureConditionLevel プロパティは、どの検出された正常性状態に基づいて再起動またはフェールオーバーを発生させるかを定義します。 "自動フェールオーバーまたは再起動なし" から自動再起動またはフェールオーバーを発生させる可能性のあるあらゆるエラー条件に至るまで、複数レベルのオプションを使用できます。 このプロパティの構成方法については、「 [FailureConditionLevel プロパティ設定の構成](../../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md)」を参照してください。  
  
 エラー状態にはレベルが設定されています。 レベル 1 ～ 5 の各レベルには、前のレベルのすべての状態に加えて独自の状態が含まれています。 これは、それぞれのレベルで、フェールオーバーまたは再起動の可能性が増加することを意味します。 次の表では、エラー状態のレベルについて説明しています。  
  
 「[sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)」を確認してください。このシステム ストアド プロシージャは、エラー条件レベルで重要な役割を果たします。  
  
|Level|条件|[説明]|  
|-----------|---------------|-----------------|  
|0|自動フェールオーバーまたは再起動なし|どのようなエラー状態でも、フェールオーバーまたは再起動が自動的に行われないことを示します。 このレベルは、システム メンテナンスの目的でのみ使用されます。|  
|1|サーバーの停止によるフェールオーバーまたは再起動|次の状態が発生した場合に、サーバーの再起動またはフェールオーバーが行われることを示します。<br /><br /> SQL Server サービスが停止した。|  
|2|サーバーの応答停止によるフェールオーバーまたは再起動|次のいずれかの状態が発生した場合に、サーバーの再起動またはフェールオーバーが行われることを示します。<br /><br /> SQL Server サービスが停止した。<br /><br /> SQL Server インスタンスが応答しない (リソース DLL が HealthCheckTimeout の設定時間内に sp_server_diagnostics からデータを受け取れない)。|  
|3*|重大なサーバー エラーによるフェールオーバーまたは再起動|次のいずれかの状態が発生した場合に、サーバーの再起動またはフェールオーバーが行われることを示します。<br /><br /> SQL Server サービスが停止した。<br /><br /> SQL Server インスタンスが応答しない (リソース DLL が HealthCheckTimeout の設定時間内に sp_server_diagnostics からデータを受け取れない)。<br /><br /> システム ストアド プロシージャ sp_server_diagnostics から 'system エラー' が返される。|  
|4|中程度のサーバー エラーによるフェールオーバーまたは再起動|次のいずれかの状態が発生した場合に、サーバーの再起動またはフェールオーバーが行われることを示します。<br /><br /> SQL Server サービスが停止した。<br /><br /> SQL Server インスタンスが応答しない (リソース DLL が HealthCheckTimeout の設定時間内に sp_server_diagnostics からデータを受け取れない)。<br /><br /> システム ストアド プロシージャ sp_server_diagnostics から 'system エラー' が返される。<br /><br /> システム ストアド プロシージャ sp_server_diagnostics から 'resource エラー' が返される。|  
|5|限定されたエラー状態によるフェールオーバーまたは再起動|次のいずれかの状態が発生した場合に、サーバーの再起動またはフェールオーバーが行われることを示します。<br /><br /> SQL Server サービスが停止した。<br /><br /> SQL Server インスタンスが応答しない (リソース DLL が HealthCheckTimeout の設定時間内に sp_server_diagnostics からデータを受け取れない)。<br /><br /> システム ストアド プロシージャ sp_server_diagnostics から 'system エラー' が返される。<br /><br /> システム ストアド プロシージャ sp_server_diagnostics から 'resource エラー' が返される。<br /><br /> システム ストアド プロシージャ sp_server_diagnostics から 'query_processing エラー' が返される。|  
  
 \* 既定値  
  
####  <a name="respond"></a> エラーへの対応  
 1 つまたは複数のエラー条件が検出された後で WSFC サービスがどのようにエラーに対応するかは、WSFC クォーラムの状態と、FCI リソース グループの再起動およびフェールオーバー設定に依存します。 FCI がその WSFC クォーラムを失った場合、FCI 全体がオフラインになり、FCI は高可用性を失います。 FCI が WSFC クォーラムを保持し続けた場合、WSFC サービスは、最初に障害が発生したノードの再起動を試み、再起動の試行が失敗した場合はフェールオーバーを実行することによって対応します。 再起動とフェールオーバーの設定は、フェールオーバー クラスター マネージャー スナップインで構成します。 これらの設定の詳細については、「[\<リソース> プロパティ: [ポリシー] タブ](https://technet.microsoft.com/library/cc725685.aspx)」を参照してください。  
  
 クォーラムの正常性の維持については、「[WSFC クォーラム モードと投票の構成 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-configuration-transact-sql.md)  
  
  
