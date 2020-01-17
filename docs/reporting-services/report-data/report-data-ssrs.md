---
title: レポート データ
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: f3aa702eef414fdc92670a51b8d374627797fe3d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265558"
---
# <a name="report-data-in-sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS) でのレポート データ

  レポート データは、組織の複数のデータ ソースから取得できます。 レポートをデザインする最初の手順は、基になるレポート データを表すデータ ソースとデータセットを作成することです。 各データ ソースには、データの接続情報が含まれます。 各データセットには、データ ソースのデータとして使用するフィールドのセットを定義するクエリ コマンドが含まれます。 各データセットのデータを視覚化するには、データ領域 (テーブル、マトリックス、グラフ、マップなど) を追加します。 レポートの処理時に、データ ソースに対してクエリが実行され、各データ領域は、データセットのクエリ結果を表示するために、必要に応じて拡張されます。  

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。
  
##  <a name="BkMk_ReportDataTerms"></a> 用語  
  
- **データ接続:** " *データ ソース*" とも呼ばれます。 データ接続には、名前と、接続の種類に依存する接続のプロパティが含まれます。 仕様上、データ接続に資格情報は含まれません。 データ接続では、どのデータを外部データ ソースから取得するかは指定されません。 これを行うには、データセットを作成するときにクエリを指定します。  
  
- **データ ソースの定義:** レポート データ ソースの XML 表現を含むファイル。 レポートをパブリッシュすると、そのデータ ソースは、レポート定義とは別にデータ ソース定義として、レポート サーバーまたは SharePoint サイトに保存されます。 たとえば、レポート サーバー管理者は、接続文字列や資格情報を更新することができます。 ネイティブのレポート サーバーでのファイルの種類は .rds です。 SharePoint サイトでのファイルの種類は .rsds です。  
  
- **接続文字列:** 接続文字列は、データ ソースに接続するために必要な接続プロパティの文字列バージョンです。 接続プロパティはデータ接続の種類に応じて異なります。 例については、「 [データ接続、データ ソース、および接続文字列](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)」を参照してください。  
  
- **共有データ ソース:** レポート サーバーまたは SharePoint サイトにあり、複数のレポートで使用することができるデータ ソースです。  
  
- **埋め込みデータ ソース:** " *レポート固有のデータ ソース*" とも呼ばれます。 1 つのレポート内で定義され、そのレポートのみで使用されるデータ ソースです。  
  
- **資格情報:** 資格情報は、外部データにアクセスするために指定する必要がある認証情報です。  
  
##  <a name="BkMk_ReportDataTips"></a> レポート データの指定に関するヒント

 次の情報を使用して、レポート データの戦略を計画します。  
  
- **データ ソース** ： データ ソースは、レポート サーバーや SharePoint サイトから切り離してパブリッシュおよび管理できます。 データ ソースごとに、ユーザーまたはデータベース所有者が接続情報を 1 か所で管理できます。 データ ソースの資格情報は、レポート サーバーに安全に格納されます。接続文字列には、パスワードを含めないでください。 テスト サーバーから実稼動サーバーにデータ ソースをリダイレクトできます。 データ ソースを無効にして、そのデータ ソースを使用するすべてのレポートを中断できます。  
  
- **データセット** : データセットは、レポートまたはレポートが依存する共有データ ソースから切り離してパブリッシュおよび管理できます。 ユーザーまたはデータベース所有者は、レポート作成者が使用する最適化されたクエリを提供できます。 クエリを変更すると、共有データセットを使用するすべてのレポートで更新されたクエリが使用されます。 データセットのキャッシュを有効にして、パフォーマンスを向上できます。 特定の時間にクエリ キャッシュをスケジュールすることも、共有スケジュールを使用することもできます。  
  
