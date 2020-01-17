---
title: XQuery のキャストの規則の種類 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, type casting
- casting rules [XML in SQL Server]
- explicit casting [SQL Server]
- type casting rules [XML in SQL Server]
- cast as operator
- implicit casting
ms.assetid: f2e91306-2b1b-4e1c-b6d8-a34fb9980057
author: rothja
ms.author: jroth
ms.openlocfilehash: a8372e5079b79cc694ccf51f1b6f7cddcf0fed43
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946216"
---
# <a name="type-casting-rules-in-xquery"></a>XQuery での型キャストの規則
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  次の W3C XQuery 1.0 and XPath 2.0 Functions and Operators 仕様の図は、組み込みのデータ型を示しています。 これには、組み込みのプリミティブ型と組み込み派生型があります。  
  
 ![XQuery 1.0 型階層](../xquery/media/xquery-typing-rules.gif "XQuery 1.0 型の階層")  
  
 このトピックでは、次のいずれかの方法を使用して、ある型から別の型へキャストする場合に適用される型キャストの規則について説明します。  
  
-   使用して実行する明示的なキャスト**としてキャスト**または型コンス トラクター関数 (たとえば、 `xs:integer("5")`)。  
  
-   型の上位変換中に行われる暗黙のキャスト  
  
## <a name="explicit-casting"></a>明示的なキャスト  
 次の表は、組み込みのプリミティブ型間で利用できる型キャストの概要を示しています。  
  
 ![XQuery のキャストの規則について説明します。](../xquery/media/casting-builtin-types.gif "XQuery のキャストの規則について説明します。")  
  
-   この表の規則に基づいて、ある組み込みのプリミティブ型を、別の組み込みのプリミティブ型にキャストできます。  
  
-   あるプリミティブ型は、そのプリミティブ型から派生したすべての型にキャストできます。 キャストなど**xs:decimal**に**xs:integer**からまたは**xs:decimal**に**xs:long**します。  
  
-   派生型は、型階層内の先祖であれば、派生元の組み込みのプリミティブ型も含めて、すべての型にキャストできます。 キャストなど**xs:token**に**xs:normalizedString**または**xs:string**します。  
  
-   ある派生型は、その先祖のプリミティブ型からキャストできる型であれば、任意のプリミティブ型にキャストできます。 たとえば、キャスト**xs:integer**、派生型、 **xs:string**、プリミティブ型のため**xs:decimal**、 **xs:integer**のキャストできるプリミティブの先祖**xs:string**します。  
  
-   ある派生型は、その先祖のプリミティブ型からキャストできるプリミティブ型の先祖であれば、任意の派生型にキャストできます。 キャストなど**xs:integer**に**xs:token**からキャストできるため、 **xs:decimal**に**xs:string**します。  
  
-   ユーザー定義型から組み込み型にキャストする場合の規則は、組み込み型の規則と同じです。 たとえば、定義、 **myInteger**型から派生した**xs:integer**型。 次に、 **myInteger**にキャストできる**xs:token**ため、 **xs:decimal**にキャストできる**xs:string**します。  
  
 次の種類のキャストは、サポートされません。  
  
-   リスト型間のキャストは許可されません。 リストのユーザー定義型と組み込みリスト型の両方をなど含みます**xs:IDREFS**、 **xs:ENTITIES**、および**xs:NMTOKENS**します。  
  
-   キャストまたはからに**xs:QName**はサポートされていません。  
  
-   **xs:NOTATION**と期間の完全な順序のサブタイプ**xdt:yearMonthDuration**と**xdt:dayTimeDuration**はサポートされていません。 したがって、これらの型間のキャストはサポートされません。  
  
 次に、明示的な型キャストの例を示します。  
  
### <a name="example-a"></a>例 A  
 次の例では、xml 型の変数をクエリしています。 このクエリは、単純型の値のシーケンスを xs:string にキャストして返します。  
  
```  
declare @x xml  
set @x = '<e>1</e><e>2</e>'  
select @x.query('/e[1] cast as xs:string?')  
go  
```  
  
