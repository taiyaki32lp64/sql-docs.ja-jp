---
title: WSFC の強制クォーラムによる災害復旧 (SQL Server) | Microsoft Docs
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
ms.assetid: 6cefdc18-899e-410c-9ae4-d6080f724046
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3c170fa1b302ccd0a1edec156b3b30429fc2daf8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224629"
---
# <a name="wsfc-disaster-recovery-through-forced-quorum-sql-server"></a>WSFC の強制クォーラムによる災害復旧 (SQL Server)
  クォーラム障害は、通常、システム障害、永続的な通信障害、または WSFC クラスター内の複数のノードにおける不適切な構成が原因で発生します。  クォーラム障害からの復旧には、手動による介入が必要になります。  
  
-   **開始前の準備:** [前提条件](#Prerequisites)、[セキュリティ](#Security)  
  
-   **WSFC の強制クォーラムの手順による災害復旧** [WSFC の強制クォーラムの手順による災害復旧](#Main)  
  
-   [関連タスク](#RelatedTasks)  
  
-   [関連コンテンツ](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a> 開始前の準備  
  
###  <a name="Prerequisites"></a> 前提条件  
 強制クォーラムの手順では、クォーラム障害の発生前に、正常なクォーラムが存在していたことを前提としています。  
  
> [!WARNING]  
>  ユーザーは、Windows Server フェールオーバー クラスタリング、WSFC クォーラム モデル、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、および環境に固有の配置構成の概念および操作に関する十分な知識を持っている必要があります。  
>   
>  詳細については、以下をご覧ください。[Windows Server のフェールオーバー クラスタ リング (WSFC) を SQL Server](https://msdn.microsoft.com/library/hh270278\(v=SQL.110\).aspx)、 [WSFC クォーラム モードと投票の構成 (SQL Server)](https://msdn.microsoft.com/library/hh270280\(v=SQL.110\).aspx)  
  
###  <a name="Security"></a> セキュリティ  
 ユーザーは、WSFC クラスターの各ノードのローカル Administrators グループのメンバーであるドメイン アカウントを使用する必要があります。  
  
##  <a name="Main"></a> WSFC の強制クォーラムの手順による災害復旧  
 クォーラム障害が発生すると、クラスターの構成どおりにノード レベルのフォールト トレランスを確保できなくなるため、WSFC クラスター内のクラスター化されているサービス、SQL Server インスタンス、および [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]がすべてオフラインになります。  クォーラム障害は、WSFC クラスター内の正常な投票ノードがクォーラム モデルを満たさなくなったことを意味します。 ノードによって、まったく機能しなくなるものもあれば、WSFC サービスがシャットダウンしただけで、クォーラムと通信できなくなったことを除けば正常なものもあります。  
  
 WSFC クラスターをオンラインに戻すには、既存の構成でクォーラム障害の根本的な原因を解決し、影響を受けたデータベースを必要に応じて復元する必要があります。また、稼働しているクラスター トポロジを反映させるために、WSFC クラスター内の残りのノードの再構成が必要になることもあります。  
  
 WSFC クラスター ノードで *強制クォーラム* の手順を使用して、クラスターをオフラインにした安全管理をオーバーライドすることができます。  これにより、クラスターでのクォーラム投票のチェックが実質的に中断され、クラスター内の任意のノードで WSFC クラスター リソースと SQL Server をオンラインに戻すことができます。  
  
 この種のディザスター リカバリー プロセスの手順を次に示します。  
  
#### <a name="to-recover-from-quorum-failure"></a>クォーラム障害から復旧するには:  
  
1.  **障害の範囲を特定します。** 応答しない可用性グループや SQL Server インスタンス、災害後に使用できるオンラインのクラスター ノードをそれぞれ特定し、Windows イベント ログと SQL Server システム ログを確認します。  必要に応じて、後で分析できるように解析データやシステム ログを保存しておきます。  
  
    > [!TIP]  
    >  応答している [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]インスタンスで、 [sys.dm_hadr_availability_group_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql) 動的管理ビュー (DMV) クエリを実行して、ローカル サーバー インスタンスに可用性レプリカを保持している可用性グループの正常性に関する情報を取得できます。  
  
2.  **1 つのノードで強制クォーラムを使用して WSFC クラスターを起動します。** WSFC クラスター サービスがシャットダウンしたもの以外で、コンポーネントの障害が最も少ないノードを特定し、  そのノードが他の大半のノードと通信できることを確認します。  
  
     このノードで、強制クォーラムの手順に従って、クラスターを手動で強制的にオンラインにします。  データ損失の可能性を最小限に抑えるには、可用性グループのプライマリ レプリカを最後にホストしていたノードを選択します。  
  
     詳細については、以下をご覧ください。[クォーラムを使用せずに WSFC クラスターを強制的に起動する](https://msdn.microsoft.com/library/hh270275\(v=SQL.110\).aspx)  
  
    > [!NOTE]  
    >  強制クォーラムの設定はクラスター全体に影響します。論理的 WSFC クラスターの投票が過半数に達し、通常のクォーラム モードの動作に自動的に切り替わるまで、クラスター全体のクォーラムのチェックがブロックされます。  
  
3.  **他の正常な各ノードで、一度に 1 つずつ、通常の方法で WSFC サービスを起動します。** 他のノードでクラスター サービスを起動するときは、強制クォーラム オプションを指定する必要はありません。  
  
     各ノードの WSFC サービスがオンラインに戻ると、他の正常なノードとの間でネゴシエーションが行われ、新しいクラスター構成の状態が同期されます。  この手順は、クラスターの最新の状態を解決するときに競合状態が発生するのを回避するために、必ず一度に 1 つのノードで行うようにしてください。  
  
    > [!WARNING]  
    >  起動した各ノードが新たにオンラインにした他のノードと通信できることを確認します。  他のノードでは WSFC サービスを無効にすることを検討してください。  そうしないと、クォーラム ノード セットが複数作成される可能性があります。これをスプリット ブレイン シナリオと呼びます。 手順 1. の結果に問題がなければ、この現象は発生しません。  
  
4.  **新しいクォーラム モードとノードの投票の構成を適用します。** クォーラムを強制することによってクラスターのすべてのノードが正常に再起動し、クォーラムのエラーの根本原因が修正された場合、元のクォーラム モードとノードの投票の構成に対する変更は必要ありません。  
  
     それ以外の場合は、新たに復元されたクラスター ノードと可用性レプリカ トポロジを評価し、必要に応じて各ノードのクォーラム モードと投票割り当てを変更します。 復元されていないノードについては、オフラインにするか、ノードの投票を 0 に設定する必要があります。  
  
    > [!TIP]  
    >  この時点で、クラスター内のノードと SQL Server インスタンスが通常の動作に戻っているように見えることがありますが、  正常なクォーラムはまだ存在しない可能性があります。  フェールオーバー クラスター マネージャー、SQL Server Management Studio の AlwaysOn ダッシュボード、または適切な DMV を使用して、クォーラムが復元されたことを確認してください。  
  
5.  **必要に応じて、可用性グループのデータベース レプリカを復旧します。** 可用性グループ以外のデータベースは、SQL Server の通常の起動処理の一環として個別に復旧されてオンラインに戻ります。  
  
     データ損失の可能性や可用性グループ レプリカの復旧時間を最小限に抑えるには、プライマリ レプリカ、同期セカンダリ レプリカ、非同期セカンダリ レプリカの順にオンラインに戻します。  
  
6.  **障害が発生したコンポーネントを修復するか交換し、クラスターを再検証します。** 最初の災害およびクォーラム障害から復旧したので、障害が発生したノードを修復するか交換し、WSFC と AlwaysOn の関連する構成を適切に調整する必要があります。  これには、可用性グループ レプリカの削除、クラスターからのノードの削除、ノードへのソフトウェアの再インストールなどが含まれます。  
  
     停止したすべての可用性レプリカを修復または削除する必要があります。  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、可用性レプリカよりもはるかに前の認識されている最後の時点からトランザクション ログが切り捨てられません。   可用性グループから停止したレプリカを修復または削除しないと、トランザクション ログが大きくなり、他のレプリカのトランザクション ログの領域が不足する可能性があります。  
  
    > [!NOTE]  
    >  WSFC クラスターに可用性グループ リスナーが存在するときに、WSFC の構成の検証ウィザードを実行すると、次のような誤った警告メッセージが生成されます。  
    >   
    >  "ネットワーク名 'Name:<network_name>' の RegisterAllProviderIP プロパティは 1 に設定されています。現在のクラスター構成の場合、この値は 0 に設定する必要があります。"  
    >   
    >  このメッセージは無視してください。  
  
7.  **必要に応じて手順 4. を繰り返します。** この目的は、正常な動作に対する適切なレベルのフォールト トレランスと高可用性を再確立することです。  
  
8.  **RPO/RTO 分析を実行します。** SQL Server システム ログ、データベースのタイムスタンプ、および Windows イベント ログを分析して、障害の根本的な原因を特定し、実際の復旧ポイントと復旧時間を文書化します。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [クォーラムを使用せずに WSFC クラスターを強制的に起動する](force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
-   [可用性グループの強制手動フェールオーバーの実行 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [クラスター クォーラムの NodeWeight 設定を表示](view-cluster-quorum-nodeweight-settings.md)  
  
-   [クラスター クォーラムの NodeWeight の設定の構成](configure-cluster-quorum-nodeweight-settings.md)  
  
-   [AlwaysOn ダッシュボードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md) 
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [フェールオーバー クラスターのイベントおよびログを表示する](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Get-ClusterLog フェールオーバー クラスター コマンドレット](https://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>参照  
 [Windows Server フェールオーバー クラスタリング &#40;WSFC&#41; と SQL Server](windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
  