- **レポート パーツで使用するデータ** : レポート パーツには、そのレポート パーツが依存するデータを含めることができます。 レポート パーツの詳細については、「[レポート デザイナーでのレポート パーツ &#40;SSRS&#41;](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md)」をご覧ください。  
  
- **データのフィルター選択** : レポート データは、クエリまたはレポートでフィルター選択できます。 データセットとクエリ変数を使用してカスケード パラメーターを作成し、ユーザーが何千もの選択肢を管理しやすい数にまで絞り込めるようにすることができます。 パラメーター値または指定するその他の値に基づいて、テーブルまたはグラフでデータをフィルター選択できます。  
  
- **パラメーター** : クエリ変数を含むデータセット クエリ コマンドを使用すると、対応するレポート パラメーターが自動的に作成されます。 パラメーターは手動で作成することもできます。 レポートを表示すると、レポート ツール バーにパラメーターが表示されます。 ユーザーは値を選択して、レポート データまたはレポートの外観を制御できます。 特定の対象ユーザー用にレポート データをカスタマイズするには、同じレポート定義にリンクされた、異なる既定値を持つレポート パラメーターのセットを作成するか、組み込みの **UserID** フィールドを使用します。 詳しくは、「[レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)」および「[式で使用される組み込みコレクション &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)」をご覧ください。  
  
- **データ警告** : レポートがパブリッシュされたら、レポート データに基づいて警告を作成し、そのレポート データが指定したルールに合致した場合に電子メール メッセージを受信できます。  
  
- **データのグループ化および集計** : レポート データは、クエリまたはレポートでグループ化および集計できます。 クエリで値を集計する場合は、重要であるという制約の範囲内で、引き続きレポートの値を結合できます。  詳しくは、「[データのフィルター、グループ化、および並べ替え &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)」および「[集計関数 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-function.md)」をご覧ください。  
  
- **データの並べ替え** : レポート データは、クエリまたはレポートで並べ替えることができます。 また、テーブルでは、対話的な並べ替えボタンを追加して、ユーザーが並べ替え順序を制御できるようにすることができます。  
  
- **式に基づくデータ** : ほとんどのレポート プロパティは式に基づくことができ、式にはデータセット フィールドおよびレポート パラメーターへの参照を含めることができるため、強力な式を記述してレポートのデータと外観を制御できます。 パラメーターを定義することで、ユーザーが表示されるデータを制御できるようにすることができます。  
  
- **データセットのデータの表示** : 通常、データセットのデータは 1 つ以上のデータ領域 (たとえば、テーブルやグラフ) に表示されます。  
  
- **複数のデータセットのデータの表示**  : 他のデータセットの値または集計を参照する 1 つのデータセットに基づいて、データ領域に式を記述できます。 1 つのデータセットに基づいてテーブルにサブレポートを含めて、別のデータ ソースのデータを表示できます。  
  
 以下を参考にすると、レポートのデータ ソースの定義が容易になります。  
  
- 埋め込みのデータ ソースおよびデータセットと、共有のデータ ソースおよびデータセットのどちらを使用するかを検討してください。 データ ソースの所有者と共同作業を行って、組織に合った認証および承認のテクノロジを実装して使用します。  
  
- 組織のソフトウェア データ層アーキテクチャと、データ型が原因で発生する可能性がある問題について理解しておいてください。 また、データ拡張機能およびデータ処理拡張機能がクエリ結果に与える可能性がある影響についても理解しておいてください。 データ型は、データ ソース、データ プロバイダー、およびレポート定義 (.rdl) ファイルに格納されているデータ型間で異なります。  
  
- [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のクライアントとサーバーのアーキテクチャおよびツールについて理解しておいてください。 たとえば、レポート デザイナーでは、組み込みのデータ ソースの種類を使用するクライアント コンピューターでレポートを作成します。 レポートをパブリッシュする場合は、データ ソースの種類がレポート サーバーまたは SharePoint サイトでサポートされている必要があります。  詳細については、「[Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)」をご覧ください。  
  
- データ ソースとデータセットはレポートで作成され、クライアント作成ツールからレポート サーバーまたは SharePoint サイトにパブリッシュされます。 データ ソースは、レポート サーバーで直接作成できます。 データ ソースとデータセットがパブリッシュされたら、レポート サーバーで資格情報とその他のプロパティを構成できます。 詳しくは、「 [データ接続、データ ソース、および接続文字列 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) 」および「 [Reporting Services ツール](../../reporting-services/tools/reporting-services-tools.md)" とも呼ばれます。  
  
- 使用できるデータ ソースは、インストールされている [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のデータ拡張機能によって異なります。 データ ソースのサポートは、クライアント作成ツール、レポート サーバーのバージョン、およびレポート サーバーのプラットフォームによって異なる可能性があります。 詳細については、「[Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)」をご覧ください。  
  
- データ ソースの資格情報は、データ ソースの種類、およびクライアントと、レポート サーバーまたは SharePoint サイトのどちらでレポートを表示しているかによって異なります。 詳しくは、「[SharePoint サイト上のレポート サーバー アイテムに対するアクセス許可の設定 &#40;Reporting Services の SharePoint 統合モード&#41;](../../reporting-services/security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)」、「[レポート データ ソースに関する資格情報と接続情報を指定する](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)」、および「[Reporting Services ツール](../../reporting-services/tools/reporting-services-tools.md)」の各ツールに固有の資格情報をご覧ください。  
  
## <a name="related-tasks"></a>Related Tasks

 以下に、データ接続の作成、外部ソース、データセット、およびクエリからのデータの追加に関連するタスクを示します。  
  
|||  
|-|-|  
|**一般的なタスク**|**リンク**|  
|データ接続の作成|[データ接続、データ ソース、および接続文字列 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)|  
|データセットとクエリの作成|[レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|  
|パブリッシュ後のデータ ソースの管理|[レポート データ ソースを管理する](../../reporting-services/report-data/manage-report-data-sources.md)|  
|パブリッシュ後の共有データセットの管理|[共有データセットを管理する](../../reporting-services/report-data/manage-shared-datasets.md)|  
|データ警告の作成および管理|[Reporting Services Data Alerts](../../reporting-services/reporting-services-data-alerts.md)|  
|共有データセットのキャッシュ|[共有データセットのキャッシュ &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)|  
|キャッシュを事前に読み込むための共有データセットのスケジュール|[スケジュール](../../reporting-services/subscriptions/schedules.md)|  
|データ拡張機能の追加|[データ処理拡張機能の実装](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)|