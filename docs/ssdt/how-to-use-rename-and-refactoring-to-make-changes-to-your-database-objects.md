---
title: 方法:名前の変更とリファクタリングを使用して、データベース オブジェクトを変更する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.dbrefactoring.previewdialog
- sql.data.tools.editor.howto.refactoring
- sql.data.tools.dbrefactoring.renamedialog
- sql.data.tools.dbrefactoring.moveschemadialog
- sql.data.tools.dbrefactoring.renameserverdatabasedialog
ms.assetid: f35520e6-8e6e-47b1-87a3-22c0cf2cabdb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0897d9498ca93e915dba5df9c32c4544fe08767d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097472"
---
# <a name="how-to-use-rename-and-refactoring-to-make-changes-to-your-database-objects"></a>方法:名前の変更とリファクタリングを使用して、データベース オブジェクトを変更する
Transact\-SQL エディターの [リファクター] コンテキスト メニューを使用すると、オブジェクトの名前を変更することも別のスキーマに移動することもできます。また、変更をコミットする前に、影響を受ける領域をすべてプレビューすることもできます。 [リファクター] メニューでは、データベース オブジェクトへのすべての参照を完全修飾することも、データベース プロジェクト内の `SELECT` ステートメントに含まれるワイルドカード文字を展開することもできます。  
  
> [!NOTE]  
> 以下に示す手順では、「[接続されているデータベース開発](../ssdt/connected-database-development.md)」および「[プロジェクト指向のオフライン データベース開発](../ssdt/project-oriented-offline-database-development.md)」に示されているこれまでの手順で作成したエンティティを使用します。  
  
### <a name="to-rename-a-type"></a>型名を変更するには  
  
1.  **ソリューション エクスプローラー**で **Products** テーブル (Products.sql) を右クリックし、 **[コードの表示]** をクリックして、Transact\-SQL エディターでスクリプトを開きます。  
  
2.  スクリプト内の `[Products]` を右クリックし、 **[リファクター]** をポイントして **[名前の変更]** をクリックします。  
  
3.  **[新しい名前]** の値を「**Product**」に変更します。 **[変更のプレビュー]** チェック ボックスをオンにしたまま **[OK]** をクリックします。  
  
4.  次の画面では、この名前変更操作による影響を受けるスクリプトの一覧をプレビューできます。 具体的には、`Products` を参照しているすべての箇所が強調表示されます。 この操作は、前の手順で学習した [すべての参照の検索] で行われるタスクによく似ています。 上のペインで任意の部分をクリックし、スクリプト内の実際の変更 (緑色で強調表示されます) を下のペインで確認します。  
  
5.  **[適用]** をクリックします。  
  
6.  テーブル デザイナーまたは Transact\-SQL エディターで既に開いていたスクリプト ファイルについても、変化が生じた箇所は、Transact\-SQL エディターの左側の緑色のバーで強調表示されています。  
  
7.  **ソリューション エクスプローラー**で、**TradeDev.refactorlog** が追加されていることに注意してください。 これをダブルクリックして開きます。 このセッションでのすべての変更が XML 表現で記述されています。  
  
8.  F5 キーを押してプロジェクトをビルドし、ローカル データベースに配置します。  
  
9. **SQL Server オブジェクト エクスプローラー**の **[ローカル]** の下で、**TradeDev** データベースを右クリックして **[更新]** をクリックします。  
  
10. **[テーブル]** を展開し、**Products** テーブルの名前が変更されていることを確認します。  
  
11. **Product** を右クリックし、 **[データの表示]** をクリックします。 名前変更の操作を行っても、既存のデータはそのまま残ります。  
  
### <a name="to-expand-wildcards"></a>ワイルドカードを展開するには  
  
1.  **ソリューション エクスプローラー**で **[関数]** ノードを展開し、**GetProductsBySupplier.sql** をダブルクリックします。  
  
2.  次に示す行のアスタリスクの部分にカーソルを置いて、右クリックします。 **[リファクター]** 、 **[ワイルドカードの展開]** の順にクリックします。  
  
    ```  
    SELECT * from Product p  
    ```  
  
3.  **[変更のプレビュー]** ダイアログ ボックスの上のペインで `SELECT * from Product p` をクリックして強調表示します。  
  
4.  **[変更のプレビュー]** の下のペインで、次に示すスクリプトのように `*` が展開されていることを確認します。  
  
    ```  
    [Id], [Name], [ShelfLife], [SupplierId], [CustomerId]  
    ```  
  
5.  **[適用]** をクリックします。  展開の操作で生じた変更を含む行が、左側の緑色のバーで強調表示されています。  
  
### <a name="to-fully-qualify-database-object-names"></a>データベース オブジェクト名を完全修飾するには  
  
1.  Transact\-SQL エディターで **GetProductsBySupplier.sql** が開いていることを確認します。  
  
2.  次に示す行の `Product` の部分にカーソルを置いて、右クリックします。 **[リファクター]** をポイントし、 **[完全修飾名]** をクリックします。  
  
    ```  
    SELECT [Id], [Name], [ShelfLife], [SupplierId], [CustomerId] from Product p  
    ```  
  
3.  **[変更のプレビュー]** ダイアログ ボックスの **[適用]** をクリックします。  すべてのオブジェクト参照が、オブジェクトのスキーマ名と、オブジェクトに親があれば親の名前を含む形式に更新されています。  
  
    ```  
    SELECT [p].[Id], [p].[Name], [p].[ShelfLife], [p].[SupplierId], [p].[CustomerId] from [dbo].[Product] p  
    ```  
  
### <a name="to-move-schema"></a>スキーマを移動するには  
  
1.  移動するオブジェクトを右クリックします。 **[リファクター]** 、 **[移動スキーマ]** の順にクリックします。  
  
2.  **[新しいスキーマ]** ボックスで、オブジェクトの移動先となるスキーマの名前を入力します。 [OK] をクリックします。  
  
    **[変更をプレビューする]** チェック ボックスをオンにした場合、 **[変更のプレビュー]** ダイアログ ボックスが表示されます。 それ以外の場合は、オブジェクト名が更新され、オブジェクトが新しいスキーマに移動します。  
  
