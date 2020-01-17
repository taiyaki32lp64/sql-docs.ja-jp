---
title: 選択的 XML インデックスのパスと最適化ヒント | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
ms.assetid: 486ee339-165b-4aeb-b760-d2ba023d7d0a
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: e4ffb1cc9a2b63047c6ade58d82001a2e0ebea4c
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257611"
---
# <a name="specify-paths-and-optimization-hints-for-selective-xml-indexes"></a>選択的 XML インデックスのパスと最適化ヒントの指定
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  このトピックでは、選択的な XML インデックスを作成または変更するときに、インデックス設定用のインデックス ヒントと最適化ヒントへのノード パスを指定する方法について説明します。  
  
 ノード パスと最適化ヒントは、次のいずれかのステートメントで同時に指定します。  
  
-   **CREATE** ステートメントの **FOR** 句の中。 詳細については、「[CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md)」を参照してください。  
  
-   **ALTER** ステートメントの **ADD** 句の中。 詳細については、「[ALTER INDEX &#40;選択的 XML インデックス&#41;](../../t-sql/statements/alter-index-selective-xml-indexes.md)」を参照してください。  
  
 選択的 XML インデックスの詳細については、「 [選択的 XML インデックス &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)」を参照してください。  
  
##  <a name="untyped"></a> 型指定されていない XML での XQuery 型と SQL Server 型について  
 選択的 XML インデックスは、XQuery 型と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型という 2 つの型システムをサポートします。 インデックスを設定するパスを使用して、XQuery 式、または XML データ型の value() メソッドの戻り値の型のいずれかと一致させることができます。  
  
-   インデックスを設定するパスに注釈が設定されていない場合、または XQUERY キーワードを使用して注釈が設定されている場合、パスは XQuery 式と一致します。 XQUERY 注釈付きノード パスには 2 種類のバリエーションがあります。  
  
    -   XQUERY キーワードと XQuery データ型を指定しない場合は、既定のマッピングが使用されます。 通常、ストレージとパフォーマンスは最適ではありません。  
  
    -   XQUERY キーワード、XQuery データ型、および他の最適化ヒント (省略可能) を指定すると、パフォーマンスと効率を最大限に高めたストレージを実現できます。 ただし、キャストが失敗する可能性があります。  
  
-   インデックスを設定するパスに SQL キーワードによる注釈が設定されている場合、パスは XML データ型の value() メソッドの戻り値の型と一致します。 適切な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型を指定します。これは value() メソッドから戻ることが想定される戻り値の型です。  
  
 XQuery 式の XML 型システムと XML データ型の value() メソッドに適用される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型システムには、多少の違いがあります。 これらの違いを次に示します。  
  
-   XQuery 型システムは、末尾の空白を認識します。 たとえば、文字列 "abc" と "abc " は、XQuery 型セマンティックでは等しくありませんが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではこれらの文字列は等しくなります。  
  
-   XQuery の浮動小数点データ型は、+/- ゼロと +/- 無限大という特殊な値をサポートします。 これらの特殊な値は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の浮動小数点データ型ではサポートされません。  
  
### <a name="xquery-types-in-untyped-xml"></a>型指定されていない XML での XQuery 型  
  
-   XQuery 型は、すべての XML データ型の value() メソッドを含むすべてのメソッド内の XQuery 式と一致します。  
  
-   XQuery 型は、次の最適化ヒントをサポートします: ()、SINGLETON、DATA TYPE、および MAXLENGTH。  
  
 型指定されていない XML に対する XQuery 式では、2 つの操作モードから選択できます。  
  
-   **既定のマッピング モード**。 このモードでは、選択的 XML インデックスの作成時にパスのみを指定します。  
  
-   **ユーザー指定のマッピング モード**。 このモードでは、パスと省略可能な最適化ヒントの両方を指定します。  
  
 既定のマッピング モードは、常に安全で一般的なストレージ オプションを使用します。 任意の型の式と一致させることができます。 既定のマッピング モードの限界は、最適化されたパフォーマンスよりも小さくなります。これは、実行時に多数のキャストが必要であり、セカンダリ インデックスを使用できないためです。  
  
 既定のマッピングで作成される選択的 XML インデックスの例を次に示します。 3 つのパスのすべてで、既定のノード型 (**xs:untypedAtomic**) とカーディナリティが使用されます。  
  
```sql  
CREATE SELECTIVE XML INDEX example_sxi_UX_default  
ON Tbl(xmlcol)  
FOR  
(  
mypath01 =  '/a/b',  
mypath02 = '/a/b/c',  
mypath03 = '/a/b/d'  
)  
```  
  
 ユーザー指定のマッピング モードでは、ノードの型とカーディナリティを指定することで、パフォーマンスを向上させることができます。 ただし、このパフォーマンスの向上は、安全性の放棄 (キャストが失敗する可能性があります) と汎用性の放棄 (指定した型のみが選択的 XML インデックスと一致します) によって実現されます。  
  
 型指定されていない XML でサポートされる XQuery の型を次に示します。  
  
-   **xs:boolean**  
  
-   **xs:double**  
  
-   **xs:string**  
  
-   **xs:date**  
  
-   **xs:time**  
  
-   **xs:dateTime**  
  
 型が指定されていない場合、ノードは **xs:untypedAtomic** データ型と見なされます。  
  
 選択的 XML インデックスは、次に示す方法で最適化できます。  
  
```sql  
CREATE SELECTIVE XML INDEX example_sxi_UX_optimized  
ON Tbl(xmlcol)  
FOR  
(  
mypath= '/a/b' as XQUERY 'node()',  
pathX = '/a/b/c' as XQUERY 'xs:double' SINGLETON,  
pathY = '/a/b/d' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON  
)  
-- mypath - Only the node value is needed; storage is saved.  
-- pathX - Performance is improved; secondary indexes are possible.  
-- pathY - Performance is improved; secondary indexes are possible; storage is saved.  
```  
  
### <a name="sql-server-types-in-untyped-xml"></a>型指定されていない XML での SQL Server 型  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型は、value() メソッドの戻り値の型と一致します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型は、次の最適化ヒントをサポートします: SINGLETON。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型を返すパスでは、型を必ず指定する必要があります。 value() メソッドで使用するものと同じ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型を使用します。  
  
 次のクエリを考えてみます。  
  
```sql  
SELECT T.record,  
    T.xmldata.value('(/a/b/d)[1]', 'NVARCHAR(200)')  
FROM myXMLTable T  
```  
  
 指定されたクエリは、NVARCHAR(200) データ型にパックされたパス `/a/b/d` の値を返すため、ノード用に指定するデータ型は明白です。 ただし、ノードのカーディナリティを型指定されていない XML で指定するスキーマはありません。 ノード `d` を親ノード `b`の下に最大で 1 つ表示するには、次に示すように、SINGLETON 最適化ヒントを使用する XML インデックスを作成します。  
  
```sql  
CREATE SELECTIVE XML INDEX example_sxi_US  
ON Tbl(xmlcol)  
FOR  
(  
node1223 = '/a/b/d' as SQL NVARCHAR(200) SINGLETON  
)  
```  
  
  
##  <a name="typed"></a> 型指定された XML に対する選択的 XML インデックスのサポートについて  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の型指定された XML は、特定の XML ドキュメントに関連付けられたスキーマです。 このスキーマは、ノードの全体的なドキュメントの構造と型を定義します。 スキーマが存在する場合、選択的 XML インデックスは、ユーザーがパスを昇格したときのスキーマ構造を適用することで、パスの XQUERY 型を指定する必要がないようにします。  
  
 選択的 XML インデックスは、次の XSD 型をサポートします。  
  
-   **xs:anyUri**  
  
-   **xs:boolean**  
  
-   **xs:date**  
  
-   **xs:dateTime**  
  
-   **xs:day**  
  
-   **xs:decimal**  
  
-   **xs:double**  
  
-   **xs:float**  
  
-   **xs:int**  
  
-   **xs:integer**  
  
-   **xs:language**  
  
-   **xs:long**  
  
-   **xs:name**  
  
-   **xs:NCName**  
  
-   **xs:negativeInteger**  
  
-   **xs:nmtoken**  
  
-   **xs:nonNegativeInteger**  
  
-   **xs:nonPositiveInteger**  
  
-   **xs:positiveInteger**  
  
-   **xs:qname**  
  
-   **xs:short**  
  
-   **xs:string**  
  
-   **xs:time**  
  
-   **xs:token**  
  
-   **xs:unsignedByte**  
  
-   **xs:unsignedInt**  
  
-   **xs:unsignedLong**  
  
-   **xs:unsignedShort**  
  
 スキーマが関連付けられたドキュメントに対して選択的 XML インデックスを作成する場合は、インデックスの設定または変更時に XQUERY 型を指定すると、エラーが返されます。 ユーザーは、パスの昇格部分で SQL 型の注釈を使用できます。 SQL 型はスキーマに定義された XSD 型の有効な変換である必要があり、そうでない場合はエラーがスローされます。 日付型または時刻型を除いて、XSD に十分な表現が指定されたすべての SQL 型がサポートされます。  
  
> [!NOTE]  
>  選択的インデックスは、選択的 XML インデックスのパスの昇格に指定された型が、value() メソッドの戻り値の型と同じ場合に使用されます。  
  
 型指定された XML ドキュメントで、次の最適化ヒントを使用できます。  
  
-   node() 最適化ヒント。  
  
-   MAXLENGTH 最適化ヒントを xs:string 型と共に使用して、インデックス値を短縮できます。  
  
 最適化ヒントの詳細については、「 [最適化ヒントの指定](#hints)」を参照してください。  
  
##  <a name="paths"></a> パスの指定  
 選択的 XML インデックスを使用して、実行する予定のクエリに関連する格納された XML データから、ノードのサブセットにのみインデックスを設定できます。 関連するノードのサブセットが XML ドキュメント内のノードの総数よりも大幅に少ない場合、選択的 XML インデックスには、関連するノードだけが格納されます。 選択的 XML インデックスを有効利用するには、インデックスを設定する適切なノードのサブセットを識別します。  
  
### <a name="choosing-the-nodes-to-index"></a>インデックスを設定するノードの選択  
 次の 2 つの単純な原則を使用して、選択的 XML インデックスに追加する適切なノードのサブセットを識別できます。  
  
1.  **原則 1**: 特定の XQuery 式を評価するには、調べる必要があるすべてのノードにインデックスを設定します。  
  
    -   その存在または値が XQuery 式で使用されるすべてのノードにインデックスを設定します。  
  
    -   XQuery 述語が適用される XQuery 式に含まれるすべてのノードにインデックスを設定します。  
  
     このトピックの [サンプル XML ドキュメント](#sample) に対する次の単純なクエリを考慮してください。  
  
    ```sql  
    SELECT T.record FROM myXMLTable T  
    WHERE T.xmldata.exist('/a/b[./c = "43"]') = 1  
    ```  
  
     このクエリを満足させる XML インスタンスを返すため、選択的 XML インデックスは、すべての XML インスタンス内の次の 2 つのノードを調べます。  
  
    -   ノード `c`。その値が XQuery 式で使用されているため。  
  
    -   ノード `b`。述語が、XQuery 式の中でノード`b` に適用されるため。  
  
2.  **原則 2**: 最大限のパフォーマンスを得るには、特定の XQuery 式を評価するために必要なすべてのノードにインデックスを設定します。 ノードの一部にのみインデックスを設定した場合、選択的 XML インデックスは、インデックス付きノードのみを含むサブ式の評価を向上させます。  

 上に示した SELECT ステートメントのパフォーマンスを向上させるには、次に示す選択的 XML インデックスを作成します。  
  
```sql  
CREATE SELECTIVE XML INDEX simple_sxi  
ON Tbl(xmlcol)  
FOR  
(  
    path123 =  '/a/b',  
    path124 =  '/a/b/c'  
)  
```  
  
### <a name="indexing-identical-paths"></a>同一パスのインデックス設定  
 同一パスを異なる名前で同じデータ型として昇格させることはできません。 たとえば、次のクエリでは、 `pathOne` と `pathTwo` が同じため、エラーが発生します。  
  
```sql  
CREATE SELECTIVE INDEX test_simple_sxi ON T1(xmlCol)  
FOR  
(  
    pathOne = 'book/authors/authorID' AS XQUERY 'xs:string',  
    pathTwo = 'book/authors/authorID' AS XQUERY 'xs:string'  
)  
```  
  
 ただし、同一パスを異なる名前を持つ異なるデータ型として昇格させることはできます。 たとえば、次のクエリはデータ型が異なるため、許容されます。  
  
```sql  
CREATE SELECTIVE INDEX test_simple_sxi ON T1(xmlCol)  
FOR  
(  
    pathOne = 'book/authors/authorID' AS XQUERY 'xs:double',  
    pathTwo = 'book/authors/authorID' AS XQUERY 'xs:string'  
)  
```  
  
### <a name="examples"></a>例  
 異なる XQuery 型用のインデックスを設定するために適切なノードを選択するいくつかの例を次に示します。  
  
 **例 1**  
  
 次に示すのは、exist() メソッドを使用する単純な XQuery です。  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b/c/d/e/h') = 1  
```  
  
 次の表に、このクエリで選択的 XML インデックスの使用を可能にするためにインデックスを設定する必要があるノードを示します。  
  
|インデックスに含めるノード|このノードにインデックスを設定する理由|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e/h**|ノード `h` が exist() メソッドで評価される。|  
  
 **例 2**  
  
 次に示すのは、前の XQuery のより複雑なバリエーションです。ここでは述語が適用されます。  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b/c/d/e[./f = "SQL"]') = 1  
```  
  
 次の表に、このクエリで選択的 XML インデックスの使用を可能にするためにインデックスを設定する必要があるノードを示します。  
  
|インデックスに含めるノード|このノードにインデックスを設定する理由|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|述語がノード `e`に適用される。|  
|**/a/b/c/d/e/f**|ノード `f` の値が述語内で評価される。|  
  
 **例 3**  
  
 次に示すのは、value() 句を使用するさらに複雑なクエリです。  
  
```sql  
SELECT T.record,  
    T.xmldata.value('(/a/b/c/d/e[./f = "SQL"]/g)[1]', 'nvarchar(100)')  
FROM myXMLTable T  
```  
  
 次の表に、このクエリで選択的 XML インデックスの使用を可能にするためにインデックスを設定する必要があるノードを示します。  
  
|インデックスに含めるノード|このノードにインデックスを設定する理由|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|述語がノード `e`に適用される。|  
|**/a/b/c/d/e/f**|ノード `f` の値が述語内で評価される。|  
|**/a/b/c/d/e/g**|ノード `g` の値が value() メソッドによって返される。|  
  
 **例 4**  
  
 次に示すのは、exist() 句の中で FLWOR 句を使用するクエリです (FLWOR という名前は、XQuery FLWOR 式を構成できる 5 つの句 (for、let、where、order by、および return) に由来します)。  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('  
  For $x in /a/b/c/d/e  
  Where $x/f = "SQL"  
  Return $x/g  
') = 1  
```  
  
 次の表に、このクエリで選択的 XML インデックスの使用を可能にするためにインデックスを設定する必要があるノードを示します。  
  
|インデックスに含めるノード|このノードにインデックスを設定する理由|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|ノード `e` の存在が FLWOR 区の中で評価される。|  
|**/a/b/c/d/e/f**|ノード `f` の値が FLWOR 句の中で評価される。|  
|**/a/b/c/d/e/g**|ノード `g` の存在が exist() メソッドによって評価される。|  
  
  
##  <a name="hints"></a> 最適化ヒントの指定  
 省略可能な最適化ヒントを使用して、選択的 XML インデックスによってインデックス設定されるノードのマッピングの詳細を指定できます。 たとえば、ノードのデータ型とカーディナリティ、およびデータの構造に関する特定の情報を指定できます。 この追加情報により、マッピングに対するサポートが向上します。 さらに、パフォーマンスの向上またはストレージの節約、あるいはその両方が実現します。  
  
 最適化ヒントの使用は任意です。 常に既定のマッピングをそのまま使用できます。これらは信頼できますが、最適化されたパフォーマンスとストレージを提供しない場合があります。  
  
 一部の最適化ヒント (SINGLETON ヒントなど) には、データに対する制約があります。 場合によっては、これらの制約が満たされないとエラーが発生します。  
  
### <a name="benefits-of-optimization-hints"></a>最適化ヒントの利点  
 次の表に、より効率的なストレージまたはパフォーマンスの向上をサポートする最適化ヒントを示します。  
  
|最適化ヒント|より効率的なストレージ|パフォーマンスの向上|  
|-----------------------|----------------------------|--------------------------|  
|**node()**|はい|いいえ|  
|**SINGLETON**|いいえ|はい|  
|**DATA TYPE**|はい|はい|  
|**MAXLENGTH**|はい|はい|  
  
### <a name="optimization-hints-and-data-types"></a>最適化ヒントとデータ型  
 ノードに XQuery データ型または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型としてインデックスを設定できます。 次の表に、各データ型でサポートされる最適化ヒントを示します。  
  
|最適化ヒント|XQuery のデータ型|SQL データ型|  
|-----------------------|-----------------------|--------------------|  
|**node()**|はい|いいえ|  
|**SINGLETON**|はい|はい|  
|**DATA TYPE**|はい|いいえ|  
|**MAXLENGTH**|はい|いいえ|  
  
### <a name="node-optimization-hint"></a>node() 最適化ヒント  
 適用対象:XQuery のデータ型  
  
 node() 最適化ヒントを使用して、一般的なクエリではその値を評価する必要がないノードを指定できます。 このヒントは、通常のクエリがノードの存在のみを評価する必要があるときに必要なメモリ量が減少します (既定では、選択的 XML インデックスは、complex ノード型以外の昇格されたすべてのノードの値を格納します)。  
  
 次の例を確認してください。  
  
```sql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b[./c=5]') = 1  
```  
  
 このクエリを選択的 XML インデックスを使用して評価するには、ノード `b` とノード `c`を昇格します。 ただし、ノード `b` の値は必要ないため、次の構文で node() ヒントを使用できます。  
  
 `/a/b/ as node()`  
  
 node() ヒントでインデックス設定されているノードの値がクエリで必要な場合、選択的 XML インデックスは使用できません。  
  
### <a name="singleton-optimization-hint"></a>SINGLETON 最適化ヒント  
 適用対象:XQuery データ型または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型  
  
 SINGLETON 最適化ヒントは、ノードのカーディナリティを指定します。 このヒントは、ノードが親または先祖の中で最大で 1 回出現することを事前に通知するため、クエリのパフォーマンスが向上します。  
  
 このトピックの [サンプル XML ドキュメント](#sample) を参考にしてください。  
  
 選択的 XML を使用してこのドキュメントのクエリを実行するには、ノード `d` が親の中で最大 1 回出現するため、そのノードに対して SINGLETON ヒントを指定できます。  
  
 SINGLETON ヒントは指定されているが、ノードがその親または先祖の中で複数回出現した場合は、インデックスの作成時 (既存のデータの場合) またはクエリの実行時 (新規データの場合) にエラーが発生します。  
  
### <a name="data-type-optimization-hint"></a>DATA TYPE 最適化ヒント  
 適用対象:XQuery のデータ型  
  
 DATA TYPE 最適化ヒントを使用して、インデックス付きノードに対して XQuery データ型または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型を指定できます。 このデータ型は、選択的 XML インデックスのデータ テーブル内のインデックス付きノードに対応する列で使用されます。  
  
 既存の値の指定されたデータ型へのキャストが失敗した場合でも、インデックスへの挿入操作は失敗しません。ただし、インデックスのデータ テーブルには NULL 値が挿入されます。  
  
### <a name="maxlength-optimization-hint"></a>MAXLENGTH 最適化ヒント  
 適用対象:XQuery のデータ型  
  
 MAXLENGTH 最適化ヒントを使用して、xs:string データの長さを制限できます。 VARCHAR データ型または NVARCHAR データ型を指定するときに長さを指定するため、MAXLENGTH は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型には関連しません。  
  
 既存の文字列が指定された MAXLENGTH よりも長い場合は、その値をインデックスに挿入する操作は失敗します。  
  
  
##  <a name="sample"></a> 例で参照されるサンプル XML ドキュメント  
 このトピックの例では、次に示すサンプル XML ドキュメントが参照されています。  
  
```xml  
<a>  
    <b>  
         <c atc="aa">10</c>  
         <c atc="bb">15</c>  
         <d atd1="dd" atd2="ddd">md </d>  
    </b>  
     <b>  
        <c></c>  
        <c atc="">117</c>  
     </b>  
</a>  
```  
  
  
## <a name="see-also"></a>参照  
 [選択的 XML インデックス &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [選択的 XML インデックスの作成、変更、および削除](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)  
  
  
