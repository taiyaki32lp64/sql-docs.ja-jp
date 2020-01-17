---
title: XPath データ型 (SQLXML)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping XDR types to XPath types [SQLXML]
- data types [XPath]
- arithmetic operators
- mapping data types [SQLXML]
- relational operators [SQLXML]
- node-set [SQLXML]
- data types [SQLXML], XPath
- XPath operators [SQLXML]
- XDR data type [SQLXML]
- equality operators [SQLXML]
- XPath conversions [SQLXML]
- converting data types [SQLXML]
- Boolean operators
- XPath queries [SQLXML], data types
- XPath data types [SQLXML]
- operators [SQLXML]
ms.assetid: a90374bf-406f-4384-ba81-59478017db68
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 089b2b006d0159c63e480c8627762ac37dec98b8
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247086"
---
# <a name="xpath-data-types-sqlxml-40"></a>XPath のデータ型 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、XPath、および XML スキーマ (XSD) のデータ型は大きく異なります。 たとえば、XPath に整数や日付のデータ型はありませんが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と XSD にはこれらのデータ型が多く用意されています。 また、XSD では時間値の精度はナノ秒ですが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の精度は最大でも 1/300 秒です。 このため、あるデータ型から別のデータ型へのマッピングが常に可能であるとは限りません。 データ型の XSD データ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]型へのマッピングの詳細については、「[データ型の強制変換」と「Sql: DATATYPE 注釈 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)」を参照してください。  
  
 XPath には、**文字列**、**数値**、**ブール値**の3つのデータ型があります。 **数値**データ型は、常に IEEE 754 の倍精度浮動小数点です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Float (53)** データ型は、XPath の最も近い**数値**です。 ただし、 **float (53)** は正確には IEEE 754 ではありません。 たとえば、非数 (NaN) も無限大も使用されません。 数値以外の文字列を**数値**に変換しようとして、0で除算しようとすると、エラーになります。  
  
## <a name="xpath-conversions"></a>XPath 変換  
 
  `OrderDetail[@UnitPrice > "10.0"]` などの XPath クエリを使用する場合は、データ型の変換を暗黙的に行うか明示的に行うかによって、クエリの意味が微妙に変わります。 このため、XPath データ型の実装方法について理解しておくことが重要です。 XPath 言語仕様である XML Path Language (XPath) バージョン 1.0 W3C 勧告では、1999年10月8日に、W3C Web サイトhttp://www.w3.org/TR/1999/PR-xpath-19991008.htmlの「」を参照してください。  
  
 XPath の演算子は、次の 4 つのカテゴリに分けられます。  
  
-   論理演算子 (and、or)  
  
-   関係演算子 (\<、>、 \<=、>=)  
  
-   等価演算子 (=、!=)  
  
-   算術演算子 (+、-、*、div、mod)  
  
 各カテゴリの演算子では、それぞれ異なる方法で各自のオペランドが変換されます。 XPath の演算子では、必要に応じて各自のオペランドが暗黙的に変換されます。 算術演算子はオペランドを**数値**に変換し、結果は数値になります。 ブール演算子はオペランドを**ブール**値に変換し、結果はブール値になります。 関係演算子と等価演算子では、ブール値が得られます。 ただし、次の表に示すように、オペランドの変換元のデータ型に応じて、それぞれ異なる変換規則が使用されます。  
  
|オペランド|関係演算子|等値演算子|  
|-------------|-------------------------|-----------------------|  
|両方のオペランドがノード セットの場合|1つのセットにノードがあり、2番目のセットにノードがあり、その**文字列**値の比較が true である場合にのみ、true になります。|同じ。|  
|1つはノードセットで、もう1つは**文字列**です。|ノードセット内にノードがあり、そのノードが**数値**に変換されたときに、数値に変換された**文字列**と**比較され**た場合にのみ true になります。|ノードセット内にノードがあり、そのノードが**文字列**に**変換され**た場合に限り、true になります。|  
|1つはノードセットで、もう1つは**数字**です。|ノードセット内にノードがあり、そのノードが**数値**に変換されたときに、その**値と数値**との比較が true である場合にのみ true を指定します。|同じ。|  
|一方はノードセットで、もう1つは**ブール値**です。|ノードセット内にノードがあり、それを**ブール値**に変換してから**数値**に変換する場合にのみ、true に**変換され**た**ブール値**と比較します。|ノードセット内にノードがあり、**ブール値**に変換された場合に、ブール**値とブール値**の比較が true である場合にのみ true。|  
|どちらもノード セットでない場合|両方のオペランドを**数値**に変換してから比較します。|両方のオペランドを共通のデータ型に変換し比較。 が**ブール値**の場合は**boolean**に変換します。**数値**の場合は**number**です。それ以外の場合は、**文字列**に変換します。|  
  
