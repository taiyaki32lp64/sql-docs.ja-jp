---
title: PowerPivot から SharePoint への移行 2013 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: f698ceb1-d53e-4717-a3a0-225b346760d0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f792790e6bdc8c116c629910cdd64ec9aa0e6701
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797260"
---
# <a name="migrate-powerpivot-to-sharepoint-2013"></a>SharePoint 2013 への PowerPivot の移行
  
  
 SharePoint 2013 では、インプレース アップグレードはサポートされていません。 ただし、 **データベース接続アップグレードの手順はサポートされています**。 インプレース アップグレードとデータベース アタッチ アップグレードの 2 つの基本的なアップグレード方法をユーザーが選択できた SharePoint 2010 へのアップグレードとは動作が異なります。  
  
 SharePoint 2010 と統合された [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] のインストールを使用している場合は、SharePoint サーバーのインプレース アップグレードを行うことはできません。 ただし、SharePoint 2010 ファームから SharePoint 2013 ファームにコンテンツ データベースとサービス アプリケーション データベースを移行することは可能です。 このトピックでは、データベース アタッチ アップグレードを完了し、PowerPivot に関連する移行を完了するために必要な手順の概要について説明します。  
  
 **[!INCLUDE[applies](../../../includes/applies-md.md)]**  SharePoint 2013  
  
### <a name="migration-overview"></a>移行の概要  
  
|@shouldalert|2|3|4|  
|-------|-------|-------|-------|  
|SharePoint 2013 ファームを準備する|データベースをバックアップ、コピー、および復元する|コンテンツ データベースをマウントする|[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] のスケジュールを移行する|  
||[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]|SharePoint サーバーの全体管理<br /><br /> Windows PowerShell|SharePoint アプリケーション ページ<br /><br /> Windows PowerShell|  
  
 **このトピックの内容:**  
  
