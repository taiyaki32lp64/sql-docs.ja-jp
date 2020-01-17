---
title: WSFC クォーラム モードと投票の構成 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
- failover clustering [SQL Server], AlwaysOn Availability Groups
ms.assetid: ca0d59ef-25f0-4047-9130-e2282d058283
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7febab9f8ecf6cae4df08f110a16c0bdc512a948
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62711437"
---
# <a name="wsfc-quorum-modes-and-voting-configuration-sql-server"></a>WSFC クォーラム モードと投票の構成 (SQL Server)
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] と AlwaysOn フェールオーバー クラスター インスタンス (FCI) のどちらも、Windows Server フェールオーバー クラスタリング (WSFC) をプラットフォーム テクノロジとして使用します。  WSFC は、クォーラム ベースのアプローチを使用してクラスターの全体的な正常性を監視し、ノード レベルのフォールト トレランスを最大限に高めます。 WSFC クォーラム モードおよびノード投票構成の基本について理解することは、AlwaysOn 高可用性およびディザスター リカバリー ソリューションの設計、運用、トラブルシューティングのために非常に重要です。  
  
 **このトピックの内容:**  
  
-   [クォーラムによるクラスター状態検出](#ClusterHealthDetectionbyQuorum)  
  
-   [クォーラム モード](#QuorumModes)  
  
-   [投票と非投票ノード](#VotingandNonVotingNodes)  
  
-   [クォーラム投票に推奨される調整](#RecommendedAdjustmentstoQuorumVoting)  
  
-   [関連タスク](#RelatedTasks)  
  
-   [関連コンテンツ](#RelatedContent)  
  
##  <a name="ClusterHealthDetectionbyQuorum"></a> クォーラムによるクラスター状態検出  
 WSFC クラスター内の各ノードは、定期的なハートビート通信に参加し、ノードの正常性状態を他のノードと共有します。 応答しないノードは、エラー状態であると見なされます。  
  
 *クォーラム* ノード セットは、WSFC クラスター内の大多数の投票ノードおよび監視サーバーです。 WSFC クラスターの全体的な正常性と状態は、定期的な *クォーラムの投票*によって決定されます。  クォーラムの存在は、クラスターが正常であり、ノード レベルのフォールト トレランスを提供できることを表します。  
  
 クォーラムがない状態は、クラスターが正常でないことを示します。  プライマリ ノードのフェールオーバー先として正常なセカンダリ ノードを使用できるようにするために、WSFC クラスターの全体的な正常性が維持される必要があります。  クォーラム投票に失敗した場合、WSFC クラスターは、予防策としてオフラインに設定されます。  これによって、クラスターに登録されている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスがすべて停止します。  
  
> [!IMPORTANT]  
>  クォーラム障害のために WSFC クラスターがオフラインに設定されると、オンラインに戻すために手動介入が必要です。  
>   
>  詳細については、以下をご覧ください。[WSFC の強制クォーラムによる災害復旧 &#40;SQL Server&#41;](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
##  <a name="QuorumModes"></a> クォーラム モード  
 *クォーラム モード* は、WSFC クラスター レベルで構成され、クォーラム投票の方法を指定します。  フェールオーバー クラスター マネージャー ユーティリティは、クラスター内のノード数に基づいて、クォーラム モードを推奨します。  
  
 投票クォーラムの構成を決定するために、次のクォーラム モードを使用できます。  
  
-   **ノード マジョリティ。** クラスターが正常であるためには、クラスター内の半分以上の投票ノードが肯定的に投票する必要があります。  
  
-   **ノードおよびファイル共有マジョリティ。** ノード マジョリティ クォーラム モードに似ていますが、リモート ファイル共有も投票監視として構成され、その共有に対する各ノードからの接続も肯定的な投票としてカウントされます。  クラスターが正常であるためには、使用可能な投票の半分以上が肯定的である必要があります。  
  
     推奨事項として、監視ファイル共有はクラスター内のノードに存在せず、クラスター内のすべてのノードから見える必要があります。  
  
-   **ノードおよびディスク マジョリティ。** ノード マジョリティ クォーラム モードに似ていますが、共有ディスク クラスター リソースも投票監視として使用され、その共有ディスクに対する各ノードからの接続も肯定的な投票としてカウントされます。  クラスターが正常であるためには、使用可能な投票の半分以上が肯定的である必要があります。  
  
-   **ディスクのみ。** 共有ディスク クラスター リソースが監視として使用され、その共有ディスクに対する各ノードからの接続も肯定的な投票としてカウントされます。  
  
> [!TIP]  
>  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]の非対称的なストレージ構成を使用する際には、通常、投票ノード数が奇数の場合はノード マジョリティ クォーラム モード、投票ノード数が偶数の場合はノードおよびファイル共有マジョリティ クォーラム モードを使用してください。  
  
##  <a name="VotingandNonVotingNodes"></a> 投票と非投票ノード  
 既定では、WSFC クラスター内の各ノードがクラスター クォーラムのメンバーとして含まれます。各ノードはクラスターの全体的な正常性の決定において 1 つの投票を持ちます。また、各ノードはクォーラムの構築を試行し続けます。  クォーラムに関するここまでの説明では、クラスター状態について投票する WSFC クラスター ノードのセットを *投票ノード*として注意深く限定してきました。  
  
 WSFC クラスター内のノードは、クラスターが全体として正常であるまたは正常でないと明確に決定することはできません。  特定の時点で、各ノードからは、他のノードの一部はオフラインに見えるか、フェールオーバー中であるか、またはネットワーク通信のエラーにより応答不能に見えます。  クォーラム投票の主な機能は、WSFC クラスターの各ノードの外観の状態が、本当にそれらのノードの実際の状態であるかどうかを判断することです。  
  
 "ディスクのみ" 以外のすべてのクォーラム モデルでは、クォーラム投票の有効性は、クラスター内のすべての投票ノード間の信頼できる通信によります。 同じ物理サブネット上のノード間のネットワーク通信は信頼性が高いと見なす必要があります。クォーラム投票は、信頼される必要があります。  
  
 しかし、クォーラム投票で他のサブネット上のノードが応答しないように見えるが実際はオンラインで正常である場合、サブネット間のネットワーク通信のエラーが原因であることが考えられます。  クラスター トポロジ、クォーラム モード、およびフェールオーバー ポリシー構成によっては、ネットワーク通信エラーによって投票ノードのセット (またはサブセット) が実質的に複数作成されてしまう可能性があります。  
  
 投票ノードの複数のサブセットが自身でクォーラムを構築できる場合、それは *スプリット ブレイン シナリオ*と呼ばれます。  このようなシナリオでは、各クォーラム上のノードが別々の動作をし、相互に競合します。  
  
> [!NOTE]  
>  スプリット ブレイン シナリオは、システム管理者が強制クォーラム動作を手動で実行、または非常にまれですが強制フェールオーバーを実行することで、クォーラム ノード セットが明示的に細分化された場合にのみ発生する可能性があります。  
  
 クォーラム構成を単純化し、稼働時間を増やすために、クォーラムに対するノードの投票がカウントされないように各ノードの *NodeWeight* 設定を調整することもできます。  
  
> [!IMPORTANT]  
>  NodeWeight 設定を使用するには、次の修正プログラムが WSFC クラスターのすべてのサーバーに適用されている必要があります。  
>   
>  [KB2494036](https://support.microsoft.com/kb/2494036):この修正プログラムを使用すると、[!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] および [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] でクォーラムの投票のないクラスター ノードを構成することができます。  
  
##  <a name="RecommendedAdjustmentstoQuorumVoting"></a> クォーラム投票に推奨される調整  
 特定の WSFC ノードの投票を有効または無効にする場合は、次のガイドラインに従ってください。  
  
-   **既定では、投票は行いません。** 各ノードは明白な正当性がなければ投票しないものとします。  
  
-   **すべてのプライマリ レプリカを含めます。** 可用性グループのプライマリ レプリカをホストしているか、FCI の優先所有者である各 WSFC ノードは、投票を持つ必要があります。  
  
-   **可能性のある自動フェールオーバーの所有者を含めます。** 自動可用性グループ フェールオーバーまたは FCI フェールオーバーの結果として、プライマリ レプリカをホストする可能性がある各ノードは、投票を持つ必要があります。 WSFC クラスターに可用性グループが 1 つだけあり、可用性レプリカがスタンドアロン インスタンスだけによってホストされている場合、この規則には自動フェールオーバー ターゲットであるセカンダリ レプリカだけが含まれます。  
  
-   **セカンダリ サイト ノードを除外します。** 通常は、セカンダリ ディザスター リカバリー サイトに存在する WSFC ノードには投票を提供しないでください。  プライマリ サイトに問題がない場合、セカンダリ サイト内のノードがクラスターをオフラインにするという判断に影響を与えることは避けるべきです。  
  
-   **投票数を奇数にします。** 必要に応じて、監視ファイル共有、監視ノード、または監視ディスクをクラスターに追加し、クォーラム モードを調整してクォーラム投票内の結合を防止します。  
  
-   **フェールオーバー後の投票割り当てを再評価します。** 正常なクォーラムをサポートしないクラスター構成にフェールオーバーすることは避けます。  
  
> [!IMPORTANT]
>  WSFC クォーラム投票の構成を検証するときに、以下の条件が該当する場合、AlwaysOn 可用性グループ ウィザードで警告が表示されます。  
> 
>  -   プライマリ レプリカをホストしているクラスター ノードが投票を持たない。  
> -   セカンダリ レプリカが自動フェールオーバー用に構成されており、そのクラスター ノードが投票を持たない。  
> -   可用性レプリカをホストしているすべてのクラスター ノードに[KB2494036](https://support.microsoft.com/kb/2494036) がインストールされていない。 この修正プログラムは、マルチサイト配置でのクラスター ノードに対する投票の追加または削除のために必要です。 ただし、単一サイト配置では通常は不要であり、警告を無視しても安全です。  
> 
> [!TIP]
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] WSFC クラスター構成およびノード クォーラム投票に関する設定を管理するために、いくつかのシステム動的管理ビュー (DMV) を公開しています。  
> 
>  詳細については、  [sys.dm_hadr_cluster](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-transact-sql), [sys.dm_hadr_cluster_members](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-members-transact-sql), [sys.dm_os_cluster_nodes](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-nodes-transact-sql), [sys.dm_hadr_cluster_networks](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-cluster-networks-transact-sql)を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [クラスター クォーラムの NodeWeight 設定を表示](view-cluster-quorum-nodeweight-settings.md)  
  
-   [クラスター クォーラムの NodeWeight の設定の構成](configure-cluster-quorum-nodeweight-settings.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [Microsoft SQL Server AlwaysOn ソリューション ガイド高可用性とディザスター リカバリー](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [AlwaysOn 可用性グループ ウィザードでのクォーラム投票の構成チェック](https://blogs.msdn.com/b/sqlalwayson/archive/2012/03/13/quorum-vote-configuration-check-in-alwayson-availability-group-wizards-andy-jing.aspx)  
  
-   [Windows Server テクノロジ:フェールオーバー クラスター](https://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx)  
  
-   [フェールオーバー クラスターのステップ バイ ステップ ガイド:フェールオーバー クラスターのクォーラムの構成](https://technet.microsoft.com/library/cc770620\(WS.10\).aspx)  
  
## <a name="see-also"></a>参照  
 [WSFC の強制クォーラムによる災害復旧 &#40;SQL Server&#41;](wsfc-disaster-recovery-through-forced-quorum-sql-server.md)   
 [Windows Server フェールオーバー クラスタリング &#40;WSFC&#41; と SQL Server](windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
  
