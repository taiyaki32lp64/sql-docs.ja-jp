---
title: FLWOR ステートメントと繰り返し (XQuery) |Microsoft Docs
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
- return clause
- FLWOR statement
- effective Boolean value [XQuery]
- multiple variable binding
- order by clause [XQuery]
- for clause [XQuery]
- where clause [XQuery]
- iterations [XQuery]
- XQuery, FLWOR statement
- EBV
ms.assetid: d7cd0ec9-334a-4564-bda9-83487b6865cb
author: rothja
ms.author: jroth
ms.openlocfilehash: 9deb87d506e167d3de3439e0a07cfbb8bc040fac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038905"
---
# <a name="flwor-statement-and-iteration-xquery"></a>FLWOR ステートメントと繰り返し (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery では FLWOR 繰り返し構文が定義されています。 FLWOR とは、`for`、`let`、`where`、`order by`、および `return` の頭文字です。  
  
 FLWOR ステートメントの構成要素を次に示します。  
  
-   1 つ以上の反復子変数を入力シーケンスにバインドする 1 つ以上の FOR 句。  
  
     入力シーケンスは、XPath 式などの他の XQuery 式でもかまいません。 その場合、ノードのシーケンス、またはアトミック値のシーケンスのいずれかを指定します。 アトミック値のシーケンスは、リテラルまたはコンス トラクター関数を使用して構築できます。 構成された XML ノードは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の入力シーケンスとしては使用できません。  
  
-   省略可能な `let` 句。 この句は、特定の繰り返し処理の変数に値を割り当てます。 割り当てる式として XPath 式などの XQuery 式を指定でき、ノードのシーケンスまたはアトミック値のシーケンスを返すことができます。 アトミック値のシーケンスを構成するには、リテラルまたはコンストラクター関数を使用できます。 構成された XML ノードは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の入力シーケンスとしては使用できません。  
  
-   反復子変数。 反復子変数には `as` キーワードを使用して、型アサーションをオプションで指定できます。  
  
-   省略可能な `where` 句。 繰り返しにフィルター述語を適用します。  
  
-   省略可能な `order by` 句。  
  
-   `return` 式。 `return` 句の式で FLWOR ステートメントの結果を構成します。  
  
 たとえば、次のクエリは最初の製造拠点で <`Step`> 要素を繰り返し、<`Step`> ノードの文字列値を返します。  
  
```sql
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $step in /ManuInstructions/Location[1]/Step  
   return string($step)  
')  
```  
  
 これは、結果です。  
  
```  
Manu step 1 at Loc 1 Manu step 2 at Loc 1 Manu step 3 at Loc 1  
```  
  
 次のクエリは上記のクエリと似ていますが、ProductModel テーブルの型指定された xml 列である Instructions 列に対して指定されている点が異なります。 特定の製品に対し、最初のワーク センター拠点で行われるすべての製造手順 (<`step`> 要素) を繰り返します。  
  
```sql
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in //AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   `$Step` は反復子変数です。  
  
-   [パス式](../xquery/path-expressions-xquery.md)、 `//AWMI:root/AWMI:Location[1]/AWMI:step`、入力シーケンスが生成されます。 このシーケンスは、最初の <`Location`> 要素ノードに含まれる <`step`> 子要素のシーケンスです。  
  
-   省略可能な述語句 `where` は使用しません。  
  
-   `return` 式は、<`step`> 要素の文字列値を返します。  
  
 [String 関数 (XQuery)](../xquery/data-accessor-functions-string-xquery.md)の文字列値を取得するために使用します <`step`> ノード。  
  
 結果の一部を次に示します。  
  
```  
Insert aluminum sheet MS-2341 into the T-85A framing tool.   
Attach Trim Jig TJ-26 to the upper and lower right corners of   
the aluminum sheet. ....         
```  
  
 これ以外に許可されている入力シーケンスの例を示します。  
  
```sql
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in (1, 2, 3)  
  return $a')  
-- result = 1 2 3   
  
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in   
   for $b in (1, 2, 3)  
      return $b  
return $a')  
-- result = 1 2 3  
  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('  
  for $a in (xs:string( "test"), xs:double( "12" ), data(/ROOT/a ))  
  return $a')  
-- result test 12 111  
```  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では異種シーケンスが許可されていません。 つまり、アトミック値とノードが混在したシーケンスは使用できません。  
  
 イテレーションがと共によく使用、 [XML の構築](../xquery/xml-construction-xquery.md)次のクエリで示すように、XML を変換する構文が書式設定します。  
  
 製造手順は、AdventureWorks サンプル データベースに格納されている、**指示**の列、 **Production.ProductModel**テーブルがある、次の形式。  
  
