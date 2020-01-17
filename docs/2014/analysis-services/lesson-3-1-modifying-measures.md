---
title: メジャーの変更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7bd48810-15ce-45ff-862b-372d08606995
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 663ef21dc9c4d0f3698ae468637fe0a8fd55a16e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078901"
---
# <a name="modifying-measures"></a>メジャーの変更
  **FormatString** プロパティを使用して書式設定を定義することによって、メジャーの表示方法を調整できます。 この実習では、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial キューブの通貨メジャーと比率メジャーの書式プロパティを指定します。  
  
### <a name="to-modify-the-measures-of-the-cube"></a>キューブのメジャーを変更するには  
  
1.  **Tutorial キューブのキューブ デザイナーで、** [キューブ構造] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] タブに切り替えます。次に、 **[メジャー]** ペインの **[Internet Sales]** メジャー グループを展開し、 **[Order Quantity]** を右クリックして、 **[プロパティ]** をクリックします。  
  
2.  [プロパティ] ウィンドウの **[自動的に隠す]** 押しピン アイコンをクリックし、[プロパティ] ウィンドウを開いたまま固定します。  
  
     [プロパティ] ウィンドウを開いたままにしておくと、キューブ内のアイテムごとにプロパティを変更する操作が容易になります。  
  
3.  [プロパティ] ウィンドウで、 **[FormatString]** ボックスの一覧をクリックし、「 **#,#** 」と入力します。  
  
4.  **[キューブ構造]** タブのツール バーで、左側の **[メジャー グリッドの表示]** アイコンをクリックします。  
  
     グリッド ビューで複数のメジャーを同時に選択できます。  
  
5.  次のメジャーを選択します。 Ctrl キーを押しながらクリックすると、複数のメジャーを選択できます。  
  
    -   **Unit Price**  
  
    -   **Extended Amount**  
  
    -   **Discount Amount**  
  
    -   **Product Standard Cost**  
  
    -   **Total Product Cost**  
  
    -   **Sales Amount**  
  
    -   **Tax Amt**  
  
    -   **Freight**  
  
6.  [プロパティ] ウィンドウで、 **FormatString** プロパティのセルをクリックして、 **[Currency]** を選択します。  
  
7.  [プロパティ] ウィンドウの一番上 (タイトル バーのすぐ下) にあるドロップダウン リストで、 **[Unit Price Discount Pct]** メジャーを選択します。次に、 **FormatString** プロパティのセルをクリックして **[Percent]** を選択します。  
  
8.  [プロパティ] ウィンドウで変更、**名前**プロパティを**Unit Price Discount Pct**メジャーを`Unit Price Discount Percentage`します。  
  
9. **メジャー**ウィンドウで、をクリックして**Tax Amt**このメジャーの名前を変更および`Tax Amount`します。  
  
10. [プロパティ] ウィンドウの **[自動的に隠す]** アイコンをクリックし、[プロパティ] ウィンドウを非表示にします。次に、 **[キューブ構造]** タブのツール バーで、 **[メジャー ツリーの表示]** をクリックします。  
  
11. **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [Customer ディメンションの変更](lesson-3-2-modifying-the-customer-dimension.md)  
  
## <a name="see-also"></a>参照  
 [データベース ディメンションを定義します。](multidimensional-models/define-database-dimensions.md)   
 [メジャーのプロパティの構成](multidimensional-models/configure-measure-properties.md)  
  
  
