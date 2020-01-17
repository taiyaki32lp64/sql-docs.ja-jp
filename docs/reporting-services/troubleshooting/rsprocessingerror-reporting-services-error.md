---
title: rsProcessingError - Reporting Services エラー | Microsoft Docs
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rsProcessingError
ms.assetid: 414ee58a-8251-4367-9a8e-10c068d17280
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 684f2ec1878e7918f9aa43017feb4b4f8d32cfa1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65573821"
---
# <a name="rsprocessingerror---reporting-services-error"></a>rsProcessingError - Reporting Services エラー
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|rsProcessingError|  
|イベント ソース|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources|  
|コンポーネント|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|メッセージ テキスト|レポートの処理中にエラーが発生しました。|  
  
## <a name="explanation"></a>説明  
 レポートのサブスクリプションをパブリッシュ、処理、ローカルでプレビュー、レポート サーバーから表示、または作成しているときに、1 つ以上のエラーが発生しました。 このエラー メッセージは、少なくとも 1 つのエラーが検出されたことを示しています。  
  
### <a name="possible-causes"></a>考えられる原因  
 次の原因が考えられます。  
  
-   レポート サーバーで処理エラーが発生した。  
  
-   レポートをプレビューするときに、ローカルでのレポート処理の際、処理エラーが発生した。  
  
-   グループ式が、不適切なデータ型に評価された。  
  
-   比較できないデータ型として評価される 2 つの式をフィルター定義で指定した。  
  
-   Fields コレクションに存在しないフィールドを式で参照した。  
  
-   無効または競合するスコープを使用した集計関数呼び出しが式に含まれていた。  
  
-   レポート パラメーター コレクションに存在しないパラメーターを式で参照した。  
  