```xml
<Location LocationID="10" LaborHours="1.2"   
            SetupHours=".2" MachineHours=".1">  
  <step>describes 1st manu step</step>  
   <step>describes 2nd manu step</step>  
   ...  
</Location>  
...  
```  
  
 次のクエリは、ワーク センター拠点の属性を子要素として返す <`Location`> 要素を含んだ新しい XML を生成します。  
  
```xml
<Location>  
   <LocationID>10</LocationID>  
   <LaborHours>1.2</LaborHours>  
   <SetupHours>.2</SetupHours>  
   <MachineHours>.1</MachineHours>  
</Location>  
...  
```  
  
 クエリは次のとおりです。  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $WC in /AWMI:root/AWMI:Location  
        return  
          <Location>  
            <LocationID> { data($WC/@LocationID) } </LocationID>  
            <LaborHours>   { data($WC/@LaborHours) }   </LaborHours>  
            <SetupHours>   { data($WC/@SetupHours) }   </SetupHours>  
            <MachineHours> { data($WC/@MachineHours) } </MachineHours>  
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   FLWOR ステートメントで、特定の製品の <`Location`> 要素のシーケンスを取得します。  
  
-   [Data 関数 (XQuery)](../xquery/data-accessor-functions-data-xquery.md)属性としての代わりにテキスト ノードとして結果の XML に追加されますので、各属性の値を抽出するために使用します。  
  
-   RETURN 句の式で、必要な XML を生成します。  
  
 これは、結果の一部です。  
  
```xml
<Location>  
  <LocationID>10</LocationID>  
  <LaborHours>2.5</LaborHours>  
  <SetupHours>0.5</SetupHours>  
  <MachineHours>3</MachineHours>  
</Location>  
<Location>  
   ...  
<Location>  
...  
```  
  
