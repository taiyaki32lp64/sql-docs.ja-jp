---
title: 更新可能トランザクション サブスクリプションの更新モードの切り替え | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, updatable subscriptions
- updatable subscriptions, update modes
- subscriptions [SQL Server replication], updatable
ms.assetid: ab5ebab1-7ee4-41f4-999b-b4f0c420c921
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5ee768eb4e50e4501af204c885916cd14409df2c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68210754"
---
# <a name="switch-between-update-modes-for-an-updatable-transactional-subscription"></a>更新可能トランザクション サブスクリプションの更新モードの切り替え
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、更新可能トランザクション サブスクリプションの更新モードを切り替える方法について説明します。 サブスクリプションの新規作成ウィザードを使用して、更新可能サブスクリプションのモードを指定します。 このウィザードを使用する場合のモードの設定については、「[プル サブスクリプションのプロパティの表示または変更](../view-and-modify-pull-subscription-properties.md)」を参照してください。  
  
  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   即時更新からキュー更新に、いつでもフェールオーバーできます。 ただしそれ以降、サブスクライバーとパブリッシャーが接続され、キュー リーダー エージェントによってキュー内の保留中メッセージがすべてパブリッシャーに適用されるまで、即時更新に戻すことはできません。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   トランザクション パブリケーションへの更新サブスクリプションで更新モード間のフェールオーバーがサポートされている場合、接続が短時間で変化する状況に対応するために、更新モードをプログラムで変更することができます。 更新モードはレプリケーション ストアド プロシージャを使用して、プログラムから設定することも、要求時に設定することもできます。 詳細については、「 [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)を使用して、更新可能トランザクション サブスクリプションの更新モードを切り替える方法について説明します。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
> [!NOTE]  
>  サブスクリプションを作成した後で更新モードを変更するには、 **update_mode** プロパティを **failover** (即時更新をキュー更新に切り替え) または **queued failover** (キュー更新を即時更新に切り替え) に設定する必要があります。 これらのプロパティは、サブスクリプションの新規作成ウィザードで自動的に設定されます。  
  
#### <a name="to-set-the-updating-mode-for-a-push-subscription"></a>プッシュ サブスクリプションの更新モードを設定するには  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]でサブスクライバーに接続して、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル サブスクリプション]** フォルダーを展開します。  
  
3.  更新モードを設定するサブスクリプションを右クリックしてから、 **[更新方法の設定]** をクリックします。  
  
4.  **[更新方法の設定 - \<サブスクライバー>:\<サブスクリプション データベース>]** ダイアログ ボックスで、 **[即時更新]** または **[キュー更新]** を選択します。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-set-the-updating-mode-for-a-pull-subscription"></a>プル サブスクリプションの更新モードを設定するには  
  
1.  **[サブスクリプションのプロパティ - \<パブリッシャー>:\<パブリケーション データベース>]** ダイアログ ボックスの **[サブスクライバーの更新方法]** オプションで、 **[変更をすぐにレプリケートする]** または **[変更をキューに登録]** のいずれかの値を選択します。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 **[サブスクリプションのプロパティ - \<パブリッシャー>:\<パブリケーション データベース>]** ダイアログ ボックスへのアクセスについて詳しくは、[「プル サブスクリプションのプロパティの表示または変更](../view-and-modify-pull-subscription-properties.md)」をご覧ください。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-switch-between-update-modes"></a>更新モードを切り替えるには  
  
1.  プル サブスクリプションの場合は [sp_helppullsubscription](/sql/relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql) 、プッシュ サブスクリプションの場合は [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql) を実行して、サブスクリプションでフェールオーバーがサポートされていることを確認します。 結果セットの **update mode** の値が **3** または **4**の場合、フェールオーバーがサポートされます。  
  
2.  サブスクライバー側のサブスクリプション データベースに対して、 [sp_setreplfailovermode](/sql/relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql)を実行します。 **@publisher** 、 **@publisher_db** 、 **@publication** を指定し、 **@failover_mode** に次のいずれかの値を指定します。  
  
    -   **queued** - 接続が一時的に失われた場合、キュー更新にフェールオーバーします。  
  
    -   **immediate** - 接続が回復した場合、即時更新にフェールオーバーします。  
  
## <a name="see-also"></a>関連項目  
 [Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
