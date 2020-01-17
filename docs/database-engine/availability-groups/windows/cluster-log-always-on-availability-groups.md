---
title: 可用性グループ用の CLUSTER.LOG を生成および分析する
description: 'Always On 可用性グループ用にクラスター ログを生成および分析する方法について説明します。 '
ms.custom: seo-lt-2019
ms.date: 06/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 01a9e3c1-2a5f-4b98-a424-0ffc15d312cf
author: rothja
ms.author: jroth
ms.openlocfilehash: 045444c2141027854e54480483f09ab8eb9a04b6
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244381"
---
# <a name="generate-and-analyze-the-clusterlog-for-an-always-on-availability-group"></a>Always On 可用性グループ用の CLUSTER.LOG を生成および分析する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  フェールオーバー クラスター リソースとして SQL Server 内で監視できない外部的な対話があります。それは SQL Server、Windows Server フェールオーバー クラスター サービス (WSFC) クラスター、および SQL Server リソース DLL (hadrres.dll) の間で行われるものです。 WSFC ログ (CLUSTER.LOG) を使用すると、WSFC クラスターでの問題、または SQL Server リソース DLL での問題を診断することができます。 
  
## <a name="generate-cluster-log"></a>クラスター ログを生成する  
 クラスター ログを生成するには、次の 2 つの方法があります。  
  
