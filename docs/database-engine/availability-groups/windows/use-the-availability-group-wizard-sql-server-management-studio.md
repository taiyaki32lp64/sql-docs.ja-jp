---
title: SSMS での可用性グループの構成
description: SQL Server Management Studio (SSMS) の [新しい可用性グループ ウィザード] を使用して、Always On 可用性グループを作成および構成します。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.newagwizard.f1
- sql13.swb.newavgroupwiz.f1
helpviewer_keywords:
- New Availability Group Wizard, availability replicas
- Availability Groups [SQL Server], wizards
- Availability Groups [SQL Server], creating
ms.assetid: e1f1dccc-9e65-471d-8fd1-b45085c9484a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0b5cbbd49d331f838bd0047f259f8b5addf8de84
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74821968"
---
# <a name="use-the-availability-group-wizard-sql-server-management-studio"></a>可用性グループ ウィザードの使用 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] の**新しい可用性グループ ウィザード**を使用して、[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で Always On 可用性グループを作成および構成する方法について説明します。 *可用性グループ* は、1 つのまとまりとしてフェールオーバーする一連のユーザー データベースと、フェールオーバーをサポートする一連のフェールオーバー パートナー ( *可用性レプリカ*) を定義します。  
  
> [!NOTE]  
>  可用性グループの概要については、「 [Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)の Always On 可用性グループを PowerShell コマンドレットで作成および構成する方法について説明します。  
    
##  <a name="BeforeYouBegin"></a> はじめに  
 可用性グループを初めて作成する場合は、あらかじめこのセクションに目を通しておくことを強くお勧めします。  
  
###  <a name="Prerequisites"></a> 前提条件、制限事項、および推奨事項  

ほとんどの場合、可用性グループの作成と構成に必要なすべての作業は、新しい可用性グループ ウィザードで行うことができます。 ただし、一部手作業が必要になる場合があります。  
  
- Windows Server フェールオーバー クラスター (WSFC) クラスター タイプを使用して可用性グループをホストする場合は、可用性レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスが、同じ WSFC 内の別のクラスター サーバー (またはノード) に存在していることを確認します。 また、各サーバー インスタンスが [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] の他のすべての前提条件を満たしていることも確認します。 詳細については、「[Always On 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)」を参照することを強くお勧めします。  
  
-   可用性レプリカのホストとして選択したサーバー インスタンスがドメイン ユーザー アカウントで実行されていて、まだデータベース ミラーリング エンドポイントが存在しない場合、ウィザードでエンドポイントを作成し、サーバー インスタンスのサービス アカウントに CONNECT 権限を許可することができます。 ただし、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービスがビルトイン アカウント (Local System、Local Service、Network Service など) で実行されている場合または非ドメイン アカウントで実行されている場合は、エンドポイント認証に証明書を使用する必要があります。ウィザードは、サーバー インスタンス上でデータベース ミラーリング エンドポイントを作成できなくなります。 この場合は、データベース ミラーリング エンドポイントを手動で作成してから、新しい可用性グループ ウィザードを起動することをお勧めします。  
  
     **データベース ミラーリング エンドポイントで証明書を使用するには:**  
  
     [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-endpoint-transact-sql.md)  
  
     [データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   SQL Server フェールオーバー クラスター インスタンス (FCI) は可用性グループによる自動フェールオーバーをサポートしないため、FCI によってホストされる可用性レプリカは手動フェールオーバー用にのみ構成できます。  
  
-   **ウィザードによって初期データの完全同期を実行するための前提条件**  
  
    -   可用性グループのレプリカをホストするすべてのサーバー インスタンスで、すべてのデータベース ファイルのパスが同じである必要があります。  
  
    -   セカンダリ レプリカをホストするサーバー インスタンスにプライマリ データベース名が存在することはできません。 これは、新しいセカンダリ データベースがまだ存在しないことを意味します。  
  
    -   ウィザードでバックアップを作成し、バックアップにアクセスするために、ネットワーク共有を指定する必要があります。 プライマリ レプリカでは、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] の起動に使用するアカウントにネットワーク共有での読み取り/書き込みファイルシステム権限が必要です。 セカンダリ レプリカでは、アカウントは、ネットワーク共有に対する読み取り権限を持つ必要があります。  
  
        > [!IMPORTANT]  
        >  ログ バックアップは、ログ バックアップ チェーンの一部になります。 ログ バックアップ ファイルは適切に保存してください。  
  
     ウィザードを使用して初期データの完全同期を実行できない場合は、セカンダリ データベースを手動で準備する必要があります。 これは、ウィザードの実行前でも実行後でもかまいません。 詳細については、「 [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)、または PowerShell を使用して、AlwaysOn 可用性グループにセカンダリ データベースを参加させる方法について説明します。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 **sysadmin** 固定サーバー ロールのメンバーシップと、CREATE AVAILABILITY GROUP サーバー権限、ALTER ANY AVAILABILITY GROUP 権限、CONTROL SERVER 権限のいずれかが必要です。  
  
 また、可用性グループ ウィザードでデータベース ミラーリング エンドポイントを管理できるようにする場合は、CONTROL ON ENDPOINT 権限も必要です。  
  
