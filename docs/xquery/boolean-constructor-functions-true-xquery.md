---
title: true 関数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 08/10/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:true function
- true function
ms.assetid: 318e370d-0444-4812-afe4-307df7ef9f3b
author: rothja
ms.author: jroth
ms.openlocfilehash: 56f2dde1899340f036024253405379e094de59a6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039043"
---
# <a name="boolean-constructor-functions---true-xquery"></a>ブール値コンストラクター関数 - true (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  xs:boolean 値 True を返します。 これは、`xs:boolean("1")` と同じです。  
  
## <a name="syntax"></a>構文  
  
```  
fn:true() as xs:boolean  
```  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**型の列には、AdventureWorks データベース。  
  
### <a name="a-using-the-true-xquery-boolean-function"></a>A. XQuery 論理関数 true() の使用  
 次の例は、型指定されていないクエリ**xml**変数。 内の式、 **value()** メソッドはブール値を返します**true()** "aaa"属性値である場合。 **Value()** のメソッド、 **xml**データ型がビットにブール値を変換し、それを返します。  
  
```  
DECLARE @x XML  
SET @x= '<ROOT><elem attr="aaa">bbb</elem></ROOT>'  
select @x.value(' if ( (/ROOT/elem/@attr)[1] eq "aaa" ) then fn:true() else fn:false() ', 'bit')  
go  
-- result = 1  
```  
  
 次の例では、クエリを指定する型指定されたに対して**xml**列。 `if` 式では、<`ROOT`> 要素の型指定されたブール値が確認され、その結果に応じて、構築された XML が返されます。 この例では、次の操作が実行されます。  
  
-   xs:boolean 型の <`ROOT`> 要素を定義する、XML スキーマ コレクションを作成します。  
  
-   型指定されたテーブルを作成します。 **xml** XML スキーマ コレクションを使用して列。  
  
-   XML インスタンスを列に保存し、クエリを実行します。  
  
```  
-- Drop table if exist  
--DROP TABLE T  
--go  
DROP XML SCHEMA COLLECTION SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="QNameXSD" >  
      <element name="ROOT" type="boolean" nillable="true"/>  
</schema>'  
go  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- following OK  
insert into T values ('<ROOT xmlns="QNameXSD">true</ROOT>')  
 go  
-- Retrieve the local name.   
SELECT xmlCol.query('declare namespace a="QNameXSD";   
   if (/a:ROOT[1] eq true()) then  
       <result>Found boolean true</result>  
   else  
       <result>Found boolean false</result>')  
  
FROM T  
-- result = <result>Found boolean true</result>  
-- Clean up  
DROP TABLE T  
go  
DROP XML SCHEMA COLLECTION SC  
go  
```  
  
## <a name="see-also"></a>参照  
 [ブール値コンス トラクター関数&#40;XQuery&#41;](https://msdn.microsoft.com/library/fa907f39-d4b7-4495-b829-c788928e0f64)  
  
  
