---
title: XML インデックス (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- removing indexes
- deleting indexes
- secondary indexes [XML in SQL Server]
- xml data type [SQL Server], indexes
- dropping indexes
- PATH index
- DROP_EXISTING clause
- XML [SQL Server], indexes
- primary indexes [XML in SQL Server]
- indexes [SQL Server], XML
- XML indexes [SQL Server], secondary
- BLOBs, XML indexes
- disabling indexes
- XML indexes [SQL Server], modifying
- XML indexes [SQL Server]
- XML indexes [SQL Server], primary
- modifying indexes
- XML indexes [SQL Server], dropping
- VALUE index
- XML indexes [SQL Server], xml data type
- PROPERTY index
- XML indexes [SQL Server], creating
ms.assetid: f5c9209d-b3f3-4543-b30b-01365a5e7333
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7004f2cae60ab69c6c4bf94ceee47d270579570b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62631368"
---
# <a name="xml-indexes-sql-server"></a>XML インデックス (SQL Server)
  `xml` データ型の列には XML インデックスを作成できます。 列に保存されている XML インスタンスのすべてのタグ、値、およびパスにインデックスが設定されるので、クエリのパフォーマンスが向上します。 次のような場合、XML インデックスの効果が得られる可能性があります。  
  
-   ワークロードで XML 列へのクエリが頻繁に行われる場合。 データ変更時の XML インデックスのメンテナンス コストを考慮する必要があります。  
  
-   XML 値が比較的大きいのに対し、取得する部分が比較的小さい場合。 インデックスを作成すると、実行時にデータ全体が解析されることを回避し、クエリ処理を効率化するためのインデックス参照を利用できます。  
  
 XML のインデックスは、次のカテゴリに分類されます。  
  
-   プライマリ XML インデックス  
  
-   セカンダリ XML インデックス  
  
 `xml` 型の列の最初のインデックスは、プライマリ XML インデックスである必要があります。 プライマリ XML インデックスを使用している場合は、PATH、VALUE、および PROPERTY という種類のセカンダリ XML インデックスがサポートされます。 クエリの種類によって異なりますが、これらのセカンダリ XML インデックスを使用することで、クエリのパフォーマンス向上に役立つ場合があります。  
  
> [!NOTE]  
>  XML インデックスを作成したり変更したりするには、`xml` データ型を操作できるようにデータベース オプションが正しく設定されている必要があります。 詳細については、「 [XML 列でのフルテキスト検索の使用](use-full-text-search-with-xml-columns.md)」を参照してください。  
  
 XML インスタンスは、BLOB (バイナリ ラージ オブジェクト) として `xml` 型の列に格納されます。 これらの XML インスタンスは大きくなる可能性がありますが、`xml` データ型インスタンスをバイナリ表記したものを最大 2 GB まで格納できます。 インデックスを設定しない場合、クエリを評価するためにこのようなバイナリ ラージ オブジェクトが実行時に細分化されます。 この細分化には時間がかかる場合があります。 たとえば、次のクエリについて考えてみます。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.query('  
  /PD:ProductDescription/PD:Summary  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist ('/PD:ProductDescription/@ProductModelID[.="19"]') = 1  
```  
  
 `WHERE` 句の条件を満たす XML インスタンスを選択するために、テーブル `Production.ProductModel` の各行内の XML BLOB (バイナリ ラージ オブジェクト) が実行時に細分化されます。 次に、 `(/PD:ProductDescription/@ProductModelID[.="19"]`メソッドの式 `exist()` ) が評価されます。 このような実行時の細分化は、列に格納されたインスタンスのサイズや数によってはコストが高くなる場合があります。  
  
 使用しているアプリケーション環境で、XML BLOB (バイナリ ラージ オブジェクト) に対するクエリを頻繁に実行する場合は、`xml` 型の列のインデックスを設定することが役に立ちます。 ただし、データの変更時には、インデックスのメンテナンスに関するコストがかかります。  
  
## <a name="primary-xml-index"></a>プライマリ XML インデックス  
 プライマリ XML インデックスにより、XML 列に保存されている XML インスタンスのすべてのタグ、値、およびパスにインデックスが設定されます。 プライマリ XML インデックスを作成するには、XML 列があるテーブルの主キーにクラスター化インデックスが作成されている必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] この主キーを使用して、プライマリ XML インデックスの行を、XML 列を含むテーブルの行に関連付けます。  
  
 プライマリ XML インデックスは、`xml` データ型列内の XML BLOB の細分化された永続化表現です。 インデックスでは、列内の XML BLOB (バイナリ ラージ オブジェクト) ごとに、数行のデータ行が作成されます。 インデックス内の行数は、XML バイナリ ラージ オブジェクトのノード数とほぼ等しくなります。 クエリで完全な XML インスタンスを取得する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって XML 列からインスタンスが返されます。 XML インスタンス内でクエリを実行するときはプライマリ XML インデックスが使用され、インデックス自体によってスカラー値または XML サブツリーが返すことができます。  
  
 各行には、次のノード情報が格納されます。  
  
-   要素名、属性名などのタグ名。  
  
-   ノード値。  
  
-   要素ノード、属性ノード、テキスト ノードなどのノードの型。  
  
-   ドキュメント内の表示順情報。内部ノード識別子によって表現されます。  
  
-   各ノードから XML ツリーのルートまでのパス。 クエリ内のパス式ではこの列を検索します。  
  
-   ベース テーブルの主キー。 ベース テーブルとの逆結合のため、ベース テーブルの主キーがプライマリ XML インデックスにコピーされます。ベース テーブルの主キーの最大列数は 15 です。  
  
 このノード情報は、指定されたクエリに対して XML の結果を評価し構築するために使用されます。 最適化のために、タグ名とノード型の情報は整数値でエンコードされるので、パス列でも同じエンコードを使用します。 また、パスのサフィックスが既知の場合にのみパスを照合できるように、パスは逆の順序で格納されます。 例 :  
  
-   `//ContactRecord/PhoneNumber` 最後の 2 つのロケーション ステップだけが既知です。  
  
 スイッチまたは  
  
-   `/Book/*/Title` 式の中間でワイルドカード文字 (`*`) が指定されています。  
  
 [xml データ型のメソッド](/sql/t-sql/xml/xml-data-type-methods) に関係するクエリの場合、クエリ プロセッサでプライマリ XML インデックスが使用され、スカラー値またはプライマリ インデックス自体の XML サブツリーのどちらかが返されます。 (このプライマリ XML インデックスには XML インスタンスの再構築に必要なすべての情報が格納されています)。  
  
 たとえば、次のクエリに格納されている概要情報を返します、`CatalogDescription``xml`型の列、`ProductModel`テーブル。 このクエリでは、カタログの説明に <`Features`> の説明も含まれている製品モデルに限り <`Summary`> 情報が返されます。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")SELECT CatalogDescription.query('  /PD:ProductDescription/PD:Summary') as ResultFROM Production.ProductModelWHERE CatalogDescription.exist ('/PD:ProductDescription/PD:Features') = 1  
```  
  
 プライマリ XML インデックスでは、ベース テーブルの各 XML バイナリ ラージ オブジェクト インスタンスを細分化するのではなく、各 XML バイナリ ラージ オブジェクトに対応するインデックスの行が `exist()` メソッドで指定された式に対して順番に検索されます。 インデックスのパス列にそのパスが見つかると、プライマリ XML インデックスから <`Summary`> 要素とそのサブツリーが共に取得され、`query()` メソッドの結果として XML バイナリ ラージ オブジェクトに変換されます。  
  
 XML インスタンス全体を取得するときには、プライマリ XML インデックスが使用されないことに注意してください。 たとえば、次のクエリでは、特定の製品モデルの製造手順を説明する XML インスタンス全体をテーブルから取得します。  
  
```  
USE AdventureWorks2012;SELECT InstructionsFROM Production.ProductModel WHERE ProductModelID=7;  
```  
  
## <a name="secondary-xml-indexes"></a>セカンダリ XML インデックス  
 検索のパフォーマンスを向上するために、セカンダリ XML インデックスを作成できます。 セカンダリ XML インデックスを作成する前に、プライマリ XML インデックスが存在している必要があります。 セカンダリ XML インデックスの種類を次に示します。  
  
-   PATH セカンダリ XML インデックス  
  
-   VALUE セカンダリ XML インデックス  
  
-   PROPERTY セカンダリ XML インデックス  
  
 次に、セカンダリ インデックスを 1 種類以上作成する場合のガイドラインを示します。  
  
-   ワークロードで XML 列にパス式が多用されている場合、PATH セカンダリ XML インデックスを作成するとワークロードを高速に処理できることがあります。 一般的な例では、Transact-SQL の WHERE 句で XML 列に対し **exist()** メソッドが使用される場合があります。  
  
-   パス式を使用して個々の XML インスタンスから複数の値を取得する場合、PROPERTY インデックスで各 XML インスタンス内のパスをクラスター化すると効果が得られる可能性があります。 このシナリオは、主キーの値がわかっていてオブジェクトのプロパティをフェッチするプロパティ バッグ シナリオで主に発生します。  
  
-   XML インスタンスの値を、要素名または属性名がわからないままクエリで取得する場合、VALUE インデックスを作成できます。 //author[last-name="Howard"]\(\<author> 要素が階層のどのレベルにあってもよい) のように、descendant 軸を参照する場合がその典型です。 また、ワイルドカードを使用するクエリ (いずれかの属性に値 "novel" が指定された \<book> 要素をクエリで検索する /book [@* = "novel"] など) もこれに該当します。  
  
### <a name="path-secondary-xml-index"></a>PATH セカンダリ XML インデックス  
 クエリで `xml` 型列のパス式をよく指定している場合、PATH セカンダリ インデックスにより検索速度を向上できる場合があります。 このトピックで既に説明したように、WHERE 句に **exist()** メソッドを指定するクエリを使用する場合には、プライマリ インデックスが役に立ちます。 PATH セカンダリ インデックスを追加することでも、そのようなクエリの検索パフォーマンスが向上する場合があります。  
  
 プライマリ XML インデックスにより、XML バイナリ ラージ オブジェクトを実行時に細分化せずに済むようになりますが、パス式に基づくクエリのパフォーマンスが最適にならない場合があります。 XML バイナリ ラージ オブジェクトに対応するプライマリ XML インデックスのすべての行は大きな XML インスタンスに対して順番に検索されるので、検索速度が低下する場合があります。 このような場合、プライマリ インデックスのパス値とノード値にセカンダリ インデックスを構築すると、インデックス検索の速度を大幅に向上できます。 PATH セカンダリ インデックスではパス値とノード値がキー列になり、パスの検索時により効率的にシークできるようになります。 クエリ オプティマイザーでは、次に示すような式に PATH インデックスを使用できます。  
  
-   `/root/Location` パスだけを指定しています。  
  
 スイッチまたは  
  
-   `/root/Location/@LocationID[.="10"]` パスとノード値の両方を指定しています。  
  
 次のクエリでは、PATH インデックスが役立つケースを示します。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.query('  
  /PD:ProductDescription/PD:Summary  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist ('/PD:ProductDescription/@ProductModelID[.="19"]') = 1  
```  
  
 このクエリでは、 `/PD:ProductDescription/@ProductModelID` メソッド内のパス式 `"19"` と値 `exist()` が PATH インデックスのキー フィールドに対応しています。 これにより、PATH インデックス内を直接シークできるようになり、プライマリ XML インデックスでパス値を順番に検索するよりも検索のパフォーマンスが向上します。  
  
### <a name="value-secondary-xml-index"></a>VALUE セカンダリ XML インデックス  
 `/Root/ProductDescription/@*[. = "Mountain Bike"]` や `//ProductDescription[@Name = "Mountain Bike"]`などのように、クエリが値に基づいており、パスが完全に指定されていない場合や、パスにワイルドカードが含まれている場合は、プライマリ XML インデックスのノード値にセカンダリ XML インデックスを構築すると、より迅速に結果を得られる場合があります。  
  
 VALUE インデックスのキー列は、プライマリ XML インデックスの列 (ノード値とパス) です。 値を格納している要素名または属性名がわからない状態で XML インスタンスの値に対するクエリを実行する作業がワークロードに含まれている場合、VALUE インデックスが役立つことがあります。 たとえば、次の式は VALUE インデックスを使用すると効率的になります。  
  
-   `//author[LastName="someName"]`: <`LastName`> 要素の値はわかっていますが、親である <`author`> はどこにでも存在し得ます。  
  
-   `/book[@* = "someValue"]`: `"someValue"` という値の属性を持つ <`book`> 要素を検索します。  
  
 次のクエリは、 `ContactID` テーブルから `Contact` を返します。 `WHERE`句内の値を検索するフィルターを指定する、`AdditionalContactInfo``xml`型の列。 連絡先 ID は、対応する追加の連絡先情報の XML バイナリ ラージ オブジェクトに特定の電話番号が含まれている場合にのみ返されます。 <`telephoneNumber`> 要素は XML 内のどこにでも存在し得るので、パス式で descendent-or-self 軸を指定しています。  
  
```  
WITH XMLNAMESPACES (  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS CI,  
  'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.exist('//ACT:telephoneNumber/ACT:number[.="111-111-1111"]') = 1  
```  
  
 この場合、検索する <`number`> の値はわかっていますが、この値は <`telephoneNumber`> 要素の子として XML インスタンス内のどこにでも存在できます。 このようなクエリでは特定の値に基づいてインデックス参照を行うと、効率的になる場合があります。  
  
### <a name="property-secondary-index"></a>PROPERTY セカンダリ XML インデックス  
 個々の XML インスタンスから 1 つ以上の値を取得するクエリでは、PROPERTY インデックスを使用するとメリットが得られる場合があります。 このシナリオは、オブジェクトのプロパティを使用して取得したときに発生します。、 **value()** のメソッド、`xml`型とオブジェクトの主キーの値をいいます。  
  
 PROPERTY インデックスは、プライマリ XML インデックスの列 (PK、パス、およびノード値) について構築されます。PK はベース テーブルの主キーです。  
  
 たとえば、次のクエリでは、製品モデル `19`の `ProductModelID` 属性と `ProductModelName` 属性の値を `value()` メソッドを使用して取得しています。 プライマリ XML インデックスや他のセカンダリ XML インデックスではなく PROPERTY インデックスを使用すると、クエリをより迅速に実行できる場合があります。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.value('(/PD:ProductDescription/@ProductModelID)[1]', 'int') as ModelID,  
       CatalogDescription.value('(/PD:ProductDescription/@ProductModelName)[1]', 'varchar(30)') as ModelName          
FROM Production.ProductModel     
WHERE ProductModelID = 19  
```  
  
 このトピックの後半で説明する違いを除けばのインデックス、XML の作成、`xml`型の列はインデックスを作成する以外に似ています`xml`型の列。 XML インデックスの作成と管理には、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] DDL ステートメントを使用できます。  
  
-   [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
-   [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)  
  
-   [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
## <a name="getting-information-about-xml-indexes"></a>XML インデックスに関する情報の取得  
 XML インデックス エントリは、カタログ ビュー sys.indexes にインデックスの "type" 3 として表示されます。 name 列には XML インデックスの名前が格納されています。  
  
 XML インデックスはカタログ ビュー sys.xml_indexes にも記録されます。 このビューには、sys.indexes のすべての列および XML インデックスに有用な特定の列が含まれています。 列 secondary_type に値 NULL がある場合はプライマリ XML インデックスであることを示します。セカンダリ XML インデックスの値 "P"、"R"、および "V" はそれぞれ PATH、PROPERTY、VALUE を示します。  
  
 XML インデックスによる領域の使用状況は、テーブル値関数 [sys.dm_db_index_physical_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql)でわかります。 この関数は、すべてのインデックスの種類について、占有しているディスク ページの数、バイト単位の平均行サイズ、レコードの数などの情報を示します。 また、この情報には XML インデックスも含まれています。 この情報はデータベース パーティションごとに取得できます。 どの XML インデックスにも同一の、ベース テーブルのパーティション構成とパーティション関数が使用されます。  
  
## <a name="see-also"></a>関連項目  
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql)   
 [XML Data &#40;SQL Server&#41;](../xml/xml-data-sql-server.md)  
  
  