## <a name="using-the-let-clause"></a>let 句の使用  
 `let` 句を使用すると、繰り返し出現する式に名前を付けて変数とすることで、式を参照できます。 `let` 変数に割り当てられた式は、変数がクエリ内で参照されるたびにクエリに挿入されます。 つまり、ステートメントは、式が参照される回数だけ実行されます。  
  
 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベース内の製造手順には、必要なツールとツールを使用する場所の情報が保存されています。 次のクエリは、`let` 句を使用して、製品モデルの作成に必要なツールと、それぞれのツールが必要となる場所を一覧表示します。  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $T in //AWMI:tool  
            let $L := //AWMI:Location[.//AWMI:tool[.=data($T)]]  
        return  
          <tool desc="{data($T)}" Locations="{data($L/@LocationID)}"/>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="using-the-where-clause"></a>where 句の使用  
 使用することができます、`where`句をイテレーションの結果をフィルター処理します。 このことを次の例で説明します。  
  
 自転車を製造するときは、ワーク センター拠点をいくつか経て製造プロセスが進行します。 ワーク センター拠点ごとに、一連の製造手順が定義されています。 次のクエリは、あるモデルの自転車を製造するためのワーク センター拠点のうち、製造手順が 3 工程未満の拠点を取得します。 つまり、<`step`> 要素が 3 つ未満のものだけが取得されます。  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location  
      where count($WC/AWMI:step) < 3  
      return  
          <Location >  
           { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   `where`キーワードを使用して、 **count()** 関数の数をカウント <`step`> 子要素で、各ワーク センターの場所。  
  
-   `return` 式で、繰り返しの結果から必要な XML を生成します。  
  
 これは、結果です。  
  
```  
<Location LocationID="30"/>   
```  
  
 `where` 句内の式の結果は、次の規則を順に適用してブール値に変換されます。 この規則は整数を使用できない点を除き、パス式の述語を評価するときの規則と同じです。  
  
1.  `where` 式が空のシーケンスを返す場合、有効なブール値は False です。  
  
2.  `where` 式が単純な Boolean 型の値を 1 つ返す場合、その値が有効なブール値になります。  
  
3.  `where` 式が 1 つ以上のノードを含んだシーケンスを返す場合、有効なブール値は True です。  
  
4.  上記以外の場合、静的エラーが発生します。  
  
## <a name="multiple-variable-binding-in-flwor"></a>FLWOR での複数の変数のバインド  
 1 つの FLWOR 式で入力シーケンスに複数の変数をバインドできます。 次の例では、型指定されていない xml 変数に対してクエリを指定しています。 FLWOR 式が、各 <`Location`> 要素の最初の <`Step`> 子要素を返します。  
  
```sql
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $Loc in /ManuInstructions/Location,  
       $FirstStep in $Loc/Step[1]  
   return   
       string($FirstStep)  
')  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   `for`式を定義`$Loc`と $`FirstStep`変数。  
  
-   `two` の値が `/ManuInstructions/Location` の値に依存しているので、2 つの式 `$FirstStep in $Loc/Step[1]` と `$FirstStep` には相関関係があります。`$Loc`  
  
-   `$Loc` に関連付けられた式により、<`Location`> 要素のシーケンスが生成されます。 各 <`Location`> 要素について、`$FirstStep` により 1 つの <`Step`> 要素から成るシーケンス (シングルトン) が生成されます。  
  
-   `$Loc` は、`$FirstStep` 変数に関連付けられた式で指定しています。  
  
 これは、結果です。  
  
```  
Manu step 1 at Loc 1   
Manu step 1 at Loc 2  
```  
  
 次のクエリは、型指定された、Instructions 列に対して指定されている点と同様、 **xml**  列の**ProductModel**テーブル。 [XML の構築 (XQuery)](../xquery/xml-construction-xquery.md)する XML を生成するために使用します。  
  
```sql
SELECT Instructions.query('  
     declare default element namespace "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /root/Location,  
            $S  in $WC/step  
      return  
          <Step LocationID= "{$WC/@LocationID }" >  
            { $S/node() }  
          </Step>  
') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   `for` 句で 2 つの変数 `$WC` および `$S` を定義します。 `$WC` に関連付けられた式により、ある製造モデルの自転車の製造で使用されるワーク センター拠点のシーケンスが生成されます。 `$S` 変数に代入されたパス式は、`$WC` で示すワーク センター拠点のシーケンスごとに製造手順のシーケンスを生成します。  
  
-   Return ステートメントを持つ XML を構築します、<`Step`> 製造ステップが含まれている要素と**LocationID**属性とします。  
  
-   **既定要素の名前空間宣言**結果の XML 内のすべての名前空間宣言を最上位の要素に表示されるように、XQuery プロローグ内で使用されます。 これにより、結果が読みやすくなります。 既定の名前空間の詳細については、次を参照してください。[名前空間の処理では、XQuery](../xquery/handling-namespaces-in-xquery.md)します。  
  
 結果の一部を次に示します。  
  
```xml
<Step xmlns=  
    "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
  LocationID="10">  
     Insert <material>aluminum sheet MS-2341</material> into the <tool>T-   
     85A framing tool</tool>.   
</Step>  
...  
<Step xmlns=  
      "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
    LocationID="20">  
        Assemble all frame components following blueprint   
        <blueprint>1299</blueprint>.  
</Step>  
...  
```  
  
## <a name="using-the-order-by-clause"></a>order by 句の使用  
 XQuery の並べ替えを行うには、FLWOR 式で `order by` 句を使用します。 渡した並べ替え式、`order by`句型を持つのに対して有効な値を返す必要があります、 **gt**演算子。 それぞれの並べ替え式は、シングルトン (項目が 1 つのシーケンス) になる必要があります。 既定の並べ替えは昇順です。 並べ替え式ごとに昇順か降順かをオプションとして選択できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に実装された XQuery で行う、文字列値を並べ替えるための比較には、常にバイナリの Unicode コード ポイントの照合順序が使用されます。  
  
 次のクエリは、AdditionalContactInfo 列から特定の顧客のすべての電話番号を取得します。 結果は電話番号順に並べ替えます。  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT AdditionalContactInfo.query('  
   declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 なお、[アトミック化 (XQuery)](../xquery/atomization-xquery.md)のアトミック値を取得するプロセス、<`number`> 要素に渡す前に`order by`します。 使用して、式を記述して、 **data()** 関数の場合、それは必要ありません。  
  
```  
order by data($a/act:number[1]) descending  
```  
  
 これは、結果です。  
  
```xml
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3334</act:number>  
</act:telephoneNumber>  
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3333</act:number>  
</act:telephoneNumber>  
```  
  
 名前空間は、クエリのプロローグではなく WITH XMLNAMESPACES でも宣言できます。  
  
```sql
WITH XMLNAMESPACES (  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo'  AS aci)  
  
SELECT AdditionalContactInfo.query('  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 属性値による並べ替えも行えます。 たとえば、次のクエリでは、新しく作成した、LocationID 属性および LaborHours 属性を含む <`Location`> 要素を LaborHours 属性の降順で並べ替えて取得します。 結果として、労働時間が最も長いワーク センター拠点が最初に返されます。  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location   
order by $WC/@LaborHours descending  
        return  
          <Location>  
             { $WC/@LocationID }   
             { $WC/@LaborHours }   
          </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 これは、結果です。  
  
```  
<Location LocationID="60" LaborHours="4"/>  
<Location LocationID="50" LaborHours="3"/>  
<Location LocationID="10" LaborHours="2.5"/>  
<Location LocationID="20" LaborHours="1.75"/>  
<Location LocationID="30" LaborHours="1"/>  
<Location LocationID="45" LaborHours=".5"/>  
```  
  
 次のクエリは、結果を要素名順に並べ替えます。 製品カタログから特定の製品の仕様を取得します。 製品仕様は <`Specifications`> 要素の子です。  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace  
 pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $a in /pd:ProductDescription/pd:Specifications/*   
     order by local-name($a)  
      return $a  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19;  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   `/p1:ProductDescription/p1:Specifications/*` 式が <`Specifications`> の子要素を返します。  
  
-   `order by (local-name($a))` 式でシーケンスを要素名のローカル部分の順に並べ替えます。  
  
 これは、結果です。  
  
```xml
<Color>Available in most colors</Color>  
<Material>Almuminum Alloy</Material>  
<ProductLine>Mountain bike</ProductLine>  
<RiderExperience>Advanced to Professional riders</RiderExperience>  
<Style>Unisex</Style>    
```  
  
 並べ替え式が空の結果を返したノードは、次の例のようにシーケンスの先頭に来ます。  
  
```sql
declare @x xml  
set @x='<root>  
  <Person Name="A" />  
  <Person />  
  <Person Name="B" />  
</root>  
'  
select @x.query('  
  for $person in //Person  
  order by $person/@Name  
  return   $person  
')  
```  
  
 これは、結果です。  
  
```xml
<Person />  
<Person Name="A" />  
<Person Name="B" />  
```  
  
 次の例のように、並べ替え条件は複数指定できます。 この例のクエリは、<`Employee`> 要素をまず Title 属性の値で並べ替え、次に Administrator 属性の値で並べ替えます。  
  
```sql
declare @x xml  
set @x='<root>  
  <Employee ID="10" Title="Teacher"        Gender="M" />  
  <Employee ID="15" Title="Teacher"  Gender="F" />  
  <Employee ID="5" Title="Teacher"         Gender="M" />  
  <Employee ID="11" Title="Teacher"        Gender="F" />  
  <Employee ID="8" Title="Administrator"   Gender="M" />  
  <Employee ID="4" Title="Administrator"   Gender="F" />  
  <Employee ID="3" Title="Teacher"         Gender="F" />  
  <Employee ID="125" Title="Administrator" Gender="F" /></root>'  
SELECT @x.query('for $e in /root/Employee  
order by $e/@Title ascending, $e/@Gender descending  
  
  return  
     $e  
')  
```  
  
 これは、結果です。  
  
```xml
<Employee ID="8" Title="Administrator" Gender="M" />  
<Employee ID="4" Title="Administrator" Gender="F" />  
<Employee ID="125" Title="Administrator" Gender="F" />  
<Employee ID="10" Title="Teacher" Gender="M" />  
<Employee ID="5" Title="Teacher" Gender="M" />  
<Employee ID="11" Title="Teacher" Gender="F" />  
<Employee ID="15" Title="Teacher" Gender="F" />  
<Employee ID="3" Title="Teacher" Gender="F" />  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   並べ替え式では、型を混在させないようにする必要があります。 この点は静的にチェックされます。  
  
-   空のシーケンスの並べ替えを制御することはできません。  
  
-   `order by` ではキーワード empty least、empty greatest、および collation を使用できません。  
  
## <a name="see-also"></a>参照  
 [XQuery 式](../xquery/xquery-expressions.md)  
  
  
