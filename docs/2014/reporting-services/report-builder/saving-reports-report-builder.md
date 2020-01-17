---
title: レポートの保存 (レポート ビルダー) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 59ddc4b8-9517-4d3f-9c88-a07e9907cecb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e21b1c9e48dcccf8b72a60fbd381aac3d878c0dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107630"
---
# <a name="saving-reports-report-builder"></a>レポートの保存 (レポート ビルダー)
  レポート ビルダーでは、自分が書き込み権限を持っているレポート サーバー、SharePoint ライブラリ、またはファイル共有、あるいは自分のコンピューターにレポートを保存できます。 レポートは、レポートを開いた場所に保存することも、別の場所に保存することもできます。また、新しい名前を付けてそれらの場所に保存することもできます。 既定では、レポートは、レポートを開いた場所に再保存されます。 レポートを保存する場合、実際に保存されるのは、レポート レイアウトを記述したレポート定義です。 データは保存されません。 レポートを実行するたびにレポート データは更新され、ほとんどの場合、前回の実行時とは異なります。  
  
 レポートを他の形式で保存する場合やレポート定義をデータと共に保存する場合は、次の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の機能のいずれかを使用します。  
  
-   表示されたレポートをコンマ区切り (CSV) や Excel ブックなどの別のファイル形式にエクスポートし、その形式でレポートを保存する。 レポートからデータ フィードを生成し、レポート データを保存することもできます。  
  
-   レポート サブスクリプションを作成し、ファイル共有にレポートを配信して保存する。  
  
-   レポート履歴を使用して、表示されたレポートのバージョンを履歴コピーとして保存する。  
  
 レポート サーバー上のレポートを直接表示し、管理する方法の詳細については、msdn.microsoft.com で、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [オンライン ブック](https://go.microsoft.com/fwlink/?LinkId=154888)の「[レポートの検索、表示、管理 (レポート ビルダーおよび SSRS)](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)」および「[Reporting Services レポート サーバー (ネイティブ モード)](../report-server/reporting-services-report-server-native-mode.md)」を参照してください。  
  
##  <a name="SavingReportDefinitions"></a> レポート定義の保存  
 レポートは自分のコンピューターに保存することもできますが、レポート サーバーに保存すると多くの利点があります。  
  
 レポートをレポート サーバーに保存すると、次のような利点があります。  
  
-   レポートを保存したフォルダーへのアクセス権限を持つ他のユーザーに対して、レポートが利用可能になります。  
  
-   レポート マネージャーを使用してレポートの管理や表示を行うことができます。  
  
-   データ ソース、画像、サブレポートなどのレポート リソースを 1 か所に保存するのでアクセスが容易です。  
  
-   サブスクリプションによって、レポートを他のユーザーに配信できます。  
  
-   レポートは、レポート サーバー データベースに安全に保存されます。  
  
-   レポートの実行はログに記録され、パフォーマンスと監査に関する情報が提供されます。  
  
 レポートをレポート サーバーに保存することを、レポートのパブリッシュと呼びます。 レポートを保存すると、レポート定義のみが保存されます。 レポートを実行するたびにレポート データは更新され、ほとんどの場合、前回の実行時とは異なります。 レポート定義をデータと共に保存する場合は、レポート履歴機能を使用する必要があります。 この機能を使用すると、レポートのコピーとそのデータが一緒に保存されます。  
  

  
##  <a name="ExportingAndSavingReports"></a> レポートのエクスポートと保存  
 アーカイブするレポートの数が少ない場合、レポートをエクスポートしてファイルとして保存することを検討してください。 レポートをアプリケーション (PDF や Excel など) にエクスポートしたら、そのレポートをファイルとして保存し、ネットワーク上の保護された共有ディレクトリに配置できます。 また、形式にかかわらず、レポート サーバー データベースにレポートのすべてのコピーを保存する場合、リソース アイテムとして保存した PDF または Excel ファイルをアップロードできます。 レポートのエクスポートの詳細については、次を参照してください。[レポートのエクスポート&#40;レポート ビルダーおよび SSRS&#41; ](export-reports-report-builder-and-ssrs.md)と[ファイルまたはレポートをアップロード&#40;レポート マネージャー&#41;](../reports/upload-a-file-or-report-report-manager.md)します。  
  

  
##  <a name="UsingFileShareDelivery"></a> ファイル共有配信の使用  
 アーカイブするレポートが多数ある場合、ファイル システムにレポートを直接配信するサブスクリプションを作成します。 この方法の場合、レポートごとにサブスクリプションを作成し、レポートを格納するための共有フォルダーを選択して、ファイルの作成日時を決定するスケジュールを定義する必要があります。 サブスクリプションを定義したら、レポート サーバーによるレポートの自動実行や、指定したスケジュールによるレポート ファイルのアーカイブへの追加が可能になります。 また、定期的にレポートをアーカイブしない場合は、1 回のみ使用するスケジュールを作成することもできます。 サブスクリプションとファイル共有配信の詳細については、 [Reporting Services のドキュメント](https://go.microsoft.com/fwlink/?linkid=121312) (SQL Server オンライン ブック) の「Reporting Services でのファイル共有の配信」を参照してください。  
  

  
##  <a name="UsingReportHistory"></a> レポート履歴の使用  
 レポート履歴機能を使用して、履歴のコピーを作成することもできます。 その後、レポート サーバー データベースをバックアップし、今後使用するために安全な場所にバックアップを格納することができます。 すべてのレポート履歴は (レポート、共有データ ソース アイテム、フォルダー、サブスクリプション、および共有スケジュールと共に)、レポート サーバー データベースに格納されます。 レポート履歴およびメタデータの永続的なコピーを保持するために、バックアップを作成できます。メタデータには、レポートの受信者を示すサブスクリプション情報などがあります。 詳細については、 [Reporting Services のドキュメント](https://go.microsoft.com/fwlink/?linkid=121312) (SQL Server オンライン ブック) の「レポート履歴の管理」を参照してください。  
  

  
##  <a name="HowTo"></a> 操作方法に関するトピック  
  
-   [レポートのレポート サーバーへの保存 (レポート ビルダー)](save-reports-to-a-report-server-report-builder.md)  
  
-   [SharePoint ライブラリへのレポートの保存 &#40;レポート ビルダー&#41;](save-a-report-to-a-sharepoint-library-report-builder.md)  
  
-   [お使いのコンピューターにレポートを保存&#40;レポート ビルダー&#41;](../save-reports-to-your-computer-report-builder.md)  
  

  
## <a name="see-also"></a>参照  
 [レポート、レポート パーツ、およびレポート定義 (レポート ビルダーおよび SSRS)](../report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [インストール、アンインストール、およびレポート ビルダーのサポート](../install-uninstall-and-report-builder-support.md)   
 [レポートの検索、表示、管理 (レポート ビルダーおよび SSRS)](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [レポートのエクスポート&#40;レポート ビルダーおよび SSRS&#41;](export-reports-report-builder-and-ssrs.md)   
 [レポートの印刷 &#40;レポート ビルダーおよび SSRS&#41;](print-reports-report-builder-and-ssrs.md)  
  
  
