---
title: XML スキーマ コレクションに対する権限の取り消し | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- revoking permissions [SQL Server]
ms.assetid: 4e542b70-2d56-4a65-8a39-96a1ed477ca6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 864a310044d2bf6b903b69b1b53bd6cd5bd3b38d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240725"
---
# <a name="revoke-permissions-on-an-xml-schema-collection"></a>XML スキーマ コレクションに対する権限の取り消し
  XML スキーマ コレクションを作成する権限は、次のいずれかの方法で取り消すことができます。  
  
-   リレーショナル スキーマの ALTER 権限を取り消します。 その結果、プリンシパルはリレーショナル スキーマで XML スキーマ コレクションを作成できなくなります。 ただし、同じデータベースの他のリレーショナル スキーマでは作成できます。  
  
-   プリンシパルのデータベースの ALTER ANY SCHEMA 権限を取り消します。 その結果、プリンシパルはデータベースのどこでも XML スキーマ コレクションを作成できなくなります。  
  
-   プリンシパルのデータベースの CREATE XML SCHEMA COLLECTION 権限または ALTER XML SCHEMA COLLECTION 権限を取り消します。 これにより、プリンシパルはデータベース内に XML スキーマ コレクションをインポートできなくなります。 データベースの ALTER 権限または CONTROL 権限を取り消しても、同じ効果があります。  
  
## <a name="revoking-permissions-on-an-existing-xml-schema-collection-object"></a>既存の XML スキーマ コレクション オブジェクトに対する権限の取り消し  
 次に、XML スキーマ コレクションで取り消し可能な権限と権限を取り消した結果を示します。  
  
-   ALTER 権限を取り消すと、XML スキーマ コレクションのコンテンツを変更するプリンシパルの権限が取り消されます。  
  
-   TAKE OWNERSHIP 権限を取り消すと、XML スキーマ コレクションの所有権を転送するプリンシパルの権限が取り消されます。  
  
-   REFERENCES 権限を取り消すと、テーブルやビュー内の xml 型の列やパラメーターを、型指定または制約するために XML スキーマ コレクションを使用するプリンシパルの権限が取り消されます。 また、他の XML スキーマ コレクションからこのスキーマ コレクションを参照する権限も取り消されます。  
  
-   VIEW DEFINITION 権限を取り消すと、XML スキーマ コレクションのコンテンツを表示するプリンシパルの権限が取り消されます。  
  
-   EXECUTE 権限を取り消すと、XML コレクションによって型指定または制約された列、変数、およびパラメーターの値を挿入または更新するプリンシパルの権限が取り消されます。 これにより、そのような **xml** 型の列、変数、またはパラメーターにクエリする権限も取り消されます。  
  
## <a name="examples"></a>使用例  
 次の例に示すシナリオでは、XML スキーマ権限のしくみを説明します。 各例では、必要なテスト データベース、リレーショナル スキーマ、およびログインを作成します。 それらのログインには、必要な XML スキーマ コレクション権限が許可されています。 最後に必要なクリーンアップを行います。  
  
### <a name="a-revoking-permissions-to-create-an-xml-schema-collection"></a>A. XML スキーマ コレクションを作成するための権限の取り消し  
 この例では、ログインとサンプル データベースを作成します。 データベースにはリレーショナル スキーマも追加します。 最初に、ログインに両方のリレーショナル スキーマの ALTER 権限を許可し、XML スキーマ コレクションを作成するのに必要なその他の権限を許可します。 次に、データベースのリレーショナル スキーマのいずれかの ALTER 権限を取り消します。 これにより、このログインは XML スキーマ コレクションを作成できなくなります。  
  
```  
setuser  
go  
create login TestLogin1 with password='SQLSvrPwd1'  
go  
create database SampleDBForSchemaPermissions  
go  
use SampleDBForSchemaPermissions  
go  
-- Create another relational schema in the db (in addition to dbo schema)  
CREATE SCHEMA myOtherDBSchema  
go  
CREATE USER TestLogin1  
go  
-- For TestLogin1 to create/import XML schema collection, following  
-- permission needed  
-- CREATE XML SCHEMA is a database level permission  
GRANT CREATE XML SCHEMA COLLECTION TO TestLogin1  
go  
GRANT ALTER ON SCHEMA::myOtherDBSchema TO TestLogin1  
go  
GRANT ALTER ON SCHEMA::dbo TO TestLogin1  
go  
-- Now TestLogin1 can import an XML schema collection in both relational schemas.  
setuser 'TestLogin1'  
go  
CREATE XML SCHEMA COLLECTION dbo.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
-- TestLogin1 can create XML schema collection in myOtherDBSchema relational schema  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
-- Let us drop XML schema collections from both relational schemas  
DROP XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection  
go  
DROP XML SCHEMA COLLECTION dbo.myTestSchemaCollection  
go  
-- now REVOKE permission from TestLogin1 to alter myOtherDBSchema  
setuser  
go  
REVOKE ALTER ON SCHEMA::myOtherDBSchema FROM TestLogin1  
go  
-- now TestLogin1 cannot create xml schema collection in myOtherDBSchema  
setuser 'TestLogin1'  
go  
CREATE XML SCHEMA COLLECTION myOtherDBSchema.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
  
-- TestLogin1 can still create XML schema collections in dbo  
-- It cannot create XML schema collections anywhere in the database  
-- if we REVOKE CREATE XML SCHEMA COLLECTION permission  
SETUSER  
go  
REVOKE CREATE XML SCHEMA COLLECTION FROM TestLogin1  
go  
  
setuser 'TestLogin1'  
go  
-- the following now should fail  
CREATE XML SCHEMA COLLECTION dbo.myTestSchemaCollection AS '<?xml version="1.0" encoding="UTF-8" ?>  
<xsd:schema targetNamespace="http://schemas.adventure-works.com/Additional/ContactInfo"   
            xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
elementFormDefault="qualified">  
<xsd:element name="telephone" type="xsd:string" />  
</xsd:schema>'  
go  
  
-- Final cleanup  
SETUSER  
go  
USE master  
go  
DROP DATABASE SampleDBForSchemaPermissions  
go  
DROP LOGIN TestLogin1  
Go  
```  
  
## <a name="see-also"></a>参照  
 [XML データ &#40;SQL Server&#41;](xml-data-sql-server.md)   
 [型指定された XML と型指定されていない XML の比較](compare-typed-xml-to-untyped-xml.md)   
 [XML スキーマ コレクション &#40;SQL Server&#41;](xml-schema-collections-sql-server.md)   
 [サーバー上の XML スキーマ コレクションの要件と制限](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
