---
title: 日付または通貨として軸ラベルを書式設定する (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e9a01a74-2f51-4b35-be3a-a6138568f6cf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d328f58da2be026046fc2688a4959b37f5ff7d65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105881"
---
# <a name="format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs"></a>日付または通貨として軸ラベルを書式設定する (レポート ビルダーおよび SSRS)
  適切に書式設定された DateTime 値を軸に表示すると、これらの値が日数として自動的にグラフに表示されます。 月や時間の間隔など、X 軸の日付や期間を指定するには、軸ラベルの書式を設定し、軸間隔の種類を有効な日付または期間に設定する必要があります。  
  
> [!NOTE]  
>  縦棒グラフおよび散布図の横軸 (X 軸) はカテゴリ軸です。 横棒グラフの縦軸 (Y 軸) もカテゴリ軸です。  
  
 期間を適切に書式設定するには、X 軸に表示される値が <xref:System.DateTime> データ型に評価される必要があります。 フィールドに <xref:System.String>のデータ型が設定されている場合、グラフでは間隔が日付や時間として計算されません。 グラフ要素の詳細については、「 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)」を参照してください。  
  
 数値を Y 軸に追加した場合、既定では、グラフに数値が表示されるまで書式が設定されません。 数値フィールドが売上額の場合、グラフを読みやすくするために、数値を通貨として書式設定することを検討してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-format-x-axis-labels-as-monthly-intervals"></a>X 軸のラベルの間隔を月単位に書式設定するには  
  
1.  グラフの横軸 (X 軸) を右クリックし、 **[横軸のプロパティ]** を選択します。  
  
2.  **[横軸のプロパティ]** ダイアログ ボックスで、 **[数値]** を選択します。  
  
3.  **[カテゴリ]** ボックスの一覧で、 **[日付]** を選択します。 **[種類]** ボックスの一覧で、X 軸のラベルに適用する日付書式を選択します。  
  
4.  **[軸のオプション]** を選択します。  
  
5.  **[間隔]** で、「 **1**」と入力します。 **[間隔の種類]** プロパティで、 **[月]** を選択します。  
  
    > [!NOTE]  
    >  間隔の種類を指定しない場合、グラフでは日単位の間隔が計算されます。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-format-y-axis-labels-using-a-currency-format"></a>通貨の書式を使用して Y 軸ラベルを書式設定するには  
  
1.  グラフの縦軸 (Y 軸) を右クリックし、 **[縦軸のプロパティ]** を選択します。  
  
2.  **[縦軸のプロパティ]** ダイアログ ボックスで、 **[数値]** を選択します。  
  
3.  **[カテゴリ]** ボックスの一覧で、 **[通貨]** を選択します。 **[記号]** ボックスの一覧で、Y 軸ラベルに適用する通貨書式を選択します。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [グラフの軸ラベルの書式設定 (レポート ビルダーおよび SSRS)](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [グラフの書式設定 (レポート ビルダーおよび SSRS)](formatting-a-chart-report-builder-and-ssrs.md)   
 [対数スケールの指定 &#40;レポート ビルダーおよび SSRS&#41;](specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [軸の間隔の指定 &#40;レポート ビルダーおよび SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md)  
  
  
