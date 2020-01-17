---
title: XML スキーマ コレクションに対する権限の拒否 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- denying permissions [SQL Server], XML server collections
ms.assetid: e2b300b0-e734-4c43-a4da-c78e6e5d4fba
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2fe1a42540b21fd11dbfb9747a77991073d35c97
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62637570"
---
# <a name="deny-permissions-on-an-xml-schema-collection"></a>XML スキーマ コレクションに対する権限の拒否
  新しい XML スキーマ コレクションを作成したり、既存の XML スキーマ コレクションを使用する権限を拒否できます。  
  
## <a name="denying-permission-to-create-an-xml-schema-collection"></a>XML スキーマ コレクションを作成する権限の拒否  
 次の方法で、XML スキーマ コレクションを作成する権限を拒否できます。  
  
-   リレーショナル スキーマに対する ALTER 権限を拒否します。  
  
-   リレーショナル スキーマやスキーマに含まれるすべてのオブジェクトに対するすべての権限を拒否するには、リレーショナル スキーマに対する CONTROL 権限を拒否します。  
  
-   データベースに対する ALTER ANY SCHEMA を拒否します。 この場合、プリンシパルはデータベースのどこにも XML スキーマ コレクションを作成できなくなります。 データベースに対する ALTER 権限または CONTROL 権限を拒否すると、データベース内のすべてのオブジェクトに対するすべての権限を拒否することになるので注意が必要です。  
  
## <a name="denying-permissions-on-an-xml-schema-collection-object"></a>XML スキーマ コレクション オブジェクトの権限の拒否  
 既存の XML スキーマ コレクションで拒否可能な権限とその結果を次に示します。  
  
-   ALTER 権限を拒否すると、XML スキーマ コレクションの内容を変更するプリンシパルの権限を拒否することになります。  
  
-   CONTROL 権限を拒否すると、XML スキーマ コレクションで操作を実行するプリンシパルの権限を拒否することになります。  
  
-   REFERENCES 権限を拒否すると、XML スキーマ コレクションを使用して xml 型の列やパラメーターを型指定または制約するプリンシパルの権限を拒否することになります。 また、他の XML スキーマ コレクションからこの XML スキーマ コレクションを参照するプリンシパルの権限も拒否することになります。  
  
-   VIEW DEFINITION 権限を拒否すると、XML スキーマ コレクションのコンテンツを表示するプリンシパルの権限を拒否することになります。  
  
-   EXECUTE 権限を拒否すると、XML スキーマ コレクションによって型指定または制約された列、変数、およびパラメーターの値を挿入または更新するプリンシパルの権限を拒否することになります。 また、同じ xml 型の列や変数の値のクエリを実行するプリンシパルの権限も拒否することになります。  
  
## <a name="examples"></a>使用例  
 次の例のシナリオでは、XML スキーマ権限の動作を示します。 各例では、必要なテスト データベース、リレーショナル スキーマ、およびログインを作成します。 それらのログインには、必要な XML スキーマ コレクション権限が許可されています。 最後に必要なクリーンアップを行います。  
  
### <a name="a-preventing-a-user-from-creating-an-xml-schema-collection"></a>A. ユーザーによる XML スキーマ コレクションの作成を防止する  
 ユーザーが XML スキーマ コレクションを作成できないようにする方法の 1 つは、リレーショナル スキーマの ALTER 権限を拒否することです。 次の例を参照してください。  
  
 この例では、ユーザー `TestLogin1`とデータベースを作成します。 このデータベースには、 `dbo` スキーマに加えてリレーショナル スキーマも作成します。 まず、 `CREATE XML SCHEMA` 権限によって、データベース内の任意の場所にスキーマ コレクションを作成する権限をユーザーに許可します。 次に、リレーショナル スキーマの 1 つに対して、そのユーザーの `ALTER` 権限を拒否します。 これにより、ユーザーはこのリレーショナル スキーマで XML スキーマ コレクションを作成できなくなります。  
  
