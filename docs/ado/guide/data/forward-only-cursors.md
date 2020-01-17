---
title: 順方向専用カーソル |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], forward-only
- forward-only cursors [ADO]
ms.assetid: 2b1e062f-3294-4a6f-8241-a17045c4df18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e84fbf2b8fda2fa2b14088af1e0830d8109aba8a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925307"
---
# <a name="forward-only-cursors"></a>順方向専用カーソル
順方向専用 (またはスクロールを可能な) カーソルと呼ばれる代表的な既定カーソルの種類は、結果セットを順方向にのみ移動できます。 順方向専用カーソルはスクロール (結果セットで前方と後方に移動する機能) をサポートしていません結果セットの末尾に、開始から行のフェッチのみサポートします。 順方向専用カーソルの一部 (など、SQL Server カーソル ライブラリを使用した) すべて、insert、update、および delete ステートメント、現在のユーザーによって行われた (またはその他のユーザーによってコミットされる) は、行をフェッチすると、結果セットの行に影響を表示することです。 ただし、カーソルは後方にスクロールできないので、データベース内の行のフェッチ後にその行に対して行われた変更内容は、カーソル内で確認できません。  
  
 現在の行のデータが処理された後、順方向専用カーソルは、そのデータを保持するために使用されたリソースを解放します。 順方向専用カーソルは既定では動的であり、現在の行が処理されるとすべての変更が検出されることを意味します。 これにより、カーソルを開く時間が短縮され、基になるテーブルに対して行われた更新を結果セットで表示できるようになります。  
  
 順方向専用カーソルは、後方スクロールをサポートしていません、アプリケーションは、カーソルを閉じて、結果セットの先頭に戻ります。 これは、少量のデータを使用する効果的な方法です。 アプリケーションが結果セットを 1 回読み取りでした代わりには、データをローカルにキャッシュされ、ローカル データ キャッシュを参照します。  
  
 場合は、アプリケーションでは、結果セットのスクロールは必要ありませんが、順方向専用カーソルは、最小限のオーバーヘッドで迅速にデータを取得する最適な方法です。 使用して、 **adOpenForwardOnly CursorTypeEnum** ADO では順方向専用カーソルを使用することを指定します。  
  
## <a name="see-also"></a>関連項目  
 [静的カーソル](../../../ado/guide/data/static-cursors.md)   
 [Keyset カーソル](../../../ado/guide/data/keyset-cursors.md)   
 [動的カーソル](../../../ado/guide/data/dynamic-cursors.md)
