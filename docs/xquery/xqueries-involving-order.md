---
title: 注文に関連する XQueries |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- XQuery, sequence
- ordered expressions [XQuery]
ms.assetid: 4f1266c5-93d7-402d-94ed-43f69494c04b
author: rothja
ms.author: jroth
ms.openlocfilehash: 4fc30086978e26f53f7a4fdbab8a731ac2334181
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946114"
---
# <a name="xqueries-involving-order"></a>順序に関係する XQuery
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  リレーショナル データベースにはシーケンスの概念はありません。 たとえば、"データベースから最初の顧客を取得する" などの要求を行うことはできません。 ただし、XML ドキュメントのクエリを実行し、最初に取得\<顧客 > 要素。 その後は、常に、同じ顧客が取得されます。  
  
 このトピックでは、ドキュメントにノードが表示される順序に基づいたクエリについて説明します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-retrieve-manufacturing-steps-at-the-second-work-center-location-for-a-product"></a>A. 2 番目のワーク センターの場所で製品の製造手順の取得  
 次のクエリでは、特定の製品モデルに対して、製造プロセス内にあるワーク センターの場所の順序で 2 番目のワーク センターの場所で製造手順が取得されます。  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    <ManuStep ProdModelID = "{sql:column("Production.ProductModel.ProductModelID")}"  
                ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
     <Location>  
       { (//AWMI:root/AWMI:Location)[2]/@* }  
       <Steps>  
         { for $s in (//AWMI:root/AWMI:Location)[2]//AWMI:step  
           return  
              <Step>  
               { string($s) }  
              </Step>  
         }  
        </Steps>  
      </Location>  
     </ManuStep>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   かっこ内の式は、評価結果に置き換えられます。 詳細については、次を参照してください。 [XML の構築&#40;XQuery&#41;](../xquery/xml-construction-xquery.md)します。  
  
-   **@\*** 2 番目のワーク センター拠点のすべての属性を取得します。  
  
-   FLWOR の繰り返し (FOR ...RETURN) は、2 番目のワーク センターの場所のすべての <`step`> 子要素を取得します。  
  
-   [Sql:column() 関数 (XQuery)](../xquery/xquery-extension-functions-sql-column.md)構築される XML にリレーショナル値が含まれています。  
  
 これは、結果です。  
  
```  
<ManuStep ProdModelID="7" ProductModelName="HL Touring Frame">  
  <Location LocationID="20" SetupHours="0.15"   
              MachineHours="2"  LaborHours="1.75" LotSize="1">  
  <Steps>  
   <Step>Assemble all frame components following blueprint 1299.</Step>  
     ...  
  </Steps>  
 </Location>  
</ManuStep>    
```  
  
 上記のクエリでは、テキスト ノードだけを取得します。 全体の場合 <`step`> 代わりに、返された要素を削除、 **string()** クエリから関数。  
  
### <a name="b-find-all-the-material-and-tools-used-at-the-second-work-center-location-in-the-manufacturing-of-a-product"></a>B. 製品を製造する際の 2 番目のワーク センターの場所で使用されるすべての材料とツールの検索  
 次のクエリでは、特定の製品モデルに対して、製造プロセス内にあるワーク センターの場所の順序で 2 番目のワーク センターの場所で使用されるツールと材料が取得されます。  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   <Location>  
      { (//AWMI:root/AWMI:Location)[1]/@* }  
       <Tools>  
         { for $s in (//AWMI:root/AWMI:Location)[1]//AWMI:step//AWMI:tool  
           return  
              <Tool>  
                { string($s) }  
              </Tool>  
          }  
        </Tools>  
        <Materials>  
            { for $s in (//AWMI:root/AWMI:Location)[1]//AWMI:step//AWMI:material  
              return  
                 <Material>  
                    { string($s) }  
                 </Material>  
             }  
         </Materials>  
  </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   クエリでは、<Loca`tion`> 要素が構築され、その属性値がデータベースから取得されます。  
  
-   このとき 2 つの FLWOR (for...return) の繰り返しが使用されます。1 つはツールの取得のため、もう 1 つは使用される材料の取得のためです。  
  
 これは、結果です。  
  
```xml
<Location LocationID="10" SetupHours=".5"   
          MachineHours="3" LaborHours="2.5" LotSize="100">  
  <Tools>  
    <Tool>T-85A framing tool</Tool>  
    <Tool>Trim Jig TJ-26</Tool>  
    <Tool>router with a carbide tip 15</Tool>  
    <Tool>Forming Tool FT-15</Tool>  
  </Tools>  
  <Materials>  
    <Material>aluminum sheet MS-2341</Material>  
  </Materials>  
</Location>  
```  
  
### <a name="c-retrieve-the-first-two-product-feature-descriptions-from-the-product-catalog"></a>C. 製品カタログからの最初の 2 製品の機能説明の取得  
 次のクエリでは、特定の製品モデルに対して、製品モデル カタログの <`Features`> 要素から最初の 2 つの機能説明が取得されます。  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <ProductModel ProductModelID= "{ data( (/p1:ProductDescription/@ProductModelID)[1] ) }"  
                   ProductModelName = "{ data( (/p1:ProductDescription/@ProductModelName)[1] ) }" >  
       {  
         for $F in /p1:ProductDescription/p1:Features  
         return   
           $F/*[position() <= 2]   
       }  
     </ProductModel>  
      ') as x  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
 クエリ本文では、ProductModelID 属性と ProductModelName 属性を備えた <`ProductModel`> 要素が含まれる XML が構築されます。  
  
-   クエリでは、FOR ...RETURN ループを使用して、製品モデルの機能説明を取得します。 **Position()** 関数を使用して、最初の 2 つの機能を取得します。  
  
 これは、結果です。  
  
```xml
<ProductModel ProductModelID="19" ProductModelName="Mountain 100">  
 <p1:Warranty   
  xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
  <p1:Description>parts and labor</p1:Description>  
 </p1:Warranty>  
 <p2:Maintenance   
  xmlns:p2="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
  <p2:NoOfYears>10</p2:NoOfYears>  
  <p2:Description>maintenance contact available through your dealer   
            or any AdventureWorks retail store.  
  </p2:Description>  
 </p2:Maintenance>  
</ProductModel>   
```  
  
### <a name="d-find-the-first-two-tools-used-at-the-first-work-center-location-in-the-manufacturing-process-of-the-product"></a>D. 製品の製造プロセス内にある最初のワーク センターの場所で使用される最初の 2 つのツールの検索  
 次のクエリでは、製品モデルに対して、製造プロセス内にあるワーク センターの場所の順序で、最初のワーク センターの場所で使用される最初の 2 つのツールが返されます。 格納された製造手順に対してクエリを指定、**指示**の列、 **Production.ProductModel**テーブル。  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   for $Inst in (//AWMI:root/AWMI:Location)[1]  
   return   
     <Location>  
       { $Inst/@* }  
       <Tools>  
         { for $s in ($Inst//AWMI:step//AWMI:tool)[position() <= 2]  
           return  
             <Tool>  
               { string($s) }  
             </Tool>  
         }  
       </Tools>  
     </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 これは、結果です。  
  
```xml
<Location LocationID="10" SetupHours=".5"   
            MachineHours="3" LaborHours="2.5" LotSize="100">  
  <Tools>  
    <Tool>T-85A framing tool</Tool>  
    <Tool>Trim Jig TJ-26</Tool>  
  </Tools>  
</Location>   
```  
  
### <a name="e-find-the-last-two-manufacturing-steps-at-the-first-work-center-location-in-the-manufacturing-of-a-specific-product"></a>E. 特定の製品を製造する際の最初のワーク センターの場所で最後の 2 つの製造手順の検索  
 クエリを使用して、 **last()** 最後の 2 つの製造ステップを取得する関数。  
  
```sql
SELECT Instructions.query('   
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  <LastTwoManuSteps>  
   <Last-1Step>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[(last()-1)]/text() }  
   </Last-1Step>  
   <LastStep>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[last()]/text() }  
   </LastStep>  
  </LastTwoManuSteps>') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 これは、結果です。  
  
```xml
<LastTwoManuSteps>  
   <Last-1Step>When finished, inspect the forms for defects per   
               Inspection Specification .</Last-1Step>  
   <LastStep>Remove the frames from the tool and place them in the   
             Completed or Rejected bin as appropriate.</LastStep>  
</LastTwoManuSteps>  
```  
  
## <a name="see-also"></a>参照  
 [XML データ &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [XQuery 言語リファレンス &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [XML の構築&#40;XQuery&#41;](../xquery/xml-construction-xquery.md)  
  
  
