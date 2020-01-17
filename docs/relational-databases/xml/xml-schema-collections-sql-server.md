---
title: XML スキーマ コレクション (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XSD schemas [SQL Server]
- xml_schema_namespace function
- XML schema collections [SQL Server], about XML schema collections
- metadata [SQL Server], XML schema collections
- queries [XML in SQL Server], XML schema collections
- schema collections [SQL Server]
- schemas [SQL Server], XML
- XML [SQL Server], schema collections
- XML schema collections [SQL Server]
- schema collections [SQL Server], about XML schema collections
ms.assetid: 659d41aa-ccec-4554-804a-722a96ef25c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4a334b4a02126023b94e5623b45050b067b48ce6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096818"
---
# <a name="xml-schema-collections-sql-server"></a>XML スキーマ コレクション (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  「[xml &#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md)」で説明したように、SQL Server には、**xml** データ型を使った XML データのネイティブ ストレージが用意されています。 必要に応じて、XML スキーマ コレクションを使って **xml** 型の変数や列と XSD スキーマを関連付けることができます。 XML スキーマ コレクションにはインポートした XML スキーマが格納され、その後このコレクションを次の操作に使用します。  
  
-   XML インスタンスの検証  
  
-   XML データをデータベースに格納するときの型指定  
  
 XML スキーマ コレクションは、データベース内のテーブルに似たメタデータ エンティティです。 XML スキーマ コレクションは作成、変更、削除できます。 [CREATE XML SCHEMA COLLECTION (Transact-SQL)](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) ステートメントで指定されたスキーマが、新しく作成される XML スキーマ コレクション オブジェクトに自動的にインポートされます。 [ALTER XML SCHEMA COLLECTION (Transact-SQL)](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md) ステートメントを使用して、追加のスキーマやスキーマ コンポーネントをデータベース内の既存のコレクション オブジェクトにインポートできます。  
  
 「[型指定された XML と型指定されていない XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)」で説明したように、スキーマが関連付けられる列や変数に格納されている XML を、**型指定された** XML と呼びます。これは、インスタンス データに必要なデータ型情報をスキーマが提供しているためです。 SQL Server ではこの型情報を使用して、データ ストレージを最適化します。  
  
 クエリ処理エンジンでも、型の確認、クエリの最適化、およびデータの変更にスキーマが使用されます。  
  
 また SQL Server では、型指定された **xml**の場合、XML インスタンスを検証するために関連付けられた XML スキーマ コレクションが使用されます。 XML インスタンスがスキーマを使ってコンパイルされると、そのデータベースはインスタンスを型情報と共にシステムに格納できます。 それ以外の場合は、インスタンスを拒否します。  
  
 固有の関数 XML_SCHEMA_NAMESPACE を使用して、データベースに格納されているスキーマ コレクションを取得できます。 詳細については、「 [格納されている XML スキーマ コレクションの表示](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)」を参照してください。  
  
 また、XML スキーマ コレクションは、XML 変数、パラメーター、および列の型指定にも使用できます。  
  
##  <a name="ddl"></a> スキーマ コレクションを管理するための DDL  
 データベースに XML スキーマ コレクションを作成し、 **xml** 型の変数や列に関連付けることができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、データベースでスキーマ コレクションを管理するために、次の DDL ステートメントが用意されています。  
  
-   [CREATE XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-schema-collection-transact-sql.md): データベースにスキーマ コンポーネントをインポートします。  
  
-   [ALTER XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md): 既存の XML スキーマ コレクションのスキーマ コンポーネントを変更します。  
  
-   [ DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md): XML スキーマ コレクション全体とそのすべてのコンポーネントを削除します。  
  
 XML スキーマ コレクションとそのコレクションに含まれるスキーマを使用するには、まず CREATE XML SCHEMA COLLECTION ステートメントを使用して、コレクションとスキーマを作成する必要があります。 スキーマ コレクションを作成したら、 **xml** 型の変数および列を作成し、スキーマ コレクションに関連付けることができます。 スキーマ コレクションを作成すると、さまざまなスキーマ コンポーネントがメタデータに格納されます。 ALTER XML SCHEMA COLLECTION ステートメントを使用して、既存のスキーマにコンポーネントを追加したり、既存のスキーマ コレクションに新しいスキーマを追加することもできます。  
  
 スキーマ コレクションを削除するには、DROP XML SCHEMA COLLECTION ステートメントを使用します。 このステートメントを実行すると、スキーマ コレクションに含まれているすべてのスキーマが削除され、コレクション オブジェクトが削除されます。 スキーマ コレクションを削除する前に、「[DROP XML SCHEMA COLLECTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-xml-schema-collection-transact-sql.md)」に記載されている条件を満たしていることを確認してください。  
  
##  <a name="components"></a> スキーマ コンポーネントについて  
 CREATE XML SCHEMA COLLECTION ステートメントを使用すると、さまざまなスキーマ コンポーネントがデータベースにインポートされます。 スキーマ コンポーネントには、スキーマの要素、属性、および型の定義などがあります。 DROP XML SCHEMA COLLECTION ステートメントを使用すると、コレクション全体が削除されます。  
  
 CREATE XML SCHEMA COLLECTION ステートメントを使用すると、さまざまなシステム テーブルにスキーマ コンポーネントが保存されます。  
  
 たとえば、次のスキーマを考えてみます。  
  
```xml
<?xml version="1.0"?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            targetNamespace="uri:Cust_Orders2"  
            xmlns="uri:Cust_Orders2" >  
  <xsd:attribute name="SomeAttribute" type="xsd:int" />  
  <xsd:complexType name="SomeType" />  
  <xsd:complexType name="OrderType" >  
    <xsd:sequence>  
      <xsd:element name="OrderDate" type="xsd:date" />  
      <xsd:element name="RequiredDate" type="xsd:date" />  
      <xsd:element name="ShippedDate" type="xsd:date" />  
    </xsd:sequence>  
    <xsd:attribute name="OrderID" type="xsd:ID" />  
    <xsd:attribute name="CustomerID"  />  
    <xsd:attribute name="EmployeeID"  />  
  </xsd:complexType>  
  <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order" type="OrderType"  
                     maxOccurs="unbounded" />  
       </xsd:sequence>  
      <xsd:attribute name="CustomerID" type="xsd:string" />  
      <xsd:attribute name="OrderIDList" type="xsd:IDREFS" />  
  </xsd:complexType>  
  <xsd:element name="Customer" type="CustomerType" />  
</xsd:schema>  
```  
  
 上記のスキーマは、データベースに格納できる、異なる型のコンポーネントを示しています。 これには、 `SomeAttribute`、 `SomeType`、 `OrderType`、 `CustomerType`、 `Customer`、 `Order`、 `CustomerID`、 `OrderID`、 `OrderDate`、 `RequiredDate`、および `ShippedDate`があります。  
  
### <a name="component-categories"></a>コンポーネントのカテゴリ  
 データベースに格納されるスキーマ コンポーネントは、次のように分類されます。  
  
-   ELEMENT  
  
-   ATTRIBUTE  
  
-   TYPE (単純型用または複合型用)  
  
-   ATTRIBUTEGROUP  
  
-   MODELGROUP  
  
 例:  
  
-   **SomeAttribute** は、ATTRIBUTE コンポーネントです。  
  
-   **SomeType**、 **OrderType**、および **CustomerType** は、TYPE コンポーネントです。  
  
-   **Customer** は、ELEMENT コンポーネントです。  
  
 スキーマをデータベースにインポートするとき、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではスキーマ自体は格納されません。 代わりに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって個々のさまざまなコンポーネントが格納されます。 つまり、\<Schema> タグは格納されず、定義されているコンポーネントのみが保持されます。 すべてのスキーマの要素は保持されません。 \<Schema> タグにそのコンポーネントの既定の動作を指定する属性が含まれている場合、次の表に示すように、そのような属性はインポート処理中にスキーマ コンポーネントに移動されます。  
  
|属性名|動作|  
|--------------------|--------------|  
|**attributeFormDefault**|**form** 属性が存在しないスキーマ内のすべての属性の宣言に適用され、値は **attributeFormDefault** 属性の値に設定されます。|  
|**elementFormDefault**|**form** 属性が存在しないスキーマ内のすべての要素の宣言に適用され、値は **elementFormDefault** 属性の値に設定されます。|  
|**blockDefault**|**block** 属性が存在しないすべての要素の宣言と型定義に適用され、値は **blockDefault** 属性の値に設定されます。|  
|**finalDefault**|**final** 属性が存在しないすべての要素の宣言と型定義に適用され、値は **finalDefault** 属性の値に設定されます。|  
|**targetNamespace**|対象の名前空間に属するコンポーネントに関する情報がメタデータに格納されます。|  
| &nbsp; | &nbsp; |
  
##  <a name="perms"></a> XML スキーマ コレクションに対する権限  
 次の操作を行うためには必要な権限を持っている必要があります。  
  
-   XML スキーマ コレクションを作成する、または読み込む  
  
-   XML スキーマ コレクションを変更する  
  
-   XML スキーマ コレクションを削除する  
  
-   XML スキーマ コレクションを、 **xml** 型の列、変数、およびパラメーターの型指定に使用したり、テーブルまたは列の制約で使用する  
  
 SQL Server セキュリティ モデルでは、すべてのオブジェクトで CONTROL 権限が許可されています。 この権限が許可されたユーザーは、オブジェクトに対する他のすべての権限を取得したことになります。 オブジェクトの所有者も、オブジェクトに対するすべての権限を持っています。  
  
 オブジェクトの所有者とオブジェクトの CONTROL 権限があるユーザーは、オブジェクトに対する任意の権限を許可することができます。 オブジェクトの所有者でなく、CONTROL 権限を持っていないユーザーでも、WITH GRANT OPTION が指定されていれば、オブジェクトに対する権限を許可できます。 たとえば、ユーザー A は、WITH GRANT OPTION により、XML スキーマ コレクション S に対して REFERENCES 権限を持っていますが、S に対する他の権限は持っていないとします。ユーザー A は、スキーマ コレクション S に対する REFERENCES 権限をユーザー B に許可することができます。  
  
 セキュリティ モデルでは、XML スキーマ コレクションを作成および使用する権限を許可したり、あるユーザーから他のユーザーに所有権を転送することが許可されています。 次のトピックでは、XML スキーマ コレクションの権限について説明しています。  
  
-   [XML スキーマ コレクションに対する権限の許可](../../relational-databases/xml/grant-permissions-on-an-xml-schema-collection.md)  
  
     XML スキーマ コレクションを作成する権限を許可する方法、および XML スキーマ コレクション オブジェクトに対する権限を許可する方法について説明します。  
  
-   [XML スキーマ コレクションに対する権限の取り消し](../../relational-databases/xml/revoke-permissions-on-an-xml-schema-collection.md)  
  
     権限の取り消しを使用して XML スキーマ コレクションの作成を回避する方法、および XML スキーマ コレクション オブジェクトに対する権限を取り消す方法について説明します。  
  
-   [XML スキーマ コレクションに対する権限の拒否](../../relational-databases/xml/deny-permissions-on-an-xml-schema-collection.md)  
  
     XML スキーマ コレクションを作成する権限を拒否する方法、および XML スキーマ コレクション オブジェクトに対する権限を拒否する方法について説明します。  
  
##  <a name="info"></a> XML スキーマおよびスキーマ コレクションに関する情報の取得  
 カタログ ビュー sys.xml_schema_collections には XML スキーマ コレクションが列挙されます。 XML スキーマ コレクション "sys" がシステムにより定義されています。 このコレクションには、すべてのユーザー定義 XML スキーマ コレクションで明示的に読み込むことなく使用できる定義済みの名前空間が含まれています。 一覧には xml、xs、xsi、fn、および xdt 用の名前空間が含まれています。 この他に、各 XML スキーマ コレクションのすべての名前空間を列挙する sys.xml_schema_namespaces、および各 XML スキーマのすべての XML スキーマ コンポーネントを列挙する sys.xml_components の 2 つのカタログ ビューがあります。  
  
 組み込み関数 **XML_SCHEMA_NAMESPACE**, *schemaName, XmlSchemacollectionName, namespace-uri* により、**xml** データ型のインスタンスが生成されます。 このインスタンスには、XML スキーマ コレクションに含まれるスキーマ (定義済みの XML スキーマを除く) の XML スキーマ フラグメントが含まれます。  
  
 XML スキーマ コレクションのコンテンツは、次のようにして列挙できます。  
  
-   XML スキーマ コレクションのカタログ ビューに対する Transact-SQL クエリを記述します。  
  
-   組み込み関数 **XML_SCHEMA_NAMESPACE()** を使用します。 この関数の出力には **xml** データ型のメソッドを適用できます。 ただし、基になる XML スキーマは変更できません。  
  
 このことを次の例で説明します。  
  
### <a name="example-enumerate-the-xml-namespaces-in-an-xml-schema-collection"></a>例:XML スキーマ コレクションでの XML 名前空間の列挙  
 XML スキーマ コレクション "myCollection" に次のクエリを実行します。  
  
```sql
SELECT XSN.name  
FROM    sys.xml_schema_collections XSC JOIN sys.xml_schema_namespaces XSN  
    ON (XSC.xml_collection_id = XSN.xml_collection_id)  
WHERE    XSC.name = 'myCollection'     
```  
  
### <a name="example-enumerate-the-contents-of-an-xml-schema-collection"></a>例:XML スキーマ コレクションのコンテンツの列挙  
 次のステートメントは、リレーショナル スキーマ dbo 内の XML スキーマ コレクション "myCollection" のコンテンツを列挙します。  
  
```sql
SELECT XML_SCHEMA_NAMESPACE (N'dbo', N'myCollection')  
```  
  
 **XML_SCHEMA_NAMESPACE()** の 3 番目の引数として対象になる名前空間を指定することで、コレクション内の個別の XML スキーマを **xml**データ型のインスタンスとして取得できます。 次の例を参照してください。  
  
### <a name="example-output-a-specified-schema-from-an-xml-schema-collection"></a>例:XML スキーマ コレクションからの指定したスキーマの出力  
 次のステートメントを実行すると、リレーショナル スキーマ dbo の XML スキーマ コレクション "myCollection" から、"_架空の_" ターゲット名前空間 https/\/www.microsoft.com/was-books で XML スキーマが出力されます。  
  
```sql
SELECT XML_SCHEMA_NAMESPACE (N'dbo', N'myCollection',   
N'https://www.microsoft.com/was-books')  
```  
  
### <a name="querying-xml-schemas"></a>XML スキーマへのクエリ  
 XML スキーマ コレクションに読み込んだ XML スキーマには、次のようにしてクエリを実行できます。  
  
-   XML スキーマ名前空間のカタログ ビューに対する Transact-SQL クエリを記述します。  
  
-   **xml** データ型の列を含むテーブルを作成し、その列に XML スキーマを保存して XML 型のシステムに読み込みます。 その後、 **xml** データ型のメソッドを使用して XML 列にクエリを実行できます。 また、この列に XML インデックスを作成することもできます。 ただしこの方法を使用する場合は、XML 列に保存されている XML スキーマと XML 型のシステムとの整合性をアプリケーションで保つ必要があります。 たとえば、XML 型のシステムから XML スキーマ名前空間を削除する場合、整合性を保つためにテーブルからもその名前空間を削除する必要があります。  
  
## <a name="see-also"></a>参照  
 [格納されている XML スキーマ コレクションの表示](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [含まれているスキーマをマージするためのスキーマの前処理](../../relational-databases/xml/preprocess-a-schema-to-merge-included-schemas.md)   
 [サーバー上の XML スキーマ コレクションの要件と制限](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
