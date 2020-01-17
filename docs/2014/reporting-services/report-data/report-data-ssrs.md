---
title: レポート データ
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: be36e61a44a416283e77638f01005f1b3e16883b
ms.sourcegitcommit: 0a4879dad09c6c42ad1ff717e4512cfea46820e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67413054"
---
# <a name="report-data-in-sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS) でのレポート データ

  レポート データは、組織の複数のデータ ソースから取得できます。 レポートをデザインする最初の手順は、基になるレポート データを表すデータ ソースとデータセットを作成することです。 各データ ソースには、データの接続情報が含まれます。 各データセットには、データ ソースのデータとして使用するフィールドのセットを定義するクエリ コマンドが含まれます。 各データセットのデータを視覚化するには、データ領域 (テーブル、マトリックス、グラフ、マップなど) を追加します。 レポートの処理時に、データ ソースに対してクエリが実行され、各データ領域は、データセットのクエリ結果を表示するために、必要に応じて拡張されます。  
  
##  <a name="BkMk_ReportDataTerms"></a> 用語

 慣れていない場合[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]の概念では、次の用語を確認する[Reporting Services の概念&#40;SSRS&#41;](../reporting-services-concepts-ssrs.md):*データ接続*、*埋め込みデータソース*、*共有データ ソース*、*埋め込みデータセット*、*共有データセット*、*データセット クエリ*、*レポート パーツ*、および*データ警告*します。  
  
##  <a name="BkMk_ReportDataTips"></a> レポート データの指定に関するヒント

 次の情報を使用して、レポート データの戦略を計画します。  
  
- **データ ソース** ： データ ソースは、レポート サーバーや SharePoint サイトから切り離してパブリッシュおよび管理できます。 データ ソースごとに、ユーザーまたはデータベース所有者が接続情報を 1 か所で管理できます。 データ ソースの資格情報は、レポート サーバーに安全に格納されます。接続文字列には、パスワードを含めないでください。 テスト サーバーから実稼動サーバーにデータ ソースをリダイレクトできます。 データ ソースを無効にして、そのデータ ソースを使用するすべてのレポートを中断できます。 サポートされるデータ ソースの一覧は、次を参照してください。[データ接続、データ ソース、および Reporting Services の接続文字列](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)します。  
  
- **データセット** : データセットは、レポートまたはレポートが依存する共有データ ソースから切り離してパブリッシュおよび管理できます。 ユーザーまたはデータベース所有者は、レポート作成者が使用する最適化されたクエリを提供できます。 クエリを変更すると、共有データセットを使用するすべてのレポートで更新されたクエリが使用されます。 データセットのキャッシュを有効にして、パフォーマンスを向上できます。 特定の時間にクエリ キャッシュをスケジュールすることも、共有スケジュールを使用することもできます。  
  
- **レポート パーツで使用するデータ** : レポート パーツには、そのレポート パーツが依存するデータを含めることができます。 レポート パーツの詳細については、「[レポート デザイナーでのレポート パーツ &#40;SSRS&#41;](../report-design/report-parts-in-report-designer-ssrs.md)」をご覧ください。  
  
- **データのフィルター選択** : レポート データは、クエリまたはレポートでフィルター選択できます。 データセットとクエリ変数を使用してカスケード パラメーターを作成し、ユーザーが何千もの選択肢を管理しやすい数にまで絞り込めるようにすることができます。 パラメーター値または指定するその他の値に基づいて、テーブルまたはグラフでデータをフィルター選択できます。  
  
- **パラメーター** : クエリ変数を含むデータセット クエリ コマンドを使用すると、対応するレポート パラメーターが自動的に作成されます。 パラメーターは手動で作成することもできます。 レポートを表示すると、レポート ツール バーにパラメーターが表示されます。 ユーザーは値を選択して、レポート データまたはレポートの外観を制御できます。 特定の対象ユーザー用にレポート データをカスタマイズするには、同じレポート定義にリンクされた、異なる既定値を持つレポート パラメーターのセットを作成するか、組み込みの `UserID` フィールドを使用します。 詳しくは、「[レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)」および「[式で使用される組み込みコレクション &#40;レポート ビルダーおよび SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md)」をご覧ください。  
  
- **データ警告** : レポートがパブリッシュされたら、レポート データに基づいて警告を作成し、そのレポート データが指定したルールに合致した場合に電子メール メッセージを受信できます。  
  
- **データのグループ化および集計** : レポート データは、クエリまたはレポートでグループ化および集計できます。 クエリで値を集計する場合は、重要であるという制約の範囲内で、引き続きレポートの値を結合できます。  詳しくは、「[データのフィルター、グループ化、および並べ替え &#40;レポート ビルダーおよび SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)」および「[集計関数 &#40;レポート ビルダーおよび SSRS&#41;](../report-design/report-builder-functions-aggregate-function.md)」をご覧ください。  
  
- **データの並べ替え** : レポート データは、クエリまたはレポートで並べ替えることができます。 また、テーブルでは、対話的な並べ替えボタンを追加して、ユーザーが並べ替え順序を制御できるようにすることができます。  
  
- **式に基づくデータ** : ほとんどのレポート プロパティは式に基づくことができ、式にはデータセット フィールドおよびレポート パラメーターへの参照を含めることができるため、強力な式を記述してレポートのデータと外観を制御できます。 パラメーターを定義することで、ユーザーが表示されるデータを制御できるようにすることができます。  
  
- **データセットのデータの表示** : 通常、データセットのデータは 1 つ以上のデータ領域 (たとえば、テーブルやグラフ) に表示されます。  
  
- **複数のデータセットのデータの表示**  : 他のデータセットの値または集計を参照する 1 つのデータセットに基づいて、データ領域に式を記述できます。 1 つのデータセットに基づいてテーブルにサブレポートを含めて、別のデータ ソースのデータを表示できます。  
  
## <a name="data-connections-data-sources-and-datasets"></a>データ接続、データ ソース、およびデータセット

 以下を参考にすると、レポートのデータ ソースの定義が容易になります。  
  
- 埋め込みのデータ ソースおよびデータセットと、共有のデータ ソースおよびデータセットのどちらを使用するかを検討してください。 データ ソースの所有者と共同作業を行って、組織に合った認証および承認のテクノロジを実装して使用します。  
  
- 組織のソフトウェア データ層アーキテクチャと、データ型が原因で発生する可能性がある問題について理解しておいてください。 また、データ拡張機能およびデータ処理拡張機能がクエリ結果に与える可能性がある影響についても理解しておいてください。 データ型は、データ ソース、データ プロバイダー、およびレポート定義 (.rdl) ファイルに格納されているデータ型間で異なります。  
  
- [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のクライアントとサーバーのアーキテクチャおよびツールについて理解しておいてください。 たとえば、レポート デザイナーでは、組み込みのデータ ソースの種類を使用するクライアント コンピューターでレポートを作成します。 レポートをパブリッシュする場合は、データ ソースの種類がレポート サーバーまたは SharePoint サイトでサポートされている必要があります。  詳細については、「[Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)」をご覧ください。  
  
- データ ソースとデータセットはレポートで作成され、クライアント作成ツールからレポート サーバーまたは SharePoint サイトにパブリッシュされます。 データ ソースは、レポート サーバーで直接作成できます。 データ ソースとデータセットがパブリッシュされたら、レポート サーバーで資格情報とその他のプロパティを構成できます。 詳細については、次を参照してください。[データ接続、データ ソース、および Reporting Services の接続文字列](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)と[Reporting Services ツール](../tools/reporting-services-tools.md)します。  
  
- 使用できるデータ ソースは、インストールされている [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のデータ拡張機能によって異なります。 データ ソースのサポートは、クライアント作成ツール、レポート サーバーのバージョン、およびレポート サーバーのプラットフォームによって異なる可能性があります。 詳細については、「[Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)」をご覧ください。  
  
- データ ソースの資格情報は、データ ソースの種類、およびクライアントと、レポート サーバーまたは SharePoint サイトのどちらでレポートを表示しているかによって異なります。 詳しくは、「[SharePoint サイト上のレポート サーバー アイテムに対するアクセス許可の設定 &#40;Reporting Services の SharePoint 統合モード&#41;](../security/set-permissions-for-report-server-items-on-a-sharepoint-site.md)」、「[レポート データ ソースに関する資格情報と接続情報を指定する](../../integration-services/connection-manager/data-sources.md)」、および「[Reporting Services ツール](../tools/reporting-services-tools.md)」の各ツールに固有の資格情報をご覧ください。  
  
## <a name="related-tasks"></a>Related Tasks

 以下に、データ接続の作成、外部ソース、データセット、およびクエリからのデータの追加に関連するタスクを示します。  
  
|||  
|-|-|  
|**一般的なタスク**|**リンク**|  
|データ接続の作成|[Reporting Services でのデータ接続、データ ソース、および接続文字列](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|データセットとクエリの作成|[レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|  
|パブリッシュ後のデータ ソースの管理|[レポート データ ソースを管理する](manage-report-data-sources.md)|  
|パブリッシュ後の共有データセットの管理|[共有データセットを管理する](manage-shared-datasets.md)|  
|データ警告の作成および管理|[Reporting Services Data Alerts](../tutorial-creating-a-basic-table-report-report-builder.md)|  
|共有データセットのキャッシュ|[共有データセットのキャッシュ &#40;SSRS&#41;](../report-server/cache-shared-datasets-ssrs.md)|  
|キャッシュを事前に読み込むための共有データセットのスケジュール|[スケジュール](../subscriptions/schedules.md)|  
|データ拡張機能の追加|[データ処理拡張機能の実装](../extensions/data-processing/implementing-a-data-processing-extension.md)|