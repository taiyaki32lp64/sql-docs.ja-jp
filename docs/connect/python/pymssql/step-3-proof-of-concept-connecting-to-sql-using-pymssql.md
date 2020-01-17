---
title: 'ステップ 3: pymssql を使用した SQL への接続を概念実証する | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2246ddeb-7c2f-46f3-8a91-cdd718d39b40
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27b56a20a0456bef04553c614432bde270d8e98d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935777"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-pymssql"></a>ステップ 3: pymssql を使用した SQL への接続を概念実証する
[!INCLUDE[Driver_Python_Download](../../../includes/driver_python_download.md)]

この例は概念実証としてのみ検討してください。  わかりやすさのためにサンプル コードは簡略化されており、Microsoft が推奨するベスト プラクティスを表しているとは限りません。  
  
## <a name="step-1--connect"></a>手順 1: 接続する  
  
SQL Database に接続するには、 [pymssql](https://pymssql.org/en/latest/ref/pymssql.html)関数を使用します。  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
```  
  
  
## <a name="step-2--execute-query"></a>手順 2: クエリを実行する  
  
[Cursor. execute](https://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.execute)関数を使用すると、SQL Database に対するクエリから結果セットを取得できます。 この関数は、基本的に任意のクエリを受け取り、カーソルを使用して反復処理できる結果セットを返し[ます。 fetch one ()](https://pymssql.org/en/latest/ref/pymssql.html#pymssql.Cursor.fetchone)。  
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute('SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC;')  
    row = cursor.fetchone()  
    while row:  
        print str(row[0]) + " " + str(row[1]) + " " + str(row[2])     
        row = cursor.fetchone()  
```  
  
## <a name="step-3--insert-a-row"></a>手順 3: 行を挿入する  
  
この例では、[INSERT](../../../t-sql/statements/insert-transact-sql.md) ステートメントを安全に実行し、[SQL インジェクション](../../../relational-databases/tables/primary-and-foreign-key-constraints.md)の値からアプリケーションを保護するパラメーターを渡す方法を確認します。    
  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express', 'SQLEXPRESS', 0, 0, CURRENT_TIMESTAMP)")  
    row = cursor.fetchone()  
    while row:  
        print "Inserted Product ID : " +str(row[0])  
        row = cursor.fetchone()  
    conn.commit()
    conn.close()
```  
  
## <a name="step-4--rollback-a-transaction"></a>手順 4: トランザクションをロールバックする  
  
このコード例では、次のようなトランザクションの使用方法を示します。  
  
* トランザクションの開始  
* データ行の挿入  
* トランザクションをロールバックして、挿入を元に戻します  
  
```python
    import pymssql  
    conn = pymssql.connect(server='yourserver.database.windows.net', user='yourusername@yourserver', password='yourpassword', database='AdventureWorks')  
    cursor = conn.cursor()  
    cursor.execute("BEGIN TRANSACTION")  
    cursor.execute("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES ('SQL Server Express New', 'SQLEXPRESS New', 0, 0, CURRENT_TIMESTAMP)")  
    conn.rollback()  
    conn.close()
```  
    
  ## <a name="next-steps"></a>次の手順  
  
詳細については、 [Python デベロッパーセンター](https://azure.microsoft.com/develop/python/)を参照してください。
