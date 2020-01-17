---
title: HealthCheckTimeout プロパティ設定の構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 3bbeb979-e6fc-4184-ad6e-cca62108de74
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cfcb5d25b207af35e9a26b95b86997c803828f3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002472"
---
# <a name="configure-healthchecktimeout-property-settings"></a>HealthCheckTimeout プロパティ設定の構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  HealthCheckTimeout 設定を使用して、SQL Server リソース DLL が [sp_server_diagnostics](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) ストアド プロシージャによって返される情報を待機する時間を、ミリ秒単位で指定できます。この待機時間を経過すると、AlwaysOn フェールオーバー クラスター インスタンス (FCI) は応答不能としてレポートされます。 タイムアウトの設定に加えられた変更は直ちに有効になり、SQL Server リソースを再起動する必要はありません。  
  
-   **作業を開始する準備:** [制限事項と制約事項](#Limits)、[セキュリティ](#Security)  
  
-   **HeathCheckTimeout 設定を構成するには、次を使用:** [PowerShell](#PowerShellProcedure)、[フェールオーバー クラスター マネージャー](#WSFC)、[Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Limits"></a> 制限事項と制約事項  
 このプロパティの既定値は 30,000 ミリ秒 (30 秒) です。 最小値は 15,000 ミリ秒 (15 秒) です。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 ALTER SETTINGS 権限および VIEW SERVER STATE 権限が必要です。  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
  
##### <a name="to-configure-healthchecktimeout-settings"></a>HealthCheckTimeout 設定を構成するには  
  
1.  **[実行管理者として実行]** から高度な権限で Windows PowerShell を起動します。  
  
2.  **FailoverClusters** モジュールをインポートしてクラスター コマンドレットを有効にします。  
  
3.  **Get-ClusterResource** コマンドレットを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースを検索し、次に **Set-ClusterParameter** コマンドレットを使用してフェールオーバー クラスター インスタンスの **HealthCheckTimeout** プロパティを設定します。  
  
> [!TIP]  
>  新しい PowerShell ウィンドウを開くたびに、 **FailoverClusters** モジュールをインポートする必要があります。  
  
### <a name="example-powershell"></a>例 (PowerShell)  
 次の例では、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソース "`SQL Server (INST1)`" の HealthCheckTimeout 設定が 60000 ミリ秒に変更されます。  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter HealthCheckTimeout 60000  
  
```  
  
### <a name="related-content-powershell"></a>関連コンテンツ (PowerShell)  
  
-   [クラスターと高可用性](https://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (フェールオーバー クラスタリングとネットワーク負荷分散のチームのブログ)  
  
-   [フェールオーバー クラスターの Windows PowerShell の概要](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [クラスター リソースのコマンドと同等の Windows PowerShell コマンドレット](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="WSFC"></a> フェールオーバー クラスター マネージャー スナップインの使用  
 **HealthCheckTimeout 設定を構成するには**  
  
1.  フェールオーバー クラスター マネージャー スナップインを開きます。  
  
2.  **[サービスとアプリケーション]** を展開し、FCI を選択します。  
  
3.  **[その他のリソース]** の下の **[SQL Server リソース]** を右クリックし、表示されるメニューの **[プロパティ]** をクリックします。 SQL Server リソースの **[プロパティ]** ダイアログ ボックスが表示されます。  
  
4.  **[プロパティ]** タブをクリックし、 **[HealthCheckTimeout]** プロパティに適切な値を入力し、 **[OK]** をクリックして変更を適用します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 [ALTER SERVER CONFIGURATION](../../../t-sql/statements/alter-server-configuration-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用すると、HealthCheckTimeOut プロパティ値を指定できます。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、HealthCheckTimeout オプションを 15,000 ミリ秒 (15 秒) に設定します。  
  
```  
ALTER SERVER CONFIGURATION   
SET FAILOVER CLUSTER PROPERTY HealthCheckTimeout = 15000;  
```  
  
## <a name="see-also"></a>参照  
 [フェールオーバー クラスター インスタンスのフェールオーバー ポリシー](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)  
  
  
