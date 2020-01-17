---
title: 対話的な並べ替え (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 00cafed5-1a3c-4ce0-a1fb-ff1e2613f495
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d3f379c104b5b957fba197f9ed9317b2d5b23f16
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580188"
---
# <a name="interactive-sort-report-builder-and-ssrs"></a>対話的な並べ替え (レポート ビルダーおよび SSRS)
  対話的な並べ替えボタンを追加すると、ユーザーがテーブルの行またはマトリックスの行と列を昇順および降順で並べ替えることができるようになります。 対話的な並べ替えの最も一般的な使用方法は、各列ヘッダーに並べ替えボタンを追加することです。 これにより、ユーザーは並べ替えの基準となる列を選択できます。  
  
 ただし、対話的な並べ替えボタンは、列ヘッダーだけでなく任意のテキスト ボックスにも追加できます。 たとえば、行グループの外側にある行のテキスト ボックスの場合、親グループ行または列、子グループ行または列、あるいは詳細行または列の並べ替えを指定できます。 複数のフィールドを 1 つのグループ式にまとめて、複数のフィールドを基準にして並べ替えることもできます。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 対話的な並べ替えを追加する場合、次の項目を指定する必要があります。  
  
-   **並べ替え対象:** 行または列。  
  
-   **並べ替えの基準:** テーブル列に表示されるフィールド、 または表示されないフィールド。  
  
-   **並べ替えを行うコンテキスト:** たとえば、行グループに関連付けられた行、列グループに関連付けられた列、詳細行、親グループ内の子グループ、親グループと子グループの両方などを並べ替えることができます。  
  
-   **並べ替えボタンを追加するテキスト ボックス:** 列ヘッダーまたはグループ行ヘッダー。  
  
-   **複数のデータ領域の並べ替えを同期するかどうか:** ユーザーが並べ替え順序を切り替えたとき、同じ祖先を持つ他のデータ領域も並べ替えられるようにレポートをデザインできます。  
  
 詳細な手順については、「 [テーブルまたはマトリックスへの対話的な並べ替えの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)」を参照してください。  
  
 対話型の並べ替えボタンを使用して実現できる効果を次の表にまとめます。  
  
|操作|並べ替え対象|並べ替えボタンを追加する場所|並べ替え基準|並べ替えの範囲|  
|------------|------------------|----------------------------------|---------------------|----------------|  
|グループのないテーブルの詳細行を並べ替える|詳細|列ヘッダー|この列にバインドされたデータセット フィールド|データ領域|  
|マトリックスの最上位レベルのグループ インスタンスを並べ替える|グループ|列ヘッダー|親グループのグループ式|データ領域|  
|テーブル内の子グループの詳細行を並べ替える|詳細|子グループのヘッダー行|並べ替えの基準となるデータセット フィールド|子グループ|  
|テーブル内の複数の行グループおよび詳細行の行を並べ替える|グループ (グループ式を再定義する必要があります)|列ヘッダー|並べ替えの基準となるデータセット フィールドの集計|データ領域|  
|複数のデータ領域の並べ替え順序を同期する|グループ|通常、列ヘッダー|グループ式|データセット|  
  
 対話的な並べ替えは、すべてのデータ領域およびグループの並べ替え式が適用された後に適用されます。 詳細については、「 [データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="adding-interactive-sort-for-multiple-groups"></a>複数のグループの対話的な並べ替えの追加  
 入れ子になった行グループがそれぞれ 1 つのデータセット フィールドに基づいているテーブルでは、親グループの値、子グループの値、または詳細行を並べ替える対話的な並べ替えボタンを追加できます。 ただし、ユーザーが何度もクリックしなくても親グループの値と子グループの値の両方でテーブルを並べ替えることができるようにすることもできます。  
  
 それには、複数のフィールドを組み合わせる式に基づいてグループ化するようにテーブルをデザインし直す必要があります。 たとえば、在庫数を含むデータセットで、元のテーブルがサイズ、色の順にグループ化されている場合、サイズと色を組み合わせたグループ式で 1 つのグループを指定できます。 詳細については、「 [テーブルまたはマトリックスへの対話的な並べ替えの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データ領域内のデータの並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [データのフィルター、グループ化、および並べ替え (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [テーブルまたはマトリックスへの対話的な並べ替えの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  
