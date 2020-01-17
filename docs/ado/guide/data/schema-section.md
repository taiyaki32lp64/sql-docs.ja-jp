---
title: スキーマ セクション |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Schema section [ADO]
ms.assetid: 4ac6e524-2c92-48e8-b871-0a4b5c8fda18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5b6e591ecc9f366f3914986b0ae11e0e301b782d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924297"
---
# <a name="schema-section"></a>スキーマ セクション
スキーマ セクションが必要です。 前の例に示すように、ADO は更新可能な限りデータ値のセマンティクスを保持するには、各列に関する詳細なメタデータを書き込みます。 ただし、XML に読み込むには、ADO のみが必要です、列および所属する行セットの名前。 最小限のスキーマの例を次に示します。  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"  
    xmlns:rs="urn:schemas-microsoft-com:rowset"  
    xmlns:z="#RowsetSchema">  
  <s:Schema id="RowsetSchema">  
    <s:ElementType name="row" content="eltOnly">  
      <s:AttributeType name="ShipperID"/>  
      <s:AttributeType name="CompanyName"/>  
      <s:AttributeType name="Phone"/>  
      <s:Extends type="rs:rowbase"/>  
    </s:ElementType>  
  </s:Schema>  
  <rs:data>  
...  
  </rs:data>  
</xml>  
```  
  
 前の例では、スキーマの型情報が含まれていないために、ADO は、可変長の文字列としてデータを扱います。  
  
## <a name="creating-aliases-for-column-names"></a>列名のエイリアスの作成  
 Rs: name 属性を使用して、フレンドリ名の行セットによって公開されている列情報が含まれるおよびデータ セクションに短い名前を使用するように、列名のエイリアスを作成できます。 たとえば、前のスキーマを変更して、運送を s1、s2、CompanyName にマップし、次のように、s3 に電話するでした。  
  
```  
<s:Schema id="RowsetSchema">   
<s:ElementType name="row" content="eltOnly" rs:updatable="true">   
<s:AttributeType name="s1" rs:name="ShipperID" rs:number="1" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s2" rs:name="CompanyName" rs:number="2" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s3" rs:name="Phone" rs:number="3" ...>   
...  
</s:AttributeType>   
...  
</s:ElementType>   
</s:Schema>  
```  
  
 その後、データのセクションで、行は、その列を参照する、name 属性 (rs: 名ではなく) を使用します。  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 列名が有効な属性または xml タグ名ではないときに、列名のエイリアスを作成することが必要です。 たとえば、"LastName"は別名を持つ必要がありますに埋め込まれたスペース名が無効な属性であるためです。 次の行は正しく処理されません、XML パーサーで、埋め込みスペースがない別の名前に別名を作成する必要がありますようにします。  
  
```  
<row last name="Jones"/>  
```  
  
 Name 属性を使用する値は、XML ドキュメントのスキーマとデータの両方のセクションで、列が参照されている適切な各場所で常に使用する必要があります。 次の例は、s1 の一貫した使用を示しています。  
  
```  
<s:Schema id="RowsetSchema">  
  <s:ElementType name="row" content="eltOnly">  
    <s:attribute type="s1"/>  
    <s:attribute type="CompanyName"/>  
    <s:attribute type="s3"/>  
    <s:extends type="rs:rowbase"/>  
  </s:ElementType>  
  <s:AttributeType name="s1" rs:name="ShipperID" rs:number="1"   
    rs:maydefer="true" rs:writeunknown="true">  
    <s:datatype dt:type="i4" dt:maxLength="4" rs:precision="10"   
      rs:fixedlength="true" rs:maybenull="true"/>  
  </s:AttributeType>  
</s:Schema>  
<rs:data>  
  <z:row s1="1" CompanyName="Speedy Express" s3="(503) 555-9831"/>  
</rs:data>  
```  
  
 同様があるため、エイリアスに対して定義されていない`CompanyName`前の例では、`CompanyName`ドキュメント全体で一貫して使用する必要があります。  
  
## <a name="data-types"></a>データ型  
 データ型は、dt:type 属性を持つ列に適用できます。 使用できる XML 型に説明するものでは、データ型を参照してください、 [W3C の XML データの指定](http://www.w3.org/TR/1998/NOTE-XML-data/)します。 2 つの方法でデータ型を指定できます。 列の定義自体で直接 dt:type 属性を指定するか、入れ子になった列定義の要素として s:datatype コンストラクトを使用します。 例を次に示します。  
  
```  
<s:AttributeType name="Phone" >  
  <s:datatype dt:type="string"/>  
</s:AttributeType>  
```  
  
 上記の式は、次の式と同じです。  
  
```  
<s:AttributeType name="Phone" dt:type="string"/>  
```  
  
 既定では、行の定義全体から dt:type 属性を省略した場合、列の型は可変長の文字列になります。  
  
 単純型名 (たとえば、dt:maxLength) よりも多くの型情報があれば、そのことが見やすくなります s:datatype の子要素を使用します。 これは単なる慣習、ただし、および要件ではありません。  
  
 次の例では、さらに、スキーマに型情報を含める方法を示します。  
  
```  
<!-- 1. String with no max length -->  
<s:AttributeType name="title_id"/>  
<!-or -->  
<s:AttributeType name="title_id" dt:type="string"/>  
  
<!-- 2. Fixed length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" rs:fixedlength="true" />  
</s:AttributeType>  
  
<!-- 3. Variable length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" />  
</s:AttributeType>  
  
<!-- 4. Integer -->  
<s:AttributeType name="title_id" dt:type="int"/>  
```  
  
 これは、2 番目の例では、rs: fixedlength 属性の微妙な使用です。 Rs: fixedlength 属性を持つ列は、データがスキーマで定義された長さの必要な場合は true を設定します。 この場合、title_id の有効な値は「123456、」は「123」 ただし、「123」は有効なためにできません、長さが 3、6 ではなくです。 OLE DB プログラマーズ ガイドより完了 fixedlength プロパティの説明を参照してください。  
  
## <a name="handling-nulls"></a>Null 値の処理  
 Null 値は、rs: maybenull 属性によって処理されます。 この属性設定されている場合は true、列の内容は、null 値を含めることができます。 さらに、行のデータの列が見つからない場合、行セットからデータを読み取り、ユーザーは null 状態 IRowset::GetData() から受け取ります。 Shippers テーブルから次の列の定義を検討してください。  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 定義により`CompanyName`、null にすることが、 `ShipperID` null 値を含めることはできません。 永続化プロバイダーでのデータの状態を設定とデータ セクションに次の行が含まれている場合、 `CompanyName` OLE DB 状態定数 DBSTATUS_S_ISNULL 列。  
  
```  
<z:row ShipperID="1"/>  
```  
  
 行が次のようにまったく空があった場合、永続化プロバイダーは、OLE DB のリターン ステータスの DBSTATUS_E_UNAVAILABLE`ShipperID`と CompanyName を DBSTATUS_S_ISNULL します。  
  
```  
<z:row/>   
```  
  
 長さ 0 の文字列が null の場合と同じに注意してください。  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 前の行では、永続化プロバイダーは DBSTATUS_S_OK の両方の列の OLE DB 状態を返します。 `CompanyName`ここでは単に""(長さ 0 の文字列)。  
  
 For OLE DB、XML ドキュメントのスキーマ内で使用可能な構造、OLE DB の詳細については、の定義を参照してください"urn: スキーマ-microsoft-com:rowset"と OLE DB プログラマ ガイド。  
  
## <a name="see-also"></a>関連項目  
 [レコードを XML 形式で保持する](../../../ado/guide/data/persisting-records-in-xml-format.md)
