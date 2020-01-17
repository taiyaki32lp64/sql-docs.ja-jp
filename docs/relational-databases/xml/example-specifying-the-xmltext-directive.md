---
title: '例: XMLTEXT ディレクティブの指定 | Microsoft Docs'
ms.custom: ''
ms.date: 04/05/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XMLTEXT directive
ms.assetid: e78008ec-51e8-4fd1-b86f-1058a781de17
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 52e3d6ea8cff9d1984ee11a510a6c21833034c29
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006676"
---
# <a name="example-specifying-the-xmltext-directive"></a>例:XMLTEXT ディレクティブの指定
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  この例では、EXPLICIT モードを使用した **ステートメントで、** XMLTEXT `SELECT` ディレクティブによりオーバーフロー列のデータを指定する方法を示します。  
  
 `Person` テーブルについて考えます。 このテーブルには、XML ドキュメントの未使用部分を格納している `Overflow` 列があります。  
  
```  
USE tempdb;  
GO  
CREATE TABLE Person(PersonID varchar(5), PersonName varchar(20), Overflow nvarchar(200));  
GO  
INSERT INTO Person VALUES   
    ('P1','Joe',N'<SomeTag attr1="data">content</SomeTag>')  
   ,('P2','Joe',N'<SomeTag attr2="data"/>')  
   ,('P3','Joe',N'<SomeTag attr3="data" PersonID="P">content</SomeTag>');  
```  
  
 このクエリでは、 `Person` テーブルから列を取得します。 `Overflow` 列には *AttributeName* が指定されていませんが、ユニバーサル テーブルの列名の一部として、  *ディレクティブ* `XMLTEXT` が設定されています。  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!!XMLTEXT] -- No AttributeName; XMLTEXT directive  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 結果の XML ドキュメントは次のようになります。  
  
-   `Overflow` 列には *AttributeName* が指定されていませんが、`xmltext` ディレクティブが指定されているので、<`overflow`> 要素の属性は、囲み要素である <`Parent`> の属性リストに追加されます。  
  
-   <`xmltext`> 要素の `PersonID` 属性は、同じ要素レベルで取得される `PersonID` 属性と競合するので、<`xmltext`> 要素の属性は無視されます。これは、`PersonID` 属性の値が NULL であっても同じです。 一般的に、属性はオーバーフローに含まれる同じ名前の属性をオーバーライドします。  
  
 結果を次に示します。  
  
 ```   
 <Parent PersonID="P1" PersonName="Joe" attr1="data">content</Parent>  
 <Parent PersonID="P2" PersonName="Joe" attr2="data"></Parent>  
 <Parent PersonID="P3" PersonName="Joe" attr3="data">content</Parent>
 ```  
  
 オーバーフロー データにサブ要素がある場合に同じクエリを指定すると、`Overflow` 列内のサブ要素は、囲み要素である <`Parent`> のサブ要素として追加されます。  
  
 たとえば、次のように `Person` テーブルのデータを変更したとします。`Overflow` 列にサブ要素が含まれています。  
  
```  
USE tempdb;  
GO  
TRUNCATE TABLE Person;  
GO  
INSERT INTO Person VALUES   
    ('P1','Joe',N'<SomeTag attr1="data">content</SomeTag>')  
   ,('P2','Joe',N'<SomeTag attr2="data"/>')  
    ,('P3','Joe',N'<SomeTag attr3="data" PersonID="P"><name>PersonName</name></SomeTag>');  
```  
  
 同じクエリを実行すると、<`xmltext`> 要素のサブ要素は、囲み要素である <`Parent`> のサブ要素として追加されます。  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!!XMLTEXT] -- no AttributeName, XMLTEXT directive  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 結果を次に示します。  
  
 ```   
 <Parent PersonID="P1" PersonName="Joe" attr1="data">content</Parent>  
 <Parent PersonID="P2" PersonName="Joe" attr2="data"></Parent>  
 <Parent PersonID="P3" PersonName="Joe" attr3="data">  
 <name>PersonName</name>  
 </Parent>
 ```  
  
 *AttributeName* と `xmltext` ディレクティブの両方を指定した場合、<`overflow`> 要素の属性は、囲み要素である <`Parent`> のサブ要素の属性として追加されます。 *AttributeName* に指定された名前がサブ要素の名前になります。  
  
 このクエリでは、*AttributeName* (<`overflow`>) と `xmltext` ディレクティブの両方が指定されています *。*  
  
```  
SELECT 1 as Tag, NULL as parent,  
       PersonID as [Parent!1!PersonID],  
       PersonName as [Parent!1!PersonName],  
       Overflow as [Parent!1!overflow!XMLTEXT] -- Overflow is AttributeName  
                      -- XMLTEXT is a directive  
FROM Person  
FOR XML EXPLICIT  
```  
  
 結果を次に示します。  
  
 ```   
 <Parent PersonID="P1" PersonName="Joe">  
 <overflow attr1="data">content</overflow>  
 </Parent>  
 <Parent PersonID="P2" PersonName="Joe">  
 <overflow attr2="data" />  
 </Parent>  
 <Parent PersonID="P3" PersonName="Joe">  
 <overflow attr3="data" PersonID="P">  
 <name>PersonName</name>  
 </overflow>  
 </Parent>
 ```  
  
 このクエリでは、`PersonName` 属性に *element* ディレクティブを指定します。 これにより、`PersonName` 属性は、囲み要素である <`Parent`> 要素のサブ要素として追加されます。 <`xmltext`> の属性も、依然として、囲み要素 <`Parent`> に追加されます。 <`overflow`> 要素の内容 (サブ要素) は、囲み要素である <`Parent`> 要素の他のサブ要素の前に追加されます。  
  
```  
SELECT 1      AS Tag, NULL as parent,  
       PersonID   AS [Parent!1!PersonID],  
       PersonName AS [Parent!1!PersonName!element], -- element directive  
       Overflow   AS [Parent!1!!XMLTEXT]  
FROM Person  
FOR XML EXPLICIT;  
```  
  
 結果を次に示します。  
  
 ```   
 <Parent PersonID="P1" attr1="data">content<PersonName>Joe</PersonName>  
 </Parent>  
 <Parent PersonID="P2" attr2="data">  
 <PersonName>Joe</PersonName>  
 </Parent>  
 <Parent PersonID="P3" attr3="data">  
 <name>PersonName</name>  
 <PersonName>Joe</PersonName>  
 </Parent>
 ```  
  
 `XMLTEXT` 列のデータにルート要素の属性が含まれている場合、これらの属性は XML データ スキーマに反映されません。結果の XML ドキュメントのその部分に関して、MSXML パーサーによる検証は行われません。 例 :  
  
```  
SELECT 1 AS Tag,  
       0 ASParent,  
       N'<overflow a="1"/>' AS 'overflow!1!!xmltext'  
FOR XML EXPLICIT, xmldata;  
```  
  
 結果は次のとおりです。 返されたスキーマでは、オーバーフロー要素の属性 `a` が欠落している点に注意してください。  
  
 ```   
 <Schema name="Schema2"  
 xmlns="urn:schemas-microsoft-com:xml-data"  
 xmlns:dt="urn:schemas-microsoft-com:datatypes">  
 <ElementType name="overflow" content="mixed" model="open">`  
 </ElementType>`  
 </Schema>`  
 <overflow xmlns="x-schema:#Schema2" a="1">  
 </overflow>
 ```  
  
## <a name="see-also"></a>参照  
 [FOR XML での EXPLICIT モードの使用](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
