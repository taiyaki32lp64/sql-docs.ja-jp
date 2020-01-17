---
title: 削除クエリの作成 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- row removal [SQL Server], Delete query
- Delete query
- queries [SQL Server], types
- removing rows
- removing data
- data deletions [SQL Server]
- deleting rows
- deleting data
ms.assetid: 0db3af43-1ec4-48c8-b769-2bb9c76d3434
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f1103e1715c01cfc868c59af17ee0f95fa7cedff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62661686"
---
# <a name="create-delete-queries-visual-database-tools"></a>削除クエリの作成 (Visual Database Tools)
  削除クエリを使用すると、テーブル内の行をすべて削除できます。  
  
> [!NOTE]  
>  テーブルから行をすべて削除すると、テーブルのデータは削除されますが、テーブル自体は削除されません。 データベースからテーブルを削除するには、オブジェクト エクスプローラーでテーブルを右クリックして、 **[削除]** をクリックします。  
  
 削除クエリを作成すると、行の削除に使用できるオプションが抽出条件ペインに表示されます。 削除クエリではデータが表示されないため、[出力]、[並べ替え]、および [並べ替え順序] の各列は削除されます。 さらに、テーブルまたはテーブル値オブジェクトを示す四角形内の列名の横のチェック ボックスが削除されます。列を個別に指定して削除することはできないためです。  
  
 クエリおよびビュー デザイナーで削除できない行がある場合、いずれの行も削除されず、データベースから削除できない情報を含む行を示すメッセージが表示されます。  
  
> [!CAUTION]  
>  削除クエリの実行アクションを元に戻すことはできません。 念のため、削除クエリを実行する前にデータをバックアップしてください。  
  
### <a name="to-create-a-delete-query"></a>削除クエリを作成するには  
  
1.  行を削除するテーブルをダイアグラム ペインに追加します。  
  
2.  **[クエリ デザイナー]** メニューの **[クエリ タイプの変更]** をポイントし、 **[削除]** をクリックします。 **メモ** 削除クエリを開始した時点でダイアグラム ペインに複数のテーブルが表示されている場合、行を削除するテーブルの名前を要求する [[テーブルの削除] ダイアログ ボックス](visual-database-tools.md) が表示されます。  
  
 削除クエリを実行しても、 [結果ペイン](results-pane-visual-database-tools.md)には結果が表示されません。 代わりに、削除された行数を示すメッセージが表示されます。  
  
## <a name="see-also"></a>参照  
 [クエリの種類がサポートされている&#40;Visual Database Tools&#41;](supported-query-types-visual-database-tools.md)   
 [クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
