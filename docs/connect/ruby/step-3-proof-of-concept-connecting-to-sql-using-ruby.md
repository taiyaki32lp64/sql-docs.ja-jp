---
title: 'ステップ 3: Ruby を使用した SQL への接続を概念実証する | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cac20b18-0a6d-4243-bbda-a5d1b9476441
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9724fb48f6ae896d9026bfec63056070e2180a8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992490"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-ruby"></a>ステップ 3: Ruby を使用した SQL への接続を概念実証する

この例は概念実証としてのみ検討してください。  わかりやすさのためにサンプル コードは簡略化されており、Microsoft が推奨するベスト プラクティスを表しているとは限りません。  
  
## <a name="step-1--connect"></a>手順 1: 接続する  
  
[TinyTDS::Client](https://github.com/rails-sqlserver/tiny_tds) 関数を使用して SQL データベースに接続します。  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
```  
  
## <a name="step-2--execute-a-query"></a>手順 2: クエリを実行する  
  
次のコードをコピーして、空のファイルに貼り付けます。 test.rb という名前を付けます。 次に、次のコマンドを入力してコマンド プロンプトからこれを実行します。  
  
    ruby test.rb  
  
このコード サンプルでは、[TinyTds::Result](https://github.com/rails-sqlserver/tiny_tds) 関数を使用して、SQL データベースに対するクエリから結果セットを取得しています。 この関数はクエリを受け取り、結果セットを返します。 結果セットは [result.each do |行|](https://github.com/rails-sqlserver/tiny_tds) を使用して反復処理されます。  
  
``` ruby 
    require 'tiny_tds'    
    print 'test'       
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC")  
    results.each do |row|  
    puts row  
    end  
```  
  
## <a name="step-3--insert-a-row"></a>手順 3: 行を挿入する  
  
この例では、[INSERT](../../t-sql/statements/insert-transact-sql.md) ステートメントを安全に実行し、[SQL インジェクション](../../relational-databases/tables/primary-and-foreign-key-constraints.md)の値からアプリケーションを保護するパラメーターを渡す方法を確認します。    
  
Azure で TinyTDS を使用する場合、いくつかの `SET` ステートメントを実行して、現在のセッションが特定の情報を処理する方法を変更することをお勧めします。 コード サンプルには推奨される `SET` ステートメントが含まれています。 たとえば、`SET ANSI_NULL_DFLT_ON` を使用すると、列の null 値の許容状態が明示的に宣言されていない場合でも、作成する新しい列で null 値を許可することができます。  
  
Microsoft SQL Server の [datetime](../../t-sql/data-types/datetime-transact-sql.md) 形式に合わせるには、[strftime](https://ruby-doc.org/core-2.2.0/Time.html#method-i-strftime) 関数を使用して対応する datetime 形式にキャストします。  
  
``` ruby
    require 'tiny_tds'  
    client = TinyTds::Client.new username: 'yourusername@yourserver', password: 'yourpassword',  
    host: 'yourserver.database.windows.net', port: 1433,  
    database: 'AdventureWorks', azure:true  
    results = client.execute("SET ANSI_NULLS ON")  
    results = client.execute("SET CURSOR_CLOSE_ON_COMMIT OFF")  
    results = client.execute("SET ANSI_NULL_DFLT_ON ON")  
    results = client.execute("SET IMPLICIT_TRANSACTIONS OFF")  
    results = client.execute("SET ANSI_PADDING ON")  
    results = client.execute("SET QUOTED_IDENTIFIER ON")  
    results = client.execute("SET ANSI_WARNINGS ON")  
    results = client.execute("SET CONCAT_NULL_YIELDS_NULL ON")  
    require 'date'  
    t = Time.now  
    curr_date = t.strftime("%Y-%m-%d %H:%M:%S.%L")  
    results = client.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate)  
    OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, '#{curr_date}' )")  
    results.each do |row|  
    puts row  
    end  
```
