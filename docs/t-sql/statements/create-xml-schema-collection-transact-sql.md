---
title: CREATE XML SCHEMA COLLECTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE XML SCHEMA COLLECTION
- CREATE_XML_SCHEMA_COLLECTION_TSQL
- CREATE XML SCHEMA
- CREATE_XML_SCHEMA_TSQL
- COLLECTION
- COLLECTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE XML SCHEMA COLLECTION statement
- importing schema components
- schema collections [SQL Server], creating
- multiple schema namespaces
- XML schema collections [SQL Server], creating
ms.assetid: 350684e8-b3f6-4b58-9dbc-0f05cc776ebb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 28409675fda41f030e82337b1fcf0f1a6ec5821e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927725"
---
# <a name="create-xml-schema-collection-transact-sql"></a>CREATE XML SCHEMA COLLECTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  データベースにスキーマ コンポーネントをインポートします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE XML SCHEMA COLLECTION [ <relational_schema>. ]sql_identifier AS Expression  
```  
  
## <a name="arguments"></a>引数  
 *relational_schema*  
 リレーショナル スキーマ名を指定します。 指定しない場合、既定のリレーショナル スキーマが使用されます。  
  
 *sql_identifier*  
 XML スキーマ コレクションの SQL 識別子を指定します。  
  
 *[式]*  
 文字列定数またはスカラー変数を指定します。 **varchar**、**varbinary**、**nvarchar**、または **xml** 型です。  
  
## <a name="remarks"></a>Remarks  
 [ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md) を使用して、新しい名前空間をコレクションに追加したり、コレクションの既存の名前空間に新しいコンポーネントを追加したりすることもできます。  
  
 コレクションを削除するには、[DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md) を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 XML SCHEMA COLLECTION を作成するには、少なくとも次のいずれかの権限セットが必要です。  
  
-   サーバーに対する CONTROL 権限  
  
-   サーバーに対する ALTER ANY DATABASE 権限  
  
-   データベースに対する ALTER 権限  
  
-   データベースに対する CONTROL 権限  
  
-   データベースに対する ALTER ANY SCHEMA 権限と CREATE XML SCHEMA COLLECTION 権限  
  
-   リレーショナル スキーマに対する ALTER 権限または CONTROL 権限と、データベースに対する CREATE XML SCHEMA COLLECTION 権限  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-xml-schema-collection-in-the-database"></a>A. データベースに XML スキーマ コレクションを作成する  
 次の例では、XML スキーマ コレクション `ManuInstructionsSchemaCollection` を作成します。 コレクションにはスキーマ名前空間が 1 つだけ含まれます。  
  
```  
-- Create a sample database in which to load the XML schema collection.  
CREATE DATABASE SampleDB;  
GO  
USE SampleDB;  
GO  
CREATE XML SCHEMA COLLECTION ManuInstructionsSchemaCollection AS  
N'<?xml version="1.0" encoding="UTF-16"?>  
<xsd:schema targetNamespace="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"   
   xmlns          ="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"   
   elementFormDefault="qualified"   
   attributeFormDefault="unqualified"  
   xmlns:xsd="http://www.w3.org/2001/XMLSchema" >  
  
    <xsd:complexType name="StepType" mixed="true" >  
        <xsd:choice  minOccurs="0" maxOccurs="unbounded" >   
            <xsd:element name="tool" type="xsd:string" />  
            <xsd:element name="material" type="xsd:string" />  
            <xsd:element name="blueprint" type="xsd:string" />  
            <xsd:element name="specs" type="xsd:string" />  
            <xsd:element name="diag" type="xsd:string" />  
        </xsd:choice>   
    </xsd:complexType>  
  
    <xsd:element  name="root">  
        <xsd:complexType mixed="true">  
            <xsd:sequence>  
                <xsd:element name="Location" minOccurs="1" maxOccurs="unbounded">  
                    <xsd:complexType mixed="true">  
                        <xsd:sequence>  
                            <xsd:element name="step" type="StepType" minOccurs="1" maxOccurs="unbounded" />  
                        </xsd:sequence>  
                        <xsd:attribute name="LocationID" type="xsd:integer" use="required"/>  
                        <xsd:attribute name="SetupHours" type="xsd:decimal" use="optional"/>  
                        <xsd:attribute name="MachineHours" type="xsd:decimal" use="optional"/>  
                        <xsd:attribute name="LaborHours" type="xsd:decimal" use="optional"/>  
                        <xsd:attribute name="LotSize" type="xsd:decimal" use="optional"/>  
                    </xsd:complexType>  
                </xsd:element>  
            </xsd:sequence>  
        </xsd:complexType>  
    </xsd:element>  
</xsd:schema>' ;  
GO  
-- Verify - list of collections in the database.  
SELECT *  
FROM sys.xml_schema_collections;  
-- Verify - list of namespaces in the database.  
SELECT name  
FROM sys.xml_schema_namespaces;  
  
-- Use it. Create a typed xml variable. Note collection name specified.  
DECLARE @x xml (ManuInstructionsSchemaCollection);  
GO  
--Or create a typed xml column.  
CREATE TABLE T (  
        i int primary key,   
        x xml (ManuInstructionsSchemaCollection));  