-   正しく展開されていないカスタム アセンブリまたは [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アセンブリを読み込めなかった。  
  
-   Nullable プロパティが **False** に設定されたパラメーターによって、パラメーター内に NULL 値が検出された。  
  
-   データ領域の Hidden プロパティの式にエラーが含まれている。オブジェクト参照が、オブジェクトのインスタンスに設定されていない。  
  
-   無効な関数呼び出しまたは構文エラーが式に含まれていた。  
  
## <a name="user-action"></a>ユーザーの操作  
  
### <a name="finding-more-information"></a>詳細情報  
 必要に応じて以下の操作を行います。  
  
-   レポート サーバーからレポートを表示している場合、またはサブスクリプションとしてレポートを表示している場合は、エラー メッセージを通読します。 詳細テキストに追加情報が記載されています。  
  
-   レポート デザイナーでレポートを作成していて、レポートのプレビューまたはパブリッシュ中にこのエラーが表示された場合は、[エラー一覧] ウィンドウに追加情報が記載されています。  
  
-   レポート デザイナー プレビューでレポートを作成している場合は、エラー メッセージ全体に目を通します。 詳細テキストに追加情報が記載されています。  
  
-   レポート サーバーでレポートを表示していて、さらにレポート サーバーをローカル管理者として実行している場合は、ページを右クリックして **[ソースの表示]** をクリックすると、呼び出し履歴を表示できます。 呼び出し履歴には追加情報が記載されています。  
  
-   レポート サーバーでローカル管理者として処理を実行している場合は、ログ ファイル内で `ReportProcessingException`を検索します。 ログ エントリには詳細情報が含まれています。 通常、レポート サーバーのログ ファイルは \<*ドライブ*>:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles\ReportServerService__*datetimestamp*.log にあります。 詳細については、「 [Reporting Services のログ ファイルとソース](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)」を参照してください。  
  
### <a name="failed-to-load-expression-host-assembly"></a>式のホスト アセンブリの読み込みに失敗した  
 カスタム アセンブリには、厳密な名前の署名と、属性 AllowPartiallyTrustedCallers の設定が必要です。 詳細については、「 [レポートでのカスタム アセンブリの使用](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md) 」と「 [セキュリティ ポリシーの概要](../../reporting-services/extensions/secure-development/understanding-security-policies.md)」を参照してください。  
  
### <a name="a-built-in-global-name-does-not-exist"></a>組み込みのグローバル名が存在しない  
 式内のスペルを確認します。 組み込みのグローバル、パラメーター、およびフィールド名では、大文字と小文字が区別されます。 エラーが発生した式で、レポートに名前が実際に存在し、そのスペルが正しいことを確認します。 詳細については、「[式で使用される組み込みコレクション &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)」を参照してください。  
  
### <a name="parameter-properties-and-null"></a>パラメーターのプロパティと NULL  
 複数値パラメーターには NULL を設定できません。 詳細については、「 [レポート パラメーター (レポート ビルダーおよびレポート デザイナー)](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)にあります。  
  
### <a name="main-report-with-subreport-could-not-be-processed"></a>サブレポートを含むメイン レポートを処理できなかった  
 サブレポートを含むレポートは、同一バージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート プロセッサで処理する必要があります。 レポートを最新バージョンのレポート定義スキーマにアップグレードする場合、メイン レポートとサブレポートは同時に更新されることもされないこともあります。 レポートとそのサブレポートの間でバージョンが一致しないと、"サブレポートを処理できませんでした。" というメッセージが表示されます。  
  
 すべてのレポートを同一バージョンのレポート プロセッサで処理できるように、メイン レポートまたはサブレポートのいずれかを変更する必要があります。 レポートをアップグレードできない場合の原因については、「 [レポートのアップグレード](../../reporting-services/install-windows/upgrade-reports.md)」を参照してください。  
  
### <a name="verify-function-calls-are-visual-basic-and-not-sql"></a>関数呼び出しが SQL ではなく Visual Basic であることを確認する  
 リレーショナル データベースのクエリ テキストでは SQL 関数を使用できます。 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 関数はクエリ テキストで使用できません。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]では、 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 関数、System.Math 関数、System.String 関数、完全に修飾された [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 関数、またはカスタム コードやカスタム アセンブリで指定したカスタム関数を式内で使用できます。 式で SQL 関数は使用できません。  
  
 クエリ内および式内の関数呼び出しが有効であることを確認します。  
  
### <a name="cannot-compare-data-types-for-a-filter"></a>フィルターのデータ型を比較できない  
 フィルターの演算式では、フィルターの対象を定義するフィルター式とフィルター値は、比較できるように同じデータ型にする必要があります。 次のいずれかのエラーが表示された場合は、データ型が一致するようにフィールド式またはフィルター値を変更します。  
  
-   *\<report item name>* の *\<report item type>* の処理は実行できません。 データ型 *\<type>* と *\<type>* を比較できません。 *\<report item name>* によって返されたデータ型を確認してください。  
  
-   *\<property name>* を評価できませんでした。  
  
-   *\<property name>* を評価できませんでした。 次のエラーを含んでいるデータセット フィールドを参照しています。 *\<error string>* 。  
  
 詳細については、「 [データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)」を参照してください。  
  
### <a name="invalid-or-conflicting-scope-specification-in-an-aggregate-function-call"></a>集計関数呼び出しでの無効または競合するスコープの指定  
 Tablix セルの式に集計関数呼び出しを含める場合、レポート プロセッサでは、セルが属している最も内側のグループのスコープでその式を評価します。  
  
 特定のスコープの名前を集計関数に渡すこともできます。 スコープでは、データセットの名前、データ領域、またはデータ階層のより上位のスコープの名前を参照できます。 これは、次のメッセージに当てはまります。  
  
-   *\<report item type>* ' *\<report item name>* ' のスコープ " *\<scope name>* " が無効です。 スコープは現在のスコープであるか、または現在のスコープ内に含まれている必要があります。  
  
-   *\<report item type>* ' *\<report item name>* ' の *\<property name>* 式に集計関数では使用できないスコープ パラメーターがあります。 スコープのパラメーターは、含まれるグループの名前、含まれるデータ領域の名前、またはデータセットの名前のいずれかと同じ文字列の定数に設定する必要があります。  
  
 累計を計算する集計関数 (**Previous**、 **RunningValue**、または **RowNumber**) の場合、行グループ名または列グループ名をスコープのパラメーターに指定できますが、両方を指定することはできません。 これは、次のエラー メッセージに当てはまります。  
  
-   *\<report item type>* ' *\<report item name>* ' のデータ セルに使用されている **Previous**、**RunningValue**、または **RowNumber** 集計関数では、 *\<report item type>* の列と行両方のグループ化スコープが参照されています。 *\<report item type>* 内のすべての **Previous**、**RunningValue**、および **RowNumber** 集計関数のスコープのパラメーターでは、行のグループまたはデータ列のグループを参照できますが、両方を参照することはできません。  
  
 詳細については、「[合計、集計、および組み込みコレクションの式のスコープについて (レポート ビルダー 3.0 および SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)」および「[式での組み込みコレクションの使用 (レポート ビルダー 3.0 および SSRS)](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)」を参照してください。  
  
### <a name="default-dataset-scope-for-a-top-level-text-box"></a>最上位レベル テキスト ボックスの既定のデータセット スコープ  
 レポートに複数のデータセットがある場合、レポート デザイン画面に追加したテキスト ボックスの既定のスコープは使用できません。 スコープとしてデータセットの名前を含む式と、集計関数を使用してください。 たとえば、 `=First(Fields!FieldName.Value, "DataSet2")`のようにします。  
  
## <a name="see-also"></a>参照  
 [式 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [集計関数リファレンス &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)   
 [式の例 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [レポート データセット (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [一般的に使用されるフィルター (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md)   
 [データセット フィールド コレクション (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [レポート デザイナーでカスタム コードやアセンブリを式から参照する (SSRS)](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [Parameters コレクションの参照 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