### <a name="example-b"></a>例 B  
 次の例では、型指定された xml 変数をクエリします。 この例では、まず XML スキーマ コレクションを作成しています。 続いて、この XML スキーマ コレクションを使用して、型指定された XML 変数を作成します。 スキーマが、変数に代入された XML インスタンスの型情報を提供します。 その後、変数に対してクエリを指定しています。  
  
```  
create xml schema collection myCollection as N'  
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">  
      <xs:element name="root">  
            <xs:complexType>  
                  <xs:sequence>  
                        <xs:element name="A" type="xs:string"/>  
                        <xs:element name="B" type="xs:string"/>  
                        <xs:element name="C" type="xs:string"/>  
                  </xs:sequence>  
            </xs:complexType>  
      </xs:element>  
</xs:schema>'  
go  
```  
  
 次のクエリは静的エラーを返します。これは、ドキュメント インスタンス内の最上位の <`root`> 要素の数がわからないためです。  
  
```  
declare @x xml(myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
          <root><A>4</A><B>5</B><C>6</baz></C>'  
select @x.query('/root/A cast as xs:string?')  
go  
```  
  
 式で <`root`> 要素が 1 つになるように指定すると、クエリは成功します。 このクエリは、単純型の値のシーケンスを xs:string にキャストして返します。  
  
```  
declare @x xml(myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
              <root><A>4</A><B>5</B><C>6</C></root>'  
select @x.query('/root[1]/A cast as xs:string?')  
go  
```  
  
 次の例では、XML スキーマ コレクションを指定するドキュメント キーワードが xml 型の変数に含まれます。 これは、XML インスタンスが 1 つの最上位要素を含むドキュメントでなければならないことを示します。 したがって、XML インスタンスに 2 つの <`root`> 要素を作成すると、エラーが返されます。  
  
```  
declare @x xml(document myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>  
              <root><A>4</A><B>5</B><C>6</C></root>'  
go  
```  
  
 インスタンスを変更して、最上位要素を 1 つだけインスタンスに含めるようにすると、クエリは成功します。 このクエリも、単純型の値のシーケンスを xs:string にキャストして返します。  
  
```  
declare @x xml(document myCollection)  
set @x = '<root><A>1</A><B>2</B><C>3</C></root>'  
select @x.query('/root/A cast as xs:string?')  
go  
```  
  
## <a name="implicit-casting"></a>暗黙のキャスト  
 暗黙のキャストを使用できるのは、数値型と型指定されていないアトミック型だけです。 たとえば、次**min()** 関数は、2 つの値の最小値を返します。  
  
```  
min(xs:integer("1"), xs:double("1.1"))  
```  
  
 この例では、2 つの値に渡されるで XQuery **min()** 関数が別の型。 暗黙的な変換を実行するため、場所**整数**に型が昇格**二重**と 2 つの**二重**値が比較されます。  
  
 この例のような型の上位変換は、次の規則に従って行われます。  
  
-   組み込み派生数値型は、その基本型に上位変換できます。 たとえば、**整数**に昇格する可能性があります**decimal**します。  
  
-   A **decimal**に昇格する可能性があります**float、** と**float**に昇格する可能性があります**二重**します。  
  
 暗黙のキャストを使用できるのは数値型だけなので、次のキャストは許可されません。  
  
-   文字列型間の暗黙のキャストは許可されません。 たとえば、2 つ**文字列**渡すし、型が指定される、**文字列**と**トークン**暗黙的なキャストは行われず、エラーが返されます。  
  
-   数値型から文字列型への暗黙のキャストは許可されません。 たとえば、文字列型のパラメーターが必要な関数に整数型の値を渡すと、暗黙のキャストは行われず、エラーが返されます。  
  
## <a name="casting-values"></a>値のキャスト  
 ある型から別の型へキャストすると、実際の値は元の型の値空間からキャスト先の型の値空間に変換されます。 たとえば、xs:decimal から xs:double にキャストすると、decimal 値が double 値に変換されます。  
  
 次に、いくつかの変換の規則を示します。  
  