> [!NOTE]  
>  XPath 関係演算子は常にオペランドを**数値**に変換するため、**文字列**の比較はできません。 日付の比較を行うために、SQL Server 2000 では、このようなバリエーションを XPath 仕様に提供しています。関係演算子は **、文字列を****文字列、** ノードセット、文字列**に、文字列**値ノードセットを文字列値ノードセットに比較するときに、**数値**比較ではなく**文字列**比較が実行されます。  
  
## <a name="node-set-conversions"></a>ノード セット変換  
 ノード セット変換は常に直感的なものとは限りません。 ノードセットは、セット内の最初のノードの文字列値のみを取得することによって、**文字列**に変換されます。 ノードセットは、**文字列**に変換し、**文字列**を**数値**に変換することによって、**数値**に変換されます。 ノードセットは、存在するかどうかをテストすることで、**ブール値**に変換されます。  
  
> [!NOTE]  
>  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ノード セットで位置の選択は実行されません。たとえば、XPath クエリ `Customer[3]` は 3 番目の顧客を意味しますが、このような位置の選択は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではサポートされていません。 したがって、XPath 仕様で説明されているように、ノードセットから**文字列**への変換またはノードセットから**数値**への変換は実装されていません。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、XPath 仕様で "先頭" の意味で指定されているものが "任意" の意味として扱われます。 たとえば、W3C XPath 仕様に基づき、XPath クエリ`Order[OrderDetail/@UnitPrice > 10.0]`は、 **UnitPrice**が10.0 より大きい最初の**orderdetail**を持つ注文を選択します。 で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は、この XPath クエリは、 **UnitPrice**が10.0 より大きい**orderdetail**を持つ注文を選択します。  
  
 **ブール型**に変換すると存在テストが生成されます。このため、XPath クエリ`Products[@Discontinued=true()]`は sql 式 "Products. 廃止されたが null" ではなく、sql 式 "Products. 廃止 = 1" に相当します。 後者の SQL 式と同等のクエリを作成するには、まず、ノードセットを**number**などの非**ブール**型に変換します。 たとえば、`Products[number(@Discontinued) = true()]` のように指定します。  
  
 大半の演算子は、ノード セット内の 1 つ以上のノードに対して TRUE であれば TRUE となるように定義されているので、これらの演算はノード セットが空の場合は常に FALSE となります。 したがって、A が空の場合、`A = B` と `A != B` は両方とも FALSE になり、`not(A=B)` と `not(A!=B)` は TRUE になります。  
  
 通常、列にマップされる属性または要素は、データベース内のその列の値が**null**でない場合に存在します。 行にマップされる要素は、子が存在する場合に存在します。  
  
> [!NOTE]  
>  で注釈が付けられた要素**は**常に存在します。 その結果、XPath 述語**は、is 定数**要素では使用できません。  
  
 ノードセットが**文字列**または**数値**に変換されると、注釈付きスキーマでその XDR 型 (存在する場合) が検査され、その型を使用して必要な変換が決定されます。  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>XDR データ型から XPath データ型へのマッピング  
 ノードの XPath データ型は、次の表に示すように、スキーマ内の XDR データ型から派生します (この**ノードは、説明的な**目的で使用されます)。  
  
