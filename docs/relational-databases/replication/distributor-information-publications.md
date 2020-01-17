---
title: ディストリビューター情報、パブリケーション | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.Distributor.Publications.f1
- sql13.rep.monitor.Distributor.commonjobs..f1
- sql13.rep.monitor.Distributor.SubscriptionSummary.merge.f1
- sql13.rep.monitor.Distributor.SubscriptionSummary.snapshot.f1
- sql13.rep.monitor.Distributor.SubscriptionSummary.tran.f1
ms.assetid: 1f499277-7f12-42ba-8cf4-52b683434944
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 043a13a84eebe9fc1c2cac96628ce6303653e8ac
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768591"
---
# <a name="distributor-information-publications"></a>ディストリビューター情報、パブリケーション
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[パブリケーション]** タブを使用すると、左ペインで選択したディストリビューターにおけるすべてのパブリケーションに関する要約情報を取得できます。  
  
ディストリビューターによりサポートされるパブリケーションについて表示される情報には、パブリッシャーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを含む列などがあります。 それ以外は、レプリケーション モニターのパブリッシャー ビューに表示されるものと同じパブリケーション情報です。 **[パブリケーション]** タブ内の列の詳細については、「 [Publisher Information, Publications](../../relational-databases/replication/publisher-information-publications.md)」を参照してください。  

## <a name="subscription-watch-list"></a>[サブスクリプション ウォッチ リスト]