##### <a name="casting-a-value-from-a-string-or-untypedatomic-type"></a>string 型または untypedAtomic 型からの値のキャスト  
 string または untypedAtomic 型にキャストされる値は、キャスト先の型の規則に基づいて値が評価されるのと同じ方法で変換されます。 これには、最終的なパターンと空白文字の処理規則も含まれます。 たとえば、次のキャストは成功し、double 値 1.1e0 が生成されます。  
  
 `xs:double("1.1")`  
  
 string 型または untypedAtomic 型から xs:base64Binary や xs:hexBinary などのバイナリ型にキャストする場合、入力値がそれぞれ base64 または hex でエンコードされる必要があります。  
  
##### <a name="casting-a-value-to-a-string-or-untypedatomic-type"></a>string 型または untypedAtomic 型への値のキャスト  
 string 型または untypedAtomic 型にキャストすると、値は XQuery の正規字句表現に変換されます。 これは、入力時に特定のパターンや他の制約に従っていた値が、制約どおりに表記されない可能性があることを意味します。  については、ユーザーに通知する[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]フラグの型、型の制約は、それらの型がスキーマ コレクションに読み込まれるときに警告を提供することでの問題をすることができます。  
  
 xs:float 型、xs:double 型、またはこれらのサブタイプの値を string 型または untypedAtomic 型にキャストする場合、値は科学的表記法で表現されます。 これは、値の絶対値が 1.0E-6 未満であるか、1.0E6 以上である場合にのみ行われます。 つまり、0 は科学的表記法で 0.0E0 にシリアル化されます。  
  
 たとえば、`xs:string(1.11e1)` は `"11.1"` という文字列値を返しますが、`xs:string(-0.00000000002e0)` は `"-2.0E-11"` という文字列値を返します。  
  
 xs:base64Binary や xs:hexBinary などバイナリ型から string 型または untypedAtomic 型にキャストする場合、バイナリ値はそれぞれ base64 または hex エンコード形式で表現されます。  
  
##### <a name="casting-a-value-to-a-numeric-type"></a>数値型への値のキャスト  
 数値型間で値のキャストを行うと、文字列のシリアル化が行われずに、値は一方の値空間から他方の値空間にマップされます。 値がキャスト先の型の制約を満たさない場合は、次の規則が適用されます。  
  
-   元の値が既に数値型で、キャスト先の型が xs:float かそのサブタイプであり、-INF または INF 値を許容する場合、元の数値がキャスト後オーバーフローするようなときは、正の値は INF に、負の値は -INF にマップされます。 キャスト先の型が INF または -INF を許容しない場合に、オーバーフローが発生するようなときは、キャストに失敗し、このリリースの SQL Server では、結果が空のシーケンスになります。  
  
-   元の値が既に数値型で、キャスト先の型が 0、-0e0、または 0e0 を許容する数値型の場合に、元の数値がキャスト後オーバーフローするようなときは、値が次のようにマップされます。  
  
    -   キャスト先の型が decimal の場合、値は 0 にマップされます。  
  
    -   値が負のアンダーフローになる場合、値は -0e0 にマップされます。  
  
    -   キャスト先の型が float または double で、値が正のアンダーフローになる場合、値は 0e0 にマップされます。  
  
     キャスト先の型の値空間に 0 が含まれない場合、キャストに失敗し、結果が空のシーケンスになります。  
  
     値を xs:float、xs:double、またはそのサブタイプなどのバイナリ浮動小数点型にキャストすると、有効桁数が失われる可能性があることに注意してください。  
  
## <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   浮動小数点値 NaN はサポートされません。  
  
-   キャスト可能な値は、キャスト先の型に実装されている制限事項によって制約を受けます。 たとえば、負の年の日付文字列をキャストすることはできません**xs:date**します。 実行時に値が指定された場合、このようなキャストでは、(実行時エラーになるのではなく) 空のシーケンスが返されます。  
  
## <a name="see-also"></a>参照  
 [XML データのシリアル化の定義](../relational-databases/xml/define-the-serialization-of-xml-data.md)  
  
  
