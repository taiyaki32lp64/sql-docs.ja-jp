---
title: XML インデックスの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- indexes [XML in SQL Server]
- XML indexes [SQL Server], creating
ms.assetid: 6ecac598-355d-4408-baf7-1b2e8d4cf7c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7da89810a92c14f5b59ebcd546c4fb4cfa256f02
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62637762"
---
# <a name="create-xml-indexes"></a>XML インデックスの作成
  このトピックでは、プライマリ XML インデックスとセカンダリ XML インデックスの作成方法について説明します。  
  
## <a name="creating-a-primary-xml-index"></a>プライマリ XML インデックスの作成  
 プライマリ XML インデックスを作成するには、[CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] DDL ステートメントを使用します。 XML インデックスでは、XML 以外のインデックスで使用できるオプションの一部しかサポートされません。  
  
 XML インデックスの作成時には、次の事項に注意します。  
  
-   プライマリ XML インデックスを作成するには、インデックスが作成される XML 列を含んだベース テーブルと呼ばれるテーブルの主キーに、クラスター化インデックスが作成されている必要があります。 これにより、ベース テーブルをパーティション分割した場合に、同じパーティション構成とパーティション関数を使用してプライマリ XML インデックスがパーティション分割されるようになります。  
  
-   XML インデックスが存在する場合は、テーブルのクラスター化主キーを変更できません。 主キーを変更する前に、テーブルのすべての XML インデックスを削除する必要があります。  
  
-   プライマリ XML インデックスは、1 つの `xml` 型の列に作成できます。 キー列の XML 型の列には他の型のインデックスを作成できません。 ただし、XML 以外のインデックスに `xml` 型の列を含めることはできます。 テーブル内の各 `xml` 型列には、それぞれ独自のプライマリ XML インデックスを作成できます。 ただし、各 `xml` 型列に作成できるプライマリ XML インデックスは 1 つだけです。  
  
-   XML インデックスは、XML 以外のインデックスと同じ名前空間に存在します。 したがって、同じテーブルでは、XML インデックスと XML 以外のインデックスを同じ名前で作成することはできません。  
  
-   IGNORE_DUP_KEY オプションと ONLINE オプションは、XML インデックスでは常に OFF に設定されます。 これらのオプションを値 OFF で指定できます。  
  
-   ユーザー テーブルのファイル グループ情報またはパーティション分割情報が XML インデックスに適用されます。 ユーザーは、これらの情報を XML インデックスで別々に指定することはできません。  
  
-   DROP_EXISTING インデックス オプションを使用すると、プライマリ XML インデックスを削除して新しい XML インデックスを作成することや、セカンダリ XML インデックスを削除して新しいセカンダリ XML インデックスを作成することができます。 ただし、このインデックス オプションを使用して、セカンダリ XML インデックスを削除して新しいプライマリ XML インデックスを作成することや、プライマリ XML インデックスを削除して新しいセカンダリ XML インデックスを作成することはできません。  
  
-   プライマリ XML インデックスの名前にはビュー名と同じ制限事項が適用されます。  
  
 XML インデックスを作成することはできません、`xml`で、ビューの列を入力、**テーブル**を持つ変数の値を持つ`xml`種類の列、または`xml`変数を入力します。  
  
-   ALTER TABLE ALTER COLUMN オプションを使用して、`xml` 型の列を型指定されていない XML から型指定された XML に変更する場合、またはその逆の変更を行う場合は、その列に XML インデックスが存在してはいけません。 XML インデックスが存在する場合は、列の型を変更する前にその XML インデックスを削除する必要があります。  
  
-   XML インデックスを作成する場合は、ARITHABORT オプションが ON に設定されている必要があります。 XML データ型メソッドを使用して XML 列内の値のクエリ、挿入、削除、または更新を行うには、同じオプションがその接続に設定される必要があります。 異なるオプションが設定された場合、XML データ型のメソッドは失敗します。  
  
    > [!NOTE]  
    >  XML インデックスについての情報は、カタログ ビューで参照できます。 ただし、 **sp_helpindex** はサポートされません。 このトピックの後半に示す例では、カタログ ビューにクエリを実行して XML インデックスの情報を参照する方法を説明しています。  
  
 **以降のバージョンでは、プライマリ XML インデックスを作成または再作成する XML データ型の列に、XML スキーマ型** xs:date **または** xs:dateTime [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (またはこれらのサブタイプ) で 1 未満の年の値が含まれていると、インデックスの作成が失敗します。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]ではこれらの値が許可されていたため、この問題は、生成されたデータベースでインデックスを作成する際に発生する可能性があります。 詳細については、「 [型指定された XML と型指定されていない XML の比較](../xml/compare-typed-xml-to-untyped-xml.md)」を参照してください。  
  
### <a name="example-creating-a-primary-xml-index"></a>例:プライマリ XML インデックスの作成  
 ここからはほとんどの例で、型指定されていない XML 列を含んだテーブル T (pk INT PRIMARY KEY, xCol XML) を使用します。 XML 列は、型指定された XML に簡単に拡張できます。 説明を簡単にするため、次に示す XML データ インスタンスに対するクエリについて説明します。  
  
```  
<book genre="security" publicationdate="2002" ISBN="0-7356-1588-2">  
   <title>Writing Secure Code</title>  
   <author>  
      <first-name>Michael</first-name>  
      <last-name>Howard</last-name>  
   </author>  
   <author>  
      <first-name>David</first-name>  
      <last-name>LeBlanc</last-name>  
   </author>  
   <price>39.99</price>  
</book>  
```  
  
 次のステートメントを実行すると、テーブル T の XML 列 xCol に idx_xCol という XML インデックスが作成されます。  
  
