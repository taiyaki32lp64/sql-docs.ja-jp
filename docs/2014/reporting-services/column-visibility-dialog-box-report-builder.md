---
title: '[列表示] ダイアログ ボックス) (レポート ビルダー) |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10127"
ms.assetid: 0c030cab-6087-45a5-99f0-c7bd693f20a1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 58381a9e56ed6ace1f8ff18109d9746072f76774
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109809"
---
# <a name="column-visibility-dialog-box-report-builder"></a>[列表示] ダイアログ ボックス (レポート ビルダー)
  **[列表示]** ダイアログ ボックスでは、選択した列をレポートの初期実行時に表示または非表示にする操作や、別のレポート アイテムを使用して列の表示を切り替える操作を行うことができます。  
  
## <a name="options"></a>および  
 **レポートを最初に実行時**  
 レポートにレポート アイテムを表示する際の初期設定を示すオプションを選択します。  
  
 **[表示]**  
 列を表示します。  
  
 **非表示にします。**  
 列を非表示にします。  
  
 **表示または非表示の式を基に**  
 式を使用して初期表示を変化させます。  
  
 アイテムを非表示にする場合は `Boolean`、アイテムを表示する場合は `True` と評価される `False` 値の式を入力します。 式を編集するには、式 ( *[fx]* ) ボタンをクリックします。  
  
 **このレポート アイテムが表示を切り替えることができます。**  
 HTML レポート ビューアーでこの列の表示/非表示をユーザーが切り替えられるようにするための切り替えイメージを表示します。  
  
 切り替えイメージを表示するレポートのテキスト ボックスの名前 (「Textbox1」など) を入力または選択します。 選択するテキスト ボックスは、このレポート アイテムの現在のスコープまたはコンテナー スコープに存在する必要があります。 たとえば、子グループに関連付けられている行の表示を切り替えるには、親グループに関連付けられている行のテキスト ボックスを選択する必要があります。 グラフの表示を切り替えるには、レポート本文や四角形など、グラフと同じコンテナー スコープにあるテキスト ボックスを選択します。  
  
## <a name="see-also"></a>参照  
 [式の例 (レポート ビルダーおよび SSRS)](report-design/expression-examples-report-builder-and-ssrs.md)   
 [アイテムへの展開または折りたたみアクションの追加 &#40;レポート ビルダーおよび SSRS&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [画像 &#40;レポート ビルダーおよび SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [レポート ビルダーのダイアログ ボックス、ペイン、およびウィザードに関するヘルプ](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [[全般] ([画像のプロパティ] ダイアログ ボックス) (レポート ビルダーおよび SSRS)](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
