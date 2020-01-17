---
title: 集計関数リファレンス (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: db6542ee-02d0-4073-90e6-cba8f9510fbb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 243f895c22621c3f83fab38a5bab47d1f7b7b490
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893763"
---
# <a name="report-builder-functions---aggregate-functions-reference"></a>レポート ビルダー関数 - 集計関数リファレンス
  レポートに集計値を含めるには、式に組み込み集計関数を使用できます。 数値フィールドの既定の集計関数は SUM です。 式を編集して異なる組み込み集計関数を使用したり、異なるスコープを指定することもできます。 スコープにより、計算に使用するデータセットが識別されます。  
  
 レポート プロセッサではレポート データとレポート レイアウトが結合されるため、各レポート アイテムの式が評価されます。 レポートの各ページを表示すると、表示されたレポート アイテムに各式の結果が示されます。  
  
 次の表に、式に含めることのできる組み込み関数のカテゴリの一覧を示します。  
  
-   [組み込み集計関数](#CalculatingAggregates)  
  
-   [組み込みフィールド、コレクション、および集計関数に関する制限](#Restrictions)  
  
-   [入れ子集計に関する制限](#NestedRestrictions)  
  
-   [実行中の値の計算](#CalculatingRunningValues)  
  
-   [行数の取得](#RetrievingRowCounts)  
  
-   [別のデータセットの値の参照](#LookupFunctions)  
  
-   [並べ替え依存の値の取得](#RetrievingPostsortValues)  
  
-   [サーバー集計値の取得](#RetrievingServerAggregates)  
  
-   [再帰レベルの取得](#RetrievingRecursiveLevel)  
  
-   [スコープのテスト](#TestingforScope)  
  
 関数の有効なスコープを判断するには、各関数参照に関するトピックを参照してください。 詳細と例については、「 [合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="CalculatingAggregates"></a> 組み込み集計関数  
 次の組み込み関数は、既定のスコープまたは名前付きスコープ内の NULL 以外の一連の数値データの集約値を計算します。  
  
|**関数**|**[説明]**|  
|------------------|---------------------|  
|[Avg](../../reporting-services/report-design/report-builder-functions-avg-function.md)|式で指定された NULL 以外のすべての数値の平均を、指定されたスコープで評価して返します。|  
|[Count](../../reporting-services/report-design/report-builder-functions-count-function.md)|式で指定された NULL 以外の値の数を、指定されたスコープのコンテキストで評価して返します。|  
|[CountDistinct](../../reporting-services/report-design/report-builder-functions-countdistinct-function.md)|式で指定された NULL 以外の値が全部で何種類あるかを、指定されたスコープのコンテキストで評価して返します。|  
|[Max](../../reporting-services/report-design/report-builder-functions-max-function.md)|指定されたスコープのコンテキストで、式で指定された NULL 以外のすべての数値の中から最大値を返します。 グラフの軸の最大値を指定してスケールを制御する場合は、この関数を使用できます。|  
|[Min](../../reporting-services/report-design/report-builder-functions-min-function.md)|指定されたスコープのコンテキストで、式で指定された NULL 以外のすべての数値の中から最小値を返します。 グラフの軸の最小値を指定してスケールを制御する場合は、この関数を使用できます。|  
|[StDev](../../reporting-services/report-design/report-builder-functions-stdev-function.md)|式で指定された NULL 以外のすべての数値の標準偏差を、指定されたスコープで評価して返します。|  
|[StDevP](../../reporting-services/report-design/report-builder-functions-stdevp-function.md)|式で指定された NULL 以外のすべての数値の母集団標準偏差を、指定されたスコープのコンテキストで評価して返します。|  
|[Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md)|式で指定された NULL 以外のすべての数値の合計を、指定されたスコープで評価して返します。|  
|[Union](../../reporting-services/report-design/report-builder-functions-union-function.md)|式で指定された NULL 以外のすべての空間データの値 ( **SqlGeometry** 型または **SqlGeography** 型) の和集合を、指定されたスコープで評価して返します。|  
|[Var](../../reporting-services/report-design/report-builder-functions-var-function.md)|式で指定された NULL 以外のすべての数値の分散を、指定されたスコープで評価して返します。|  
|[VarP](../../reporting-services/report-design/report-builder-functions-varp-function.md)|式で指定された NULL 以外のすべての数値の母集団に対する分散を、指定されたスコープのコンテキストで評価して返します。|  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン")トップに戻る  
  
##  <a name="Restrictions"></a> 組み込みフィールド、コレクション、および集計関数に関する制限  
 以下の表には、グローバル組み込みコレクションの参照を含む式を追加できるレポートの場所に関する制限をまとめています。  
  
|レポート内の場所|フィールド|パラメーター|ReportItems|PageNumber<br /><br /> TotalPages|DataSource<br /><br /> DataSet|変数:|RenderFormat|  
|------------------------|------------|----------------|-----------------|-------------------------------|----------------------------|---------------|------------------|  
|ページ ヘッダー<br /><br /> ページ フッター|はい|はい|最大 1<br /><br /> 注 1|はい|はい|はい|はい|  
|本文|はい<br /><br /> 注 2|はい|現在のスコープまたはコンテナー スコープのアイテムのみ<br /><br /> 注 3|いいえ|はい|はい|はい|  
|レポート パラメーター|いいえ|リスト内で先に出現するパラメーターのみ<br /><br /> 注 4|いいえ|いいえ|いいえ|いいえ|いいえ|  
|フィールド|はい|はい|いいえ|いいえ|いいえ|いいえ|いいえ|  
|クエリ パラメーター|いいえ|はい|いいえ|いいえ|いいえ|いいえ|いいえ|  
|グループ式|はい|はい|いいえ|いいえ|はい|いいえ|いいえ|  
|並べ替え式|はい|はい|いいえ|いいえ|はい|はい<br /><br /> 注 5|いいえ|  
|[フィルター式]|はい|はい|いいえ|いいえ|はい|はい<br /><br /> 注 6|いいえ|  
|コード|いいえ|はい<br /><br /> 注 7|いいえ|いいえ|いいえ|いいえ|いいえ|  
|レポートの言語|いいえ|はい|いいえ|いいえ|いいえ|いいえ|いいえ|  
|変数:|はい|はい|いいえ|いいえ|はい|現在のスコープかコンテナー スコープ|いいえ|  
|集計|はい|はい|ページ ヘッダー/ページ フッター内のみ|レポート アイテムの集計内のみ|はい|いいえ|いいえ|  
|参照関数|はい|はい|はい|いいえ|はい|いいえ|いいえ|  
  
-   **注 1:** ReportItems は、表示されるレポート ページに存在する必要があります。そうでない場合は値が Null になります。 レポート アイテムの表示が式に依存し、その式が False に評価される場合、ページにはレポート アイテムが存在しません。  
  
-   **注 2:** フィールド参照がグループ スコープ内で使用されており、このフィールド参照がグループ式に含まれていない場合、スコープに 1 つしか値がない場合を除いて、フィールドの値は未定義になります。 値を指定するには、First または Last とグループ スコープを使用します。  
  
-   **注 3:** ReportItems の参照を含む式は、同じグループ スコープまたはコンテナー グループ スコープ内の他の ReportItems の値を指定できます。  
  
-   **注 4:** 先に出現するパラメーターのプロパティ値が Null の場合があります。  
  
-   **注 5:** メンバーの並べ替えのみ。 データ領域の並べ替え式には使用できません。  
  
-   **注 6:** メンバーのフィルターのみ。 データ領域またはデータセットのフィルター式には使用できません。  
  
-   **注 7:** コード ブロックが処理されるまでパラメーターのコレクションは初期化されません。そのため初期化時のパラメーターの制御にはメソッドを使用できません。  
  
-   **注 8:** Count および CountDistinct を除くすべての集計のデータ型は、すべての値で同じデータ型、または null である必要があります。  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン")トップに戻る  
  
##  <a name="NestedRestrictions"></a> 入れ子集計に関する制限  
 以下の表には、集計関数に入れ子集計として別の集計関数を指定する際の制限をまとめています。  
  
|コンテキスト|RunningValue|RowNumber|First<br /><br /> Last|Previous|Sum およびその他の事前並べ替え関数|ReportItem の集計|参照関数|集計関数|  
|-------------|------------------|---------------|--------------------|--------------|-------------------------------------|---------------------------|----------------------|------------------------|  
|Running Value|いいえ|いいえ|いいえ|いいえ|はい|いいえ|はい|いいえ|  
|First<br /><br /> Last|いいえ|いいえ|いいえ|いいえ|はい|いいえ|いいえ|いいえ|  
|Previous|はい|はい|はい|いいえ|はい|いいえ|はい|いいえ|  
|Sum およびその他の事前並べ替え関数|いいえ|いいえ|いいえ|いいえ|はい|いいえ|はい|いいえ|  
|ReportItem の集計|いいえ|いいえ|いいえ|いいえ|いいえ|いいえ|いいえ|いいえ|  
|参照関数|はい|はい<br /><br /> 注 1|はい<br /><br /> 注 1|はい<br /><br /> 注 1|はい<br /><br /> 注 1|はい<br /><br /> 注 1|いいえ|いいえ|  
|集計関数|いいえ|いいえ|いいえ|いいえ|いいえ|いいえ|いいえ|いいえ|  
  
-   **注 1:** 集計関数は、集計に参照関数が含まれていない場合に、参照関数の *Source* 式内のみに使用できます。 集計関数は、参照関数の *Destination* 式または *Result* 式内には使用できません。  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン")トップに戻る  
  
##  <a name="CalculatingRunningValues"></a> 実行中の値の計算  
 次の組み込み関数は、データのセットの実行中の値を計算します。 **RowNumber** は、コンテナー スコープ内の行ごとに増加するカウントの実行中の値を返す点で、 **RunningValue** に似ています。 これらの関数のスコープのパラメーターでは、カウントが再開されるタイミングを制御するコンテナー スコープを指定する必要があります。  
  
|**関数**|**[説明]**|  
|------------------|---------------------|  
|[RowNumber](../../reporting-services/report-design/report-builder-functions-rownumber-function.md)|指定されたスコープの実行中の行数を返します。 **RowNumber** 関数では、カウントが 0 ではなく 1 から再開されます。|  
|[RunningValue](../../reporting-services/report-design/report-builder-functions-runningvalue-function.md)|式で指定された NULL 以外のすべての数値の実行中の集計を、指定されたスコープに対して評価して返します。|  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン")トップに戻る  
  
##  <a name="RetrievingRowCounts"></a> 行数の取得  
 次の組み込み関数は、指定されたスコープの行数を計算します。 この関数を使用すると、NULL 値の行を含め、すべての行がカウントされます。  
  
|**関数**|**[説明]**|  
|------------------|---------------------|  
|[CountRows](../../reporting-services/report-design/report-builder-functions-countrows-function.md)|NULL 値の行を含めて、指定されたスコープ内の行数を返します。|  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン")トップに戻る  
  
##  <a name="LookupFunctions"></a> 別のデータセットの値の参照  
 次の参照関数では、指定されたデータセットから値を取得します。  
  
|**関数**|**[説明]**|  
|------------------|---------------------|  
|[Lookup 関数](../../reporting-services/report-design/report-builder-functions-lookup-function.md)|データセットから、指定された式に対応する値を返します。|  
|[LookupSet 関数](../../reporting-services/report-design/report-builder-functions-lookupset-function.md)|データセットから、指定された式に対応する値のセットを返します。|  
|[Multilookup 関数](../../reporting-services/report-design/report-builder-functions-multilookup-function.md)|名前と値のペアを含むデータセットから、名前のセットに最初に一致した値のセットを返します。|  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン")トップに戻る  
  
##  <a name="RetrievingPostsortValues"></a> 並べ替え依存の値の取得  
 次の組み込み関数は、指定されたスコープ内の最初、最後、または前の値を返します。 これらの関数は、データ値の並べ替え順序に依存します。 たとえば、これらの関数を使用すると、ページの最初の値と最後の値を検出して、辞書形式のページ ヘッダーを作成することができます。 また、 **Previous** を使用すると、特定のスコープ内のある行の値と前の行の値を比較し、テーブルの前年比の比率を検出する処理などを行うことができます。  
  
|**関数**|**[説明]**|  
|------------------|---------------------|  
|[First](../../reporting-services/report-design/report-builder-functions-first-function.md)|指定された式の指定されたスコープの最初の値を返します。|  
|[Last](../../reporting-services/report-design/report-builder-functions-last-function.md)|指定された式の指定されたスコープの最後の値を返します。|  
|[Previous](../../reporting-services/report-design/report-builder-functions-previous-function.md)|アイテムの、指定されたスコープ内の直前のインスタンスに対応する値または指定された集計値を返します。|  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン")トップに戻る  
  
##  <a name="RetrievingServerAggregates"></a> サーバー集計値の取得  
 次の組み込み関数は、データ プロバイダーからカスタム集計を取得します。 たとえば、データ ソースの種類に [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を使用すると、グループ ヘッダーで使用するために、データ ソース サーバーで計算された集計を取得することができます。  
  
|**関数**|**[説明]**|  
|------------------|---------------------|  
|[Aggregate](../../reporting-services/report-design/report-builder-functions-aggregate-function.md)|データ プロバイダーの定義に従い、指定された式のカスタムの集計を返します。|  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン")トップに戻る  
  
##  <a name="TestingforScope"></a> スコープのテスト  
 次の組み込み関数は、レポート アイテムの現在のコンテキストをテストし、それが特定のスコープのメンバーかどうかを確認します。  
  
|機能|[説明]|  
|--------------|-----------------|  
|[InScope](../../reporting-services/report-design/report-builder-functions-inscope-function.md)|アイテムの現在のインスタンスが、指定したスコープ内にあるかどうかを示します。|  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン")トップに戻る  
  
##  <a name="RetrievingRecursiveLevel"></a> 再帰レベルの取得  
 次の組み込み関数は、再帰型階層が処理されたときの現在のレベルを取得します。 テキスト ボックスの **Padding** プロパティに対してこの関数の結果を使用して、再帰グループの階層構造のインデント レベルを制御できます。 詳細については、「[複数の再帰型階層グループの作成 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)」を参照してください。  
  
|機能|[説明]|  
|--------------|-----------------|  
|[レベル](../../reporting-services/report-design/report-builder-functions-level-function.md)|再帰型階層の現在の深さのレベルを返します。|  
  
 ![[トップに戻る] リンクで使用される矢印アイコン](https://docs.microsoft.com/analysis-services/analysis-services/instances/media/uparrow16x16.gif "[トップに戻る] リンクで使用される矢印アイコン")トップに戻る  
  
## <a name="see-also"></a>参照  
 [レポートでの式の使用 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [式の例 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