##  <a name="RunAGwiz"></a> 新しい可用性グループ ウィザードの使用  
  
1.  オブジェクト エクスプローラーで、プライマリ レプリカをホストするサーバー インスタンスに接続します。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  新しい可用性グループ ウィザードを起動するには、 **[新しい可用性グループ ウィザード]** をクリックします。  
  
4.  このウィザードの初回実行時には、 **[説明]** ページが表示されます。 今後このページを省略するには、 **[次回からこのページを表示しない]** をクリックします。 このページの内容を確認してから、 **[次へ]** をクリックします。  
  
5.  **[可用性グループ オプションの指定]** ページの **[可用性グループ名]** フィールドに、新しい可用性グループの名前を入力します。 この名前は、クラスターおよびドメイン全体で一意となる有効な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 識別子であることが必要です。 可用性グループ名の最大文字数は 128 文字です。 e

6. 次に、クラスター タイプを指定します。 使用できるクラスター タイプは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] バージョンとオペレーティング システムによって異なります。 **WSFC**、**EXTERNAL**、**NONE** のいずれかを選択してください。 詳細については、「[Specify Availability Group Name Page](specify-availability-group-name-page.md)」 ([可用性グループ名の指定] ページ) を参照してください。
 
6.  **[データベースの選択]** ページのグリッドに、接続されているサーバー インスタンス上の *可用性データベース*として利用できるユーザー データベースが一覧表示されます。 新しい可用性グループに追加する 1 つまたは複数のデータベースを一覧から選択します。 これらのデータベースが初期 *プライマリ データベース*となります。  
  
     一覧の各データベースの **[サイズ]** 列には、データベースのサイズが表示されます (わかっている場合)。 **[状態]** 列は、データベースが可用性データベースとしての [前提条件](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)を満たしているかどうかを示します。 前提条件が満たされていない場合は、簡単な状態説明によって、データベースが不適格である理由が示されます (完全復旧モデルを使用していない、など)。 詳細については、状態の説明をクリックしてください。  
  
     要件を満たすようにデータベースを変更した場合は、 **[更新]** をクリックして、データベース グリッドを最新の情報に更新します。  
  
     データベースにデータベース マスター キーが含まれている場合、 **[パスワード]** 列にデータベース マスター キーのパスワードを入力します。  
  
