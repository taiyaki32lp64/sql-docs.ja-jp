---
title: '[最初のデータの同期を選択] ページ (可用性グループ ウィザード)'
description: SQL Server Management Studio (SSMS) の Always On 可用性グループ ウィザードの [最初のデータの同期を選択] ページの説明。
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.adddatabasewizard.selectinitialdatasync.f1
- sql13.swb.newagwizard.selectinitialdatasync.f1
- sql13.swb.addreplicawizard.selectinitialdatasync.f1
ms.assetid: 457b1140-4819-4def-8f7c-54a406e6db12
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e8a6a14a6efc6a9d5f96144364f1532c14b0c1c0
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75235342"
---
# <a name="select-initial-data-synchronization-page-always-on-availability-group-wizards"></a>[最初のデータの同期を選択] ページ (AlwaysOn 可用性グループ ウィザード)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  新しいセカンダリ データベースの初期データ同期のユーザー設定を指定するには、AlwaysOn の **[最初のデータの同期を選択]** ページを使用します。 このページは、[!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]、[!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)]、[!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] の 3 つのウィザードで共有されています。  
  
 選択肢には、 **[自動シード処理]** 、 **[完全なデータベースとログ バックアップ]** 、 **[参加のみ]** 、 **[最初のデータの同期をスキップ]** があります。 **[自動シード処理]** 、 **[完全]** 、 **[参加のみ]** を選択する前に、使用している環境が前提条件を満たしていることを確認してください。  
    
##  <a name="Recommendations"></a> 推奨事項  
  
-   初期データ同期の実行中は、プライマリ データベースのログ バックアップ タスクを中断します。  
  
