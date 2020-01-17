---
title: 無名のパラメーターを使用したクエリの作成 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- unnamed parameters
- parameters [SQL Server], unnamed
ms.assetid: 5f4b664b-3d3d-4d07-a0e7-791d78743504
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f9eebede28d257083b55ffd4b14943b7ebc1a95b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63184337"
---
# <a name="create-queries-with-unnamed-parameters-visual-database-tools"></a>無名のパラメーターを使用したクエリの作成 (Visual Database Tools)
  リテラル値のプレースホルダーとして疑問符 (?) を指定すると、無名のパラメーターを持つクエリを作成できます。 クエリおよびビュー デザイナーにより、一時的な名前が指定されます。 クエリには、必要な数の無名のパラメーターを指定できます。  
  
 クエリおよびビュー デザイナーでクエリを実行すると、一時的な名前と共に [クエリ パラメーター] ダイアログ ボックスが表示されます。  
  
### <a name="to-specify-an-unnamed-parameter"></a>無名のパラメーターを指定するには  
  
1.  検索する列または式を [抽出条件ペイン](visual-database-tools.md)に追加します。 検索列または検索式をクエリ出力に表示しない場合は、出力列から削除します。  
  
2.  検索するデータ列または式を含む行を選択し、 **[フィルター]** グリッド列に疑問符 (?) を入力します。  
  
     既定では、"=" 演算子が追加されます。 ただし、セルを編集して、">"、"<"、または他の SQL 比較演算子にも変更できます。  
  
## <a name="see-also"></a>関連項目  
 [パラメーターを使用したクエリ (Visual Database Tools)](query-with-parameters-visual-database-tools.md)  
  
  
