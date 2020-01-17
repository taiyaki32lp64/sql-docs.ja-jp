---
title: レポートの保存 (レポート ビルダー) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 59ddc4b8-9517-4d3f-9c88-a07e9907cecb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8682d55f6c805066f5b596e79a074f253db9faa9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66499630"
---
# <a name="saving-reports-report-builder"></a>レポートの保存 (レポート ビルダー)
  レポート ビルダーでは、自分が書き込み権限を持っている [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] レポート サーバー、SharePoint ライブラリ、またはファイル共有、あるいは自分のコンピューターにページ分割されたレポートを保存できます。 
  
レポートを保存する場合、実際に保存されるのは、レポート レイアウトを記述したレポート定義です。 データは保存されません。 レポートを実行するたびにレポート データは更新され、ほとんどの場合、前回の実行時とは異なります。  
  
 レポートを他の形式で保存する場合やレポート定義をデータと共に保存する場合は、次の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の機能のいずれかを使用します。  
  
-   表示されたレポートをコンマ区切り (CSV) や Excel ブックなどの別のファイル形式にエクスポートし、その形式でレポートを保存する。 レポートからデータ フィードを生成し、レポート データを保存することもできます。  
  
-   レポート サブスクリプションを作成し、ファイル共有にレポートを配信して保存する。  
  
-   レポート履歴を使用して、表示されたレポートのバージョンを履歴コピーとして保存する。  
  
 レポート サーバー上のレポートを直接表示し、管理する方法の詳細については、「[レポートの検索、表示、管理 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)」および「[Reporting Services レポート サーバー &#40;ネイティブ モード&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)」をご覧ください。  
  
##  <a name="SavingReportDefinitions"></a> レポートのレポート サーバーへの保存  
  レポートをレポート サーバーに保存することを、レポートのパブリッシュと呼びます。 レポートは自分のコンピューターに保存することもできますが、レポート サーバーに保存すると多くの利点があります。  
  
-   レポートを保存したフォルダーへのアクセス権限を持つ他のユーザーに対して、レポートが利用可能になります。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web ポータルで、レポートの管理や表示を行うことができます。  
  
-   データ ソース、画像、サブレポートなどのレポート リソースを 1 か所に保存するのでアクセスが容易です。  
  
-   サブスクリプションによって、レポートを他のユーザーに配信できます。  
  
-   レポートは、レポート サーバー データベースに安全に保存されます。  
  
-   レポートの実行はログに記録され、パフォーマンスと監査に関する情報が提供されます。  
  
##  <a name="ExportingAndSavingReports"></a> レポートのエクスポートと保存  
 アーカイブするレポートの数が少ない場合、レポートをエクスポートしてファイルとして保存することを検討してください。 レポートをアプリケーション (PDF や Excel など) にエクスポートしたら、そのレポートをファイルとして保存し、ネットワーク上の保護された共有ディレクトリに配置できます。 また、形式にかかわらず、レポート サーバー データベースにレポートのすべてのコピーを保存する場合、リソース アイテムとして保存した PDF または Excel ファイルをアップロードできます。 レポートのエクスポートの詳細については、「 [レポートのエクスポート (レポート ビルダーおよび SSRS)](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) 」および「 [ファイルまたはレポートをアップロードする](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)」をご覧ください。  
  
##  <a name="UsingFileShareDelivery"></a> ファイル共有配信の使用  
 アーカイブするレポートが多数ある場合、ファイル システムにレポートを直接配信するサブスクリプションを作成します。 この方法の場合、レポートごとにサブスクリプションを作成し、レポートを格納するための共有フォルダーを選択して、ファイルの作成日時を決定するスケジュールを定義する必要があります。 サブスクリプションを定義したら、レポート サーバーによるレポートの自動実行や、指定したスケジュールによるレポート ファイルのアーカイブへの追加が可能になります。 また、定期的にレポートをアーカイブしない場合は、1 回のみ使用するスケジュールを作成することもできます。 サブスクリプションとファイル共有配信の詳細については、「 [Reporting Services でのファイル共有の配信](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)」をご覧ください。  
  
##  <a name="UsingReportHistory"></a> レポート履歴の使用  
 レポート履歴機能を使用して、履歴のコピーを作成することもできます。 その後、レポート サーバー データベースをバックアップし、今後使用するために安全な場所にバックアップを格納することができます。 すべてのレポート履歴は (レポート、共有データ ソース アイテム、フォルダー、サブスクリプション、および共有スケジュールと共に)、レポート サーバー データベースに格納されます。 レポート履歴およびメタデータの永続的なコピーを保持するために、バックアップを作成できます。メタデータには、レポートの受信者を示すサブスクリプション情報などがあります。 詳細については、「 [レポート履歴でのスナップショットの作成、変更、および削除](../../reporting-services/report-server/create-modify-and-delete-snapshots-in-report-history.md)」を参照してください。  
 
##  <a name="HowTo"></a> 操作方法に関するトピック  
  
-   [レポートのレポート サーバーへの保存 (レポート ビルダー)](../../reporting-services/report-builder/save-reports-to-a-report-server-report-builder.md)  
  
-   [SharePoint ライブラリへのレポートの保存 (レポート ビルダー)](../../reporting-services/report-builder/save-a-report-to-a-sharepoint-library-report-builder.md)  
   
## <a name="see-also"></a>参照  
 [レポート、レポート パーツ、およびレポート定義 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [レポート ビルダーをインストール](../install-windows/install-report-builder.md)   
 [レポートの検索、表示、管理 (レポート ビルダーおよび SSRS)](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [レポートのエクスポート &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [レポートの印刷 (レポート ビルダーおよび SSRS)](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)  
  
  
