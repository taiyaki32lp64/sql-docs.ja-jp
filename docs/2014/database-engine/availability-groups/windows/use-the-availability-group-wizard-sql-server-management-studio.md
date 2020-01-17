---
title: 可用性グループ ウィザードの使用 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.newagwizard.f1
- sql12.swb.newavgroupwiz.f1
helpviewer_keywords:
- New Availability Group Wizard, availability replicas
- Availability Groups [SQL Server], wizards
- Availability Groups [SQL Server], creating
ms.assetid: e1f1dccc-9e65-471d-8fd1-b45085c9484a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70227f556ae268144549616dab0895e70ff39de8
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228739"
---
# <a name="use-the-availability-group-wizard-sql-server-management-studio"></a>可用性グループ ウィザードの使用 (SQL Server Management Studio)
  このトピックでは、"新しい可用性グループ" ウィザード ( [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]) を使用して、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]で AlwaysOn 可用性グループを作成および構成する方法について説明します。 
  *可用性グループ* は、1 つのまとまりとしてフェールオーバーする一連のユーザー データベースと、フェールオーバーをサポートする一連のフェールオーバー パートナー ( *可用性レプリカ*) を定義します。  
  
> [!NOTE]  
>  可用性グループの概要については、「[AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)」を参照してください。  
  
