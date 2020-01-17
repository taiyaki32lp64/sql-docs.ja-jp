---
title: Reporting Services のバックアップおよび復元操作 | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.assetid: 157bc376-ab72-4c99-8bde-7b12db70843a
ms.date: 05/08/2019
ms.openlocfilehash: f5d2aad7b0a306dd4bd2c8e64b7a49581c8fb5d2
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264974"
---
# <a name="backup-and-restore-operations-for-reporting-services"></a>Reporting Services のバックアップおよび復元操作

  この記事では、インストールした [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] で使用するデータ ファイルの概要と、これらのファイルをバックアップするタイミングおよび方法について説明します。 レポート サーバー データベース ファイルのバックアップ/復元プランの作成は、復旧計画の最も重要な部分です。 ただし、さらに完全な復旧計画には、暗号化キー、カスタム アセンブリや拡張機能、構成ファイル、およびレポートのソース ファイルのバックアップなども必要になります。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード | [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード  

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。
  
 バックアップ操作および復元操作は、インストールした [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の全体または一部を移動する際によく使用します。  
  
-   レポート サーバー データベースだけを移動する場合は、バックアップと復元またはアタッチとデタッチを使用して、別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにデータベースを再配置できます。 詳細については、「 [別のコンピューターへのレポート サーバー データベースの移動 (SSRS ネイティブ モード)](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)」を参照してください。  
  
-   インストールされている [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を別のコンピューターへ移動することを "移行" といいます。 インストールを移行する場合、セットアップを実行して新しいレポート サーバー インスタンスをインストールし、次にインスタンス データを移行先のコンピューターにコピーします。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インストールの移行の詳細については、次の記事を参照してください。  
  
    - [Reporting Services のアップグレードと移行](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)  
    - [Reporting Services のインストールの移行 &#40;ネイティブ モード&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)  

    ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
    - [Reporting Services の移行 &#40;SharePoint モード&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)  

    ::: moniker-end
  
## <a name="backing-up-the-report-server-databases"></a>レポート サーバー データベースのバックアップ  
 レポート サーバーはステートレス サーバーであるため、アプリケーション データはすべて、 **インスタンスで稼働している** reportserver **および** reportservertempdb [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] データベースに格納されます。 **reportserver** データベースと **reportservertempdb** データベースは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースでサポートされているバックアップ方式のいずれかを使用してバックアップできます。 レポート サーバー データベースに固有の推奨事項を次に示します。  
  
-   **reportserver** データベースをバックアップするには、完全復旧モデルを使用します。  
  
-   **reportservertempdb** データベースをバックアップするには、単純復旧モデルを使用します。  
  
-   各データベースに対して異なるバックアップ スケジュールを設定できます。 **reportservertempdb** をバックアップする唯一の理由は、ハードウェア障害が発生した場合にこのデータベースの再作成を回避することです。 ハードウェア障害が発生した場合、 **reportservertempdb**のデータを復旧する必要はありませんが、テーブル構造については復旧が必要になります。 **reportservertempdb**が失われた場合、レポート サーバー データベースの再作成以外にこのデータベースを復元する方法はありません。 **reportservertempdb**を再作成する場合、プライマリ レポート サーバー データベースと同じ名前を使用することが重要です。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データベースのバックアップおよび復旧の詳細については、「 [SQL Server データベースのバックアップと復元](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)」を参照してください。  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"  

> [!IMPORTANT]  
>  レポート サーバーが SharePoint モードの場合は、SharePoint 構成データベースや [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 警告データベースなど、考慮する必要があるデータベースがあります。 SharePoint モードでは、それぞれの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションに対して 3 つのデータベースが作成されます。 その 3 つのデータベースとは、 **reportserver**、 **reportservertempdb**、および **dataalerting** です。 詳細については、「[Reporting Services SharePoint サービス アプリケーションのバックアップと復元](../../reporting-services/report-server-sharepoint/backup-and-restore-reporting-services-sharepoint-service-applications.md)」を参照してください。  

::: moniker-end
  
## <a name="backing-up-the-encryption-keys"></a>暗号化キーのバックアップ  
 インストールした [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を初めて構成するときは、暗号化キーをバックアップする必要があります。 サービス アカウントの ID やコンピューターの名前を変更する際にも、そのつど暗号化キーをバックアップする必要があります。 詳細については、「 [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)」を参照してください。 

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

SharePoint モードのレポート サーバーについては、「[Reporting Services SharePoint サービス アプリケーションの管理](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)」の「キー管理」のセクションを参照してください。  

::: moniker-end
  
## <a name="backing-up-the-configuration-files"></a>構成ファイルのバックアップ  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、構成ファイルを使用してアプリケーション設定を格納します。 初めてサーバーを構成するときおよびカスタム拡張機能を配置した後は常に、ファイルをバックアップする必要があります。 バックアップするのは次のファイルです。  
  
-   RSReportServer.config  
  
-   Rssvrpolicy.config  
  
-   Rsmgrpolicy.config  
  
-   Reportingservicesservice.exe.config  
  
-   レポート サーバーの [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] アプリケーション用の Web.config
  
-   用の Machine.config [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]  
  
## <a name="backing-up-data-files"></a>データ ファイルのバックアップ  
 レポート デザイナーで作成およびメンテナンスしているファイルをバックアップします。 これらのファイルには、レポート定義 (.rdl) ファイル、共有データ ソース (.rds) ファイル、データ ビュー (.dv) ファイル、データ ソース (.ds) ファイル、レポート サーバー プロジェクト (.rptproj) ファイル、およびレポート ソリューション (.sln) ファイルが含まれます。  
  
 管理タスクまたは配置タスクのために作成したスクリプト ファイル (.rss) のバックアップを忘れないように注意してください。  
  
 使用しているカスタム拡張機能およびカスタム アセンブリのバックアップ コピーが存在していることを確認します。  

## <a name="next-steps"></a>次の手順

[レポート サーバー データベース](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
[Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)   
[Rskeymgmt ユーティリティ](../../reporting-services/tools/rskeymgmt-utility-ssrs.md)   
[バックアップと復元によるデータベースのコピー](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
[レポート サーバー データベースを管理する](../../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)   
[暗号化キーの構成と管理](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
