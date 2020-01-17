---
title: 何かテーブル以外のアイテム (Visual Database Tools) を使用してクエリを作成する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- user-defined functions [SQL Server], queries
- queries [SQL Server], creating
ms.assetid: 8e4a1f0a-8a42-4733-be8d-e21d6dbddb33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f6cd83135da7e5c9f4dac9e41ff562551d14ab20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63184326"
---
# <a name="create-queries-using-something-besides-a-table-visual-database-tools"></a>テーブル以外のアイテムを使用したクエリの作成 (Visual Database Tools)
  検索クエリを作成するときは常に、必要な列、必要な行、およびクエリ プロセッサが基になるデータを検索する場所を明示します。 通常、この基になるデータは 1 つのテーブル、または相互に結合された複数のテーブルで構成されています。 ただし、基になるデータは、テーブル以外のソースを使用してもかまいません。 実際、ビュー、クエリ、シノニム、またはテーブルを返すユーザー定義関数のデータを使用できます。  
  
## <a name="using-a-view-in-place-of-a-table"></a>テーブルに代わるビューの使用  
 ビューから行を選択できます。 たとえば、"ExpensiveBooks" という名前のビューを含むデータベースがあり、このビューの各行には価格が $19.99 を超える書籍の書名が格納されているものとします。 ビューの定義は次のようになります。  
  
```  
SELECT *  
FROM titles  
WHERE price > 19.99  
  
```  
  
 ExpensiveBooks ビューから心理学の本を選択するだけで、高価な心理学の本を選択できます。 結果の SQL ステートメントは次のようになります。  
  
```  
SELECT *  
FROM ExpensiveBooks  
WHERE type = 'psychology'  
  
```  
  
 同様に、JOIN 演算でビューを使用できます。 たとえば、 テーブルと  ビューを結合するだけで、高価な書籍の販売状況を検索できます。 結果の SQL ステートメントは次のようになります。  
  
```  
SELECT *  
FROM sales   
         INNER JOIN   
         ExpensiveBooks   
         ON sales.title_id   
         =  ExpensiveBooks.title_id  
  
```  
  
 ビューをクエリに追加する方法については、「[クエリへのテーブルの追加 (Visual Database Tools)](visual-database-tools.md)」を参照してください。  
  
## <a name="using-a-query-in-place-of-a-table"></a>テーブルに代わるクエリの使用  
 クエリから行を選択できます。 たとえば、共著本、つまり複数の著者によって書かれた本の署名と識別子を取得するクエリが、既に作成されているとします。 SQL ステートメントは次のようになります。  
  
```  
SELECT   
     titles.title_id, title, type  
FROM   
     titleauthor   
         INNER JOIN  
         titles   
         ON titleauthor.title_id   
         =  titles.title_id   
GROUP BY   
     titles.title_id, title, type  
HAVING COUNT(*) > 1  
  
```  
  
 この結果を利用する別のクエリを作成できます。 たとえば、心理学の共著本を取得するクエリを記述できます。 新しいクエリのデータの参照元として、既存のクエリを使用できます。 結果の SQL ステートメントは次のようになります。  
  
```  
SELECT   
    title  
FROM   
    (  
    SELECT   
        titles.title_id,   
        title,   
        type  
    FROM   
        titleauthor   
            INNER JOIN  
            titles   
            ON titleauthor.title_id   
            =  titles.title_id   
    GROUP BY   
        titles.title_id,   
        title,   
        type  
    HAVING COUNT(*) > 1  
    )   
    co_authored_books  
WHERE     type = 'psychology'  
  
```  
  
 太字で表されたテキストは、新しいクエリでデータの参照元として使用される既存のクエリを示しています。 新しいクエリでは、既存のクエリに対するエイリアスとして "co_authored_books" を使用しています。 エイリアスの詳細については、「[テーブルの別名の作成 (Visual Database Tools)](create-table-aliases-visual-database-tools.md)」と「[列の別名の作成 (Visual Database Tools)](create-column-aliases-visual-database-tools.md)」を参照してください。  
  
 同様に、JOIN 処理でクエリを使用することもできます。 たとえば、ExpensiveBooks ビューと共著本を取得するクエリを結合するだけで、高価な共著本の売り上げ情報を検索できます。 結果の SQL ステートメントは次のようになります。  
  
```  
SELECT   
    ExpensiveBooks.title  
FROM   
    ExpensiveBooks   
        INNER JOIN  
        (  
        SELECT   
            titles.title_id,   
            title,   
            type  
        FROM   
            titleauthor   
                INNER JOIN  
                titles   
                ON titleauthor.title_id   
                =  titles.title_id   
        GROUP BY   
            titles.title_id,   
            title,   
            type  
        HAVING COUNT(*) > 1  
        )  
```  
  
 クエリをクエリに追加する方法については、「[クエリへのテーブルの追加 (Visual Database Tools)](visual-database-tools.md)」を参照してください。  
  
## <a name="using-a-user-defined-function-in-place-of-a-table"></a>テーブルに代わるユーザー定義関数の使用  
 SQL Server 2000 以降では、テーブルを返すユーザー定義関数を作成できます。 この種の関数は、複雑な論理または手順論理を実行するときに役に立ちます。  
  
 たとえば、employee テーブルに employee.manager_emp_id という列があり、manager_emp_id から employee.emp_id への外部キーが存在するものとします。 employee テーブルの各行の manager_emp_id 列は従業員の上司を示します。 正確に言えば、manager_emp_id 列は従業員の上司の emp_id を示しているということになります。 これを利用すると、特定の上級管理者の組織階層に所属する各従業員に一対一で対応する行を含むテーブルを返す、ユーザー定義関数を作成できます。 この関数に fn_GetWholeTeam という名前を付け、組織の情報を取得する管理者の emp_id を入力変数として取るように関数をデザインします。  
  
 データの参照元として fn_GetWholeTeam 関数を使用するクエリを作成できます。 結果の SQL ステートメントは次のようになります。  
  
```  
SELECT *   
FROM   
     fn_GetWholeTeam ('VPA30890F')  
  
```  
  
 "VPA30890F" は、取得の対象となる組織の管理者の emp_id を示しています。 ユーザー定義関数をクエリに追加する方法については、「[クエリへのテーブルの追加 (Visual Database Tools)](visual-database-tools.md)」を参照してください。 ユーザー定義関数の詳しい説明については、「[ユーザー定義関数](../../relational-databases/user-defined-functions/user-defined-functions.md)」を参照してください。  
  
  
