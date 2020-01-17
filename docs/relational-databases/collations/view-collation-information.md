---
title: 照合順序情報の表示 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], view
ms.assetid: 1338b4ea-7142-44bc-a3b9-44e54431405f
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bedae7661398ed4281f2da460ad7ce16b5dd82de
ms.sourcegitcommit: 9702dd51410dd610842d3576b24c0ff78cdf65dc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2019
ms.locfileid: "68841616"
---
# <a name="view-collation-information"></a>照合順序情報の表示
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
    
<a name="Top"></a> サーバー、データベース、または列の照合順序は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でオブジェクト エクスプローラーのメニュー オプションを使用するか、 [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して表示できます。  
  
##  <a name="Procedures"></a> 照合順序の設定を表示する方法  
 次のいずれかを使用します。  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **サーバー (SQL Server のインスタンス) の照合順序設定をオブジェクト エクスプローラーで表示するには**  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  インスタンスを右クリックし、 **[プロパティ]** をクリックします。  
  
 **データベースの照合順序設定をオブジェクト エクスプローラーで表示するには**  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、データベースを右クリックして、 **[プロパティ]** をクリックします。  
  
 **列の照合順序設定をオブジェクト エクスプローラーで表示するには**  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、データベースを展開して、 **[テーブル]** を展開します。  
  
3.  目的の列を含んだテーブルを展開し、 **[列]** を展開します。  
  
4.  列を右クリックし、 **[プロパティ]** をクリックします。 照合順序プロパティが空の場合、列が文字データ型ではありません。  
  
###  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **サーバーの照合順序設定を表示するには**  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、ツール バーの **[新しいクエリ]** をクリックします。  
  
2.  クエリ ウィンドウで、SERVERPROPERTY システム関数を使用した次のステートメントを入力します。  
  
    ```sql  
    SELECT CONVERT (varchar(256), SERVERPROPERTY('collation'));  
    ```  
  
3.  また、sp_helpsort システム ストアド プロシージャを使用することもできます。  
  
    ```sql  
    EXECUTE sp_helpsort;  
    ```  
  
 **サポートされているすべての照合順序を表示するには [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、ツール バーの **[新しいクエリ]** をクリックします。  
  
2.  クエリ ウィンドウで、SERVERPROPERTY システム関数を使用した次のステートメントを入力します。  
  
    ```sql  
    SELECT name, description FROM sys.fn_helpcollations();  
    ```  
  
 **データベースの照合順序設定を表示するには**  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、ツール バーの **[新しいクエリ]** をクリックします。  
  
2.  クエリ ウィンドウで、sys.databases システム カタログ ビューを使用した次のステートメントを入力します。  
  
    ```sql  
    SELECT name, collation_name FROM sys.databases;  
    ```  
  
3.  また、DATABASEPROPERTYEX システム関数を使用することもできます。  
  
    ```sql  
    SELECT CONVERT (varchar(256), DATABASEPROPERTYEX('database_name','collation'));  
    ```  
  
 **列の照合順序設定を表示するには**  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、ツール バーの **[新しいクエリ]** をクリックします。  
  
2.  クエリ ウィンドウで、sys.columns システム カタログ ビューを使用した次のステートメントを入力します。  
  
    ```sql  
    SELECT name, collation_name FROM sys.columns WHERE name = N'<insert character data type column name>';  
    ```  
  
 **テーブルと列の照合順序設定を表示するには**  

1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに接続し、ツール バーの **[新しいクエリ]** をクリックします。  
  
2.  クエリ ウィンドウで、sys.columns システム カタログ ビューを使用した次のステートメントを入力します。  
  
    ```sql  
    SELECT t.name TableName, c.name ColumnName, collation_name  
    FROM sys.columns c  
    inner join sys.tables t on c.object_id = t.object_id;  
    ```  



## <a name="see-also"></a>参照  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [照合順序の優先順位 &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [照合順序と Unicode のサポート](../../relational-databases/collations/collation-and-unicode-support.md)      
 [sp_helpsort &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsort-transact-sql.md)  
  
  
