---
title: FailureConditionLevel プロパティ設定の構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 513dd179-9a46-46da-9fdd-7632cf6d0816
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 87ed68cc3540075e0fd5d357182d709394f44455
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797497"
---
# <a name="configure-failureconditionlevel-property-settings"></a>FailureConditionLevel プロパティ設定の構成
  FailureConditionLevel プロパティを使用して、AlwaysOn フェールオーバー クラスター インスタンス (FCI) がフェールオーバーまたは再起動するための状態を設定します。 このプロパティへの変更はすぐに適用され、Windows Server フェールオーバー クラスター サービス (WSFC) または FCI リソースの再起動を必要としません。  
  
-   **Before you begin:**  [FailureConditionLevel Property Settings](#Restrictions), [Security](#Security)  
  
-   **FailureConditionLevel プロパティ設定の構成に使用する機能:** [PowerShell](#PowerShellProcedure)、[フェールオーバー クラスター マネージャー](#WSFC)、[Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> FailureConditionLevel プロパティの設定  
 エラー状態にはレベルが設定されています。 レベル 1 ～ 5 の各レベルには、前のレベルのすべての状態に加えて独自の状態が含まれています。 これは、それぞれのレベルで、フェールオーバーまたは再起動の可能性が増加することを意味します。  詳細については、この「 [Failover Policy for Failover Cluster Instances](failover-policy-for-failover-cluster-instances.md) 」の「フェールオーバーの特定」セクションを参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> アクセス許可  
 ALTER SETTINGS 権限および VIEW SERVER STATE 権限が必要です。  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
  
### <a name="to-configure-failureconditionlevel-settings"></a>FailureConditionLevel 設定を構成するには  
  
1.  **[実行管理者として実行]** から高度な権限で Windows PowerShell を起動します。  
  
2.  `FailoverClusters` モジュールをインポートしてクラスター コマンドレットを有効にします。  
  
3.  `Get-ClusterResource` コマンドレットを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースを検索し、`Set-ClusterParameter` コマンドレットを使用して、フェールオーバークラスターインスタンスの**Failureconditionlevel**プロパティを設定します。  
  
> [!TIP]  
>  新しい PowerShell ウィンドウを開くたびに、`FailoverClusters` モジュールをインポートする必要があります。  

 次の例では、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソース "`SQL Server (INST1)`" の FailureConditionLevel 設定が、重大なサーバー エラー発生時のフェールオーバーまたは再起動に変更されます。  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter FailureConditionLevel 3
```  
  
### <a name="related-content-powershell"></a>関連コンテンツ (PowerShell)  
  
-   [クラスターと高可用性](https://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (フェールオーバー クラスタリングとネットワーク負荷分散のチームのブログ)  
  
-   [フェールオーバー クラスターの Windows PowerShell の概要](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [クラスター リソースのコマンドと同等の Windows PowerShell コマンドレット](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="WSFC"></a> フェールオーバー クラスター マネージャー スナップインの使用  

### <a name="to-configure-failureconditionlevel-property-settings"></a>FailureConditionLevel プロパティの設定を構成するには
  
1.  フェールオーバー クラスター マネージャー スナップインを開きます。  
  
2.  **[サービスとアプリケーション]** を展開し、FCI を選択します。  
  
3.  **[その他のリソース]** の下の **[SQL Server リソース]** を右クリックし、表示されるメニューの **[プロパティ]** をクリックします。 SQL Server リソースの **[プロパティ]** ダイアログ ボックスが表示されます。  
  
4.  **[プロパティ]** タブをクリックし、 **[FaliureConditionLevel]** プロパティに値を入力し、 **[OK]** をクリックして変更を適用します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  

### <a name="to-configure-failureconditionlevel-property-settings"></a>FailureConditionLevel プロパティの設定を構成するには
  
 [ALTER SERVER CONFIGURATION](/sql/t-sql/statements/alter-server-configuration-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用すると、FailureConditionLevel プロパティ値を指定できます。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、FailureConditionLevel プロパティを 0 に設定します。この場合、どのようなエラー状態でも、フェールオーバーまたは再起動が自動的に行われないように指定されます。  
  
```sql
ALTER SERVER CONFIGURATION SET FAILOVER CLUSTER PROPERTY FailureConditionLevel = 0;  
```  
  
## <a name="see-also"></a>参照  
 [sp_server_diagnostics &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)   
 [Failover Policy for Failover Cluster Instances](failover-policy-for-failover-cluster-instances.md)  
