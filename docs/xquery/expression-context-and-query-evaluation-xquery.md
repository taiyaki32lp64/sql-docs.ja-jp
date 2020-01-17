---
title: 式コンテキストとクエリの評価 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expression context [XQuery]
- XQuery, expression context
- XQuery, query evaluation
- static context
- dynamic context [XQuery]
ms.assetid: 5059f858-086a-40d4-811e-81fedaa18b06
author: rothja
ms.author: jroth
ms.openlocfilehash: d665b16c6b635da8b267ac0549ab8d918af8c06b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038917"
---
# <a name="expression-context-and-query-evaluation-xquery"></a>式コンテキストとクエリの評価 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  式のコンテキストは、式の分析と評価を行うために使用される情報です。 次に、XQuery を評価する際の 2 つのフェーズを示します。  
  
-   **静的コンテキスト**-これは、クエリのコンパイル フェーズ。 クエリの静的分析中に、使用できる情報に基づいて、エラーが発生する場合があります。  
  
-   **動的コンテキスト**-これは、クエリの実行フェーズ。 クエリをコンパイル中のエラーなどの静的エラーが含まれない場合でも、クエリの実行中にエラーが返ることがあります。  
  
## <a name="static-context"></a>静的コンテキスト  
 静的コンテキストの初期化とは、式の静的分析向けに、すべての情報をまとめるプロセスのことです。 静的コンテキストの初期化の一環として、次のことが行われます。  
  
-   **境界空白文字**ポリシーが分離に設定します。 そのため、境界の空白で保持されません、**任意の要素**と**属性**クエリのコンス トラクター。 以下に例を示します。  
  
    ```  
    declare @x xml  
    set @x=''  
    select @x.query('<a>  {"Hello"}  </a>,  
  
        <b> {"Hello2"}  </b>')  
    ```  
  
     XQuery 式の解析時に境界空白文字が取り除かれるので、このクエリは次の結果を返します。  
  
    ```  
    <a>Hello</a><b>Hello2</b>  
    ```  
  
-   次のプレフィックスと名前空間のバインドが初期化されます。  
  
    -   事前定義済みの一連の名前空間。  
  
    -   WITH XMLNAMESPACES を使用して定義されたすべての名前空間。 詳細については、次を参照してください。 [with XMLNAMESPACES を使用したクエリへの名前空間の追加](../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md))。  
  
    -   クエリのプロローグで定義されたすべての名前空間。 プロローグ内の名前空間宣言は、WITH XMLNAMESPACES の名前空間宣言よりもオーバーライドされます。 たとえば、次のクエリでは、WITH XMLNAMESPACES 宣言、名前空間にバインドされるプレフィックス (pd) (`https://someURI`)。 ただし、WHERE 句では、バインドよりもクエリのプロローグがオーバーライドされます。  
  
        ```  
        WITH XMLNAMESPACES ('https://someURI' AS pd)  
        SELECT ProductModelID, CatalogDescription.query('  
            <Product   
                ProductModelID= "{ sql:column("ProductModelID") }"   
                />  
        ') AS Result  
        FROM Production.ProductModel  
        WHERE CatalogDescription.exist('  
            declare namespace  pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
             /pd:ProductDescription[(pd:Specifications)]'  
            ) = 1  
        ```  
  
     これらすべての名前空間のバインドは、静的コンテキストの初期化時に解決されます。  
  
-   型指定されたクエリを実行する場合**xml**列または変数、列または変数に関連付けられた XML スキーマ コレクションのコンポーネントは静的コンテキストにインポートされます。 詳細については、「 [型指定された XML と型指定されていない XML の比較](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)」を参照してください。  
  
-   インポートされたスキーマ内のすべてのアトミック型では、静的コンテキストでキャスト関数も使用できます。 この例を次に示します。 この例でクエリを指定する、型指定されたに対して**xml**変数。 この変数に関連付けられている XML スキーマ コレクションでは、アトミック型である myType が定義されています。 キャスト関数の場合、この型に対応する**myType()** は、静的分析中に使用できます。 クエリ式 (`ns:myType(0)`) は、myType の値を返します。  
  
    ```  
    -- DROP XML SCHEMA COLLECTION SC  
    -- go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <simpleType name="myType">  
                <restriction base="int">  
                 <enumeration value="0" />  
                  <enumeration value="1"/>  
                </restriction>  
          </simpleType>  
          <element name="root" type="ns:myType"/>  
    </schema>'  
    go  
  
    DECLARE @var XML(SC)  
    SET @var = '<root xmlns="myNS">0</root>'  
    -- specify myType() casting function in the query  
    SELECT @var.query('declare namespace ns="myNS"; ns:myType(0)')  
    ```  
  
     次の例では、キャスト関数、 **int**組み込み XML 型が式で指定します。  
  
    ```  
    declare @x xml  
    set @x = ''  
    select @x.query('xs:int(5)')  
    go  
    ```  
  
 静的コンテキストが初期化されてから、クエリ式が分析 (コンパイル) されます。 静的分析では、次のことが行われます。  
  
