---
title: データ領域の表示 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 4f3b2c7d-3669-457f-899b-b758d1db3426
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 918aa5eee3aada465e904cf7f1627f93d1b9bb6b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105366"
---
# <a name="rendering-data-regions-report-builder-and-ssrs"></a>データ領域の表示 (レポート ビルダーおよび SSRS)
  データ領域には、すべてのレポート アイテムに適用される一般的な表示動作に加えて、そのデータ領域が従う改ページ動作および表示動作があります。 データ領域固有の表示規則には、データ領域の拡張方法、特殊なセル (コーナーのセルやヘッダー セルなど) の表示方法、およびデータ領域を右から左に記述して表示する方法が含まれます。 ここでは、データ領域のさまざまな部分の表示方法について説明します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="tablix-data-regions"></a>Tablix データ領域  
 Tablix データ領域では、テーブル、マトリックス、および一覧を作成でき、列と行で構成されたグリッドとして表示されます。 行と列の交差部分がセルになります。 表示されると、このセルには、データや他のレポート アイテム (画像、四角形、テキスト ボックス、サブレポートなど) が含まれます。 Tablix データ領域は、縦方向にも横方向にも拡張可能です。 さらに、コーナーのセル、データ領域のヘッダー セル、およびデータ領域の本文セルも、その内容に基づいて拡張できます。 データ領域が複数ページにわたる場合、データ領域で繰り返し使用するように設定されているレポート アイテムは、データ領域が表示される各ページに表示されます。 詳細については、次を参照してください。[一覧&#40;レポート ビルダーおよび SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)します。  
  
### <a name="right-to-left"></a>右から左  
 右から左に表示するように設定された Tablix データ領域は、左から右に表示された場合のデータ領域のミラー イメージのような構造で表示されます。 データ領域のコーナーは、右上隅に表示されます。 動的な列がレポートに存在する場合、その列は左に展開されます。 右から左方向の設定は、データ領域内のデータの順序には影響しません。単純に、列の順序が異なります。  
  
### <a name="tablix-headers"></a>Tablix のヘッダー  
 Tablix のヘッダーは、階層行グループの階層または列グループの階層でそのヘッダー セルが表示される場所に応じて、行ヘッダーまたは列ヘッダーとして表示されます。 ヘッダーのセルの内容に論理的な改ページが存在する場合、それは無視されます。 列グループの論理的な改ページは無視されます。  
  
 グループの論理的な改ページにより、外部グループのヘッダーで改ページされることがなくなります。 たとえば、レポートに、"国" という外部グループと "地域" という内部グループがあるとします。 地域グループのインスタンス間に論理的な改ページがある場合、外部グループ "国" はレポートの両ページに表示されます。  
  
#### <a name="repeated-tablix-headers"></a>繰り返し表示される Tablix のヘッダー  
 **[プロパティ]** ペインで RepeatWith プロパティが設定されている場合、データ領域内で変更されないアイテム (列ヘッダーなど) が、そのデータ領域部分が表示される各ページに繰り返し表示されます。 たとえば、データ行が次のページに表示され、RepeatWith プロパティが設定されていると、表示されたページに列ヘッダーも表示されます。  
  
### <a name="tablix-corner"></a>Tablix コーナー  
 左上隅は、Tablix コーナーと呼ばれます。 Tablix コーナーでは、その中に他のレポート アイテムを含めることができます。ただし、論理的な改ページがコーナーに挿入されている場合は、Tablix データ領域が表示されるときにその改ページは無視されます。  
  
### <a name="tablix-body"></a>Tablix 本体  
 Tablix 本体は、Tablix セルで構成されます。 Tablix 本体は、レポート アイテムの改ページ規則および表示動作に基づいて表示されます。 詳細については、「 [レポート アイテムのレンダリング (レポート ビルダーおよび SSRS)](rendering-report-items-report-builder-and-ssrs.md)」を参照してください。  
  
## <a name="chart-gauge-and-map-data-regions"></a>グラフ、ゲージ、およびマップのデータ領域  
 グラフ、ゲージ、およびマップのデータ領域は、レポート本文に描画および表示されると、画像のように動作します。 データ領域内の値には、別のレポートへのリンクやブックマークへの移動などのアクションを関連付けることができます。また、こうしたアクションは、レンダラーでサポートされる場合に同様に表示できます。  
  
## <a name="see-also"></a>参照  
 [Reporting Services の改ページ &#40;レポート ビルダーおよび SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [レンダリングの動作 &#40;レポート ビルダーおよび SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)   
 [さまざまなレポート表示拡張機能の対話機能 &#40;レポート ビルダーおよび SSRS&#41;](../report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [レポート アイテムのレンダリング &#40;レポート ビルダーおよび SSRS&#41;](rendering-report-items-report-builder-and-ssrs.md)   
 [一覧 &#40;レポート ビルダーおよび SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [グラフ &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [ゲージ &#40;レポート ビルダーおよび SSRS&#41;](gauges-report-builder-and-ssrs.md)  
  
  
