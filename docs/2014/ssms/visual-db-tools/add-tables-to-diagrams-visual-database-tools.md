---
title: ダイアグラムへのテーブルの追加 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- inserting tables
- adding tables
ms.assetid: 5440fdf7-ac04-4325-9f32-181f4cd402e5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 26c13eb6c9cb142cac3ba0981177fb2c605ab5fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63297894"
---
# <a name="add-tables-to-diagrams-visual-database-tools"></a>ダイアグラムへのテーブルの追加 (Visual Database Tools)
  データベース ダイアグラムにテーブルを追加すると、そのテーブルの構造の編集や、ダイアグラム内にある他のテーブルとの関連付けを行えます。 テーブルを追加する方法には、ダイアグラムに既存のデータベース テーブルを追加する方法と、データベースで未定義の新しいテーブルを挿入する方法があります。  
  
### <a name="to-insert-a-new-table-into-a-diagram"></a>ダイアグラムに新しいテーブルを挿入するには  
  
1.  テーブルを作成するデータベースに接続していることを確認します。  
  
     現在のダイアグラムにテーブルを作成するには、ツール バーの **[新しいテーブル]** をクリックします。  
  
     \- または -  
  
     ダイアグラムを右クリックし、 **[新しいテーブル]** をクリックします。  
  
2.  **[名前の選択]** ダイアログ ボックスで、システムによって割り当てられたテーブル名を必要に応じて変更し、 **[OK]** をクリックします。  
  
     ダイアグラムに新しいテーブルが [標準] ビューで表示されます。  
  
3.  新しいテーブルの最初のセルに列名を入力します。 次に、Tab キーを押して次のセルに移動します。  
  
4.  **[データ型]** で列のデータ型を選択します。 各列には、名前とデータ型が必要です。  
  
     テーブル デザイナーで列のその他のプロパティを設定できます。  
  
5.  テーブルに列を追加するたびに、手順 3. および手順 4. を繰り返します。  
  
> [!NOTE]  
>  データベース ダイアグラムを保存すると、データベースに新しいテーブルが追加されます。  
  
### <a name="to-add-an-existing-table-to-a-diagram"></a>ダイアグラムに既存のテーブルを追加するには  
  
1.  テーブルを編集するデータベースに接続していることを確認します。  
  
2.  **[テーブル]** フォルダーでテーブルを選択します。  
  
3.  データベース ダイアグラムにテーブルをドラッグします。  
  
4.  マウスのボタンを離します。  
  
> [!NOTE]  
>  選択したテーブルがダイアログの他のテーブルとの間にリレーションシップを持つ場合は、自動的にリレーションシップの線が引かれます。  
  
### <a name="to-add-related-tables-to-a-diagram"></a>ダイアグラムに関連テーブルを追加するには  
  
1.  データベース ダイアグラムで、外部キー制約を含む 1 つ以上のテーブルを選択します。  
  
2.  選択したテーブルの 1 つを右クリックし、 **[関連テーブルの追加]** をクリックします。  
  
> [!NOTE]  
>  選択したテーブルから外部キー制約によって参照されるテーブルと、選択したテーブルを外部キー制約によって参照するテーブルの両方が、ダイアグラムに追加されます。  
  
## <a name="see-also"></a>参照  
 [データベース ダイアグラムを扱う&#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [データベース ダイアグラムでのテーブルの使用 (Visual Database Tools)](work-with-tables-in-database-diagram-visual-database-tools.md)  
  
  
