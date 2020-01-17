---
title: ReportItems コレクションの参照 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: edc0c75f-0530-4e6d-85aa-3385301bfd00
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 24a50de92a2b182295abc926c98358fa56e2f379
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581765"
---
# <a name="built-in-collections---reportitems-collection-references-report-builder"></a>組み込みコレクション - ReportItems コレクションの参照 (レポート ビルダー)
  組み込みコレクション **ReportItems** は、データ領域の行などのレポート アイテムのテキスト ボックスや、レポート デザイン画面上のテキスト ボックスのセットです。 **ReportItems** コレクションには、ページ ヘッダー、ページ フッター、またはレポート本文の現在のスコープにあるテキスト ボックスが含まれています。 このコレクションは、レポート プロセッサおよびレポート レンダラーによって実行時に決定されます。 ユーザーがレポートのページを表示する際には、レポート プロセッサによってレポート データとレポート アイテムのレイアウト要素が連続的に結合されますが、これに伴って現在のスコープが変化します。 組み込みコレクション **ReportItems** を使用すると、各ページの最初のアイテムと最後のアイテムを表示する辞書形式のページ ヘッダーを作成できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-the-reportitems-value-property"></a>ReportItems の Value プロパティの使用  
 **ReportItems** コレクション内のアイテムに設定されるプロパティは、Value だけです。 **ReportItems** アイテムの値を使用すると、レポート内の別のフィールドのデータを表示または計算できます。 現在のテキスト ボックスの値にアクセスするには、 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] に組み込まれたグローバルの Me.Value を使用するか、単なる Value を使用します。 First 関数や集計関数などのレポート関数では、完全修飾された構文を使用してください。  
  
 例:  
  
-   テキスト ボックスで次の式を使用すると、 **という名前の** ReportItem `Textbox1`テキスト ボックスの値が表示されます。  
  
     `=ReportItems!Textbox1.Value`  
  
-   **ReportItem** テキスト ボックスの Color プロパティで次の式を使うと、値が 0 より大きい場合は黒、それ以外の場合は赤でテキストが表示されます。  
  
     `=IIF(Me.Value > 0,"Black","Red")`  
  
-   ページ ヘッダーまたはページ フッターのテキスト ボックスで次の式を使用すると、表示レポートのページごとに、 `LastName`という名前のテキスト ボックスの最初の値が表示されます。  
  
     `=First(ReportItems("LastName").Value)`  
  
## <a name="dictionary-style-page-header-expressions"></a>辞書形式のページ ヘッダー式  
 そのページ上の最初の顧客と最後の顧客を表示するページ ヘッダーを作成することができます。 ページ ヘッダーのテキスト ボックスでは、式の中で組み込みコレクション **ReportItems** を 1 回しか参照できないため、最初の顧客名用 (`=First(ReportItems!textboxLastName.Value`) と最後の顧客名用 (`=Last(ReportItems!textboxLastName.Value`) に 2 つのテキスト ボックスをページ ヘッダーに追加する必要があります。  
  
 ページ ヘッダー セクションやページ フッター セクションでは、 **ReportItems** コレクションのメンバーとして使用できるのは、現在のページのテキスト ボックスのみです。 たとえば、 `ReportItems!textboxLastName.Value` が、複数ページにわたるデータ領域の最初のページにしか表示されないテキスト ボックスを参照している場合、最初のページでは値が表示されますが、その他すべてのページでは **#Error** と表示され、式が記述したとおりに評価できなかったことを示します。  
  
## <a name="scope-for-the-reportitems-collection"></a>ReportItems コレクションのスコープ  
 レポートが処理されると、レポート本文内またはデータ領域内の各テキスト ボックスは、そのデータセット、データ領域、およびグループの関連付けのコンテキストで評価されます。 **ReportItems** コレクションへの参照のスコープは、現在のスコープまたは現在のスコープより上位の場所です。  
  
 たとえば、親グループの行の中にあるテキスト ボックスには、子グループの行の中にあるテキスト ボックスの名前を参照する式を含めることができません。 このような式は、子行のテキスト ボックスがスコープ外にあるため、レポート内の値に解決されません。 詳細については、「 [集計関数リファレンス (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [式で使用される組み込みコレクション &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [式の例 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Reporting Services の改ページ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [データのフィルター、グループ化、および並べ替え &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