|XDR データ型|同等の<br /><br /> XPath データ型|使用される SQL Server 変換|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|なし|NoneEmployeeID|  
|boolean|boolean|CONVERT(bit, EmployeeID)|  
|number、int、float,i1、i2、i4、i8、r4、r8ui1、ui2、ui4、ui8|number|CONVERT(float(53), EmployeeID)|  
|id、idref、idrefsentity、entities、enumerationnotation、nmtoken、nmtokens、chardate、Timedate、Time.tz、string、uri、uuid|string|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|N/A (XDR データ型 fixed14.4 に相当する XPath のデータ型はありません)|CONVERT(money, EmployeeID)|  
|date|string|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|string|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 日付と時刻の変換は、値が[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**データ型または**文字列**を使用してデータベースに格納されているかどうかにかかわらず機能するように設計されています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Datetime**データ型では、**タイムゾーン**を使用せず、XML**時刻**データ型よりも精度が低いことに注意してください。 **Timezone**データ型またはその他の有効桁数を含めるには[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、**文字列**型を使用してにデータを格納します。  
  
 ノードが XDR データ型から XPath データ型に変換される場合は、1 つの XPath データ型から別の XPath データ型へ、追加の変換が必要になることがあります。 たとえば、次の XPath クエリを考えてみます。  
  
```  
(@m + 3) = 4  
```  
  
 が@m **固定の 14.4** XDR データ型である場合、XDR データ型から XPath データ型への変換は、次の方法で行われます。  
  
```  
CONVERT(money, m)  
```  
  
 この変換では、ノード`m`は固定の**14.4**から**money**に変換されます。 しかし、値 3 を加算するには追加の変換が必要になります。  
  
```  
CONVERT(float(CONVERT(money, m))  
```  
  
 この XPath 式は、次のように評価されます。  
  
```  
CONVERT(float(CONVERT(money, m)) + CONVERT(float(53), 3) = CONVERT(float(53), 3)  
```  
  
 次の表に示すように、これは、リテラルや複合式など、他の XPath 式に適用される変換と同じです。  
  
||||||  
|-|-|-|-|-|  
||X が不明|X は**文字列**です。|X は**数値**です|X は**ブール型**です。|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN (X) > 0|X != 0|-|  
  
## <a name="examples"></a>例  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. XPath クエリ内のデータ型を変換する  
 注釈付き XSD スキーマに対して指定されている次の XPath クエリでは、 **EmployeeID**属性値が E-1 であるすべての**Employee**ノードが選択されます。ここで、"e-" は、 **sql: id プレフィックス**注釈を使用して指定されたプレフィックスです。  
  
 `Employee[@EmployeeID="E-1"]`  
  
 クエリ内の述語は、次の SQL 式と等価です。  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 **Employeeid**は XSD スキーマの**id** (**idref**、 **idrefs**、 **nmtoken**、 **nmtokens**など) のデータ型の値の1つであるため、前に説明した変換ルールを使用して**employeeid**が**文字列**XPath データ型に変換されます。  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 文字列に "E-" プレフィックスが追加され、結果が `N'E-1'` と比較されます。  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. XPath クエリ内で複数のデータ型変換を実行する  
 注釈付き XSD スキーマに対して指定される XPath クエリ `OrderDetail[@UnitPrice * @OrderQty > 98]` を考えてみます。  
  
 この XPath クエリは、述語`@UnitPrice * @OrderQty > 98`を満たすすべての** \<orderdetail>** 要素を返します。 注釈付きスキーマで、固定された**14.4**データ型を使用して**UnitPrice**に注釈が付けられている場合、この述語は SQL 式に相当します。  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 XPath クエリ内の値を変換するとき、最初の変換では、XDR データ型を XPath データ型に変換します。 前の表で説明したように、 **UnitPrice**の XSD データ型は**14.4 に固定**されているため、これは最初に使用される変換です。  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 算術演算子はオペランドを**number** XPath データ型に変換するので、2番目の変換 (xpath データ型から別の xpath データ型への変換) が適用され、その値は**float (53** ) に変換されます (**Float (53)** は XPath **number**データ型に近い)。  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 **Orderqty**属性に XSD データ型が含まれていない場合、 **orderqty**は1回の変換で**number** XPath データ型に変換されます。  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 同様に、値98は**number** XPath データ型に変換されます。  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  スキーマで使用されている XSD データ型がデータベース内の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]基になるデータ型と互換性がない場合、または XPath データ型の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]変換が不可能な場合は、によってエラーが返されることがあります。 たとえば、 **employeeid**属性に**id プレフィックス**の注釈が付けられている場合、 `Employee[@EmployeeID=1]` **employeeid**には**id プレフィックス**の注釈があり、**数値**に変換できないので、XPath ではエラーが生成されます。  
  
  
