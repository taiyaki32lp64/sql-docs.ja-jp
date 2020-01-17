---
title: 組み込みの XML スキーマ コレクション (sys) の参照 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- sys XML schema collections [SQL Server]
- schema collections [SQL Server], predefined
- predefined XML schema collections [SQL Server]
- XML schema collections [SQL Server], predefined
- built-in XML schema collections [SQL Server]
ms.assetid: 1e118303-5df0-4ee4-bd8d-14ced7544144
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 410dd8785ce58f87b35c6c18b5c5dc00ffcd9faa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240780"
---
# <a name="reference-the-built-in-xml-schema-collection-sys"></a>組み込みの XML スキーマ コレクション (sys) の参照
  作成したどのデータベースでも、 **sys** リレーショナル スキーマに **sys** XML スキーマ コレクションが事前に定義されています。 各データベースはこれらの事前定義されたスキーマを保持します。また、これらのスキーマは、ユーザーが作成した他の XML スキーマ コレクションからアクセスできます。 このような事前定義されたスキーマに使われているプレフィックスは、XQuery で意味があるものとして扱われます。 **xml** のみが、予約されているプレフィックスです。  
  
```  
xml = http://www.w3.org/XML/1998/namespace  
xs = http://www.w3.org/2001/XMLSchema  
xsi = http://www.w3.org/2001/XMLSchema-instance  
fn = http://www.w3.org/2004/07/xpath-functions  
sqltypes = https://schemas.microsoft.com/sqlserver/2004/sqltypes  
xdt = http://www.w3.org/2004/07/xpath-datatypes  
(no prefix) = urn:schemas-microsoft-com:xml-sql  
(no prefix) = https://schemas.microsoft.com/sqlserver/2004/SOAP  
```  
  
 **sqltypes** 名前空間には、ユーザーが作成したどの XML スキーマ コレクションからでも参照できるコンポーネントが含まれます。 **sqltypes** スキーマは、 [Microsoft Web サイト](https://go.microsoft.com/fwlink/?linkid=31850)からダウンロードできます。 組み込みのコンポーネントには、次のものが含まれます。  
  
-   XSD 型  
  
-   XML 属性 **lang**、 **base**、および **space**  
  
-   **sqltypes** 名前空間のコンポーネント  
  
 次のクエリは、ユーザーが作成した XML スキーマ コレクションから参照できる組み込みのコンポーネントを返します。  
  
```  
SELECT C.name, N.name, C.symbol_space_desc from sys.xml_schema_components C join sys.xml_schema_namespaces N  
on ((C.xml_namespace_id = N.xml_namespace_id) AND (C.xml_collection_id = N.xml_collection_id))  
join sys.xml_schema_collections SC  
on SC.xml_collection_id = C.xml_collection_id  
where ((C.xml_collection_id = 1) AND (C.name is not null) AND (C.scoping_xml_component_id is null)   
AND (SC.schema_id = 4))  
GO  
```  
  
 次の例は、これらのコンポーネントをユーザー スキーマで参照する方法を示しています。 `CREATE XML SCHEMA COLLECTION` は、 `varchar` 名前空間で定義されている `sqltypes` 型を参照する XML スキーマ コレクションを作成します。 この例では、 `lang` 名前空間で定義されている `xml` 属性も参照します。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema   
   xmlns="http://www.w3.org/2001/XMLSchema"   
   targetNamespace="myNS"  
   xmlns:ns="myNS"  
   xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes" >   
   <import namespace="http://www.w3.org/XML/1998/namespace"/>  
   <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
   <element name="root">  
      <complexType>  
          <sequence>  
             <element name="a" type="string"/>  
             <element name="b" type="string"/>  
             <!-- varchar type is defined in the sys.sys collection and   
                  can be referenced in any user-defined schema -->  
             <element name="c" type="s:varchar"/>  
          </sequence>  
          <attribute name="att" type="int"/>  
          <!-- xml:lang attribute is defined in the sys.sys collection   
               and can be referenced in any user-defined schema -->  
          <attribute ref="xml:lang"/>  
      </complexType>  
    </element>  
 </schema>'  
GO  
 -- Cleanup  
DROP xml schema collection SC   
GO  
```  
  
 注意点を次に示します。  
  
-   ユーザー定義の XML スキーマ コレクションで、これらの名前空間の XML スキーマを変更することはできません。 たとえば、次の XML スキーマ コレクションは、保護されている `sqltypes` 名前空間にコンポーネントを追加しているため、失敗します。  
  
    ```  
    CREATE XML SCHEMA COLLECTION SC AS '  
    <schema xmlns="http://www.w3.org/2001/XMLSchema"   
    targetNamespace    
        ="https://schemas.microsoft.com/sqlserver/2004/sqltypes" >   
          <element name="root" type="string"/>  
    </schema>'  
    GO  
    ```  
  
-   `sys` XML スキーマ コレクションを `xml` 型の列、変数、またはパラメーターの型指定に使用することはできません。 たとえば、次のコードではエラーが返されます。  
  
    ```  
    DECLARE @x xml (sys.sys)  
    ```  
  
-   これらの組み込みスキーマのシリアル化は、サポートされていません。 たとえば、次のコードではエラーが返されます。  
  
    ```  
    SELECT XML_SCHEMA_NAMESPACE(N'sys',N'sys')  
    GO  
    ```  
  
 `varchar` 名前空間で定義されている `sqltypes` 型を使用する XML スキーマ コレクションを作成する別の例を次に示します。  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"   
        targetNamespace="myNS" xmlns:ns="myNS"  
        xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
   <import     
     namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
            <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
go  
```  
  
 次の例に示すように、型指定した `XML` 変数を作成し、これに XML インスタンスを割り当て、<`root`> 要素の値の型が `varchar` 型であることを検証できます。  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "https://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
GO  
```  
  
 `@var` 変数に関連付けられているスキーマに従うと、<`root`> 要素の値の型が **varchar** 型の派生型であるため、`instance of sqltypes:varchar?` 式は TRUE を返します。  
  
## <a name="see-also"></a>参照  
 [XML スキーマ コレクション &#40;SQL Server&#41;](xml-schema-collections-sql-server.md)  
  
  
