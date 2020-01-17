---
title: チェック アウトの取り消し |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourcControl.UndoCheckDialog
helpviewer_keywords:
- checking out files
- checkout source controls [SQL Server]
- undoing checkouts
ms.assetid: a6596b20-3aa5-4dc4-a4c5-3649f1f5a20e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2057c78f953645c9b1a5915b9912ab99263cb005
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773398"
---
# <a name="undo-checkouts"></a>チェックアウトの取り消し
  使用することができます、**チェック アウトの取り消し**コマンドを既存のチェック アウトを取り消します。 この機能は、ファイルを変更して保存した後に、その変更をロールバックする必要が生じた場合などに特に便利です。  
  
 設定したオプションに応じて、**チェック アウトの取り消しオプションの高度な** ダイアログ ボックスでは、Studio 環境またはいずれか、ローカル ディスク上の項目の作業コピーのまま管理対象の最新バージョンに置き換えられます。 他のユーザーがソース管理システムのコンテキスト外で項目を修正した場合は、最新バージョンを取得できるとは限りません。  
  
### <a name="to-undo-a-checkout"></a>チェックアウトを元に戻すには  
  
1.  ソリューション エクスプローラーで、プロジェクトを選択します。  
  
2.  **ファイル**メニューで、**ソース管理**、 をクリックし、**チェック アウトの取り消し**します。  
  
3.  **チェック アウトの取り消し**ダイアログ ボックスで、適切なオプションを選択し、順にクリックして、**チェック アウトの取り消し**ボタンをクリックします。  
  
     **[列]**  
     表示する列と、その表示順序を指定します。  
  
     **フラット ビュー**  
     項目をソース管理接続の下に一覧表示します。  
  
     **名前**  
     チェックアウトを取り消す項目の名前を表示します。 項目になっての横にあるチェック ボックスが表示されます。 項目のチェックアウトを取り消さない場合は、チェック ボックスをオフにします。  
  
     **[オプション]**  
     ボタンの右側の矢印をクリックすると、ソース管理のプラグインに固有のチェックアウトの取り消しオプションが表示されます。  
  
     **Sort**  
     表示列の順序を並べ替えます。  
  
     **ツリー ビュー**  
     チェックアウトを元に戻す項目のフォルダーおよび項目階層を表示します。  
  
     **チェック アウトを取り消し**  
     チェックアウトを元に戻して、チェックアウトされたファイルに対する変更を破棄します。  
  
## <a name="see-also"></a>参照  
 [ファイルをチェック アウト](../../2014/database-engine/check-out-files.md)   
 [チェックアウトの管理](../../2014/database-engine/manage-checkouts.md)  
  
  
