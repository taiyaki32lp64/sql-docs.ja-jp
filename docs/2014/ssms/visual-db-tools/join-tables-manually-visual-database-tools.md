---
title: 手動でのテーブルの結合 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- manual joins [SQL Server]
- joins [SQL Server], manual
- joins [SQL Server], creating
ms.assetid: 9c785356-646b-4c87-82d4-25efd6051d9d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0299be9a1cb480a567e0b166c990d25588598aba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62711059"
---
# <a name="join-tables-manually-visual-database-tools"></a>手動でのテーブルの結合 (Visual Database Tools)
  [クエリおよびビュー デザイナー](visual-database-tools.md) では、クエリに複数のテーブルを追加すると、共通データ、またはテーブルの関連付けに関するデータベース内に格納されている情報に基づいて、テーブルが結合されます。 詳しくは、「[テーブルの自動結合 (Visual Database Tools)](join-tables-automatically-visual-database-tools.md)」をご覧ください。 ただし、クエリおよびビュー デザイナーでテーブルが自動的に結合されなかった場合、またはテーブル間の結合条件を追加作成する場合は、テーブルを手動で結合できます。  
  
 結合は、同じ情報を含む列だけでなく、任意の 2 つの列の比較に基づいて作成できます。 たとえば、データベースに `titles` および `roysched`という 2 つのテーブルがある場合、 `ytd_sales` テーブルの `titles` 列の値と、 `lorange` テーブルの `hirange` 列および `roysched` 列の値とを比較できます。 この結合を作成すると、本年度の売り上げが印税の支払いの上限と下限の範囲内にある書名を検索できます。  
  
> [!TIP]  
>  結合の処理速度は、結合条件の列にインデックスが設定されている場合、最も速くなります。 インデックスの設定されていない列を結合すると、場合によってはクエリの処理速度が遅くなります。  
  
### <a name="to-manually-join-tables-or-table-structured-objects"></a>テーブルまたはテーブル構造オブジェクトを手動で結合するには  
  
1.  結合するオブジェクトを [ダイアグラム ペイン](diagram-pane-visual-database-tools.md) に追加します。  
  
2.  最初のテーブルまたはテーブル構造オブジェクトの結合列の名前をドラッグし、2 番目のテーブルまたはテーブル結合オブジェクトの関連する列にドロップします。 `text`、`ntext`、または i`mage` 型の列を結合することはできません。  
  
    > [!NOTE]  
    >  結合列のデータ型は、同じ型か互換性のある型である必要があります。 たとえば、最初のテーブルの結合列が日付型の場合は、2 番目のテーブルの結合列も日付型としてください。 一方、最初の結合列が整数型の場合、関連付ける結合列も整数型である必要がありますが、サイズは異なってもかまいません。 クエリおよびビュー デザイナーでは、結合の作成に使用した列のデータ型がチェックされることはありません。ただしデータ型に互換性がない場合、クエリの実行時にデータベースによってエラーが表示されます。  
  
3.  必要に応じて結合演算子を変更します。既定の演算子は等号 (=) です。 詳細については、「[結合演算子の変更 (Visual Database Tools)](modify-join-operators-visual-database-tools.md)」を参照してください。  
  
 [SQL ペイン](sql-pane-visual-database-tools.md)のステートメントに INNER JOIN 句が追加されます。 結合の種類を外部結合に変更できます。 詳細については、「[外部結合の作成 (Visual Database Tools)](create-outer-joins-visual-database-tools.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [結合を使用したクエリ (Visual Database Tools)](query-with-joins-visual-database-tools.md)  
  
  
