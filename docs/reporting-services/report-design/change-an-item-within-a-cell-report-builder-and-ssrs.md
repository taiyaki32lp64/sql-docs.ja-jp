---
title: セル内のアイテムの変更 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 91a54778-8929-41f9-bb4c-826cec636be4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cc13f82453349b16e4c9fc00b8f0f083652daa75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581749"
---
# <a name="change-an-item-within-a-cell-report-builder-and-ssrs"></a>セル内のアイテムの変更 (レポート ビルダーおよび SSRS)
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のページ分割されたレポートでは、新しいレポート アイテムで置き換えることができるのは、テキスト ボックスや線、画像などの非コンテナー アイテムに限られています。 たとえば、テーブルをテキスト ボックス内にドラッグすると、テキスト ボックスをテーブルで置き換えることができます。  
  
 四角形、一覧、テーブル、マトリックスなどのコンテナー アイテムがセルに含まれている場合、新しいアイテムはコンテナー アイテムに置き換わるのではなく、コンテナー アイテムに追加されます。 コンテナー アイテムを新しいアイテムで置き換えるには、コンテナーを削除します。 コンテナー アイテムを削除すると、コンテナー アイテムはテキスト ボックスで置き換えられます。その後、テキスト ボックスを別のアイテムで置換できます。  
  
 既定では、テーブル、マトリックス、または一覧のデータ領域内にあるすべてのセルにテキスト ボックスが含まれています。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-change-an-item-within-a-cell"></a>セル内のアイテムを変更するには  
  
-   **[挿入]** タブの **[データ領域]** または **[レポート アイテム]** グループでレポートに追加するアイテムをクリックし、レポートをクリックします。 アイテムがレポートに追加されます。  
  
> [!NOTE]  
>  画像レポート アイテムをセルにドラッグすると、 **[画像のプロパティ]** ダイアログ ボックスが開きます。このダイアログ ボックスでは、画像をセルに追加する前に画像のソースなどのプロパティを設定できます。  
  
## <a name="see-also"></a>参照  
 [画像、テキスト ボックス、四角形、および罫線 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/images-text-boxes-rectangles-and-lines-report-builder-and-ssrs.md)   
 [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