1.  コマンド プロンプトで `cluster /log /g` コマンドを使用します。 このコマンドを実行すると、各 WSFC ノード上の \windows\cluster\reports ディレクトリに出力するクラスター ログが生成されます。 この方法の利点は、`/level` オプションを使用して、生成されるログの詳細レベルを指定できることです。 欠点は、生成されるクラスター ログの出力先ディレクトリを指定できないという点です。 詳細については、「[How to create the cluster.log in Windows Server 2008 Failover Clustering](https://blogs.msdn.com/b/clustering/archive/2008/09/24/8962934.aspx)」 (Windows Server 2008 フェールオーバー クラスタリングで cluster.log を作成する方法) を参照してください。  
  
2.  [Get-clusterlog](https://technet.microsoft.com/library/ee461045.aspx) PowerShell コマンドレットを使用します。 この方法の利点は、すべてのノードからクラスター ログを生成して、コマンドレットを実行するノード上の 1 つの対象ディレクトリに出力できるということです。 欠点は生成されるログの詳細レベルを指定できないことです。  
  
 次の PowerShell コマンドを実行すると、すべてのクラスター ノードから 15 分前からのクラスター ログが生成され、現在のディレクトリに配置されます。 コマンドは、PowerShell ウィンドウで管理者特権を使用して実行します。  
  
```powershell  
Import-Module FailoverClusters   
Get-ClusterLog -TimeSpan 15 -Destination .  
```  
  
## <a name="always-on-log-verbosity"></a>Always On ログの詳細レベル  
 可用性グループに対する CLUSTER.LOG ではログの詳細レベルを上げることができます。 詳細レベルを変更するには、次の手順を実行します。  
  
1.  **[スタート]** メニューから、 **[フェールオーバー クラスター マネージャー]** を開きます。  
  
2.  クラスター、 **[サービスとアプリケーション]** ノードの順に展開し、可用性グループの名前をクリックします。  
  
3.  詳細ウィンドウで、可用性グループのリソースを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[プロパティ]** タブをクリックします。  
  
5.  **VerboseLogging** プロパティを変更します。 既定では、**VerboseLogging** は `0` に設定されます。この場合、情報、警告、およびエラーがレポートされます。 **VerboseLogging** には `0` から `2` までの値を設定できます。  
  
6.  **[OK]** をクリックします。  
  
7.  可用性グループのリソースをもう一度右クリックし、 **[このリソースをオフラインにする]** をクリックします。  
  
8.  可用性グループのリソースをもう一度右クリックし、 **[このリソースをオンラインにする]** をクリックします。  
  
## <a name="availability-group-resource-events"></a>可用性グループのリソース イベント  
 次の表に、可用性グループのリソースに関連するイベントのうち、CLUSTER.LOG 内で確認できる各種イベントを示します。 WSFC のリソース ホスティング サブシステム (RHS) およびリソース コントロール モニター (RCM) の詳細については、「[Resource Hosting Subsystem (RHS) In Windows Server 2008 Failover Clusters](https://blogs.technet.com/b/askcore/archive/2009/11/23/resource-hosting-subsystem-rhs-in-windows-server-2008-failover-clusters.aspx)」 (Windows Server 2008 フェールオーバー クラスターのリソース ホスティング サブシステム (RHS)) を参照してください。  
  
|[Identifier]|source|CLUSTER.LOG の例|  
|----------------|------------|------------------------------|  
|`[RES]` と `[hadrag]` が先頭に付けられたメッセージ|hadrres.dll (Always On リソース DLL)|00002cc4.00001264::2011/08/05-13:47:42.543 INFO  [RES] SQL Server 可用性グループ \<ag>:`[hadrag]` オフライン要求。<br /><br /> 00002cc4.00003384::2011/08/05-13:47:42.558 ERR   [RES] SQL Server 可用性グループ \<ag>:`[hadrag]` リース スレッドが終了しました<br /><br /> 00002cc4.00003384::2011/08/05-13:47:42.605 INFO  [RES] SQL Server 可用性グループ \<ag>:`[hadrag]` 解放 SQL ステートメント<br /><br /> 00002cc4.00003384::2011/08/05-13:47:42.902 INFO  [RES] SQL Server 可用性グループ \<ag>:`[hadrag]` SQL Server からの切断|  
|`[RHS]` が先頭に付けられたメッセージ|RHS.EXE (リソース ホスティング サブシステム、hadrres.dll のホスト プロセス)|00000c40.00000a34::2011/08/10-18:42:29.498 INFO  [RHS] リソース ag がオフラインになりました。 RHS はリソースのステータスを RCM にレポートしようとしています。|  
|`[RCM]` が先頭に付けられたメッセージ|リソース コントロール モニター (クラスター サービス)|000011d0.00000f80::2011/08/05-13:47:42.480 INFO  [RCM] rcm::RcmGroup::Move:グループ 'ag' をまずオフラインに...<br /><br /> 000011d0.00000f80::2011/08/05-13:47:42.496 INFO  [RCM] TransitionToState(ag) Online-->OfflineCallIssued.|  
|RcmApi/ClusAPI|API 呼び出し。ほとんどの場合は、SQL Server がアクションを要求しています|000011d0.00000f80::2011/08/05-13:47:42.465 INFO  [RCM] rcm::RcmApi::MoveGroup: (ag, 2)|  
  
## <a name="debug-always-on-resource-dll-in-isolation"></a>Always On リソース DLL を分離してデバッグする  
 デバッグを行う場合は、Always On リソース DLL (hadrres.dll) を他のリソース DLL から分離して実行するように、ご使用のクラスターを構成することをお勧めします。 既定では、WSFC クラスターは rhs.exe の単一インスタンス内のすべてのリソース DLL を実行します。 これにより、クラスター内のすべてのリソースが同じ rhs.exe インスタンスを共有するようになります。 デバッガーで hadrres.dll のデバッグを試みる場合、ブレークポイントで一時停止すると、rhs.exe インスタンスを共有する他のリソースも一時停止する場合があります。 また、同じクラスター内にある複数の可用性グループを実行する場合、1 つの可用性グループをデバッグするためにブレークポイントで一時停止すると、構成が同じであるためにすべての可用性グループが一時停止する可能性があります。  
  
 可用性グループを他のクラスター リソース DLL (他の可用性グループを含む) から分離するには、次の手順に従って個別の rhs.exe プロセス内で hadrres.dll を実行します。  
  
1.  **レジストリ エディター**で、次のキーに移動します。HKEY_LOCAL_MACHINE\Cluster\Resources このキーには、それぞれ異なる GUID を持つすべてのリソースのキーが含まれています。  
  
2.  目的の可用性グループ名と一致する**名前**の値が含まれているリソース キーを探します。  
  
3.  **SeparateMonitor** の値を **1** に変更します。  
  
4.  WSFC クラスターで可用性グループ用のクラスター化されたサービスを再起動します。  
  
  