```  
CREATE PRIMARY XML INDEX idx_xCol on T (xCol)  
```  
  
## <a name="creating-a-secondary-xml-index"></a>セカンダリ XML インデックスの作成  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] DDL ステートメントを使用して、セカンダリ XML インデックスを作成したり、必要なセカンダリ XML インデックスの種類を指定したりします。  
  
 セカンダリ XML インデックスの作成時には、次の事項に注意します。  
  
-   IGNORE_DUP_KEY と ONLINE を除き、非クラスター化インデックスに適用されるすべてのオプションをセカンダリ XML インデックスで使用できます。 例外の 2 つのオプションは、セカンダリ XML インデックスでは常に OFF に設定する必要があります。  
  
-   セカンダリ XML インデックスは、プライマリ XML インデックスと同様にパーティション分割されます。  
  
-   DROP_EXISTING を使用すると、ユーザー テーブルのセカンダリ XML インデックスを削除し、そのユーザー テーブルに別のセカンダリ XML インデックスを作成できます。  
  
 **sys.xml_indexes** カタログ ビューにクエリを実行して XML インデックス情報を取得できます。 **sys.xml_indexes** カタログ ビューの **secondary_type_desc** 列には、セカンダリ インデックスの種類が示されます。  
  
```  
SELECT  *   
FROM    sys.xml_indexes;  
```  
  
 **secondary_type_desc** 列に返される値は、NULL、PATH、VALUE、または PROPERTY です。 プライマリ XML インデックスの場合、返される値は NULL です。  
  
### <a name="example-creating-secondary-xml-indexes"></a>例: セカンダリ XML インデックスの作成  
 次の例では、セカンダリ XML インデックスの作成方法を示します。 また、作成した XML インデックスに関する情報も示します。  
  
```  
CREATE TABLE T (Col1 INT PRIMARY KEY, XmlCol XML);  
GO  
-- Create primary index.  
CREATE PRIMARY XML INDEX PIdx_T_XmlCol   
ON T(XmlCol);  
GO  
-- Create secondary indexes (PATH, VALUE, PROPERTY).  
CREATE XML INDEX PIdx_T_XmlCol_PATH ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR PATH;  
GO  
CREATE XML INDEX PIdx_T_XmlCol_VALUE ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR VALUE;  
GO  
CREATE XML INDEX PIdx_T_XmlCol_PROPERTY ON T(XmlCol)  
USING XML INDEX PIdx_T_XmlCol  
FOR PROPERTY;  
GO  
```  
  
 `sys.xml_indexes` に対するクエリを実行して XML インデックス情報を取得できます。 `secondary_type_desc` 列からは、セカンダリ インデックスの種類が提供されます。  
  
```  
SELECT  *   
FROM    sys.xml_indexes;  
```  
  
 次のように、カタログ ビューに対するクエリを実行してインデックス情報を取得することもできます。  
  
```  
SELECT *  
FROM sys.xml_indexes  
WHERE object_id = object_id('T');  
```  
  
 次のように、サンプル データを追加した後で、XML インデックス情報を確認できます。  
  
```  
INSERT INTO T VALUES (1,  
'<doc id="123">  
<sections>  
<section num="2">  
<heading>Background</heading>  
</section>  
<section num="3">  
<heading>Sort</heading>  
</section>  
<section num="4">  
<heading>Search</heading>  
</section>  
</sections>  
</doc>');  
GO  
-- Check XML index information.  
SELECT *  
FROM   sys.dm_db_index_physical_stats (db_id(), object_id('T'), NULL, NULL, 'DETAILED');  
GO  
-- Space usage of primary XML index  
DECLARE @index_id int;  
SELECT  @index_id = i.index_id  
FROM    sys.xml_indexes i   
WHERE   i.name = 'PIdx_T_XmlCol' and object_name(i.object_id) = 'T';  
  
SELECT *  
FROM sys.dm_db_index_physical_stats (db_id(), object_id('T') , @index_id, DEFAULT, 'DETAILED');  
go  
--- Space usage of secondary XML index (for example PATH secondary index)  PIdx_T_XmlCol_PATH  
DECLARE @index_id int;  
SELECT  @index_id = i.index_id   
FROM    sys.xml_indexes i   
WHERE  i.name = 'PIdx_T_XmlCol_PATH' and object_name(i.object_id) = 'T';  
  
SELECT *  
FROM sys.dm_db_index_physical_stats (db_id(), object_id('T') , @index_id, DEFAULT, 'DETAILED');  
go  
  
-- Space usage of all secondary XML indexes for a particular table  
SELECT i.name, object_name(i.object_id), stats.*   
FROM   sys.dm_db_index_physical_stats (db_id(), object_id('T'), NULL, DEFAULT, 'DETAILED') stats  
JOIN sys.xml_indexes i ON (stats.object_id = i.object_id and stats.index_id = i.index_id)  
WHERE secondary_type is not null;  
-- Drop secondary indexes.  
DROP INDEX PIdx_T_XmlCol_PATH ON T;  
GO  
DROP INDEX PIdx_T_XmlCol_VALUE ON T;  
GO  
DROP INDEX PIdx_T_XmlCol_PROPERTY ON T;  
GO  
-- Drop primary index.  
DROP INDEX PIdx_T_XmlCol ON T;  
-- Drop table T.  
DROP TABLE T;  
Go  
```  
  
## <a name="see-also"></a>参照  
 [XML インデックス &#40;SQL Server&#41;](xml-indexes-sql-server.md)   
 [XML データ &#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  
