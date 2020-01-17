---
title: 複数の図形グラフでの色の統一 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d52f68e9-2ba7-4bff-9053-4089e5164ab4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d9e7b846d17fd6ad86edc45ff7dd4251c098ae1a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65578458"
---
# <a name="specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs"></a>複数の図形グラフでの色の統一 (レポート ビルダーおよび SSRS)
  改ページ調整されたレポートの図形以外のグラフの場合、 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] によって、グラフの系列のインデックスに基づいてパレットから新しい色が選択されます。 たとえば、グラフの最初の系列は、パレット内の最初の色にマップされます。 しかし、この動作は図形グラフでは異なります。 図形グラフの場合、パレットの各色は、データセット内のデータ ポイントにマップされます。 たとえば、データ ポイント 1 はパレットの最初の色にマップされ、データ ポイント 2 は 2 番目の色にマップされます。  
  
 値がないデータ ポイントは、図形グラフに表示されません。 したがって、そのデータ ポイントへの色のマッピングはスキップされます。 たとえば、ポイント 2 の値が 0 の場合、ポイント 1 にパレットの最初の色がマップされ、ポイント 3 にパレットの 2 番目の色がマップされます。 空のポイントを描画する必要がない場合、円グラフのデータセットの空のポイントにパレット色を使用する必要はないので、この方法は便利です。  
  
 その弊害として、1 つのレポートに複数の円グラフを表示する場合、同じカテゴリ グループのデータ ポイントが異なる色で表示されることがあります。 この問題を解決するには、個々のデータ値ではなく、カテゴリ グループにマップするように個々の色を定義する必要があります。 この方法は、図形グラフがテーブルまたはマトリックスのスパークラインであるか、レポート自体の図形グラフであるかによって異なります。  
  
 凡例は系列に接続されるので、系列に指定した色が自動的に凡例に表示されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-consistent-colors-across-multiple-sparkline-shape-charts-in-a-table-or-matrix"></a>テーブルまたはマトリックス内の複数のスパークライン図形グラフで色を統一するには  
  
1.  グラフをクリックして、グラフ データ ペインを表示します。  
  
2.  **[カテゴリ グループ]** 領域内のカテゴリを右クリックし、 **[カテゴリ グループのプロパティ]** をクリックします。  
  
3.  [全般] タブの **[グループの同期]** ボックスで、色を同期させるカテゴリの名前をクリックし、 **[OK]** をクリックします。  
  
## <a name="to-specify-consistent-colors-across-multiple-shape-charts"></a>複数の図形グラフで色を統一するには  
  
1.  レポート本文の外側を右クリックし、 **[レポートのプロパティ]** を選択します。  
  
2.  **[コード]** のテキスト ボックスに次のコードを入力します。  
  
    ```  
    Private colorPalette As String() = {"Color1", "Color2", "Color3"}  
    Private count As Integer = 0  
    Private mapping As New System.Collections.Hashtable()  
    Public Function GetColor(ByVal groupingValue As String) As String  
        If mapping.ContainsKey(groupingValue) Then  
            Return mapping(groupingValue)  
        End If  
        Dim c As String = colorPalette(count Mod colorPalette.Length)  
        count = count + 1  
        mapping.Add(groupingValue, c)  
        Return c  
    End Function  
    ```  
  
    > [!NOTE]  
    >  "Color1" という文字列を目的の色で置き換える必要があります。 "Red" などの名前付きの色を使用することも、"#FFFFFF" (黒) などの色を表す 6 桁の 16 進数値を使用することもできます。 3 色以上定義する場合、配列内の色の数が図形グラフのポイントの数に一致するように色の配列を拡張する必要があります。 名前付きの色または色の 16 進数表現を含む文字列値のコンマ区切りリストを指定して、配列に新しい色を追加できます。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  図形グラフ上を右クリックし、 **[系列のプロパティ]** を選択します。  
  
5.  **[塗りつぶし]** の **式** ( *[fx]* ) ボタンをクリックして、 **Color** プロパティの式を編集します。  
  
6.  次の式を入力します。ここで、"MyCategoryField" は、 **[カテゴリ グループ]** 領域に表示されるフィールドです。  
  
    ```  
    =Code.GetColor(Fields!MyCategoryField)  
    ```  
  
## <a name="see-also"></a>参照  
 [グラフの系列の色の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [グラフへの傾斜、エンボス、およびテクスチャのスタイルの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/chart-effects-add-bevel-emboss-or-texture-report-builder.md)   
 [パレットを使用したグラフの色の定義 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs.md)   
 [空のポイントのグラフへの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)   
 [図形グラフ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/shape-charts-report-builder-and-ssrs.md)   
 [同じデータセットへの複数のデータ領域のリンク &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)   
 [入れ子になったデータ領域 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)   
 [スパークラインとデータ バー (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
