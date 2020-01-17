---
title: 行の表示 ダイアログ ボックス |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.rowvisibility.f1
- "10126"
ms.assetid: 557ecf70-62b1-47f5-9322-0ebdc809d018
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fe9af16c34fa70bb8fcda0dcaae64a39786e3cd3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102407"
---
# <a name="row-visibility-dialog-box"></a>[行表示] ダイアログ ボックス
  **[行表示]** ダイアログ ボックスを使用すると、選択した行をレポートの初回実行時に表示または非表示にすることも、別のレポート アイテムを使用して行の表示を切り替えることもできます。  
  
## <a name="options"></a>および  
 **レポートを最初に実行時**  
 レポートにレポート アイテムを表示する際の初期設定を示すオプションを選択します。  
  
 **[表示]**  
 レポート アイテムを表示します。  
  
 **非表示にします。**  
 レポート アイテムを非表示にします。  
  
 **表示または非表示の式を基に**  
 式を使用して初期表示を変化させます。  
  
 アイテムを非表示にする場合は `Boolean`、アイテムを表示する場合は `True` と評価される `False` 値の式を入力します。 式を編集するには、式 ( **[fx]** ) ボタンをクリックします。  
  
 **このレポート アイテムが表示を切り替えることができます。**  
 ユーザーが HTML レポート ビューアーでこのレポート アイテムの表示/非表示を切り替えられるようにする切り替えイメージを表示します。  
  
 切り替えイメージを表示するレポートのテキスト ボックスの名前 (「Textbox1」など) を入力または選択します。 選択するテキスト ボックスは、このレポート アイテムの現在のスコープまたはコンテナー スコープに存在する必要があります。 たとえば、子グループに関連付けられている行の表示を切り替えるには、親グループに関連付けられている行のテキスト ボックスを選択する必要があります。 グラフの表示を切り替えるには、レポート本文や四角形など、グラフと同じコンテナー スコープにあるテキスト ボックスを選択します。  
  
## <a name="see-also"></a>参照  
 [式の例 (レポート ビルダーおよび SSRS)](report-design/expression-examples-report-builder-and-ssrs.md)   
 [アイテムへの展開または折りたたみアクションの追加 &#40;レポート ビルダーおよび SSRS&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [画像 &#40;レポート ビルダーおよび SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [レポート デザイナーの F1 ヘルプ](tools/report-designer-f1-help.md)  
  
  
