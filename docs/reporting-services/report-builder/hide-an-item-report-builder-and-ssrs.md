---
title: 項目の非表示 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.shared.visibility.f1
- "10503"
ms.assetid: 9d78f8de-959b-456f-8947-687fa6e2ba91
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2a6e57c1e4326f2c8a0f04a515aab7c699778f39
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580707"
---
# <a name="hide-an-item-report-builder-and-ssrs"></a>アイテムを非表示にする (レポート ビルダーおよび SSRS)
  レポート パラメーターやその他の式を指定して、アイテムを条件付きで非表示にする場合は、レポート アイテムの表示/非表示を設定します。  
  
 また、ドリルダウン レポートなどで、レポートのテキスト ボックスをクリックすることによってレポート アイテムの表示と非表示をユーザーが切り替えられるようなレポートを設計することもできます。 詳細については、「 [アイテムへの展開または折りたたみアクションの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)」を参照してください。  
  
 以下に、定数または式に基づいて表示レポートでのレポート アイテムの表示または非表示を切り替える手順について説明します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-hide-a-report-item"></a>レポート アイテムを非表示にするには  
  
1.  レポート デザイン ビューで、レポート アイテムを右クリックし、 **[プロパティ]** ページを開きます。  
  
    > [!NOTE]  
    >  テーブルまたはマトリックス データ領域全体を選択するには、領域内をクリックして選択し、行ハンドル、列ハンドル、またはコーナー ハンドルを右クリックして、 **[Tablix のプロパティ]** をクリックします。  
  
2.  **[表示]** をクリックします。  
  
3.  **[レポートの初期実行時]** で、レポートを初めて表示する際にアイテムを非表示にするかどうかを指定します。  
  
    -   アイテムを表示する場合は、 **[表示]** をクリックします。  
  
    -   アイテムを非表示にする場合は、 **[非表示]** をクリックします。  
  
    -   実行時に評価される式を指定するには、 **[式を基に表示/非表示を切り替える]** をクリックします。 **[式]** ダイアログ ボックスで、式を入力するか、式 ( **[fx]** ) ボタンをクリックして式を作成します。  
  
        > [!NOTE]  
        >  表示/非表示を設定する式を指定する場合、次の図のように、レポート アイテムの Hidden プロパティを設定します。 この値が False の場合、式の評価によってレポート アイテムが表示され、値が True の場合、レポート アイテムは非表示になります。   
        > ![[プロパティ] の [表示] のダイアログと [非表示] プロパティ](../../reporting-services/report-builder/media/hiddenproperty-propertiesvisibility.png "[プロパティ] の [表示] のダイアログと [非表示] プロパティ")  
  
4.  **[OK]** を 2 回クリックします。  
  
### <a name="to-hide-static-rows-in-a-table-matrix-or-list"></a>テーブル、マトリックス、または一覧の静的行を非表示にするには  
  
1.  レポート デザイン ビューで、テーブル、マトリックス、または一覧をクリックし、行ハンドルおよび列ハンドルを表示します。  
  
2.  行ハンドルを右クリックし、 **[行表示]** をクリックします。 **[行表示]** ダイアログ ボックスが開きます。  
  
3.  表示/非表示を設定するには、最初の手順の 3. ～ 4. に従います。  
  
### <a name="to-hide-static-columns-in-a-table-matrix-or-list"></a>テーブル、マトリックス、または一覧の静的列を非表示にするには  
  
1.  [デザイン] ビューで、テーブル、マトリックス、または一覧を選択し、行ハンドルおよび列ハンドルを表示します。  
  
2.  列ハンドルを右クリックし、 **[列表示]** をクリックします。  
  
3.  **[列表示]** ダイアログ ボックスで、最初の手順の 3 ～ 4 に従います。  
  
## <a name="see-also"></a>参照  
 [ドリルダウン アクション &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/drilldown-action-report-builder-and-ssrs.md)   
 [アイテムへの展開または折りたたみアクションの追加 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [式の例 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
