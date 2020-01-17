---
title: ドリルダウン アクション (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10249"
- "10186"
- sql12.rtp.rptdesigner.calculatedseriesproperties.visibility.f1
- sql12.rtp.rptdesigner.seriesproperties.visibility.f1
- sql12.rtp.rptdesigner.chartareaproperties.visibility.f1
- "10092"
- sql12.rtp.rptdesigner.textboxproperties.visibility.f1
- sql12.rtp.rptdesigner.charttitleproperties.visibility.f1
- "10167"
- sql12.rtp.rptdesigner.rectangleproperties.visibility.f1
- "10174"
- sql12.rtp.rptdesigner.majorgridlineproperties.visibility.f1
- "10155"
- "10123"
- sql12.rtp.rptdesigner.subreportproperties.visibility.f1
- "10425"
- sql12.rtp.rptdesigner.minorgridlineproperties.visibility.f1
- "10217"
- sql12.rtp.rptdesigner.axisproperties.visibility.f1
- sql12.rtp.rptdesigner.serieslabelproperties.visibility.f1
- "10161"
- sql12.rtp.rptdesigner.chartproperties.visibility.f1
- sql12.rtp.rptdesigner.legendproperties.visibility.f1
- sql12.rtp.rptdesigner.pictureproperties.visibility.f1
- "10215"
- "10258"
- "10144"
- "10062"
- "10053"
ms.assetid: 1f8d1ef2-0daf-40c6-9ba7-3b391249bcd4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2fe3d55dc70a606df759c049b7b147820f0e3110
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105989"
---
# <a name="drilldown-action-report-builder-and-ssrs"></a>ドリルダウン アクション (レポート ビルダーおよび SSRS)
  テキスト ボックスに正符号と負符号のアイコンを組み込むことによって、アイテムの表示/非表示をユーザーが対話的に切り替えられるように設定できます。 これを *ドリルダウン* アクションと呼びます。 テーブルまたはマトリックスの場合、静的な行や列、またはグループに関連付けられている行や列の表示と非表示を切り替えることができます。  
  
 ![rs_drilldown](../media/rs-drilldown.gif "rs_drilldown")  
  
 この図では、レポートの正符号 (+) をクリックして詳細データを表示しています。  
  
 たとえば、行グループのあるテーブルの場合、外側のグループの概要行を除いて、最初にすべての行を非表示にすることができます。 それぞれの内部グループ (詳細グループを含む) に対して、グループ化セルの展開/折りたたみを切り替えるアイコンを対象グループに追加します。 レポートが表示されると、ユーザーはこのテキスト ボックスをクリックして、詳細データを展開したり折りたたんだりすることができます。 詳細については、「[テーブル &#40;レポート ビルダーおよび SSRS&#41;](tables-report-builder-and-ssrs.md)」を参照してください。  
  
 アイテムの展開と折りたたみをユーザーが行うようにするには、アイテムの表示プロパティを設定します。  
  
> [!NOTE]  
>  ドリルダウン アクションを使用してレポートを作成する場合は、非表示にする行や列内の単一のテキスト ボックスではなく、非表示にするグループ、列、または行に、表示情報を設定する必要があります。 さらに、トグル ボタンに使用するテキスト ボックスが、表示と非表示を切り替えるアイテムを制御するコンテナー スコープの範囲内にある必要があります。  
>   
>  たとえば、入れ子構造のグループに関連付けられている行を非表示にするには、テキスト ボックスが、親グループに関連付けられている行にあるか、包含階層の上位にある必要があります。  
>   
>  グループ、列、または行の可視化の設定については、「[アイテムへの展開または折りたたみアクションの追加 &#40;レポート ビルダーおよび SSRS&#41;](add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)」を参照してください。  
  
 レポート アイテムを非表示にする方法については、「[アイテムを非表示にする &#40;レポート ビルダーおよび SSRS&#41;](../report-builder/hide-an-item-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="comparing-drilldown-and-drillthrough-reports"></a>ドリルダウン レポートと詳細レポートの比較  
 ドリルダウン レポートでは、ユーザーが正符号または負符号のボタンをクリックすると、レポートのセクションが展開または折りたたまれ、詳細データがその場所に表示されます。 詳細レポートでは、ユーザーが集計値のリンクをクリックすると、別の関連レポートが開き、詳細データが表示されます。 詳細データは、詳細レポートの実行時にのみ取得されます。 通常詳細レポートには、ドリルダウン レポートほどリソースが必要ありません。 詳細については、「 [ドリルスルー、ドリルダウン、サブレポート、および入れ子になったデータ領域 (レポート ビルダーおよび SSRS)](drillthrough-drilldown-subreports-and-nested-data-regions.md)」を参照してください。  
  
## <a name="rendering-extension-support-for-hidden-report-items"></a>非表示レポート アイテムに対する表示拡張機能のサポート  
 レポート アイテムの表示と非表示の切り替えは、レポート ビルダーやレポート マネージャーでレポートを実行するときに使用する HTML 表示拡張機能など、ユーザー対話機能をサポートする表示拡張機能でのみサポートされます。 一部の表示拡張機能では非表示アイテムが表示されます。 条件に応じて表示/非表示を切り替えるレポート アイテムのサポートは、次のようになります。  
  
-   HTML では、非表示に設定されている場合、アイテムは HTML ソース内に表示されません。  
  
-   XML 表示拡張機能では、非表示に設定されているかどうかに関係なく、すべてのレポート アイテムが表示されます。  
  
-   Excel 表示拡張機能では、テーブル、マトリックス、または一覧の非表示の行および列が表示され展開されます。 行と列がすべて表示されます。  
  
 詳しくは、「[レンダリングの動作 &#40;レポート ビルダーおよび SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [ドリルスルー、ドリルダウン、サブレポート、および入れ子になったデータ領域 (レポート ビルダーおよび SSRS)](drillthrough-drilldown-subreports-and-nested-data-regions.md)   
 [対話的な並べ替え、ドキュメント マップ、およびリンク (レポート ビルダーおよび SSRS)](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [式の例 &#40;レポート ビルダーおよび SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
  
