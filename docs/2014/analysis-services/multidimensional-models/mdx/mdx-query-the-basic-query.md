---
title: MDX の基本的なクエリ (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- queries [MDX], SELECT statement
- queries [MDX], about queries
- cellsets [MDX]
- SELECT statement [MDX]
- cubes [Analysis Services], SELECT statement
ms.assetid: 4fa5a95a-fec9-4584-875c-dbf030c53e82
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bcd55827377b72040dd142ed1f2fd094c9bd2651
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073876"
---
# <a name="the-basic-mdx-query-mdx"></a>MDX の基本的なクエリ (MDX)
  基本的な多次元式 (MDX) クエリは、MDX の SELECT ステートメント、最もよく使用されるクエリです。 MDX の SELECT ステートメントで結果セットを指定する方法や、SELECT ステートメントの構文と、SELECT ステートメントによる簡単なクエリ作成を学習すれば、MDX を使用して多次元データに対するクエリを実行する方法を理解できます。  
  
## <a name="specifying-a-result-set"></a>結果セットの指定  
 MDX の SELECT ステートメントでは、キューブから返された多次元データのサブセットを格納した結果セットが指定されます。 結果セットを指定するには、MDX クエリに次の情報を含める必要があります。  
  
-   結果セットに含める軸の数。 MDX クエリでは、軸を 128 個まで指定できます。  
  
-   MDX クエリの各軸に含めるメンバーまたは組のセット。  
  
-   MDX クエリのコンテキストを設定するキューブの名前。  
  
-   スライサー軸に含めるメンバーまたは組のセット。 スライサー軸とクエリ軸の詳細については、「[クエリ軸とスライサー軸によるクエリの制限 (MDX)](mdx-query-and-slicer-axes-restricting-the-query.md)」を参照してください。  
  
 MDX の SELECT ステートメントでは、クエリ軸、クエリ対象のキューブ、スライサー軸をそれぞれ指定するために以下の句を使用します。  
  
-   SELECT 句。MDX の SELECT ステートメントのクエリ軸を指定します。 SELECT 句でクエリ軸を作成する方法の詳細については、「[クエリ軸の内容の指定(MDX)](mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)」を参照してください。  
  
-   FROM 句。クエリ対象のキューブを指定します。 FROM 句の詳細については、[の SELECT ステートメント & #40 を参照してください。MDX と #41 です。](/sql/mdx/mdx-data-manipulation-select)  
  
-   省略可能な WHERE 句。スライサー軸で使用するメンバーまたは組を指定して、返されるデータを限定します。 WHERE 句でスライサー軸を作成する方法の詳細については、「[スライサー軸の内容の指定 (MDX)](mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)」を参照してください。  
  
> [!NOTE]  
>  SELECT ステートメントの各種の句の詳細については、「[SELECT ステートメント (MDX)](/sql/mdx/mdx-data-manipulation-select)」を参照してください。  
  
## <a name="select-statement-syntax"></a>SELECT ステートメントの構文  
 SELECT 句、FROM 句、WHERE 句を使用した基本的な SELECT ステートメントの構文を以下に示します。  
  
```  
[ WITH <SELECT WITH clause> [ , <SELECT WITH clause> ... ] ]   
SELECT [ * | ( <SELECT query axis clause>   
    [ , <SELECT query axis clause> ... ] ) ]  
FROM <SELECT subcube clause>   
[ <SELECT slicer axis clause> ]  
[ <SELECT cell property list clause> ]  
```  
  
 MDX の SELECT ステートメントでは、WITH キーワードを使用する構文、軸またはスライサー軸に含める計算されたメンバーを作成するための MDX 関数を使用する構文、クエリの一部として特定のセル プロパティの値を返すための構文など、省略可能な構文をいくつかサポートしています。 MDX の SELECT ステートメントの詳細については、[の SELECT ステートメント & #40 を参照してください。MDX と #41 です。](/sql/mdx/mdx-data-manipulation-select)  
  
### <a name="comparing-the-syntax-of-the-mdx-select-statement-to-sql"></a>MDX の SELECT ステートメントと SQL の構文の比較  
 MDX の SELECT ステートメントの構文形式は、SQL の構文とよく似ています。 ただし、次のような基本的な違いもいくつかあります。  
  
-   MDX 構文では、組またはメンバーを中かっこ ({ }) で囲んでセットと区別します。メンバー、組、およびセットの構文の詳細については、「[メンバー、組、およびセットの操作 (MDX)](working-with-members-tuples-and-sets-mdx.md)」を参照してください。  
  
-   MDX クエリでは、SELECT ステートメントにクエリ軸を 0 個、1 個、2 個、または最大で 128 個まで指定できます。 各軸は、まったく同じ動作をします。SQL の場合は、クエリの行と列とで、動作に大きな違いがあります。  
  
-   MDX クエリで使用するデータ ソースは、SQL クエリと同様に、FROM 句によって指定します。 ただし、MDX の FROM 句では 1 つのキューブしか指定できません。 他のキューブの情報は、LookupCube 関数を使用して値ごとに取得できます。  
  
-   MDX クエリでは、WHERE 句はスライサー軸を指定します。 クエリ内の見えない追加の軸のように作用し、結果セット内のセルに表示される値をスライスします。SQL の WHERE 句とは異なり、クエリの行軸に何が表示されるかに関して直接影響することはありません。 SQL の WHERE 句の機能は、FILTER 関数などの他の MDX 関数を使って実現できます。  
  
## <a name="select-statement-example"></a>SELECT ステートメントの例  
 SELECT ステートメントを使用した基本的な MDX クエリの例を以下に示します。 このクエリは、Southwest という販売地域の 2002 年と 2003 年の売上と税額を格納した結果セットを返します。  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON COLUMNS,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON ROWS  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 このクエリでは、結果セットの情報を次のように定義しています。  
  
-   SELECT 句によって、Measures ディメンションの Sales Amount メンバーと Tax Amount メンバー、Date ディメンションの 2002 メンバーと 2003 メンバーをクエリ軸に設定しています。  
  
-   FROM 句によって、Adventure Works キューブをデータ ソースに指定しています。  
  
-   WHERE 句によって、Sales Territory ディメンションの Southwest メンバーをスライサー軸として定義しています。  
  
 このクエリでは、軸の別名として COLUMNS と ROWS を使用しています。 別名の代わりに、これらの軸の位置を示す序数を使用することも可能です。 それぞれの軸の位置を示す序数を使用して MDX クエリを記述する例を以下に示します。  
  
```  
SELECT  
    { [Measures].[Sales Amount],   
        [Measures].[Tax Amount] } ON 0,  
    { [Date].[Fiscal].[Fiscal Year].&[2002],   
        [Date].[Fiscal].[Fiscal Year].&[2003] } ON 1  
FROM [Adventure Works]  
WHERE ( [Sales Territory].[Southwest] )  
```  
  
 詳細な例については、「[クエリ軸の内容の指定 (MDX)](mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)」および「[スライサー軸の内容の指定 (MDX)](mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [MDX の主な概念 (Analysis Services)](../key-concepts-in-mdx-analysis-services.md)   
 [SELECT ステートメント (MDX)](/sql/mdx/mdx-data-manipulation-select)  
  
  
