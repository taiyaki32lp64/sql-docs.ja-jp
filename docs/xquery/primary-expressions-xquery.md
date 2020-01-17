---
title: プライマリ式 (XQuery) |Microsoft Docs
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
- variable references [XQuery]
- primary expressions [XQuery]
- function calls [XQuery]
- expressions [XQuery], primary
- literals [XQuery]
- context item expressions [XQuery]
ms.assetid: d4183c3e-12b5-4ca0-8413-edb0230cb159
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e3504b4f04b1b9842f786eeef3ecf1f105563f5
ms.sourcegitcommit: 381595e990f2294dbf324ef31071e2dd2318b8dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74200511"
---
# <a name="primary-expressions-xquery"></a>原始式 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery のプライマリ式には、リテラル、変数参照、コンテキスト項目式、コンストラクター、および関数呼び出しが含まれます。  
  
## <a name="literals"></a>リテラル  
 XQuery リテラルには、数値または文字列リテラルを指定できます。 文字列リテラルには、定義済みのエンティティ参照を含めることができます。エンティティ参照は文字のシーケンスです。 シーケンスは、構文上意味を持つことも考えられる 1 文字を表すアンパサンドで始まります。 次に、XQuery の定義済みエンティティ参照を示します。  
  
|エンティティ参照|表す内容|  
|----------------------|----------------|  
|`&lt;`|\<|  
|`&gt;`|>|  
|`&amp;`|&|  
|`&quot;`|"|  
|`&apos;`|'|  
  
 文字列リテラルには、10進数または16進数のコードポイントによって識別される、Unicode 文字への XML スタイルの参照である文字参照を含めることもできます。 たとえば、"&\#8364;" という文字参照では、ユーロ記号を表すことができます。  
  
> [!NOTE]  
>  
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、XML Version 1.0 が解析の基準として使用されます。  
  
### <a name="examples"></a>例  
 次の例では、リテラルと、エンティティと文字の参照の使用方法を示します。  
  
 '`<'` 文字、および `'>`' 文字には特別な意味があるため、このコードはエラーを返します。  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <SalaryRange>Salary > 50000 and < 100000</SalaryRange>')  
GO  
```  
  
 代わりにエンティティ参照を使用すると、このクエリは動作します。  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <SalaryRange>Salary &gt; 50000 and &lt; 100000</SalaryRange>')  
GO  
```  
  
 文字参照を使用してユーロの通貨記号を表す方法を次の例に示します。  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <a>€12.50</a>')  
```  
  
 結果は次のとおりです。  
  
 `<a>€12.50</a>`  
  
 次の例では、クエリはアポストロフィで区切られています。 したがって、文字列値のアポストロフィは隣接する2つのアポストロフィで表されます。  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query('<a>I don''t know</a>')  
Go  
```  
  
 結果は次のとおりです。  
  
 `<a>I don't know</a>`  
  
 次の例に示すように、組み込みのブール関数**true ()** と**false ()** は、ブール値を表すために使用できます。  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query('<a>{true()}</a>')  
GO  
```  
  
 直接要素コンストラクターは、中かっこで囲まれた式を指定します。 結果の XML では、式の結果値で置き換えられます。  
  
 結果は次のとおりです。  
  
 `<a>true</a>`  
  
## <a name="variable-references"></a>変数参照  
 XQuery の変数参照は、QName の前に $ 記号が付きます。 この実装では、プレフィックスのない変数参照のみがサポートされます。 たとえば、次のクエリでは、変数 `$i` は FLWOR 式の中で定義されています。  
  
```  
DECLARE @var XML  
SET @var = '<root>1</root>'  
SELECT @var.query('  
 for $i in /root return data($i)')  
GO  
```  
  
 名前空間プレフィックスが変数名に追加されるため、次のクエリは機能しません。  
  
```  
DECLARE @var XML  
SET @var = '<root>1</root>'  
SELECT @var.query('  
DECLARE namespace x="https://X";  
for $x:i in /root return data($x:i)')  
GO  
```  
  
 次のクエリに示すように、sql: variable () 拡張関数を使用して SQL 変数を参照できます。  
  
```  
DECLARE @price money  
SET @price=2500  
DECLARE @x xml  
SET @x = ''  
SELECT @x.query('<value>{sql:variable("@price") }</value>')  
```  
  
 結果は次のとおりです。  
  
 `<value>2500</value>`  
  
#### <a name="implementation-limitations"></a>実装の制限事項  
 次に、実装の制限事項を示します。  
  
-   名前空間プレフィックスを持つ変数はサポートされていません。  
  
-   モジュールのインポートはサポートされていません。  
  
-   外部変数宣言はサポートされていません。 これを解決するには、 [sql: variable () 関数](../xquery/xquery-extension-functions-sql-variable.md)を使用します。  
  
## <a name="context-item-expressions"></a>コンテキスト項目の式  
 コンテキスト項目は、パス式のコンテキストで現在処理されている項目です。 これは、ドキュメントノードを持つ NULL でない XML データ型のインスタンスで初期化されます。 また、XPath 式または [] 述語のコンテキストで nodes () メソッドを使用して変更することもできます。  
  
 コンテキスト アイテムはドット (.) を含む式によって返されます。 たとえば、次のクエリでは、属性`a` `attr`の存在について> <各要素を評価します。 属性が存在する場合は、要素が返されます。 述語の条件では、コンテキストノードが1つのピリオドで指定されることを指定します。  
  
```  
DECLARE @var XML  
SET @var = '<ROOT>  
<a>1</a>  
<a attr="1">2</a>  
</ROOT>'  
SELECT @var.query('/ROOT[1]/a[./@attr]')  
```  
  
 結果は次のとおりです。  
  
 `<a attr="1">2</a>`  
  
## <a name="function-calls"></a>関数呼び出し  
 組み込みの XQuery 関数と、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sql: variable () 関数と sql: column () 関数を呼び出すことができます。 実装されている関数の一覧については、「 [Xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)」を参照してください。  
  
#### <a name="implementation-limitations"></a>実装の制限事項  
 次に、実装の制限事項を示します。  
  
-   XQuery プロローグでの関数定義はサポートされていません。  
  
-   関数のインポートはサポートされていません。  
  
## <a name="see-also"></a>参照  
 [XML 構築 &#40;XQuery&#41;](../xquery/xml-construction-xquery.md)
 