```  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
CREATE USER TestLogin1  
GO  
-- For TestLogin1 to create/import XML schema collection, following  
-- permission needed.  
-- Database-level permissions  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
GO  
GRANT ALTER ANY SCHEMA TO TestLogin1  
GO  
-- Now TestLogin1 can import an XML schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
DROP XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection  
GO  
-- Now deny permission from TestLogin1 to alter myOtherDBSchema.  
setuser  
GO  
DENY ALTER ON SCHEMA::myOtherDBSchema TO TestLogin1  
GO  
-- Now TestLogin1 cannot create xml schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
-- Final cleanup  
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
### <a name="b-denying-permissions-on-an-xml-schema-collection"></a>B. XML スキーマ コレクションに対する権限の拒否  
 次の例では、既存の XML スキーマ コレクションに対するログインの特定の権限を拒否する方法を示します。 この例では、テスト ログインは既存の XML スキーマ コレクションに対する REFERENCES 権限を拒否します。  
  
 この例では、ユーザー `TestLogin1`とデータベースを作成します。 このデータベースには、 `dbo` スキーマに加えてリレーショナル スキーマも作成します。 まず、 `CREATE XML SCHEMA` 権限によって、データベース内の任意の場所にスキーマ コレクションを作成する権限をユーザーに許可します。  
  
 `REFERENCES` に XML スキーマ コレクションに対する `TestLogin1` 権限があれば、テーブルに型指定された `xml` 列を作成するときにスキーマを使用できます。 XML スキーマ コレクションに対する `REFERENCES` 権限が拒否された場合、 `TestLogin1` は XML スキーマ コレクションを使用できません。  
  
```  
CREATE LOGIN TestLogin1 WITH password='SQLSvrPwd1'  
GO  
CREATE DATABASE SampleDBForSchemaPermissions  
GO  
USE SampleDBForSchemaPermissions  
GO  
-- Create another relational schema in the database.  
CREATE SCHEMA myOtherDBSchema  
GO  
CREATE USER TestLogin1  
GO  
-- For TestLogin1 to create/import XML schema collection, the following  
-- permission is required.  
-- Database-level permissions  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
GO  
GRANT ALTER ANY SCHEMA TO TestLogin1  
GO  
-- Now TestLogin1 can import an XML schema collection.  
SETUSER 'TestLogin1'  
GO  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
GO  
-- Grant permission to TestLogin1 to create a table and reference the XML schema collection.  
SETUSER  
GO  
GRANT CREATE TABLE TO TestLogin1  
GO  
-- The user also needs REFERENCES permission to use the XML schema collection  
-- to create a typed XML column (REFERENCES permission on the schema   
-- collection is not needed).  
GRANT REFERENCES ON XML SCHEMA COLLECTION::myOtherDBSchema.myTestSchemaCollection   
TO TestLogin1  
GO  
  
--TestLogin1 can use the schema.  
CREATE TABLE T(i int, x xml (myOtherDBSchema.myTestSchemaCollection))  
GO  
-- Drop the table.  
DROP TABLE T  
GO  
-- Now deny REFERENCES permission to TestLogin1 on the schema created previously.  
SETUSER  
GO  
DENY REFERENCES ON XML SCHEMA COLLECTION::myOtherDBSchema.myTestSchemaCollection TO TestLogin1  
  
GO  
-- Now TestLogin1 cannot create xml schema collection  
SETUSER 'TestLogin1'  
GO  
-- Following statement fails. TestLogin1 does not have REFERENCES   
-- permission on the XML schema collection.  
CREATE TABLE T(i int, x xml (myOtherDBSchema.myTestSchemaCollection))  
GO  
  
-- Final cleanup  
SETUSER  
GO  
USE master  
GO  
DROP DATABASE SampleDBForSchemaPermissions  
GO  
DROP LOGIN TestLogin1  
GO  
```  
  
## <a name="see-also"></a>参照  
 [型指定された XML と型指定されていない XML の比較](compare-typed-xml-to-untyped-xml.md)   
 [XML スキーマ コレクション &#40;SQL Server&#41;](xml-schema-collections-sql-server.md)   
 [サーバー上の XML スキーマ コレクションの要件と制限](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)   
 [DENY (オブジェクトの権限の拒否) &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-object-permissions-transact-sql)   
 [GRANT (オブジェクトの権限の許可) &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-object-permissions-transact-sql)   
 [XML データ &#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  
