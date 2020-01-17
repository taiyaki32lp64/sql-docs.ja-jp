---
title: Xml 階層レコード セット |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], in XML
ms.assetid: 5d4b11c4-c94f-4910-b99b-5b9abc50d791
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 17ed6f29442bc55f81d0ef83bfd19473a99e9a95
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925106"
---
# <a name="hierarchical-recordsets-in-xml"></a>XML での階層レコードセット
ADO には、XML に階層レコード セット オブジェクトの永続化ができます。 階層レコード セット オブジェクトでは、親レコード セット内のフィールドの値は、別のレコード セットです。 このようなフィールドは、属性ではなく、XML ストリーム内の子要素として表されます。  
  
## <a name="remarks"></a>コメント  
 次の例では、このケースを示しています。  
  
```  
Rs.Open "SHAPE {select stor_id, stor_name, state from stores} APPEND ({select stor_id, ord_num, ord_date, qty from sales} AS rsSales RELATE stor_id TO stor_id)", "Provider=MSDataShape;DSN=pubs;Integrated Security=SSPI;"  
```  
  
 永続化されたレコード セットの XML 形式を次に示します。  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"     xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"     xmlns:rs="urn:schemas-microsoft-com:rowset"   
    xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="stor_id" rs:number="1"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="4"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="stor_name" rs:number="2" rs:nullable="true"   
        rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="40"/>   
      </s:AttributeType>   
      <s:AttributeType name="state" rs:number="3" rs:nullable="true"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="2"   
          rs:fixedlength="true"/>   
      </s:AttributeType>   
      <s:ElementType name="rsSales" content="eltOnly"   
        rs:updatable="true" rs:relation="010000000100000000000000">   
        <s:AttributeType name="stor_id" rs:number="1"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="4"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_num" rs:number="2"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="20"   
            rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_date" rs:number="3"   
          rs:writeunknown="true">   
            <s:datatype dt:type="dateTime" dt:maxLength="16"   
              rs:scale="3" rs:precision="23" rs:fixedlength="true"   
              rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="qty" rs:number="4" rs:writeunknown="true">   
          <s:datatype dt:type="i2" dt:maxLength="2" rs:precision="5"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:extends type="rs:rowbase"/>   
      </s:ElementType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  <rs:data>   
    <z:row stor_id="6380" stor_name="Eric the Read Books" state="WA">   
      <rsSales stor_id="6380" ord_num="6871"   
        ord_date="1994-09-14T00:00:00" qty="5"/>   
      <rsSales stor_id="6380" ord_num="722a"   
        ord_date="1994-09-13T00:00:00" qty="3"/>   
    </z:row>   
    <z:row stor_id="7066" stor_name="Barnum's" state="CA">   
      <rsSales stor_id="7066" ord_num="A2976"   
        ord_date="1993-05-24T00:00:00" qty="50"/>   
      <rsSales stor_id="7066" ord_num="QA7442.3"   
        ord_date="1994-09-13T00:00:00" qty="75"/>   
    </z:row>   
    <z:row stor_id="7067" stor_name="News & Brews" state="CA">   
      <rsSales stor_id="7067" ord_num="D4482"   
        ord_date="1994-09-14T00:00:00" qty="10"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="40"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
    </z:row>   
  </rs:data>   
</xml>   
```  
  
 この方法で永続化されるときに、親レコード セット内の列の正確な順序は明確ではありません。 親の任意のフィールドには、子レコード セットを含めることができます。 永続化プロバイダーでは、属性として最初にすべてのスカラー列を永続化し、親の行の子要素としてすべての子レコード セット「列」が引き続き発生します。 親内のフィールドの序数位置レコード セットは、レコード セットのスキーマ定義を調べることで取得できます。 すべてのフィールドでは、そのフィールドの序数を含むレコード セットのスキーマ名前空間で定義されている rs: 数、OLE DB プロパティがあります。  
  
 子レコード セットのすべてのフィールドの名前は、親の子を含むレコード セット内のフィールドの名前で連結されます。 これは、親と子レコードの両方に 2 つの異なるテーブルから取得されますが、同じ名前のフィールドが含まれている場合、名前の競合がないことを確認します。  
  
 階層レコード セットを XML に保存するときは、ADO では、次の制限の注意する必要があります。  
  
-   保留中の更新を含む階層レコード セットは、XML に保存することはできません。  
  
-   (XML または adtg 形式のいずれかの形式) では、パラメーター化された図形コマンドで作成された階層レコード セットを保存できません。  
  
-   現在、ADO は、バイナリ ラージ オブジェクト (BLOB) として、親と子レコード セット間のリレーションシップを保存します。 行セットのスキーマ名前空間でのこの関係を記述する XML タグはまだ定義されていません。  
  
-   階層レコード セットが保存されると、すべての子のレコード セットは、これと共に保存します。 現在のレコード セットが別のレコード セットの子である場合は、その親は保存されません。 すべての子の現在のレコード セットのサブツリーを形成するレコード セットが保存されます。  
  
 その XML に永続化された形式から再開階層レコード セットは、次の制限を認識する必要があります。  
  
-   子レコードのレコードを対応する親レコードがない場合は、これらの行は書き込まれません階層レコード セットの XML 表記でします。 したがって、レコード セットが、永続化された場所から再度開いたときに、これらの行は失われます。  
  
-   子レコードには、複数の親レコードへの参照がある場合は、レコード セットをもう一度開こう子レコード セットが重複レコードを含みます。 ただし、これらの重複は場合にのみ表示、ユーザーが基になる子行セットを直接操作します。 子レコード セット (つまり ADO 内を移動する唯一の方法) を移動するチャプターを使用する場合は、重複部分は表示されません。  
  
## <a name="see-also"></a>関連項目  
 [レコードを XML 形式で保持する](../../../ado/guide/data/persisting-records-in-xml-format.md)