-   **作業を開始する準備:**  
  
     [前提条件、制限事項、および推奨事項](#PrerequisitesRestrictions)  
  
     [保護](#Security)  
  
-   **可用性グループを作成および構成するには、**[新しい可用性グループウィザード (SQL Server Management Studio)](#RunAGwiz)を使用します。    
  
> [!NOTE]  
>  新しい可用性グループ ウィザードの代わりに、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] や [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell コマンドレットを使用する方法もあります。 詳細については、「 [可用性グループの作成 &#40;Transact-SQL&#41;](create-an-availability-group-transact-sql.md) や [可用性グループの作成 &#40;SQL Server PowerShell&#41;](../../../powershell/sql-server-powershell.md)で Always On 可用性グループを作成および構成する方法について説明します。  
  
##  <a name="BeforeYouBegin"></a>開始する前に  
 可用性グループを初めて作成する場合は、あらかじめこのセクションに目を通しておくことを強くお勧めします。  
  
###  <a name="PrerequisitesRestrictions"></a>前提条件、制限事項、および推奨事項  
 ほとんどの場合、可用性グループの作成と構成に必要なすべての作業は、新しい可用性グループ ウィザードで行うことができます。 ただし、一部手作業が必要になる場合があります。  
  
-   可用性グループを作成する前に、可用性レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスが同じ Windows Server フェールオーバー クラスタリング (WSFC) フェールオーバー クラスター内の別の WSFC ノードに存在していることを確認します。 また、各サーバー インスタンスが [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の他のすべての前提条件を満たしていることも確認します。 詳細については、「[AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)」をお読みいただくことを強くお勧めします。  
  
-   可用性レプリカのホストとして選択したサーバー インスタンスがドメイン ユーザー アカウントで実行されていて、まだデータベース ミラーリング エンドポイントが存在しない場合、ウィザードでエンドポイントを作成し、サーバー インスタンスのサービス アカウントに CONNECT 権限を許可することができます。 ただし、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスがビルトイン アカウント (Local System、Local Service、Network Service など) で実行されている場合または非ドメイン アカウントで実行されている場合は、エンドポイント認証に証明書を使用する必要があります。ウィザードは、サーバー インスタンス上でデータベース ミラーリング エンドポイントを作成できなくなります。 この場合は、データベース ミラーリング エンドポイントを手動で作成してから、新しい可用性グループ ウィザードを起動することをお勧めします。  
  
     `To use certificates for a database mirroring endpoint:`  
  
     [Transact-sql&#41;&#40;エンドポイントの作成](/sql/t-sql/statements/create-endpoint-transact-sql)  
  
     [Transact-sql&#41;&#40;データベースミラーリングエンドポイントに証明書を使用する](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   SQL Server フェールオーバー クラスター インスタンス (FCI) は可用性グループによる自動フェールオーバーをサポートしないため、FCI によってホストされる可用性レプリカは手動フェールオーバー用にのみ構成できます。  
  
-   データベースが暗号化されているか、データベース暗号化キー (DEK) を含んでいる場合、 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] または [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] を使用してそのデータベースを可用性グループに追加することはできません。 暗号化されたデータベースの暗号化を解除した場合でも、そのログ バックアップには暗号化されたデータが含まれていることがあります。 この場合、データベースに対する初期データの完全同期が失敗する可能性があります。 これは、ログの復元操作にはデータベース暗号化キー (DEK) で使用された証明書が必要なことがあり、その証明書を使用できないことがあるためです。  
  
     暗号化解除されたデータベースを、ウィザードを使用して可用性グループに追加できるようにするには、次の操作を行います。  
  
    1.  プライマリ データベースのログ バックアップを作成します。  
  
    2.  プライマリ データベースの完全バックアップを作成します。  
  
    3.  セカンダリ レプリカをホストするサーバー インスタンスでデータベース バックアップを復元します。  
  
    4.  プライマリ データベースから新しいログ バックアップを作成します。  
  
    5.  セカンダリ データベースでこのログ バックアップを復元します。  
  
-   **ウィザードで初期データの完全同期を実行するための前提条件**  
  
    -   可用性グループのレプリカをホストするすべてのサーバー インスタンスで、すべてのデータベース ファイルのパスが同じである必要があります。  
  
    -   セカンダリ レプリカをホストするサーバー インスタンスにプライマリ データベース名が存在することはできません。 これは、新しいセカンダリ データベースがまだ存在しないことを意味します。  
  
    -   ウィザードでバックアップを作成し、バックアップにアクセスするために、ネットワーク共有を指定する必要があります。 プライマリ レプリカでは、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] の起動に使用するアカウントにネットワーク共有での読み取り/書き込みファイルシステム権限が必要です。 セカンダリ レプリカでは、アカウントは、ネットワーク共有に対する読み取り権限を持つ必要があります。  
  
        > [!IMPORTANT]  
        >  ログ バックアップは、ログ バックアップ チェーンの一部になります。 ログ バックアップ ファイルは適切に保存してください。  
  
     ウィザードを使用して初期データの完全同期を実行できない場合は、セカンダリ データベースを手動で準備する必要があります。 これは、ウィザードの実行前でも実行後でもかまいません。 詳細については、「 [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)、または PowerShell を使用して、AlwaysOn 可用性グループにセカンダリ データベースを参加させる方法について説明します。  
  
###  <a name="Security"></a>保護  
  
####  <a name="Permissions"></a>許可  
 
  **sysadmin** 固定サーバー ロールのメンバーシップと、CREATE AVAILABILITY GROUP サーバー権限、ALTER ANY AVAILABILITY GROUP 権限、CONTROL SERVER 権限のいずれかが必要です。  
  
 また、可用性グループ ウィザードでデータベース ミラーリング エンドポイントを管理できるようにする場合は、CONTROL ON ENDPOINT 権限も必要です。  
  
##  <a name="RunAGwiz"></a>新しい可用性グループウィザードの使用  
  
1.  オブジェクト エクスプローラーで、プライマリ レプリカをホストするサーバー インスタンスに接続します。  
  
2.  
  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  新しい可用性グループ ウィザードを起動するには、 **[新しい可用性グループ ウィザード]** をクリックします。  
  
4.  このウィザードの初回実行時には、 **[説明]** ページが表示されます。 今後このページを省略するには、 **[次回からこのページを表示しない]** をクリックします。 このページの内容を確認してから、 **[次へ]** をクリックします。  
  
5.  
  **[可用性グループ名の指定]** ページの **[可用性グループ名]** フィールドに、新しい可用性グループの名前を入力します。 この名前は、WSFC フェールオーバー クラスターおよびドメイン全体で一意となる有効な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 識別子であることが必要です。 可用性グループ名の最大文字数は 128 文字です。  
  
6.  
  **[データベースの選択]** ページのグリッドに、接続されているサーバー インスタンス上の *可用性データベース*として利用できるユーザー データベースが一覧表示されます。 新しい可用性グループに追加する 1 つまたは複数のデータベースを一覧から選択します。 これらのデータベースが初期 *プライマリ データベース*となります。  
  
     一覧の各データベースの **[サイズ]** 列には、データベースのサイズが表示されます (わかっている場合)。 
  **[状態]** 列は、データベースが可用性データベースとしての [前提条件](prereqs-restrictions-recommendations-always-on-availability.md)を満たしているかどうかを示します。 前提条件が満たされていない場合は、簡単な状態説明によって、データベースが不適格である理由が示されます (完全復旧モデルを使用していない、など)。 詳細については、状態の説明をクリックしてください。  
  
     要件を満たすようにデータベースを変更した場合は、 **[更新]** をクリックして、データベース グリッドを最新の情報に更新します。  
  
7.  
  **[レプリカの指定]** ページで、新しい可用性グループの 1 つまたは複数のレプリカを指定し、構成します。 このページには、4 つのタブがあります。 次の表では、これらのタブについて説明します。 詳細ついては、「[[レプリカの指定] ページ &#40;新しい可用性グループウィザード/レプリカの追加ウィザード&#41;](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md)」を参照してください。  
  
    |Tab|簡単な説明|  
    |---------|-----------------------|  
    |**物**|このタブを使用して、セカンダリ レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の各インスタンスを指定します。 現在接続しているサーバー インスタンスでプライマリ レプリカをホストする必要があることに注意してください。|  
    |****|このタブを使用して、既存の任意のデータベース ミラーリング エンドポイントを検証します。また、サービス アカウントが Windows 認証を使用しているサーバー インスタンスでエンドポイントが不足している場合は、エンドポイントを自動的に作成します。 **注:** ドメイン以外のユーザーアカウントで実行されているサーバーインスタンスがある場合は、ウィザードを続行する前に、サーバーインスタンスに手動で変更を加える必要があります。 詳細については、このトピックの「 [前提条件](#PrerequisitesRestrictions)」をご覧ください。|  
    |**バックアップの設定**|このタブを使用して、可用性グループ全体についてバックアップの設定を指定し、各可用性レプリカのバックアップ優先順位を指定します。|  
    |**リスナー**|このタブを使用して、可用性グループ リスナーを作成します。 既定では、ウィザードによってリスナーは作成されません。|  
  
8.  
  **[最初のデータの同期を選択]** ページで、新しいセカンダリ データベースを作成して可用性グループに参加させる方法を選択します。 次のいずれかのオプションを選択します。  
  
    -   **全角**  
  
         使用している環境が、初期データの同期を自動的に開始するための要件を満たす場合は、このオプションを選択します (詳細については、このトピックの「 [前提条件、制限事項、および推奨事項](#PrerequisitesRestrictions)」をご覧ください)。  
  
         
  **[完全]** を選択すると、可用性グループを作成後、ウィザードはすべてのプライマリ データベースとそのトランザクション ログをネットワーク共有にバックアップし、セカンダリ レプリカをホストするすべてのサーバー インスタンスでそのバックアップを復元します。 その後、ウィザードは、すべてのセカンダリ データベースを可用性グループに参加させます。  
  
         
  **[すべてのレプリカからアクセス可能な共有ネットワーク場所を指定]** フィールドで、レプリカをホストするサーバー インスタンスが読み取り/書き込み権限を持つバックアップ共有を指定します。 詳細については、このトピックの「 [前提条件](#PrerequisitesRestrictions)」をご覧ください。  
  
    -   **結合のみ**  
  
         セカンダリ レプリカをホストするサーバー インスタンス上のセカンダリ データベースを手動で準備した場合は、このオプションを選択できます。 ウィザードは、既存のセカンダリ データベースを可用性グループに参加させます。  
  
    -   **最初のデータの同期をスキップ**  
  
         プライマリ データベースの独自のデータベースとログ バックアップを使用する場合は、このオプションを選択します。 詳細については、「[AlwaysOn セカンダリ データベース上のデータ移動の開始 &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)」を参照してください。  
  
9. 
  **[検証]** ページでは、このウィザードで指定した値が、新しい可用性グループ ウィザードの要件を満たしているかどうかが確認されます。 変更が必要な場合は、 **[戻る]** をクリックして前のウィザード ページに戻り、値を変更できます。 その後、**[次へ]** をクリックして **[検証]** ページに戻り、**[検証の再実行]** をクリックします。  
  
10. 
  **[概要]** ページで、新しい可用性グループに対して選択した内容を確認します。 変更が必要な場合は、 **[戻る]** をクリックして、該当するページに戻ります。 必要な変更を加えたら、 **[次へ]** をクリックして、 **[概要]** ページに戻ります。  
  
    > [!IMPORTANT]  
    >  新しい可用性レプリカをホストするサーバー インスタンスの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントがログインとして存在していない場合は、新しい可用性グループ ウィザードでログインを作成する必要があります。 
  **[概要]** ページには、作成するログインの情報が表示されます。 
  **[完了]** をクリックすると、SQL Server サービス アカウントに対してこのログインが作成され、ログインに CONNECT 権限が付与されます。  
  
     選択内容に問題がなければ、 **[スクリプト]** をクリックして、ウィザードが実行する手順のスクリプトを作成することもできます。 新しい可用性グループを作成して構成するには、 **[完了]** をクリックします。  
  
11. 可用性グループの作成手順 (エンドポイントの構成、可用性グループの作成、グループへのセカンダリ レプリカの参加) の進行状況が、**[進行状況]** ページに表示されます。  
  
12. 以上の手順が完了すると、 **[結果]** ページに各手順の結果が表示されます。 これらのすべての手順が成功した場合は、新しい可用性グループが完全に構成されます。 手順のいずれかでエラーが発生した場合は、手動で構成を完了するか、失敗した手順に対してウィザードを使用する必要があります。 特定のエラーの原因については、 **[結果]** 列の [エラー] リンクをクリックします。  
  
     ウィザードでの作業が完了したら、 **[閉じる]** をクリックして終了します。  
  
##  <a name="RelatedTasks"></a>関連タスク  
 **可用性グループの構成を完了するには**  
  
-   [セカンダリレプリカを可用性グループに参加させる &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [可用性グループのセカンダリデータベースを手動で準備 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [セカンダリデータベースを可用性グループに参加させる &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [可用性グループリスナー &#40;SQL Server を作成または構成&#41;](create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **可用性グループを作成する別の方法**  
  
-   [[新しい可用性グループ] ダイアログボックスを使用すると &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Transact-sql&#41;&#40;可用性グループを作成する](create-an-availability-group-transact-sql.md)  
  
-   [可用性グループ &#40;SQL Server PowerShell を作成し&#41;](../../../powershell/sql-server-powershell.md)  
  
 **AlwaysOn 可用性グループを有効にするには**  
  
-   [AlwaysOn 可用性グループ &#40;SQL Server を有効または無効にする&#41;](enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **データベースミラーリングエンドポイントを構成するには**  
  
-   [AlwaysOn 可用性グループ &#40;SQL Server PowerShell のデータベースミラーリングエンドポイントを作成&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Windows 認証 &#40;Transact-sql&#41;のデータベースミラーリングエンドポイントを作成する](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [Transact-sql&#41;&#40;データベースミラーリングエンドポイントに証明書を使用する](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [可用性レプリカを追加または変更するときにエンドポイント URL を指定する &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **AlwaysOn 可用性グループの構成のトラブルシューティング方法**  
  
-   [SQL Server&#41;削除された AlwaysOn 可用性グループ構成 &#40;のトラブルシューティング](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [失敗したファイルの追加操作のトラブルシューティング &#40;AlwaysOn 可用性グループ&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a>関連するコンテンツ  
  
-   **Blog**  
  
     [AlwaysON - HADRON 学習シリーズ: HADRON 対応データベースのワーカー プールの使用](https://blogs.msdn.com/b/psssql/archive/2012/05/17/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server AlwaysOn チームのブログ:SQL Server AlwaysOn チームのオフィシャル ブログ](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](https://blogs.msdn.com/b/psssql/)  
  
-   **ビデオ**  
  
     [Microsoft SQL Server コード ネーム "Denali" AlwaysOn シリーズ パート 1: 次世代の高可用性ソリューションの概要](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server コードネーム "Denali" AlwaysOn シリーズ パート 2: AlwaysOn を使用したミッション クリティカルな高可用性ソリューションの構築](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **ペーパー**  
  
     [高可用性と災害復旧のための Microsoft SQL Server AlwaysOn ソリューション ガイド](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012 の Microsoft ホワイトペーパー](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server カスタマーアドバイザリチームのホワイトペーパー](http://sqlcat.com/)  
  
## <a name="see-also"></a>参照  
 [データベースミラーリングエンドポイント &#40;SQL Server&#41;](../../database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server の概要&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server の前提条件、制限事項、推奨事項&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