-   [1) SharePoint 2013 ファームを準備する](#bkmk_prepare_sharepoint2013)  
  
-   [2) データベースをバックアップ、コピー、および復元する](#bkmk_backup_restore)  
  
-   [3) Web アプリケーションを準備して、コンテンツ データベースをマウントする](#bkmk_prepare_mount_databases)  
  
-   [4) PowerPivot のスケジュールをアップグレードする](#bkmk_upgrade_powerpivot_schedules)  
  
-   [その他のリソース](#bkmk_additional_resources)  
  
##  <a name="bkmk_prepare_sharepoint2013"></a> 1) SharePoint 2013 ファームを準備する  
  
1.  > [!TIP]  
    >  既存の Web アプリケーション用に構成されている認証方法を確認します。 SharePoint 2013 Web アプリケーションの既定値は、要求ベースの認証です。 クラシック モード認証用に構成された SharePoint 2010 Web アプリケーションでは、SharePoint 2010 から SharePoint 2013 にデータベースを移行する追加の手順が必要です。 Web アプリケーションがクラシック モード認証用に構成されている場合は、SharePoint 2013 のドキュメントを確認してください。  
  
2.  新しい SharePoint Server 2013 ファームをインストールします。  
  
3.  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] サーバーのインスタンスを SharePoint モードでインストールします。 詳しくは、「 [PowerPivot for SharePoint 2013 Installation](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)」をご覧ください。  
  
4.  SharePoint ファーム内の各サーバーで [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] 2013 のインストール パッケージ **spPowerPivot.msi** を実行します。 詳細については、「 [PowerPivot for SharePoint アドイン&#40;SharePoint 2013&#41;をインストールまたはアンインストールする](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013)」を参照してください。  
  
5.  SharePoint 2013 サーバーの全体管理で、前の手順で作成した SharePoint モードの [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] サーバーを使用するように Excel Services サービス アプリケーションを構成します。 詳細については、「 [PowerPivot for SharePoint 2013 インストール](https://docs.microsoft.com/analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode)」の「基本的な Analysis Services SharePoint 統合の構成」セクションを参照してください。  
  
##  <a name="bkmk_backup_restore"></a> 2) データベースをバックアップ、コピー、および復元する  
 "SharePoint のデータベースアタッチアップグレード" プロセスは、PowerPivot 関連のコンテンツとサービスアプリケーションデータベースを SharePoint 2013 ファームにバックアップ、コピー、および復元する一連の手順です。  
  
1.  **データベースを読み取り専用に設定する** : [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で、データベース名を右クリックし、 **[プロパティ]** をクリックします。 **[オプション]** ページで、 **[読み取り専用データベース]** プロパティを **[True]** に設定します。  
  
2.  **バックアップする** : SharePoint 2013 ファームに移行する各コンテンツ データベースとサービス アプリケーション データベースをバックアップします。 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で、データベース名を右クリックし、 **[タスク]** 、 **[バックアップ]** を順にクリックします。  
  
3.  データベース バックアップ ファイル (.bak) をバックアップ先サーバーにファイル コピーします。  
  
4.  **復元する** : データベースを復元先の [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]に復元します。 この手順は、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]を使用して行うことができます。  
  
5.  **データベースを読み取り/書き込み用に設定する** : **[読み取り専用データベース]** を **[False]** に設定します。  
  
##  <a name="bkmk_prepare_mount_databases"></a> 3) Web アプリケーションを準備して、コンテンツ データベースをマウントする  
 次の手順の詳細については、「 [sharepoint 2010 から sharepoint 2013 にデータベースをアップグレードする](https://go.microsoft.com/fwlink/p/?LinkId=256690)」 (https://go.microsoft.com/fwlink/p/?LinkId=256690) を参照してください。  
  
1.  **データベースをオフラインにする**  
  
     SharePoint サーバーの全体管理を使用して、SharePoint 2013 の各コンテンツ データベースをオフラインにします。 コンテンツ データベースを、コピーしたデータベースに置き換えます。 使用環境にとってどのシーケンスが最適かを検討してください。 次のコンテンツ データベースをオフラインにする前に、各データベースをオフラインにして、関連する置換データベースをマウントすることを検討します。 もう 1 つの方法として、すべてのコンテンツ データベースをグループとしてオフラインにします。  
  
    1.  SharePoint サーバーの全体管理で、 **[アプリケーション構成の管理]** をクリックします。  
  
    2.  **[コンテンツ データベースの管理]** をクリックします。  
  
    3.  データベース名をクリックします。  
  
    4.  **[コンテンツ データベース設定の管理]** で、 **[データベースの状態]** を **[オフライン]** に設定します。  
  
    5.  **[コンテンツ データベースの削除]** を選択します。 コンテンツ データベースに格納されているサイトにアクセスできなくなるという警告に注意してください。  
  
-   **コンテンツ データベースをマウントする:**  
  
     移行したコンテンツ データベースをマウントするには、SharePoint 2013 管理シェルで PowerShell コマンドレットを使用します。 サービスアプリケーションデータベースは、コンテンツデータベースのみをマウントする必要はありません。 ![PowerShell 関連コンテンツ](../../../reporting-services/media/rs-powershellicon.jpg "PowerShell 関連コンテンツ")  
  
    ```powershell
    Mount-SPContentDatabase "SharePoint_Content_O14-KJSP1" -DatabaseServer "[server name]\powerpivot" -WebApplication [web application URL]  
    ```  
  
     詳細については、「[コンテンツデータベースを接続またはデタッチする (SharePoint Server 2010)](https://technet.microsoft.com/library/ff628582.aspx) 」 (https://technet.microsoft.com/library/ff628582.aspx) を参照してください。  
  
     **手順の完了後の状態**  : マウント操作が完了すると、前のコンテンツ データベースに格納されていたファイルが表示されます。 そのため、ユーザーはドキュメント ライブラリのブックを表示して開くことができます。  
  
    > [!TIP]  
    >  移行したブックの新しいスケジュールは、移行プロセスのこの時点で作成することができます。 ただし、スケジュールは、前の SharePoint ファームからコピーしたデータベースではなく、新しい [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] サービス アプリケーション データベースで作成されるため、 古いスケジュールは含められません。 前のデータベースを使用して古いスケジュールを移行する次の手順を完了すると、新しいスケジュールは使用できなくなります。  
  
### <a name="troubleshoot-issues-when-you-attempt-to-mount-databases"></a>データベースをマウントしようとすると発生する問題のトラブルシューティング  
 ここでは、データベースをマウントするときに発生する可能性のある問題についてまとめます。  
  
1.  **認証エラー** : 認証関連のエラーが発生する場合は、元の Web アプリケーションで使用している認証モードを確認します。 エラーは、SharePoint 2013 と SharePoint 2010 の Web アプリケーション間の認証の不一致によって発生する可能性があります。 詳細については、「 [1) SharePoint 2013 ファームを準備する](#bkmk_prepare_sharepoint2013) 」を参照してください。  
  
2.  **PowerPivot ファイルの不足:** PowerPivot の .dll ファイルの不足に関連するエラーが発生する場合は、 **spPowerPivot.msi** がインストールされていないか、 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] 構成ツールを使用して PowerPivot が構成されていません。  
  
##  <a name="bkmk_upgrade_powerpivot_schedules"></a>4) PowerPivot のスケジュールをアップグレードする  
 ここでは、PowerPivot のスケジュールの移行に関する詳細とオプションについて説明します。 スケジュールを移行するには、2 つの手順を実行します。 まず、移行したサービス アプリケーション データベースを使用するように PowerPivot サービス アプリケーションを構成し、 次に、スケジュールを移行する 2 つの方法のうちいずれかを選択します。  
  
 **移行したサービス アプリケーション データベースを使用するようにサービス アプリケーションを構成する**  
  
 SharePoint サーバーの全体管理で、コピーした前のサービス アプリケーション データベースを使用するように PowerPivot サービス アプリケーションを構成します。 PowerPivot サービスによって、サービス アプリケーション データベースが新しいスキーマにアップグレードされます。  
  
1.  SharePoint サーバーの全体管理で **[サービス アプリケーションの管理]** をクリックします。  
  
2.  PowerPivot サービスアプリケーション ("既定の PowerPivot サービスアプリケーション" など) を探し、サービスアプリケーションの名前をクリックし、SharePoint リボンで **[プロパティ]** をクリックします。  
  
3.  データベース サーバーの名前付きインスタンスとデータベース名を、 バックアップ、コピー、および復元したデータベースの正しい名前に更新します。 **[OK]** をクリックすると、サービス アプリケーション データベースがアップグレードされます。 エラーは ULS ログに格納されます。  
  
 **PowerPivot のスケジュールをアップグレードする**  
  
 更新スケジュールを移行するには、PowerPivot サービス アプリケーションを構成します。  
  
-   **スケジュールを移行するオプション 1: SharePoint ファームの管理者**  
  
    1.  SharePoint 2013 管理で、`Set-PowerPivotServiceApplication` コマンドレットを `-StartMigratingRefreshSchedules` スイッチを使用して実行し、オンデマンドスケジュール移行![PowerShell 関連コンテンツ](../../../reporting-services/media/rs-powershellicon.jpg "PowerShell 関連コンテンツ")を有効にします。 次の Windows PowerShell スクリプトは、PowerPivot サービス アプリケーションが 1 つだけであることを前提としています。  
  
        ```powershell
        $app = Get-PowerPivotServiceApplication  
        Set-PowerPivotServiceApplication $app -StartMigratingRefreshSchedules  
        ```  
  
         この Windows PowerShell スクリプトを実行すると、スケジュールがアクティブになり、次回の適切なタイミングで実行されるようになります。 ただし、定期更新ページ上の状態は有効になりません。 スケジュールは初めて実行するときに移行され、定期更新ページで **[有効]**  が [True] に変わります。  
  
    2.  StartMigratingRefreshSchedules プロパティの現在値を確認する場合は、次の PowerShell スクリプトを実行します。 このスクリプトは、すべての PowerPivot サービス アプリケーション オブジェクトをループし、名前とプロパティ値を表示します。  
  
        ```powershell
        $apps = Get-PowerPivotServiceApplication  
        foreach ($app in $apps){ Get-PowerPivotServiceApplication $app | Format-Table -Property displayname, id, StartMigratingRefreshSchedules }
        ```  
  
     **スケジュールを移行するオプション 2: ユーザーが各ブックを更新する**  
  
    1.  スケジュールを移行するもう 1 つの方法は、ブックごとに定期更新を有効にすることです。 ブックがあるドキュメント ライブラリに移動します。  
  
    2.  ショートカット メニューを開き、 **[PowerPivot のデータ更新の管理]** をクリックします。  
  
    3.  **[定期更新]** セクションで、 **[有効化]** をクリックします。  
  
    4.  **[さらに、できるだけ早く更新を行います]** を選択できます。 このオプションでは、[OK] をクリックするとすぐに更新のインスタンスが 1 つキューに追加されます。 通常の更新スケジュールも適切な時間にトリガーされます。  
  
    5.  **[OK]** をクリックします。 これで、更新ページに更新履歴が表示されるようになり、スケジュールは通常の時間に実行されます。  
  
 **SQL Server 2008 R2 PowerPivot ブック**  
  
-   SQL Server 2008 R2 PowerPivot ブックを SQL Server 2012 SP1 PowerPivot for SharePoint 2013 で使用している場合は、自動的にはアップグレードされません。 2008 R2 ブックが格納されたコンテンツ データベースを移行すると、ブックを使用できるようにはなりますが、スケジュールはアップグレードされません。  
  
-   詳細については、「 [ブックのアップグレードと定期データ更新 &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013)」を参照してください。  
  
##  <a name="bkmk_additional_resources"></a> その他のリソース  
  
> [!NOTE]  
>  [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] および SharePoint データベース アタッチ アップグレードの詳細については、以下を参照してください。  
  
-   [ブックのアップグレードと定期データ更新 &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013)  
  
-   [SharePoint 2013 へのアップグレードプロセスの概要](https://go.microsoft.com/fwlink/p/?LinkId=256688)(https://go.microsoft.com/fwlink/p/?LinkId=256688) 。  
  
-   [SharePoint 2013 (https://go.microsoft.com/fwlink/p/?LinkId=256689) にアップグレードする前に準備を整える](https://go.microsoft.com/fwlink/p/?LinkId=256689)。  
  
-   [Sharepoint 2010 から sharepoint 2013 (https://go.microsoft.com/fwlink/p/?LinkId=256690) にデータベースをアップグレード](https://go.microsoft.com/fwlink/p/?LinkId=256690)します。
