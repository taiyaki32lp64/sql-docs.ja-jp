---
title: "追加、移動、または削除 (レポート ビルダーおよび SSRS) は、テキスト ボックス |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f042cf81-d933-4ac7-9287-c074a46bde98
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 75444343968c9901a24c1a4d431d4d8cfacb1567
ms.contentlocale: ja-jp
ms.lasthandoff: 08/09/2017

---
# <a name="add-move-or-delete-a-text-box-report-builder-and-ssrs"></a>テキスト ボックスの追加、移動、または削除 (レポート ビルダーおよび SSRS)
  テキスト ボックスは [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] のページ分割されたレポート内で最も一般的に使用されるレポート アイテムです。 テキスト ボックスをレポート本文に追加して、タイトル、パラメーターの選択肢、組み込みフィールド、日付などの情報を表示できます。  
  
 テーブルやマトリックスのすべてのセルは、実際にはテキスト ボックスです。 テーブルおよびマトリックスと共にレポートに表示されるほとんどのレポート データは、レポートの各テキスト ボックスの内容を評価するレポート プロセッサの結果です。 したがってセルは、データ領域の外部にあるその他のテキスト ボックスと同じように書式設定できます。  
  
 テキスト ボックスを一覧データ領域に追加するには、テキスト ボックスを追加してから一覧にドラッグする必要があります。  
  
> [!NOTE]  
>  テキスト ボックスをクリックすると、すぐにテキスト ボックスのテキストを編集できる状態になります。 テキストではなくテキスト ボックスそのものを選択するには、Esc キーを押します。  
  
## <a name="to-add-a-text-box"></a>テキスト ボックスを追加するには  
  
1.  [デザイン] ビューの **[挿入]** タブで、 **[テキスト ボックス]**をクリックします。  
  
2.  デザイン画面で、ボックスをクリックし、テキスト ボックスの目的のサイズにドラッグします。  
  
## <a name="to-add-a-text-box-in-a-list"></a>一覧にテキスト ボックスを追加するには  
  
1.  レポート デザイン ビューの **[挿入]** タブで、 **[一覧]**をクリックします。  
  
2.  デザイン画面で、ボックスをクリックし、一覧の目的のサイズにドラッグします。  
  
3.  **[挿入]** タブの **[テキスト ボックス]**をクリックします。  
  
4.  デザイン画面の手順 1. で追加した一覧内で、ボックスをクリックし、テキスト ボックスの目的のサイズにドラッグします。   
  
5.  テキスト ボックスが一覧内で正しく入れ子になっていることを確認するには、テキスト ボックスを選択します。  
  
    > [!NOTE]  
    >  テキスト ボックスの中をクリックして編集モードになった場合は、Esc キーを押すとテキスト ボックスを選択できます。  
  
6.  プロパティ ペインで、 **Parent** プロパティが一覧データ領域に自動的に追加された四角形であることを確認します。  
  
    > [!NOTE]  
    >  プロパティ ペインが表示されていない場合は、 **[表示]** タブの **[プロパティ]** をオンにします。  
  
## <a name="to-move-a-text-box"></a>テキスト ボックスを移動するには  
  
1.  レポート デザイン ビューで、テキスト ボックス内の空白部分をクリックして、テキスト ボックスを選択します。  
  
    > [!NOTE]  
    >  テキスト ボックスの中をクリックして編集モードになった場合は、Esc キーを押すとテキスト ボックスを選択できます。  
  
2.  テキスト ボックスのハンドルをクリックし、テキスト ボックスを新しい場所にドラッグします。   
    または、方向キーを使用して、選択したテキスト ボックスを横方向または縦方向に移動します。 デザイン画面でテキスト ボックスを細かく移動するには、&lt;localizedText&gt;Ctrl&lt;/localizedText&gt; キーを押しながら方向キーを使用します。  
  
## <a name="to-delete-a-text-box"></a>テキスト ボックスを削除するには  
  
1.  レポート デザイン ビューで、テキスト ボックス内の空白部分を右クリックして選択し、 **[削除]**をクリックします。 または、テキスト ボックス内の空白部分をクリックして、Del キーを押します。  
  
    > [!NOTE]  
    >  テキスト ボックスの中をクリックして編集モードになった場合は、Esc キーを押すとテキスト ボックスを選択できます。  
  
## <a name="see-also"></a>参照  
 [テキスト ボックス & #40 です。レポート ビルダーおよび SSRS &#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [式と &#40; です。レポート ビルダーおよび SSRS &#41; です。](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [キーボード ショートカットと #40 です。レポート ビルダー"&"#41;](../../reporting-services/report-builder/keyboard-shortcuts-report-builder.md)  
  
  