7.  **[レプリカの指定]** ページで、新しい可用性グループの 1 つまたは複数のレプリカを指定し、構成します。 このページには、4 つのタブがあります。 次の表では、これらのタブについて説明します。 詳細については、「[[レプリカの指定] ページ &#40;新しい可用性グループウィザード: レプリカの追加ウィザード&#41;](../../../database-engine/availability-groups/windows/specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md)」のトピックを参照してください。  
  
    |タブ|簡単な説明|  
    |---------|-----------------------|  
    |**レプリカ**|このタブを使用して、セカンダリ レプリカをホストする [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の各インスタンスを指定します。 現在接続しているサーバー インスタンスでプライマリ レプリカをホストする必要があることに注意してください。|  
    |**エンドポイント**|このタブを使用して、既存の任意のデータベース ミラーリング エンドポイントを検証します。また、サービス アカウントが Windows 認証を使用しているサーバー インスタンスでエンドポイントが不足している場合は、エンドポイントを自動的に作成します。<br /><br /> 注:ドメイン以外のユーザー アカウントで実行されているサーバー インスタンスが 1 つでもある場合、ウィザードを続行するには、サーバー インスタンスに手動で変更を加える必要があります。 詳細については、このトピックの「 [前提条件](#Prerequisites)」をご覧ください。|  
    |**バックアップの設定**|このタブを使用して、可用性グループ全体についてバックアップの設定を指定し、各可用性レプリカのバックアップ優先順位を指定します。|  
    |**リスナー**|このタブを使用して、可用性グループ リスナーを作成します。 既定では、ウィザードによってリスナーは作成されません。|  
  
8.  **[最初のデータの同期を選択]** ページで、新しいセカンダリ データベースを作成して可用性グループに参加させる方法を選択します。 次のいずれかのオプションを選択します。  
  
    -   **[自動シード処理]**  
  
         グループの各データベースのセカンダリ レプリカが SQL Server で自動的に作成されます。 自動シード処理には、データとログ ファイルのパスが、グループに参加しているすべての SQL Server インスタンスで同じである必要があります。 [!INCLUDE[sssql15-md.md](../../../includes/sssql15-md.md)] 以降で使用できます。 「[AlwaysOn 可用性グループを自動的に初期化する](automatically-initialize-always-on-availability-group.md)」を参照してください。
    
    -   **[完全なデータベースとログ バックアップ]**  
  
         使用している環境が、初期データの同期を自動的に開始するための要件を満たす場合は、このオプションを選択します (詳細については、このトピックの「 [前提条件、制限事項、および推奨事項](#Prerequisites)」をご覧ください)。  
  
         **[完全]** を選択すると、可用性グループを作成後、ウィザードはすべてのプライマリ データベースとそのトランザクション ログをネットワーク共有にバックアップし、セカンダリ レプリカをホストするすべてのサーバー インスタンスでそのバックアップを復元します。 その後、ウィザードは、すべてのセカンダリ データベースを可用性グループに参加させます。  
  
         **[すべてのレプリカからアクセス可能な共有ネットワーク場所を指定]** フィールドで、レプリカをホストするサーバー インスタンスが読み取り/書き込み権限を持つバックアップ共有を指定します。 詳細については、このトピックの「 [前提条件](#Prerequisites)」をご覧ください。  検証手順で、指定されたネットワークの場所が有効であることを確認するテストが行われます。このテストにより、プライマリ レプリカにデータベースが作成されますが、その名前は "BackupLocDb_" に GUID を続ける方式で付けられます。さらに、指定されたネットワークの場所にバックアップが実行され、セカンダリ レプリカでそれが復元されます。 このデータベースがウィザードで削除できなかった場合、そのバックアップ履歴とバックアップ ファイルと共に削除しておくことをお勧めします。
  
    -   **[参加のみ]**  
  
         セカンダリ レプリカをホストするサーバー インスタンス上のセカンダリ データベースを手動で準備した場合は、このオプションを選択できます。 ウィザードは、既存のセカンダリ データベースを可用性グループに参加させます。  
  
    -   **[最初のデータの同期をスキップ]**  
  
         プライマリ データベースの独自のデータベースとログ バックアップを使用する場合は、このオプションを選択します。 詳細については、「 [AlwaysOn セカンダリ データベース上のデータ移動の開始 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)」を参照してください。  
  
9. **[検証]** ページでは、このウィザードで指定した値が、新しい可用性グループ ウィザードの要件を満たしているかどうかが確認されます。 変更が必要な場合は、 **[戻る]** をクリックして前のウィザード ページに戻り、値を変更できます。 その後、 **[次へ]** をクリックして **[検証]** ページに戻り、 **[検証の再実行]** をクリックします。  
  
10. **[概要]** ページで、新しい可用性グループに対して選択した内容を確認します。 変更が必要な場合は、 **[戻る]** をクリックして、該当するページに戻ります。 必要な変更を加えたら、 **[次へ]** をクリックして、 **[概要]** ページに戻ります。  
  
    > [!IMPORTANT]  
    >  新しい可用性レプリカをホストするサーバー インスタンスの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] サービス アカウントがログインとして存在していない場合は、新しい可用性グループ ウィザードでログインを作成する必要があります。 **[概要]** ページには、作成するログインの情報が表示されます。 **[完了]** をクリックすると、SQL Server サービス アカウントに対してこのログインが作成され、ログインに CONNECT 権限が付与されます。  
  
     選択内容に問題がなければ、 **[スクリプト]** をクリックして、ウィザードが実行する手順のスクリプトを作成することもできます。 新しい可用性グループを作成して構成するには、 **[完了]** をクリックします。  
  
11. 可用性グループの作成手順 (エンドポイントの構成、可用性グループの作成、グループへのセカンダリ レプリカの参加) の進行状況が、 **[進行状況]** ページに表示されます。  
  
12. 以上の手順が完了すると、 **[結果]** ページに各手順の結果が表示されます。 これらのすべての手順が成功した場合は、新しい可用性グループが完全に構成されます。 手順のいずれかでエラーが発生した場合は、手動で構成を完了するか、失敗した手順に対してウィザードを使用する必要があります。 特定のエラーの原因については、 **[結果]** 列の [エラー] リンクをクリックします。  
  
     ウィザードでの作業が完了したら、 **[閉じる]** をクリックして終了します。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **可用性グループの構成を完了するには**  
  
-   [可用性グループへのセカンダリ レプリカの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [可用性グループ リスナーの作成または構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **別の方法で可用性グループを作成する**  
  
-   [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [可用性グループの作成 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
-   [可用性グループの作成 &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)  
  
 **Always On 可用性グループを有効にするには**  
  
-   [AlwaysOn 可用性グループの有効化と無効化 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
 **データベース ミラーリング エンドポイントを構成するには**  
  
-   [AlwaysOn 可用性グループのデータベース ミラーリング エンドポイントの作成 &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](../../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   [可用性レプリカを追加または変更する場合のエンドポイント URL の指定 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
 **Always On 可用性グループの構成のトラブルシューティング方法**  
  
-   [AlwaysOn 可用性グループの構成のトラブルシューティング &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
-   [失敗したファイルの追加操作のトラブルシューティング &#40;AlwaysOn 可用性グループ&#41;](../../../database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   **ブログ:**  
  
     [Always On - HADRON 学習シリーズ:HADRON 対応データベースでのワーカー プールの使用](https://blogs.msdn.com/b/psssql/archive/2012/05/17/Always%20On-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases.aspx)  
  
     [SQL Server Always On チーム ブログ:SQL Server Always On チームのオフィシャル ブログ](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
     [CSS SQL Server エンジニアのブログ](https://blogs.msdn.com/b/psssql/)  
  
-   **ビデオ:**  
  
     [Microsoft SQL Server コードネーム "Denali" Always On シリーズ パート 1: 次世代高可用性ソリューションの概要](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server コードネーム "Denali" Always On シリーズ パート 2: Always On を使用したミッション クリティカルな高可用性ソリューションの構築](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **ホワイト ペーパー:**  
  
     [高可用性と災害復旧のための Microsoft SQL Server AlwaysOn ソリューション ガイド](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
     [SQL Server 2012 に関する Microsoft ホワイト ペーパー](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server ユーザー諮問チームのホワイト ペーパー](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="alternate-ways-to-create-availability-groups"></a>別の方法で可用性グループを作成する

新しい可用性グループ ウィザードの代わりに、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] や [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell コマンドレットを使用する方法もあります。 詳細については、「 [可用性グループの作成 &#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md) や [可用性グループの作成 &#40;SQL Server PowerShell&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-sql-server-powershell.md)で Always On 可用性グループを作成および構成する方法について説明します。  


## <a name="see-also"></a>参照  
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループの前提条件、制限事項、および推奨事項 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