### <a name="transactional-replication"></a>トランザクション レプリケーション
  トランザクション サブスクリプションの情報にはパブリッシャーの名前が含まれます。 それ以外は、このダイアログ ボックスで提供される機能と情報はパブリッシャーのビューと同様です。 このダイアログ ボックスに関する情報については、「[Publisher Information, Subscription Watch List &#40;Transactional Publication, SQL Server 2005 and Later&#41;](../../relational-databases/replication/publisher-information-subscription-watch-list-transactional.md)」 (パブリッシャー情報、サブスクリプション ウォッチ リスト スナップショット (トランザクション パブリケーション、SQL Server 2005 以降)) を参照してください。 

### <a name="merge-replication"></a>マージ レプリケーション
  マージ パブリケーションのサブスクリプションの情報にはパブリッシャーの名前が含まれます。 それ以外は、このダイアログ ボックスで提供される機能と情報はパブリッシャーのビューと同様です。 このダイアログ ボックスに関する情報については、「[Publisher Information, Subscription Watch List &#40;Merge Publication, SQL Server 2005 and Later&#41;](../../relational-databases/replication/publisher-information-subscription-watch-list-merge-publication.md)」 (パブリッシャー情報、サブスクリプション ウォッチ リスト スナップショット (マージ パブリケーション、SQL Server 2005 以降)) を参照してください。  

### <a name="snapshot-replication"></a>スナップショット レプリケーション 
  スナップショット パブリケーションのサブスクリプションの情報にはパブリッシャーの名前が含まれます。 それ以外は、このダイアログ ボックスで提供される機能と情報はパブリッシャーのビューと同様です。 このダイアログ ボックスに関する情報については、「[Publisher Information, Subscription Watch List &#40;Snapshot Publication, SQL Server 2005 and Later&#41;](../../relational-databases/replication/publisher-information-subscription-watch-list-snapshot.md)」 (パブリッシャー情報、サブスクリプション ウォッチ リスト スナップショット (スナップショット パブリケーション、SQL Server 2005 以降)) を参照してください。  

## <a name="agents"></a>[エージェント]
**[エージェント]** タブには、パブリッシャーおよびサブスクライバーに関連するエージェントおよびメンテナンス ジョブに関する詳細情報が表示されます。  
  
 ディストリビューター ビューのディストリビューターの **[エージェント]** タブで利用可能なエージェントには、パブリッシャーの **[エージェント]** タブで利用可能なすべてのエージェントが含まれています。 ただし、ディストリビューター ビューのディストリビューターの **[エージェント]** タブには、ディストリビューター エージェントおよびマージ エージェントも含まれています。  
  
 スナップショット エージェント、ログ リーダー エージェント、キュー リーダー エージェント、およびメンテナンス ジョブの詳細については、「 [Publisher Information, Agents](../../relational-databases/replication/publisher-information-agents.md)」を参照してください。 ディストリビューターの **[エージェント]** タブでエージェント情報を表示する場合は、スナップショット エージェントおよびログ リーダー エージェントのパブリッシャー情報があることに注意してください ただし、ディストリビューター ビューのディストリビューターの **[エージェント]** タブでは、 **[ディストリビューター エージェント]** および **[マージ エージェント]** も選択できます。  
  
### <a name="options"></a>オプション  
 この後のセクションでは、このタブで表示されるディストリビューター エージェントおよびマージ エージェントのデータについて説明します。  
  
### <a name="distributor-agent"></a>[ディストリビューター エージェント]  
 **ステータス**  
 エージェントの状態です。 表示される状態の種類を、次に示します。  
  
-   Error    
-   [再試行]    
-   実行中    
-   停止中   
-   [一度も開始していない]  
  
 **パブリッシャー**  
 パブリッシャーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスです。  
  
 **パブリケーション**  
 エージェントが関連付けられているパブリケーションの名前です。  
  
 **サブスクリプション**  
 [*SubscriberName*].[*Database*] という形式のサブスクリプションの名前です。  
  
 **型**  
 レプリケーションの種類 (プッシュ、プル、または匿名) です。  
  
 **[前回の開始時刻]**  
 前回のエージェントの開始時刻です。  
  
 **Duration**  
 エージェントが実行された時間の長さです。 この時間は、エージェントが現在実行中の場合は経過時間、エージェントが以前に実行されている場合は合計時間を表します。  
  
 **[最後のアクション]**  
 エージェントが最後に実行されたときに最後に実行されたアクションです。  
  
 **[配信率]**  
 エージェントが最後に実行されたときにディストリビューション データベースで初期化コマンドがコミットされた頻度 (1 秒あたりのコマンド数) です。  
  
 **[待機時間]**  
 パブリケーション データベースで最新の変更がコミットされてから、ディストリビューション データベースで対応するコマンドがコミットされるまでに経過した時間 (秒単位) です。  
  
 **[#Trans]**  
 エージェントが最後に実行されたときにディストリビューション データベースでコミットされたトランザクションの数です。  
  
 **[#Cmds]**  
 エージェントが最後に実行されたときにディストリビューション データベースでコミットされたコマンドの数です。 更新などのデータ変更がコマンドに相当します。  
  
 **[コマンド数の平均]**  
 エージェントが最後に実行されたときの 1 トランザクションあたりの平均コマンド数です。  
  
### <a name="merge-agent"></a>[マージ エージェント]  
 **ステータス**  
 エージェントの状態です。 表示される状態の種類を、次に示します。  
  
-   Error  
  
-   [再試行]  
  
-   実行中  
  
-   停止中  
  
-   [一度も開始していない]  
  
 **パブリッシャー**  
 パブリッシャーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスです。  
  
 **パブリケーション**  
 エージェントが関連付けられているパブリケーションの名前です。  
  
 **サブスクリプション**  
 [*SubscriberName*].[*Database*] という形式のサブスクリプションの名前です。  
  
 **型**  
 レプリケーションの種類 (プッシュ、プル、または匿名) です。  
  
 **[前回の開始時刻]**  
 前回のエージェントの開始時刻です。  
  
 **Duration**  
 エージェントが実行された時間の長さです。 この時間は、エージェントが現在実行中の場合は経過時間、エージェントが以前に実行されている場合は合計時間を表します。  
  
 **[最後のアクション]**  
 エージェントが最後に実行されたときに最後に実行されたアクションです。  
  
 **[配信率]**  
 ディストリビューション データベースで変更がコミットされた頻度 (1 秒あたりのコマンド数) です。  
  
 **[パブリッシャーの挿入]**  
 パブリッシャー側で適用される INSERT コマンドの数です。  
  
 **[パブリッシャーの更新]**  
 パブリッシャー側で適用される UPDATE コマンドの数です。  
  
 **[パブリッシャーの削除]**  
 パブリッシャー側で適用される DELETE コマンドの数です。  
  
 **[パブリッシャーの競合]**  
 マージ プロセス中にパブリッシャー側で発生した競合の数です。  
  
 **[サブスクライバーの挿入]**  
 サブスクライバー側で適用される INSERT コマンドの数です。  
  
 **[サブスクライバーの更新]**  
 サブスクライバー側で適用される UPDATE コマンドの数です。  
  
 **[サブスクライバーの削除]**  
 サブスクライバー側で適用される DELETE コマンドの数です。  
  
 **[サブスクライバーの競合]**  
 マージ プロセス中にサブスクライバー側で発生した競合の数です。  

  
## <a name="see-also"></a>参照  
 [レプリケーション モニターの開始](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [レプリケーションの監視](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md)  
  
  
