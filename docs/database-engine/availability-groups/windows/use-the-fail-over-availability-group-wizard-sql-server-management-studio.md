---
title: 可用性グループでフェールオーバーを行う
description: SQL Server Management Studio (SSMS)、Transact-SQL (T-SQL)、または SQL PowerShell を使用して Always On 可用性グループの計画的な手動フェールオーバーまたは強制手動フェールオーバーを実行する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.failoverwizard.connecttoreplicas.f1
- sql13.swb.failoverwizard.progress.f1
- sql13.swb.failoverwizard.selectnewprimary.f1
- sql13.swb.failoverwizard.f1
- sql13.swb.failoverwizard.confirmdataloss.f1
helpviewer_keywords:
- failover [SQL Server], failover
- Availability Groups [SQL Server], wizards
- Availability Groups [SQL Server], configuring
ms.assetid: 4a602584-63e4-4322-aafc-5d715b82b834
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5a98049201636bf521ae7162bd4ac0de71d74725
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74821944"
---
# <a name="use-the-fail-over-availability-group-wizard-sql-server-management-studio"></a>可用性グループのフェールオーバー ウィザードの使用 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]の [!INCLUDE[tsql](../../../includes/tsql-md.md)]、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、または PowerShell を使用して、AlwaysOn 可用性グループ上で計画的な手動フェールオーバーまたは強制手動フェールオーバー (強制フェールオーバー) を実行する方法について説明します。 可用性グループは、可用性レプリカのレベルでフェールオーバーします。 SYNCHRONIZED 状態のセカンダリ レプリカにフェールオーバーする場合は、ウィザードで計画的な手動フェールオーバー (データ損失なし) を実行します。 UNSYNCHRONIZED 状態または NOT SYNCHRONIZING 状態のセカンダリ レプリカにフェールオーバーする場合は、ウィザードで "*強制フェールオーバー*" とも呼ばれる強制手動フェールオーバー (データ損失の可能性あり) を実行します。 どちらの形式の手動フェールオーバーでも、接続先のセカンダリ レプリカはプライマリ ロールに移行します。 計画的な手動フェールオーバーでは、同時に、元のプライマリ レプリカはセカンダリ ロールに移行します。 強制フェールオーバー後は、元のプライマリ レプリカはオンラインになると、セカンダリ ロールに移行します。  

##  <a name="BeforeYouBegin"></a> はじめに  
 計画的な手動フェールオーバーを初めて実行する前に、「 [可用性グループの計画的な手動フェールオーバーの実行 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)、または PowerShell を使用して、AlwaysOn 可用性グループ上で計画的な手動フェールオーバーまたは強制手動フェールオーバー (強制フェールオーバー) を実行する方法について説明します。  
  
 強制手動フェールオーバーを初めて実行する前に、「[可用性グループの強制手動フェールオーバーの実行 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)」の「補足情報: 強制フェールオーバー後の必須タスク」セクションを参照してください。  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   フェールオーバー コマンドは、ターゲットのセカンダリ レプリカがコマンドを受け入れた直後に戻ります。 ただし、データベースの復旧は、可用性グループがフェールオーバーを完了した後に非同期で行われます。  
    
###  <a name="Prerequisites"></a> 可用性グループのフェールオーバー ウィザードを使用するための前提条件  
  
-   現在使用可能な可用性レプリカをホストするサーバー インスタンスに接続している必要があります。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **可用性グループのフェールオーバー ウィザードを使用するには**  
  
1.  オブジェクト エクスプローラーで、フェールオーバーを行う可用性グループのセカンダリ レプリカをホストするサーバー インスタンスに接続し、サーバー ツリーを展開します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  可用性グループのフェールオーバー ウィザードを起動するには、フェールオーバーを行う可用性グループを右クリックして **[フェールオーバー]** をクリックします。  
  
4.  **[説明]** ページに表示される情報は、セカンダリ レプリカが計画的フェールオーバーの対象であるかどうかによって異なります。 このページに **"この可用性グループの計画的フェールオーバーを実行します"** と表示されている場合は、データを失わずに可用性グループをフェールオーバーできます。  
  
