---
title: 方法:クエリを使用して新しいデータベース オブジェクトを作成する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: ac983ac7-f9c4-495d-8a99-e1ba370fb271
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 778783c61be2d3b9cfac784d271bce584ef37f68
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897197"
---
# <a name="how-to-create-new-database-objects-using-queries"></a>方法:クエリを使用して新しいデータベース オブジェクトを作成する
スクリプトを使用して、ビュー、ストアド プロシージャ、関数、トリガー、ユーザー定義型などを作成または編集する場合は、Transact\-SQL エディターを使用します。 Transact\-SQL エディターは IntelliSense およびその他の言語サポートを提供します。 詳しくは、「[Transact-SQL エディターを使用したスクリプトの編集と実行](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)」をご覧ください。  
  
Transact\-SQL エディターは、 **[コードの表示]** コンテキスト メニューを使用して、接続されているデータベースまたはプロジェクトのデータベース エンティティを開くと起動されます。 SQL Server オブジェクト エクスプローラーの **[新しいクエリ]** コンテキスト メニューを使用するときと、データベース プロジェクトに新しいスクリプト オブジェクトを追加するときにも、このエディターが自動的に開きます。 データベースに対するクエリを実行するときに、まだデータベースに接続していない場合にも、 **[SQL]** メニューの **[Transact-SQL エディター]** メニューを選択して **[新しいクエリ接続]** ダイアログ ボックスからデータベースに接続し、Transact\-SQL エディターを起動できます。  
  
> [!WARNING]  
> 以下に示す手順では、「[接続されているデータベース開発](../ssdt/connected-database-development.md)」に示されているこれまでの手順で作成したエンティティを使用します。  
  
### <a name="to-create-a-new-table-using-a-transact-sql-query"></a>Transact\-SQL クエリを使用して新しいテーブルを作成するには  
  
1.  **Trade** データベース ノードを右クリックし、 **[新しいクエリ]** をクリックします。  
  
2.  スクリプト ペインに次のコードを貼り付けます。  
  
    ```  
  
    CREATE TABLE [dbo].[Fruits] (  
        [Id]         INT NOT NULL,  
        [Perishable] BIT DEFAULT ((1)) NULL,  
        PRIMARY KEY CLUSTERED ([Id] ASC),  
        FOREIGN KEY ([Id]) REFERENCES [dbo].[Products] ([Id])   
    );  
    ```  
  
3.  Transact\-SQL エディターのツール バーにある **[クエリの実行]** ボタンをクリックして、このクエリを実行します。  
  
4.  **SQL Server オブジェクト エクスプローラー**で **Trade** データベースを右クリックし、 **[更新]** をクリックします。 新しく **Fruits** テーブルがデータベースに追加されていることを確認します。  
  
### <a name="to-create-a-new-function"></a>新しい関数を作成するには  
  
1.  現在の Transact\-SQL エディターで、コードを次のコードに置き換えます。  
  
    ```  
  
    CREATE FUNCTION [dbo].GetProductsBySupplier  
    (  
    @SupplierId int  
    )  
    RETURNS @returntable TABLE   
    (  
    [Id] int NOT NULL,   
    [Name] NVARCHAR (128) NOT NULL,  
    [Shelflife] INT NOT NULL,  
    [SupplierId] INT NOT NULL,  
    [CustomerId] INT NOT NULL  
    )  
    AS  
    BEGIN  
    INSERT @returntable  
    SELECT *  from Products p  
    where p.SupplierId = @SupplierId  
    RETURN   
    END  
    ```  
  
    この関数は、`Products` テーブルの行のうち、`SupplierId` の値が指定されたパラメーターと等しい行をすべて返します。 Transact\-SQL エディターのツール バーにある **[クエリの実行]** ボタンをクリックして、このクエリを実行します。  
  
2.  SQL Server オブジェクト エクスプローラーで、**Trade** ノードの下にある **[プログラミング]** ノードと **[関数]** ノードを展開します。 先ほど作成した新しい関数が、 **[テーブル値関数]** の下に表示されています。  
  
### <a name="to-create-a-new-view"></a>新しいビューを作成するには  
  
1.  現在の Transact\-SQL エディターで、コードを次のコードに置き換えます。 次に、エディターの上にある **[クエリの実行]** をクリックして、このクエリを実行します。  
  
    ```  
    CREATE VIEW [dbo].PerishableFruits   
    AS SELECT p.Id, p.Name FROM dbo.Products p  
    join dbo.Fruits f on f.Id = p.Id  
    where f.Perishable = 1  
    ```  
  
2.  SQL Server オブジェクト エクスプローラーで、**Trade** ノードの下にある **[ビュー]** ノードを展開して、先ほど作成した新しいビューを確認します。  
  
## <a name="see-also"></a>参照  
[テーブルとリレーションシップの管理およびエラーの修正](../ssdt/manage-tables-relationships-and-fix-errors.md)  
[Transact-SQL エディターを使用したスクリプトの編集と実行](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)  
  