1.  クエリの解析。  
  
2.  式で指定された関数名や型名の解決。  
  
3.  クエリの静的な型指定。 これにより、クエリがタイプ セーフであることを確認できます。 に、次のクエリが、静的なエラーを返しますなど、 **+** 演算子には、プリミティブ型の引数が必要です。  
  
    ```  
    declare @x xml  
    set @x=''  
    SELECT @x.query('"x" + 4')  
    ```  
  
     次の例では、 **value()** 演算子には、シングルトンが必要です。 XML スキーマの指定に従ってがあります複数\<Elem > 要素。 式を静的に分析することでタイプ セーフではないと判断され、静的エラーが返されます。 エラーを解決するには、単一の結果になることを明示的に指定するように (`data(/x:Elem)[1]`)、式を書き直す必要があります。  
  
    ```  
    DROP XML SCHEMA COLLECTION SC  
    go  
    CREATE XML SCHEMA COLLECTION SC AS '<schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="myNS" xmlns:ns="myNS"  
    xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
          <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
          <element name="Elem" type="string"/>  
    </schema>'  
    go  
  
    declare @x xml (SC)  
    set @x='<Elem xmlns="myNS">test</Elem><Elem xmlns="myNS">test2</Elem>'  
    SELECT @x.value('declare namespace x="myNS"; data(/x:Elem)[1]','varchar(20)')  
    ```  
  
     詳細については、次を参照してください。 [XQuery と静的な型指定](../xquery/xquery-and-static-typing.md)します。  
  
### <a name="implementation-restrictions"></a>実装の制限  
 次に、静的コンテキストに関する制限事項を示します。  
  
-   XPath 互換性モードはサポートされません。  
  
-   XML の構築では、分離構築モードだけがサポートされます。 これが既定の設定です。 構築される要素ノードの型は、そのため、 **xdt: 型指定されていない**型で、属性は**xdt:untypedAtomic**型。  
  
-   順序付けられた順序モードだけがサポートされます。  
  
-   XML 領域の分離ポリシーだけがサポートされます。  
  
-   基本 URI 機能はサポートされません。  
  
-   **fn:doc()** はサポートされていません。  
  
-   **fn:collection()** はサポートされていません。  
  
-   XQuery の静的フラッガは提供されません。  
  
-   関連付けられている照合順序、 **xml**データ型を使用します。 この照合順序は常に Unicode コードポイントの照合順序に設定されます。  
  
## <a name="dynamic-context"></a>動的コンテキスト  
 動的コンテキストとは、式の実行時に使用できる必要のある情報のことです。 静的コンテキスト以外に、動的コンテキストの一環として、次の情報が初期化されます。  
  
-   次に示すように、コンテキスト アイテム、コンテキストの位置、コンテキスト サイズなどの式のフォーカスが初期化されます。 これらすべての値で上書きできますが、 [nodes() メソッド](../t-sql/xml/nodes-method-xml-data-type.md)します。  
  
    -   **Xml**データ型は、コンテキスト アイテム、ドキュメント ノードに、処理されているノードを設定します。  
  
    -   コンテキストの位置、つまり処理対象のノードからのコンテキスト アイテムの相対位置が、最初は 1 に設定されます。  
  
    -   コンテキスト サイズ、つまり処理対象のシーケンス内のアイテム数が、最初は 1 に設定されます。これは、常にドキュメント ノードが 1 つあるためです。  
  
### <a name="implementation-restrictions"></a>実装の制限  
 次に、動的コンテキストに関する制限事項を示します。  
  
-   **現在の日付と時刻**コンテキスト関数では、 **fn:current--日付**、 **fn:current--時間**、および**fn:current--dateTime**、いません。サポートされています。  
  
-   **暗黙のタイム ゾーン**UTC + 0 に固定されており、変更できません。  
  
-   **Fn:doc()** 関数がサポートされていません。 すべてのクエリに対して実行されます**xml**列または変数を入力します。  
  
-   **Fn:collection()** 関数がサポートされていません。  
  
## <a name="see-also"></a>参照  
 [XQuery の基礎](../xquery/xquery-basics.md)   
 [型指定された XML と型指定されていない XML の比較](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [XML スキーマ コレクション &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