5.  **[新しいプライマリ レプリカの選択]** ページで、新しいプライマリ レプリカになるセカンダリ レプリカ ( *フェールオーバー ターゲット*) を選択する前に、現在のプライマリ レプリカと WSFC クォーラムの状態を確認できます。 計画的な手動フェールオーバーの場合は、 **[フェールオーバーの準備]** の値が **[データ損失なし]** になっているセカンダリ レプリカを選択する必要があります。 強制フェールオーバーの場合は、すべてのフェールオーバー ターゲット候補について、この値は **[データ損失、警告 (** _#_ **)]** になります。 *#* は、特定のセカンダリ レプリカに存在する警告の数を示します。 特定のフェールオーバー ターゲットの警告を表示するには、その [フェールオーバーの準備] の値をクリックします。  
  
     詳細については、このトピックの「 [[新しいプライマリ レプリカの選択] ページ](#SelectNewPrimaryReplica)」を参照してください。  
  
6.  **[レプリカへの接続]** ページで、フェールオーバー ターゲットに接続します。 詳細については、このトピックの「 [[レプリカへの接続] ページ](#ConnectToReplica)」を参照してください。  
  
7.  強制フェールオーバーを実行する場合は、 **[データ損失の可能性の確認]** ページが表示されます。 フェールオーバーを続行するには、 **[ここをクリックしてデータ損失の可能性があるフェールオーバーを実行する]** を選択する必要があります。 詳細については、このトピックの「[[データ損失の可能性の確認] ページ](#ConfirmPotentialDataLoss)」を参照してください。  
  
8.  **[概要]** ページで、選択したセカンダリ レプリカへのフェールオーバーの影響を確認します。  
  
     選択内容に問題がなければ、 **[スクリプト]** をクリックして、ウィザードが実行する手順のスクリプトを作成することもできます。 その後、可用性グループを選択したセカンダリ レプリカにフェールオーバーするには、 **[完了]** をクリックします。  
  
9. **[進行状況]** ページに、可用性グループのフェールオーバーの進行状況が表示されます。  
  
10. フェールオーバー操作が完了すると、 **[結果]** ページに結果が表示されます。 ウィザードでの作業が完了したら、 **[閉じる]** をクリックして終了します。  
  
     詳細については、「 [[結果] ページ &#40;AlwaysOn 可用性グループ ウィザード&#41;](../../../database-engine/availability-groups/windows/results-page-always-on-availability-group-wizards.md)、または PowerShell を使用して、AlwaysOn 可用性グループ上で計画的な手動フェールオーバーまたは強制手動フェールオーバー (強制フェールオーバー) を実行する方法について説明します。  
  
11. 強制フェールオーバーの後は、「[可用性グループの強制手動フェールオーバーの実行 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)」の「補足情報: 強制フェールオーバー後」セクションを参照してください。  
  
## <a name="help-for-pages-that-are-exclusive-to-this-wizard"></a>このウィザードに固有のページのヘルプ  
 ここでは、 [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]に固有のページについて説明します。  
  
 **このセクションの内容**  
  
-   [[新しいプライマリ レプリカの選択] ページ](#SelectNewPrimaryReplica)  
  
-   [[レプリカへの接続] ページ](#ConnectToReplica)  
  
-   [[データ損失の可能性の確認] ページ](#ConfirmPotentialDataLoss)  
  
 このウィザードの他のページのヘルプは、他の AlwaysOn 可用性グループ ウィザードと共通で、個別の F1 ヘルプ トピックに記載されています。  
  
###  <a name="SelectNewPrimaryReplica"></a> Select New Primary Replica Page  
 ここでは、 **[新しいプライマリ レプリカの選択]** ページのオプションについて説明します。 このページを使用すると、可用性グループのフェールオーバー先のセカンダリ レプリカ (フェールオーバー ターゲット) を選択できます。 このレプリカは新しいプライマリ レプリカになります。  
  
#### <a name="page-options"></a>ページのオプション  
 **現在のプライマリ レプリカ**  
 オンラインの場合、現在のプライマリ レプリカの名前を表示します。  
  
 **[プライマリ レプリカの状態]**  
 オンラインの場合、現在のプライマリ レプリカの状態を表示します。  
  
 **[クォーラムの状態]**  
 クラスター タイプ WSFC の場合は、可用性レプリカのクォーラムの状態を表示します。次のいずれかになります。  
  
   |値|[説明]|  
   |-----------|-----------------|  
   |**[標準のクォーラム]**|クラスターは、標準のクォーラムを使用して起動しました。|  
   |**強制されたクォーラム**|クラスターは、強制されたクォーラムを使用して起動しました。|  
   |**[不明なクォーラム]**|クラスター クォーラムの状態が不明です。|  
   |**適用不可**|可用性レプリカをホストするノードにクォーラムがありません。|  
  
 詳細については、「[WSFC クォーラム モードと投票の構成 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)」を参照してください。  

 クラスター タイプ NONE の場合、クォーラムの状態は適用されません。

 クラスター タイプ EXTERNAL の場合、クォーラムの状態はクラスター マネージャーで管理され、SQL Server には表示されません。
  
 **[新しいプライマリ レプリカの選択]**  
 このグリッドを使用して、新しいプライマリ レプリカになるセカンダリ レプリカを選択します。 このグリッドの列は次のとおりです。  
  
 **サーバー インスタンス**  
 セカンダリ レプリカをホストするサーバー インスタンスの名前を表示します。  
  
 **可用性モード**  
 サーバー インスタンスの可用性モードを表示します。次のいずれかになります。  
  
|値|[説明]|  
|-----------|-----------------|  
|**[同期コミット]**|同期コミット モードの場合、同期コミット プライマリ レプリカは、同期コミット セカンダリ レプリカによるログ書き込みが確認されるまで待機した後で、トランザクションをコミットします。 同期コミット モードでは、特定のセカンダリ データベースがプライマリ データベースに 1 回同期されれば、コミットされたトランザクションが完全に保護されることが保証されます。|  
|**[非同期コミット]**|非同期コミット モードでは、非同期コミット セカンダリ レプリカによりログが書き込まれことが確認されるまで待機せずに、プライマリ レプリカがトランザクションをコミットします。 非同期コミット モードでは、セカンダリ データベースでのトランザクションの遅延が最小になりますが、セカンダリ データベースがプライマリ データベースよりも遅延する場合があるため、一部のデータが失われる可能性があります。|  
  
 詳細については、「[可用性モード &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)」を参照してください。  
  
 **フェールオーバー モード**  
 サーバー インスタンスのフェールオーバー モードを表示します。次のいずれかになります。  
  
|値|[説明]|  
|-----------|-----------------|  
|**自動**|自動フェールオーバー用に構成されているセカンダリ レプリカでは、そのセカンダリ レプリカがプライマリ レプリカと同期されている場合は計画的な手動フェールオーバーもサポートされます。|  
|**手動**|手動フェールオーバーには、計画的 (データ損失なし) および強制 (データ損失の可能性あり) の 2 種類があります。 特定のセカンダリ レプリカでサポートされる手動フェールオーバーはどちらか 1 つだけで、このサポートは可用性モードによって異なり、同期コミット モードのサポートはセカンダリ レプリカの同期状態によって決まります。 特定のセカンダリ レプリカで現在サポートされている手動フェールオーバーの形式を調べるには、このグリッドの **[フェールオーバーの準備]** 列を参照してください。|  
  
 詳細については、「 [フェールオーバーとフェールオーバー モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)、または PowerShell を使用して、AlwaysOn 可用性グループ上で計画的な手動フェールオーバーまたは強制手動フェールオーバー (強制フェールオーバー) を実行する方法について説明します。  
  
 **[フェールオーバーの準備]**  
 セカンダリ レプリカのフェールオーバーの準備を表示します。次のいずれかになります。  
  
|値|[説明]|  
|-----------|-----------------|  
|**[データ損失なし]**|このセカンダリ レプリカでは現在、計画的フェールオーバーがサポートされています。 この値は、同期コミット モードのセカンダリ レプリカが現在、プライマリ レプリカと同期されている場合にのみ表示されます。|  
|**[データ損失、警告 (** _#_ **)]**|このセカンダリ レプリカでは現在、強制フェールオーバー (データ損失の可能性あり) がサポートされています。 この値は、セカンダリ レプリカがプライマリ レプリカと同期されていない場合に表示されます。 データ損失の警告リンクをクリックすると、データ損失の可能性に関する情報が表示されます。|  
  
 **[更新]**  
 グリッドを更新します。  
  
 **キャンセル**  
 ウィザードをキャンセルします。 **[新しいプライマリ レプリカの選択]** ページでウィザードをキャンセルすると、何もアクションを実行せずに終了します。  
  
###  <a name="ConfirmPotentialDataLoss"></a> Confirm Potential Data Loss Page  
 ここでは、強制フェールオーバーを実行する場合にのみ表示される **[データ損失の可能性の確認]** ページのオプションについて説明します。 このトピックの対象は、 [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]だけです。 このページを使用すると、可用性グループを強制的にフェールオーバーするためにデータの損失を許容できるかどうかを指定できます。  
  
#### <a name="confirm-potential-data-loss-options"></a>[データ損失の可能性の確認] のオプション  
 選択したセカンダリ レプリカがプライマリ レプリカと同期されていない場合は、このセカンダリ レプリカにフェールオーバーすると 1 つ以上のデータベースのデータが失われる可能性があるという警告が表示されます。  
  
 **[ここをクリックしてデータ損失の可能性があるフェールオーバーを実行する。]**  
 ユーザーがこの可用性グループのデータベースを使用できるようにするためにデータの損失を許容できる場合は、このチェック ボックスをオンにします。 データの損失を許容できない場合は、 **[戻る]** をクリックして **[新しいプライマリ レプリカの選択]** ページに戻るか、 **[キャンセル]** をクリックして可用性グループをフェールオーバーせずにウィザードを終了することができます。  
  
 **キャンセル**  
 ウィザードをキャンセルします。 **[データ損失の可能性の確認]** ページでウィザードをキャンセルすると、何もアクションを実行せずに終了します。  
  
###  <a name="ConnectToReplica"></a> Connect to Replica Page  
 ここでは、 **の** [レプリカへの接続] [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]ページのオプションについて説明します。 このページは、ターゲット セカンダリ レプリカに接続していない場合にのみ表示されます。 このページを使用すると、新しいプライマリ レプリカとして選択したセカンダリ レプリカに接続できます。  
  
#### <a name="page-options"></a>ページのオプション  
 **グリッド列:**  
 **サーバー インスタンス**  
 可用性レプリカをホストするサーバー インスタンスの名前を表示します。  
  
 **接続ユーザー**  
 接続が確立されると、サーバー インスタンスに接続されるアカウントを表示します。 この列で、特定のサーバー インスタンスについて **"未接続"** と表示される場合、 **[接続]** ボタンをクリックする必要があります。  
  
 **のインスタンスに接続するときには、**  
 このサーバー インスタンスが、接続する他のサーバー インスタンスとは異なるアカウントで実行されている場合にクリックします。  
  
 **キャンセル**  
 ウィザードをキャンセルします。 **[レプリカへの接続]** ページでウィザードをキャンセルすると、何もアクションを実行せずに終了します。  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [可用性モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [フェールオーバーとフェールオーバー モード &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)   
 [可用性グループの計画的な手動フェールオーバーの実行 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)   
 [可用性グループの強制手動フェールオーバーの実行 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)   
 [WSFC の強制クォーラムによる災害復旧 &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
