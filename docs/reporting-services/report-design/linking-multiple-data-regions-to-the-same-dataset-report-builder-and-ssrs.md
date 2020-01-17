---
title: 同じデータセットへの複数のデータ領域のリンク (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 90c94a91-8fb2-42cb-b998-563691f30d2d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7c67ddcb48847d3618c9544c50868b555e263fd7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580148"
---
# <a name="linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs"></a>同じデータセットへの複数のデータ領域のリンク (レポート ビルダーおよび SSRS)

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のページ分割された 1 つのレポートに複数のデータ領域を追加し、同じレポート データセットのデータをさまざまな形式で表示することができます。 たとえば、データをテーブルとして表示し、さらにグラフで表示することができます。 そのためには、適切なフィルター式、並べ替え式、およびグループ式として同一の式とスコープを使用する必要があります。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 グラフとテーブル、またはマトリックスを使用して同じデータを表示する場合、テーブルと図形グラフ、マトリックスと面グラフ、横棒グラフ、および縦棒グラフの類似点を理解することが役に立ちます。 1 つの行グループで構成されるテーブルは、円グラフとして簡単に表示できます。 複数の行グループを追加する場合は、数種類のグラフの中から、入れ子構造のグループを最も効果的に表示できるグラフを選択できます。 入れ子構造の行グループを円グラフに追加すると、円グラフのスライスの数が増えます。 親グループと子グループを組み合わせたグループ インスタンスの数が 1 つの円グラフで表示するには多すぎるかどうかは、ユーザーが判断する必要があります。 円グラフで小さいスライスとして表示される複数のグループ値の場合は、特定のしきい値以下のすべての値は 1 つのスライスとして表示されるようにプロパティを設定できます。 詳細については、「[円グラフの小さいスライスをまとめる](../../reporting-services/report-design/collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)」を参照してください。  
  
 複数の行グループを含むテーブルは、複数のカテゴリ グループのある縦棒グラフとして表示できます。 詳細については、「[マトリックスとグラフでの同じデータの表示](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md)」を参照してください。 同じレポート データセットを異なる形式で表示するテーブルとグラフの例については、AdventureWorks サンプル レポートの Product Line Sales レポートを参照してください。 このレポートでは、テーブルとグラフがどちらも同じデータセットにリンクしているので、Top Employees テーブルで Employee Name の対話型の並べ替えボタンをクリックすると、Top Employees グラフにも新しい並べ替え順序が反映されます。 このサンプル レポートおよびその他のサンプル レポートをダウンロードする方法の詳細については、 [レポート ビルダーおよびレポート デザイナーのサンプル レポート](https://go.microsoft.com/fwlink/?LinkId=198283)に関するページを参照してください。  
  
 複数の行および列グループを含むマトリックスの表示は、カテゴリ グループと系列グループの両方がある面グラフ、横棒グラフ、または縦棒グラフを使用すると、最も効果的です。 マトリックスの列グループとグラフのカテゴリ グループに同じグループ式を使用し、マトリックスの行グループとグラフの系列グループに同じグループ式を使用します。 グループ インスタンスの数は、グラフの読みやすさに影響することに留意する必要があります。 範囲値に基づきグループを定義すると、レポート内のグループ インスタンスの数を減らすことができます。 詳細については、「[グループ式の例](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="next-steps"></a>次の手順

[グラフ](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[テーブル、マトリックス、および一覧](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
[入れ子になったデータ領域](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
