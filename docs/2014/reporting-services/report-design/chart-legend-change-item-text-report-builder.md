---
title: 凡例アイテムのテキストの変更 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9e82fa34-17ed-494f-b25d-03dcc353a21f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3e34f0a34030dab62a876a41043dc4c4f4c86f0c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106312"
---
# <a name="change-the-text-of-a-legend-item-report-builder-and-ssrs"></a>凡例アイテムのテキストの変更 (レポート ビルダーおよび SSRS)
  グラフの [値] 領域にフィールドを配置すると、このフィールドの名前を含む凡例アイテムが自動的に生成されます。 すべての凡例アイテムは、グラフ上の個々の系列に接続されています。ただし、図形グラフの場合は例外で、凡例は個々の系列ではなく個々のデータ ポイントに接続されています。  
  
 図形グラフで、凡例アイテムのテキストを変更して個々のデータ ポイントの詳細を表示できます。 たとえば、データ ポイントの値を凡例にパーセンテージで表示する場合、`#PERCENT` などのキーワードを使用できます。 .NET Framework 形式のコードをキーワードと組み合わせて追加し、数値と日付の形式を適用できます。 キーワードの詳細については、「[グラフでのデータ ポイントの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)」を参照してください。  
  
 ![シャープ チャート](../media/sharpchart.png "シャープ チャート")  
  
 図形以外のグラフで、凡例アイテムのテキストを変更できます。 たとえば、系列名が "Series1" の場合、"Sales for 2008" などわかりやすい名前に変更できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-modify-the-text-that-appears-in-the-legend-on-a-shape-chart"></a>図形グラフの凡例に表示されるテキストを変更するには  
  
1.  系列を右クリックするか、 **[値]** 領域のフィールドを右クリックし、 **[系列のプロパティ]** をクリックします。  
  
2.  **[凡例]** をクリックし、 **[凡例のユーザー定義テキスト]** ボックス内をクリックして、キーワードを入力します。  
  
 次の表は、 **[凡例のユーザー定義テキスト]** プロパティに使用するグラフに固有のキーワードの例を示します。 キーワードの詳細については、「[グラフでのデータ ポイントの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)」を参照してください。  
  
|Keyword|説明|凡例のテキストとして表示される内容の例|  
|-------------|-----------------|---------------------------------------------------|  
|`#PERCENT{P1}`|合計値のパーセンテージを小数点以下 1 桁に表示します。|85.0%|  
|`#VALY`|データ フィールドの実際の数値を表示します。|17000|  
|`#VALY{C2}`|データ フィールドの実際の数値を小数点以下 2 桁の通貨として表示します。|$17000.00|  
|`#AXISLABEL (#PERCENT{P0})`|カテゴリ フィールドのテキスト表現が表示され、後ろに各カテゴリのグラフに対するパーセンテージが表示されます。|Michael Blythe (85%)|  
  
> [!NOTE]  
>  **[系列グループ]** 領域にフィールドが指定されていない場合、#AXISLABEL キーワードは実行時にのみ評価されます。  
  
### <a name="to-modify-the-text-that-appears-in-the-legend-on-a-non-shape-chart"></a>図形以外のグラフで凡例に表示されるテキストを変更するには  
  
1.  系列を右クリックするか、 **[値]** 領域のフィールドを右クリックし、 **[系列のプロパティ]** をクリックします。  
  
2.  **[凡例]** をクリックし、 **[凡例のユーザー定義テキスト]** ボックス内をクリックして、凡例ラベルを入力します。 シリーズは、テキストで更新されます。  
  
## <a name="see-also"></a>関連項目  
 [グラフの凡例の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](chart-legend-formatting-report-builder.md)   
 [グラフの系列の色の書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [グラフの凡例項目を非表示にする &#40;レポート ビルダーおよび SSRS&#41;](chart-legend-hide-items-report-builder.md)  
  
  