GO  
-- Clean up  
DROP TABLE T;  
GO  
DROP XML SCHEMA COLLECTION ManuInstructionsSchemaCollection;  
Go  
USE master;  
GO  
DROP DATABASE SampleDB;  
```  
  
 または、次のようにスキーマ コレクションを変数に割り当て、その変数を `CREATE XML SCHEMA COLLECTION` ステートメントで指定することもできます。  
  
```  
DECLARE @MySchemaCollection nvarchar(max)  
Set @MySchemaCollection  = N' copy the schema collection here'  
CREATE XML SCHEMA COLLECTION MyCollection AS @MySchemaCollection   
```  
  
 この例の変数は `nvarchar(max)` 型です。 変数のデータ型としては **xml** も有効です。この場合、変数は暗黙的に文字列に変換されます。  
  
 詳細については、「 [格納されている XML スキーマ コレクションの表示](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)」を参照してください。  
  
 スキーマ コレクションを格納する、**xml** 型の列です。 この場合、XML スキーマ コレクションを作成するには、次の操作を行います。  
  
1.  SELECT ステートメントを使用して列からスキーマ コレクションを取得し、**xml** 型または **varchar** 型の変数に割り当てます。  
  
2.  CREATE XML SCHEMA COLLECTION ステートメントで変数名を指定します。  
  
 CREATE XML SCHEMA COLLECTION には、SQL Server で認識されるスキーマ コンポーネントだけが格納されます。XML スキーマ内のすべてがデータベースに格納されるわけではありません。 したがって、XML スキーマ コレクションを、提供されたときと同じ状態に戻す場合は、データベース列またはコンピューター上の他のフォルダーに XML スキーマを保存することをお勧めします。  
  
### <a name="b-specifying-multiple-schema-namespaces-in-a-schema-collection"></a>B. スキーマ コレクションに複数のスキーマ名前空間を指定する  
 XML スキーマ コレクションを作成するときには、複数の XML スキーマを指定できます。 例:  
  
```  
CREATE XML SCHEMA COLLECTION MyCollection AS N'  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
<!-- Contents of schema here -->    
</xsd:schema>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
<!-- Contents of schema here -->  
</xsd:schema>';  
```  
  
 次の例では、2 つの XML スキーマ名前空間を含む XML スキーマ コレクション `ProductDescriptionSchemaCollection` を作成します。  
  
```  
CREATE XML SCHEMA COLLECTION ProductDescriptionSchemaCollection AS   
'<xsd:schema targetNamespace="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"  
    xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
    elementFormDefault="qualified"   
    xmlns:xsd="http://www.w3.org/2001/XMLSchema" >  
    <xsd:element name="Warranty"  >  
        <xsd:complexType>  
            <xsd:sequence>  
                <xsd:element name="WarrantyPeriod" type="xsd:string"  />  
                <xsd:element name="Description" type="xsd:string"  />  
            </xsd:sequence>  
        </xsd:complexType>  
    </xsd:element>  
</xsd:schema>  
 <xs:schema targetNamespace="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
    xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
    elementFormDefault="qualified"   
    xmlns:mstns="https://tempuri.org/XMLSchema.xsd"   
    xmlns:xs="http://www.w3.org/2001/XMLSchema"  
    xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" >  
    <xs:import   
namespace="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain" />  
    <xs:element name="ProductDescription" type="ProductDescription" />  
        <xs:complexType name="ProductDescription">  
            <xs:sequence>  
                <xs:element name="Summary" type="Summary" minOccurs="0" />  
            </xs:sequence>  
            <xs:attribute name="ProductModelID" type="xs:string" />  
            <xs:attribute name="ProductModelName" type="xs:string" />  
        </xs:complexType>  
        <xs:complexType name="Summary" mixed="true" >  
            <xs:sequence>  
                <xs:any processContents="skip" namespace="http://www.w3.org/1999/xhtml" minOccurs="0" maxOccurs="unbounded" />  
            </xs:sequence>  
        </xs:complexType>  
</xs:schema>'  
;  
GO -- Clean up  
DROP XML SCHEMA COLLECTION ProductDescriptionSchemaCollection;  
GO  
```  
  
### <a name="c-importing-a-schema-that-does-not-specify-a-target-namespace"></a>C. 対象の名前空間が指定されていないスキーマをインポートする  
 次の例に示すように、**targetNamespace** 属性が含まれていないスキーマをコレクションにインポートする場合、スキーマのコンポーネントは空文字列の対象の名前空間に関連付けられます。 コレクションにインポートされる 1 つ以上のスキーマについて関連付けを行わない場合は、複数のスキーマ コンポーネント (場合によっては関係のないコンポーネント) が既定の空文字列の名前空間に関連付けられるため注意してください。  
  
```  
-- Create a collection that contains a schema with no target namespace.  
CREATE XML SCHEMA COLLECTION MySampleCollection AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  xmlns:ns="http://ns">  
<element name="e" type="dateTime"/>  
</schema>';  
go  
-- Query will return the names of all the collections that   
--contain a schema with no target namespace.  
SELECT sys.xml_schema_collections.name   
FROM   sys.xml_schema_collections   
JOIN   sys.xml_schema_namespaces   
ON     sys.xml_schema_collections.xml_collection_id =   
       sys.xml_schema_namespaces.xml_collection_id   
WHERE  sys.xml_schema_namespaces.name='';  
```  
  
### <a name="d-using-an-xml-schema-collection-and-batches"></a>D. XML スキーマ コレクションとバッチを使用する  
 スキーマ コレクションを作成した同じバッチ内で、そのスキーマ コレクションを参照することはできません。 作成した同じバッチ内でコレクションを参照しようとすると、コレクションが存在しないというエラーを受け取ります。 次の例は動作しますが、`GO` を削除し、同じバッチ内で、`xml` 変数を入力するために XML スキーマ コレクションを参照しようとすると、エラーが返されます。  
  
```  
CREATE XML SCHEMA COLLECTION mySC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="string"/>  
</schema>  
';  
GO  
CREATE TABLE T (Col1 xml (mySC));  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ALTER XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md)   
 [DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [型指定された XML と型指定されていない XML の比較](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md)   
 [サーバー上の XML スキーマ コレクションの要件と制限](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
