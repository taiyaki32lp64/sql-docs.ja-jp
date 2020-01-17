---
title: 可用性グループへのレプリカ追加 (SSMS)
ms.description: Add a replica to an Always On availability group using the wizard found in SQL Server Management Studio.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.addreplicawizard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], wizards
ms.assetid: 60d962b6-2af4-4394-9190-61939a102bc0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: afca5e00f95056fc201f37260088c90004ff3d1f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244981"
---
# <a name="add-a-replica-to-your-always-on-availability-group-using-the-availability-group-wizard-in-sql-server-management"></a>SQL Server Management で可用性グループ ウィザードを使用し、Always On 可用性グループにレプリカを追加する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **可用性グループへのレプリカの追加ウィザード**を使用して、既存の Always On 可用性グループに新しいセカンダリ レプリカを追加できます。  
  
> [!NOTE]  
>  [!INCLUDE[tsql](../../../includes/tsql-md.md)] または PowerShell を使用して可用性グループにセカンダリ レプリカを追加する方法については、「[可用性グループへのセカンダリ レプリカの追加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)」を参照してください。  
    
##  <a name="BeforeYouBegin"></a> はじめに  
 これまでに可用性グループに可用性レプリカを追加したことがない場合は、「 [Always On 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」の、「サーバー インスタンス」と「可用性グループとレプリカ」のセクションを参照してください。  
  
##  <a name="Prerequisites"></a> 前提条件  
  
-   現在のプライマリ レプリカをホストするサーバー インスタンスに接続されている必要があります。  
  
-   セカンダリ レプリカを追加する前に、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のホスト インスタンスが、既存のレプリカとして同じ Windows Server フェールオーバー クラスター (WSFC) にあり、さらに、異なるクラスター ノードにあることを確認します。 また、このサーバー インスタンスが [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の他のすべての前提条件を満たしていることも確認します。 詳細については、「 [Always On 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)の構成に関する一般的な問題のトラブルシューティングに役立つ情報を提供します。  
  
-   可用性レプリカのホストとして選択したサーバー インスタンスがドメイン ユーザー アカウントで実行されていて、まだデータベース ミラーリング エンドポイントが存在しない場合、ウィザードでエンドポイントを作成し、サーバー インスタンスのサービス アカウントに CONNECT 権限を許可することができます。 ただし、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスがビルトイン アカウント (Local System、Local Service、Network Service など) で実行されている場合または非ドメイン アカウントで実行されている場合は、エンドポイント認証に証明書を使用する必要があります。ウィザードは、サーバー インスタンス上でデータベース ミラーリング エンドポイントを作成できなくなります。 この場合は、データベース ミラーリング エンドポイントを手動で作成してから、可用性グループへのレプリカ追加ウィザードを起動することをお勧めします。  
  
     **データベース ミラーリング エンドポイントで証明書を使用するには:**  
  
     [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-endpoint-transact-sql.md)  
  
     [データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   **初期データの完全同期を使用するための前提条件**  
  
    -   可用性グループのレプリカをホストするすべてのサーバー インスタンスで、すべてのデータベース ファイルのパスが同じである必要があります。  
  
    -   セカンダリ レプリカをホストするサーバー インスタンスにプライマリ データベース名が存在することはできません。 これは、新しいセカンダリ データベースがまだ存在しないことを意味します。  
  
    -   ウィザードでバックアップを作成し、バックアップにアクセスするために、ネットワーク共有を指定する必要があります。 プライマリ レプリカでは、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] の起動に使用するアカウントにネットワーク共有での読み取り/書き込みファイルシステム権限が必要です。 セカンダリ レプリカでは、アカウントは、ネットワーク共有に対する読み取り権限を持つ必要があります。  
  
     ウィザードを使用して初期データの完全同期を実行できない場合は、セカンダリ データベースを手動で準備する必要があります。 これは、ウィザードの実行前でも実行後でもかまいません。 詳細については、「 [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)、または PowerShell を使用して、AlwaysOn 可用性グループにセカンダリ データベースを参加させる方法について説明します。  
   
## <a name="Permissions"></a> Permissions  
 可用性グループの ALTER AVAILABILITY GROUP 権限、CONTROL AVAILABILITY GROUP 権限、ALTER ANY AVAILABILITY GROUP 権限、または CONTROL SERVER 権限が必要です。  
  
 また、可用性グループへのレプリカ追加ウィザードでデータベース ミラーリング エンドポイントを管理できるようにする場合は、CONTROL ON ENDPOINT 権限も必要です。  
  
##  <a name="SSMSProcedure"></a> 可用性グループへのレプリカ追加ウィザードの使用 (SQL Server Management Studio)  
 **可用性グループへのレプリカ追加ウィザードを使用するには**  
  
1.  オブジェクト エクスプローラーで、可用性グループのプライマリ レプリカをホストするサーバー インスタンスに接続し、サーバー ツリーを展開します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  セカンダリ レプリカを追加する可用性グループを右クリックし、 **[レプリカの追加]** をクリックします。 可用性グループへのレプリカ追加ウィザードが起動します。  
  
4.  **[既存のセカンダリ レプリカへの接続]** ページで、可用性グループのすべてのセカンダリ レプリカに接続します。 詳細については、「[既存のセカンダリ レプリカ ページへの接続 &#40;レプリカの追加ウィザード:データベース追加ウィザード&#41;](../../../database-engine/availability-groups/windows/connect-to-existing-secondary-replicas-page.md)」を参照してください。  
  
5.  **[レプリカの指定]** ページで、可用性グループの 1 つまたは複数の新しいセカンダリ レプリカを指定し、構成します。 このページには、3 つのタブがあります。 次の表では、これらのタブについて説明します。 詳細については、「[[レプリカの指定] ページ &#40;新しい可用性グループウィザード/レプリカの追加ウィザード&#41;](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md)」を参照してください。  
  
    |タブ|簡単な説明|  
    |---------|-----------------------|  
    |**レプリカ**|このタブを使用して、新しいセカンダリ レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の各インスタンスを指定します。|  
    |**エンドポイント**|このタブを使用して、新しいセカンダリ レプリカに対する既存のデータベース ミラーリング エンドポイントを検証します (存在する場合)。 サービス アカウントが Windows 認証を使用しているサーバー インスタンスでエンドポイントが不足している場合、ウィザードは、エンドポイントの自動作成を試行します。<br /><br /> <br /><br /> 注:ドメイン以外のユーザー アカウントで実行されているサーバー インスタンスが 1 つでもある場合、ウィザードを続行するには、サーバー インスタンスに手動で変更を加える必要があります。 詳細については、このトピックの「 [前提条件](#Prerequisites)」をご覧ください。|  
    |**バックアップの設定**|このタブを使用して、可用性グループ全体のバックアップ設定を指定し (現在の設定を変更する場合)、各可用性レプリカのバックアップの優先順位を指定します。|  
  
6.  選択したレプリカにデータベース マスター キーを保有しているデータベースが含まれている場合は、そのデータベース マスター キーのパスワードを **[パスワード]** 列に入力します。 **[状態]** 列には、データベース マスター キーを保有しているデータベースに **パスワードが必要** であることが示されます。 **[パスワード]** 列に正しいパスワードが入力されるまで、 **[次へ]** は淡色表示されます。 パスワードを入力したら、 **[更新]** をクリックします。 パスワードを正しく入力した場合、[状態] 列に **[パスワードが入力されました]** が表示され、 **[次へ]** が有効になります。  
  
7.  **[最初のデータの同期を選択]** ページで、新しいセカンダリ データベースを作成して可用性グループに参加させる方法を選択します。 次のいずれかのオプションを選択します。  
  
    -   **完全**  
  
         使用している環境が、初期データの同期を自動的に開始するための要件を満たす場合は、このオプションを選択します (詳細については、このトピックの「 [前提条件、制限事項、および推奨事項](#Prerequisites)」をご覧ください)。  
  
         **[完全]** を選択すると、可用性グループを作成後、ウィザードはすべてのプライマリ データベースとそのトランザクション ログをネットワーク共有にバックアップし、新しいセカンダリ レプリカをホストするすべてのサーバー インスタンスでそのバックアップを復元します。 その後、ウィザードは、すべての新しいセカンダリ データベースを可用性グループに参加させます。  
  
         **[すべてのレプリカからアクセス可能な共有ネットワーク場所を指定]** フィールドで、レプリカをホストするサーバー インスタンスが読み取り/書き込み権限を持つバックアップ共有を指定します。 ログ バックアップは、ログ バックアップ チェーンの一部になります。 ログ バックアップ ファイルは適切に保存してください。  
  
        > [!IMPORTANT]  
        >  必要なファイル システム権限については、このトピックの「 [前提条件](#Prerequisites)」を参照してください。  
  
    -   **[参加のみ]**  
  
         新しいセカンダリ レプリカをホストするサーバー インスタンス上のセカンダリ データベースを手動で準備した場合は、このオプションを選択できます。 ウィザードは、新しいセカンダリ データベースを可用性グループに参加させます。  
  
    -   **[最初のデータの同期をスキップ]**  
  
         プライマリ データベースの独自のデータベースとログ バックアップを使用する場合は、このオプションを選択します。 詳細については、「 [AlwaysOn セカンダリ データベース上のデータ移動の開始 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)」を参照してください。  
  
8.  **[検証]** ページでは、このウィザードで指定した値が、可用性グループへのレプリカ追加ウィザードの要件を満たしているかどうかが確認されます。 変更が必要な場合は、 **[戻る]** をクリックして前のウィザード ページに戻り、値を変更できます。 その後、 **[次へ]** をクリックして **[検証]** ページに戻り、 **[検証の再実行]** をクリックします。  
  
9. **[概要]** ページで、新しい可用性グループに対して選択した内容を確認します。 変更が必要な場合は、 **[戻る]** をクリックして、該当するページに戻ります。 必要な変更を加えたら、 **[次へ]** をクリックして、 **[概要]** ページに戻ります。  
  
     選択内容に問題がなければ、[スクリプト] をクリックして、ウィザードが実行する手順のスクリプトを作成することもできます。 新しい可用性グループを作成して構成するには、 **[完了]** をクリックします。  
  
10. 可用性グループの作成手順 (エンドポイントの構成、可用性グループの作成、グループへのセカンダリ レプリカの参加) の進行状況が、 **[進行状況]** ページに表示されます。  
  
11. 以上の手順が完了すると、 **[結果]** ページに各手順の結果が表示されます。 これらのすべての手順が成功した場合は、新しい可用性グループが完全に構成されます。 手順のいずれかでエラーが発生した場合は、手動で構成を完了する必要があります。 特定のエラーの原因については、 **[結果]** 列の [エラー] リンクをクリックします。  
  
     ウィザードでの作業が完了したら、 **[閉じる]** をクリックして終了します。  
  
> [!IMPORTANT]  
>  レプリカ追加後の操作については、「[可用性グループへのセカンダリ レプリカの追加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)」の「補足情報: レプリカの追加後」 を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [可用性グループへのセカンダリ レプリカの追加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)   
 [可用性グループへのセカンダリ レプリカの追加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