-   大規模なデータベースでは、完全バックアップ操作と復元操作に多くの時間とリソースが必要となる場合があります。 このような場合は、セカンダリ データベースを手動で準備することをお勧めします。 詳細については、このトピックの「 [セカンダリ データベースを手動で準備するには](#PrepareSecondaryDbs)」を参照してください。  
  
-   初期データの完全同期では、ネットワーク共有を指定する必要があります。 ウィザードを使用して初期データの完全同期を実行する前に、ネットワーク共有フォルダーのアクセス権限のセキュリティ プランを実装することをお勧めします。 この対策が重要なのは、フォルダーの読み取り権限を持つ人はだれでもバックアップ ファイル内の機密情報にアクセス可能であるためです。 また、バックアップおよび復元操作を保護するために、可用性レプリカをホストする各サーバー インスタンスとネットワーク共有フォルダー間のネットワーク チャネルをセキュリティで保護することをお勧めします。  
  
     バックアップおよび復元操作を高いセキュリティで保護する必要がある場合は、 **[参加のみ]** または **[最初のデータの同期をスキップ]** オプションのどちらかを選択することをお勧めします。  
  
## <a name="Auto"></a> 自動シード処理
 
 グループの各データベースのセカンダリ レプリカが SQL Server で自動的に作成されます。 自動シード処理には、データとログ ファイルのパスが、グループに参加しているすべての SQL Server インスタンスで同じである必要があります。 [!INCLUDE[sssql15-md.md](../../../includes/sssql15-md.md)] 以降で使用できます。 「[AlwaysOn 可用性グループを自動的に初期化する](automatically-initialize-always-on-availability-group.md)」を参照してください。

##  <a name="Full"></a> 完全なデータベースとログ バックアップ 
 各プライマリ データベースに対して **[完全なデータベースとログ バックアップ]** オプションを選択すると、1 つのワークフローで、プライマリ データベースの完全バックアップとログ バックアップを作成する、セカンダリ レプリカをホストする各サーバー インスタンスでこれらのバックアップを復元して、対応するセカンダリ データベースを作成する、各セカンダリ データベースを可用性グループに参加させる、という操作を実行します。  
  
 使用している環境が、次の「初期データの完全同期を使用するための前提条件」を満たしており、ウィザードでデータ同期を自動的に開始する場合にのみ、このオプションを選択してください。  
  
 **完全なデータベースとログ バックアップの初期データ同期を使用するための前提条件**  
  
-   可用性グループのレプリカをホストするすべてのサーバー インスタンスで、すべてのデータベース ファイルのパスが同じである必要があります。  
  
    > [!NOTE]  
    >  ウィザードを実行するサーバー インスタンスとセカンダリ レプリカをホストするサーバー インスタンスで、バックアップ ファイルと復元ファイルのパスが異なる場合は、 WITH MOVE オプションを使用して、バックアップ操作と復元操作を手動で実行する必要があります。 詳細については、このトピックの「 [セカンダリ データベースを手動で準備するには](#PrepareSecondaryDbs)」を参照してください。  
  
-   セカンダリ レプリカをホストするサーバー インスタンスにプライマリ データベース名が存在することはできません。 これは、新しいセカンダリ データベースがまだ存在しないことを意味します。  
  
-   ウィザードでバックアップを作成し、バックアップにアクセスするために、ネットワーク共有を指定する必要があります。 プライマリ レプリカでは、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] の起動に使用するアカウントにネットワーク共有での読み取り/書き込みファイルシステム権限が必要です。 セカンダリ レプリカでは、アカウントは、ネットワーク共有に対する読み取り権限を持つ必要があります。  
  
    > [!IMPORTANT]  
    >  ログ バックアップは、ログ バックアップ チェーンの一部になります。 ログ バックアップ ファイルは適切に保存してください。  
  
 **前提条件を満たしていない場合**  
  
 ウィザードでは、この可用性グループのセカンダリ データベースを作成できません。 セカンダリ データベースを準備する方法については、このトピックの「 [セカンダリ データベースを手動で準備するには](#PrepareSecondaryDbs)」を参照してください。  
  
 **前提条件を満たしている場合**  
  
 前の前提条件がすべて満たされており、ウィザードで初期データの完全同期を実行する場合は、 **[完全なデータベースとログ バックアップ]** オプションを選択し、ネットワーク共有を指定します。 これにより、ウィザードによって選択した各データベースの完全バックアップとログ バックアップが作成され、指定したネットワーク共有に配置されます。 その後、新しいセカンダリ レプリカの 1 つをホストする各サーバー インスタンスで、RESTORE WITH NORECOVERY を使用してバックアップを復元することで、セカンダリ データベースが作成されます。 各セカンダリ データベースが作成された後、新しいセカンダリ データベースを可用性グループに参加させます。 セカンダリ データベースを参加させるとすぐに、データベース上でデータの同期が開始されます。  
  
 **[すべてのレプリカからアクセス可能な共有ネットワーク場所を指定]**  
 バックアップを作成および復元するには、ウィザードでネットワーク共有を指定する必要があります。 可用性レプリカをホストする各サーバー インスタンス上で [!INCLUDE[ssDE](../../../includes/ssde-md.md)] を起動するために使用されるアカウントは、ネットワーク共有での読み取り/書き込みファイルシステム権限を持つ必要があります。  
  
> [!IMPORTANT]  
>  ログ バックアップは、ログ バックアップ チェーンの一部になります。 それらのバックアップ ファイルは、適切に保存してください。  
  
##  <a name="Joinonly"></a> [参加のみ]  
 このオプションは、可用性グループのセカンダリ レプリカをホストする各サーバー インスタンス上に、新しいセカンダリ データベースが既に存在する場合にのみ選択します。 セカンダリ データベースの準備については、このセクションの「 [セカンダリ データベースを手動で準備するには](#PrepareSecondaryDbs)」を参照してください。  
  
 **[参加のみ]** を選択すると、既存の各セカンダリ データベースを可用性グループに参加させます。  
  
## <a name="Skip"></a> [最初のデータの同期をスキップ]  
 このオプションは、各プライマリ データベースのデータベースおよびログ バックアップを実行し、セカンダリ レプリカをホストする各サーバー インスタンスに復元する場合に選択します。 ウィザードの終了後、各セカンダリ レプリカのすべてのセカンダリ データベースを参加させる必要があります。  
  
> [!NOTE]  
>  詳細については、「 [AlwaysOn セカンダリ データベース上のデータ移動の開始 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)」を参照してください。  
  
##  <a name="PrepareSecondaryDbs"></a> セカンダリ データベースを手動で準備するには  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] ウィザードを使用せずにセカンダリ データベースを準備するには、次の方法のどちらかを使用できます。  
  
-   RESTORE WITH NORECOVERY を使用してプライマリ データベースの最新のデータベース バックアップを手動で復元し、その後、RESTORE WITH NORECOVERY を使用して後続のログ バックアップを復元する。 プライマリ データベースとセカンダリ データベースのファイル パスが異なる場合は、WITH MOVE オプションを使用する必要があります。 可用性グループのセカンダリ レプリカをホストする各サーバー インスタンスで、この復元シーケンスを実行します。  これらのバックアップ操作と復元操作は、 [!INCLUDE[tsql](../../../includes/tsql-md.md)] または PowerShell を使用して実行できます。  
  
     **詳細:**  
  
     [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   可用性グループに 1 つ以上のログ配布プライマリ データベースを追加する場合、対応する 1 つ以上のセカンダリ データベースをログ配布から [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]に移行できる場合があります。 詳細については、このトピックの「 [ログ配布から AlwaysOn 可用性グループへの移行の前提条件 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md)の 3 つのウィザードで共有されています。  
  
    > [!NOTE]  
    >  可用性グループのすべてのセカンダリ データベースを作成した後、セカンダリ レプリカにバックアップを実行する場合は、可用性グループの自動バックアップ設定を再構成する必要があります。  
  
     **詳細:**  
  
     [ログ配布から AlwaysOn 可用性グループへの移行の前提条件 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-migrating-log-shipping-to-always-on-availability-groups.md)  
  
     [可用性レプリカでのバックアップの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
 セカンダリ データベースの作成後、現在のすべてのログ バックアップを新しいセカンダリ データベースに適用します。  
  
 すべてのセカンダリ データベースを準備してから、ウィザードを実行することもできます。 この場合、ウィザードの **[最初のデータの同期を選択]** ページで **[参加のみ]** を選択して、準備した新しいセカンダリ データベースを可用性グループに自動的に参加させます。  
  
##  <a name="LaunchWiz"></a> 関連タスク  
  
-   [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [可用性グループへのレプリカ追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [可用性グループへのデータベース追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
-   [可用性グループのフェールオーバー ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)  
  
-   [AlwaysOn セカンダリ データベース上のデータ移動の開始 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/start-data-movement-on-an-always-on-secondary-database-sql-server.md)  
  
-   [可用性グループへのセカンダリ データベースの参加 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
-   [[新しい可用性グループ] ダイアログ ボックスの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
## <a name="see-also"></a>参照  
 [Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
