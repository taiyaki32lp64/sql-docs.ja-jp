---
title: 既定のテーブル名の変更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ddd97483-a76d-43c1-8b40-fc7cc57fb0c2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b6e43196f5bc318630a52073e22969dc58a0e64a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079231"
---
# <a name="modifying-default-table-names"></a>既定のテーブル名の変更
  データ ソース ビューのオブジェクトの **FriendlyName** プロパティ値を変更することで、オブジェクトをわかりやすく、また使いやすくすることができます。  
  
 この実習では、データ ソース ビューの各テーブルの表示名から "**Dim**" プレフィックスと "**Fact**" プレフィックスを削除して、わかりやすい名前にします。 これにより、次のレッスンで定義するキューブ オブジェクトとディメンション オブジェクトがわかりやすく (使いやすく) なります。  
  
> [!NOTE]  
>  より簡単に使用できるようにするため、列の表示名を変更して、計算列を定義し、データ ソース ビューのテーブルやビューを結合します。  
  
### <a name="to-modify-the-default-name-of-a-table"></a>テーブルの既定の名前を変更するには  
  
1.  **データ ソース ビュー デザイナー** の **[テーブル]** ペインで **FactInternetSales** テーブルを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  Microsoft Visual Studio ウィンドウの右側の [プロパティ] ウィンドウが表示されていない場合は、[プロパティ] ウィンドウのタイトル バーにある **[自動的に隠す]** ボタンをクリックして、[プロパティ] ウィンドウが常に開いたままになるようにします。  
  
     データ ソース ビューの各テーブルのプロパティを変更するときは、[プロパティ] ウィンドウを開いたままにしておくと便利です。 **[自動的に隠す]** ボタンをクリックしてウィンドウを開いたまま固定しておかないと、 **ダイアグラム** ペイン内の別のオブジェクトをクリックしたときに [プロパティ] ウィンドウが閉じてしまいます。  
  
3.  変更、 **FriendlyName**プロパティを**FactInternetSales**オブジェクトを *`InternetSales`* します。  
  
     **FriendlyName** 以外のセルをクリックすると、変更が適用されます。 次のレッスンでは、このファクト テーブルを基にしてメジャー グループを定義します。 このレッスンで表示名を変更したので、次に作成するファクト テーブルの名前も FactInternetSales ではなく InternetSales になります。  
  
4.  **[テーブル]** ペインで **[DimProduct]** をクリックします。 [プロパティ] ウィンドウで変更、 **FriendlyName**プロパティを *`Product`* します。  
  
5.  データ ソース ビューの他のテーブルについても、同じ方法で **FriendlyName** プロパティを変更します。つまり、**Dim**プレフィックスを削除します。  
  
6.  操作が完了したら、 **[自動的に隠す]** ボタンをクリックして、[プロパティ] ウィンドウを再び非表示にします。  
  
7.  **[ファイル]** メニューまたは [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]のツール バーで、 **[すべてを保存]** をクリックして、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial プロジェクトに対するこの時点までの変更を保存します。 ここでチュートリアルを終了しても、後でこの続きから再開できます。  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 2:定義と、キューブの配置](lesson-2-defining-and-deploying-a-cube.md)  
  
## <a name="see-also"></a>参照  
 [多次元モデルのデータ ソース ビュー](multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [データ ソース ビューのプロパティの変更 &#40;Analysis Services&#41;](multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md)  
  
  
