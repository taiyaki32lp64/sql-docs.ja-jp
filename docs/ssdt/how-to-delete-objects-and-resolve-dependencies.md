---
title: 方法:オブジェクトを削除し、依存関係を解決する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- Microsoft.VisualStudio.Data.Tools.Project.HelpKeywords.SqlProjectDropDatabaseConfirmationDialog
- sql.data.tools.dropdatabaseconfirmation.dialog
- sql.data.tools.dropmultipledatabasesconfirmation.dialog
ms.assetid: fb31c2b1-ca4f-4e11-a0b6-5c26430f1c8c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ae25dbc584e564130348507e5aef657823502923
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026613"
---
# <a name="how-to-delete-objects-and-resolve-dependencies"></a>方法:オブジェクトを削除し、依存関係を解決する
**SQL Server オブジェクト エクスプローラー** でオブジェクトの名前変更または削除を行うと、SQL Server Data Tools によって自動的に、依存関係オブジェクトがすべて検出され、必要に応じて名前の変更または依存関係の削除を行うための ALTER スクリプトが用意されます。  
  
> [!WARNING]  
> 以下に示す手順では、「[接続されているデータベース開発](../ssdt/connected-database-development.md)」に示されているこれまでの手順で作成したエンティティを使用します。  
  
### <a name="to-delete-a-database"></a>データベースを削除するには  
  
1.  **SQL Server オブジェクト エクスプローラー**でデータベースを右クリックし、 **[削除]** をクリックします。  
  
2.  **[データベースの削除]** ダイアログ ボックスで既定の設定をすべてそのままにして、 **[OK]** をクリックします。  
  
### <a name="to-rename-a-table"></a>テーブル名を変更するには  
  
1.  テーブル デザイナーおよび Transact\-SQL エディターで、`Customer` テーブルが開いていないことを確認します。  
  
2.  **SQL Server オブジェクト エクスプ ローラー**で **[テーブル]** ノードを展開します。 **Customer** テーブルを右クリックし、 **[名前の変更]** をクリックします。  
  
3.  テーブルの名前を **Customers** に変更して Enter キーを押します。  
  
4.  直ちに、**データベースの更新**操作が自動的に実行されます。 SSDT が自動的に sp_rename ストアド プロシージャを呼び出し、テーブルの名前を変更します。 外部キー制約などの依存オブジェクトがある場合は、これらも更新されます。  
  
    > [!WARNING]  
    > スクリプトベースの依存関係 (ビューからテーブルへの参照など) およびストアド プロシージャについては、SSDT による自動的な更新は行われません。 名前変更の後で**エラー一覧**ペインを使用すると、他の依存関係をすべて確認し、手動で修正できます。  
  
5.  前の「[接続されているデータベースを Power Buffer で更新する方法](../ssdt/how-to-update-a-connected-database-with-power-buffer.md)」の手順に従って、変更を適用します。  
  
6.  **SQL Server オブジェクト エクスプローラー**で再度 **Customers** テーブルを右クリックし、 **[データの表示]** をクリックします。 名前変更の操作を行っても、テーブル データはそのまま残ります。  
  
7.  **Products** テーブルを右クリックして、 **[コードの表示]** をクリックします。 外部キー参照が、名前の変更を反映して自動的に `REFERENCES [dbo].[Customers] ([Id])` に更新されています。  
  
### <a name="to-delete-a-table"></a>テーブルを削除するには  
  
1.  **SQL Server オブジェクト エクスプローラー**で **Customers** テーブルを右クリックし、 **[削除]** をクリックします。  
  
2.  **[データベース更新のプレビュー]** ダイアログ ボックスの **[ユーザー動作]** の下に、SSDT によって特定された依存オブジェクト (ここでは、削除される外部キー参照) がすべて表示されています。  
  
3.  **[データベースの更新]** をクリックします。  
  
4.  **SQL Server オブジェクト エクスプローラー**で **Products** テーブルを右クリックして、 **[コードの表示]** をクリックします。 `Customers` テーブルに対する外部キー参照がなくなっています。  
  
    > [!WARNING]  
    > 削除操作の実行時にテーブル デザイナーまたは Transact\-SQL エディターで **Products** テーブルが既に開いていた場合、外部キー参照の削除を反映する表示更新は自動的に行われません。 さらに、未解決の参照に関するエラーが **[エラー一覧]** に表示される場合もあります。 この問題を解決するには、テーブル デザイナーまたは Transact\-SQL エディターを閉じてから、再度 Products テーブルを開きます。  
  
