---
title: XML 保存形式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence format
ms.assetid: 6e146738-ac4d-47bb-b6cd-d87b2260aead
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e2d1c30546a8466ba9950f31cffdfb9447bd89ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923388"
---
# <a name="xml-persistence-format"></a>XML 保存形式
ADO では、utf-8 が保持する XML ストリームのエンコードを使用します。  
  
 ADO の XML 形式は、2 つのセクションでは、[データ] セクションの後にスキーマ セクションに分割されます。 次に、Northwind データベースから Shippers テーブルの XML ファイルの例を示します。 次の例では、XML のさまざまな部分を説明します。  
  
## <a name="remarks"></a>コメント  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"   
xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"   
xmlns:rs="urn:schemas-microsoft-com:rowset"   
xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="ShipperID" rs:number="1"   
        rs:basetable="shippers" rs:basecolumn="ShipperID"  
        rs:keycolumn="true">   
        <s:datatype dt:type="int" dt:maxLength="4" rs:precision="10"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="CompanyName" rs:number="2"   
        rs:nullable="true" rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="CompanyName">   
        <s:datatype dt:type="string" dt:maxLength="40" />   
      </s:AttributeType>   
      <s:AttributeType name="Phone" rs:number="3" rs:nullable="true"   
        rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="Phone">   
        <s:datatype dt:type="string" dt:maxLength="24"/>   
      </s:AttributeType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  
  <rs:data>   
    <z:row ShipperID="1" CompanyName="Speedy Express"   
      Phone="(503) 555-9831"/>   
    <z:row ShipperID="2" CompanyName="United Package"   
      Phone="(503) 555-3199"/>   
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>   
  </rs:data>   
</xml>  
```  
  
 スキーマでは、名前空間、スキーマ」セクションで、[データ] セクションの宣言を示します。 スキーマ セクションには、行、運送、CompanyName、および電話の定義が含まれています。  
  
 準拠しているスキーマの定義、 [W3C の XML データの指定](http://www.w3.org/TR/1998/NOTE-XML-data/)(ただし、検証は、Internet Explorer 5 では発生しません) を完全に検証することができます。 XML データは、現在は、レコード セットの永続化のみサポートされているスキーマ形式です。  
  
 [データ] セクションでは、運送会社に関する情報を含む 3 つの行があります。 [データ] セクションが空である空の行セットが、 \<rs: データ > タグが存在する必要があります。 データのない、書き込めるのタグの短縮形単に\<rs: データ/>。 "Rs"の付いた任意のタグは、urn: スキーマによって定義された名前空間内にあることを示します-microsoft-com:rowset します。  
  
## <a name="see-also"></a>関連項目  
 [レコードを XML 形式で保持する](../../../ado/guide/data/persisting-records-in-xml-format.md)
