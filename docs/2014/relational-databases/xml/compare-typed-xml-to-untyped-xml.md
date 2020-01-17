---
title: 型指定された XML と型指定されていない XML の比較 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xml data type [SQL Server], variables
- parameters [XML in SQL Server]
- facets [XML in SQL Server]
- xml data type [SQL Server], columns
- untyped XML
- xml data type [SQL Server], typed xml
- XML [SQL Server], typed
- variables [XML in SQL Server], creating
- xml data type [SQL Server], untyped xml
- columns [XML in SQL Server], creating
- typed XML
- document mode processing [SQL Server]
- XML [SQL Server], untyped
- xml data type [SQL Server], parameters
ms.assetid: 4bc50af9-2f7d-49df-bb01-854d080c72c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98cbaa59ea78e0033e9a534915987576347db604
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62637620"
---
# <a name="compare-typed-xml-to-untyped-xml"></a>型指定された XML と型指定されていない XML の比較
  `xml` 型の変数、パラメーター、および列を作成できます。 必要に応じて、XML スキーマのコレクションを、`xml` 型の変数、パラメーター、または列に関連付けることができます。 ここで、`xml`データ型のインスタンスと呼びます*型指定された*します。 それ以外の場合は、XML インスタンスを *型指定されていない*と呼びます。  
  
## <a name="well-formed-xml-and-the-xml-data-type"></a>適切な形式の XML と xml データ型  
 `xml` データ型には、ISO 標準の `xml` データ型が実装されています。 したがって、型指定されていない XML 列には、適切な形式の XML Version 1.0 ドキュメントを保存できるほか、テキスト ノードや任意の数の最上位要素が含まれた、いわゆる XML コンテンツ フラグメントを保存することもできます。 システムにより、データが適切な形式であることが確認されます。このとき XML スキーマに列をバインドする必要はなく、広義の適切な形式でないデータは拒否されます。 このことは、型指定されていない XML の変数やパラメーターにも該当します。  
  
## <a name="xml-schemas"></a>XML スキーマ  
 XML スキーマでは、次のものが提供されます。  
  
-   **検証制約。** 型指定された xml インスタンスが割り当てまたは変更されるときは、常に、SQL Server によってそのインスタンスが検証されます。  
  
-   **データ型情報。** スキーマでは、`xml` データ型のインスタンス内の属性と要素の型に関する情報が提供されます。 この型情報により、インスタンスに含まれている値には、型指定されていない `xml` より正確な演算のセマンティクスが提供されます。 たとえば、10 進数の算術演算は 10 進数値では実行できますが、文字列値では実行できません。 スキーマで型情報が指定されるので、型指定された XML ストレージは、型指定されていない XML よりも大幅に小さくすることができます。  
  
## <a name="choosing-typed-or-untyped-xml"></a>型指定された XML と型指定されていない XML の選択  
 次の条件に該当する場合は、型指定されていない `xml` データ型を使用してください。  
  
-   XML データに対応するスキーマがない場合。  
  
-   スキーマはあるが、サーバーでデータを検証しない場合。 サーバーにデータを保存する前にクライアント側で検証を行う場合、スキーマに従っていない無効な XML データを一時的に保存する場合、サーバーでサポートされていないスキーマ コンポーネントを使用する場合などが該当します。  
  
 型指定された使用`xml`次の状況でのデータ型。  
  
-   使用する XML データのスキーマがあり、その XML スキーマに従ってサーバーで XML データを検証する場合。  
  
-   型情報を基にしたストレージやクエリの最適化を行う場合。  
  
-   クエリをコンパイルするときに型情報を使用する場合。  
  
 型指定された XML の列、パラメーター、および変数には、XML ドキュメントまたは XML コンテンツを保存できます。 ただし、宣言のときに保存の対象がドキュメントなのかコンテンツなのかをフラグで指定する必要があります。 また、XML スキーマのコレクションを指定する必要があります。 各 XML インスタンスの最上位要素が 1 つだけの場合、DOCUMENT を指定します。 それ以外の場合は CONTENT を指定します。 クエリのコンパイルで型を確認するとき、クエリ コンパイラにより DOCUMENT フラグが使用され、シングルトンの最上位要素が推測されます。  
  
## <a name="creating-typed-xml"></a>型指定された XML の作成  
 型指定されたを作成する前に`xml`変数、パラメーター、または列を使用して、XML スキーマ コレクションを登録する必要がありますまず[CREATE XML SCHEMA COLLECTION &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-xml-schema-collection-transact-sql)します。 その後、XML スキーマ コレクションを `xml` データ型の変数、パラメーター、または列に関連付けることができます。  
  
 次の例では、XML スキーマ コレクション名を指定する際に、2 つの要素で構成された名前付け規則が使用されます。 最初の要素はスキーマ名で、2 番目の要素は XML スキーマ コレクション名です。  
  
### <a name="example-associating-a-schema-collection-with-an-xml-type-variable"></a>例: スキーマ コレクションと xml 型の変数の関連付け  
 次の例では、作成、`xml`型の変数と、それにスキーマ コレクションを関連付けます。 例で指定されているスキーマ コレクションは、 **AdventureWorks** のデータベースに既にインポートされています。  
  
```  
DECLARE @x xml (Production.ProductDescriptionSchemaCollection);   
```  
  
### <a name="example-specifying-a-schema-for-an-xml-type-column"></a>例: xml 型の列のスキーマの指定  
 次の例では、`xml` 型の列を持つテーブルを作成し、列のスキーマを指定します。  
  
```  
CREATE TABLE T1(  
 Col1 int,   
 Col2 xml (Production.ProductDescriptionSchemaCollection)) ;  
```  
  
### <a name="example-passing-an-xml-type-parameter-to-a-stored-procedure"></a>例: xml 型のパラメーターのストアド プロシージャへの受け渡し  
 次の例では、`xml` 型のパラメーターをストアド プロシージャに渡し、変数にスキーマを指定します。  
  
```  
CREATE PROCEDURE SampleProc   
  @ProdDescription xml (Production.ProductDescriptionSchemaCollection)   
AS   
...  
```  
  
 XML スキーマ コレクションに関して次の点に注意してください。  
  
-   XML スキーマ コレクションは、「 [CREATE XML SCHEMA COLLECTION (Transact-SQL)](/sql/t-sql/statements/create-xml-schema-collection-transact-sql)」を使用して登録されたデータベースでのみ使用できます。  
  
-   文字列から型指定された `xml` データ型にキャストする場合、指定したコレクションの XML スキーマの名前空間に基づいて、解析時に検証と型指定も行われます。  
  
-   型指定された `xml` データ型から、型指定されていない `xml` データ型にキャストできます。その逆も可能です。  
  
 SQL Server で XML を生成するその他の方法の詳細については、「 [XML データのインスタンスの作成](create-instances-of-xml-data.md)」を参照してください。 XML を生成後、それを `xml` データ型の変数に代入できます。また、その後の処理のために `xml` 型の列に格納することもできます。  
  
 データ型の階層では、`xml` データ型は `sql_variant` やユーザー定義型の下、組み込み型の上に表示されます。  
  
### <a name="example-specifying-facets-to-constrain-a-typed-xml-column"></a>例: 型指定された xml 列を制約するためのファセットの指定  
 型指定された `xml` 列では、格納されているインスタンスごとに、最上位要素を 1 つだけ許可するように、列を制約できます。 これを行うには、次の例で示すように、テーブルを作成するときに、オプションの `DOCUMENT` ファセットを指定します。  
  
```  
CREATE TABLE T(Col1 xml   
   (DOCUMENT Production.ProductDescriptionSchemaCollection));  
GO  
DROP TABLE T;  
GO  
```  
  
 既定では、型指定された `xml` 列に格納されるインスタンスは、XML ドキュメントではなく、XML コンテンツとして格納されます。 これにより、次のことが可能になります。  
  
-   ゼロ (0) 個以上の最上位要素  
  
-   最上位要素のテキスト ノード  
  
 また、次の例に示すように、 `CONTENT` ファセットを追加することにより、この動作を明示的に指定することもできます。  
  
```  
CREATE TABLE T(Col1 xml(CONTENT Production.ProductDescriptionSchemaCollection));  
GO -- Default  
```  
  
 `xml` 型 (型指定された xml) を定義する場所ならどこでも、オプションの DOCUMENT/CONTENT ファセットを指定することができます。 たとえば、型指定された `xml` 変数を作成するときに、次に示すように DOCUMENT/CONTENT ファセットを追加できます。  
  
```  
declare @x xml (DOCUMENT Production.ProductDescriptionSchemaCollection);  
```  
  
## <a name="document-type-definition-dtd"></a>DTD (文書型定義)  
 `xml` データ型の列、変数、およびパラメーターは XML スキーマを使用して型指定できますが、DTD では型指定できません。 ただしインライン DTD は型指定された XML にも型指定されていない XML にも使用できるので、それを使用して既定値を指定したり、エンティティ参照を展開した形に置き換えることができます。  
  
 サード パーティのツールを使用すると、DTD を XML スキーマ ドキュメントに変換できます。変換した XML スキーマはデータベースに読み込むことができます。  
  
## <a name="upgrading-typed-xml-from-sql-server-2005"></a>型指定された XML の SQL Server 2005 からのアップグレード  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] では、lax 検証のサポート、 **xs:date**、 **xs:time** 、および **xs:dateTime** のインスタンス データの処理の強化、list 型と union 型のサポートの追加など、XML スキーマのサポートがいくつかの点で拡張されています。 ほとんどの場合は、アップグレードの際にこれらの変更を意識する必要はありません。 ただし、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で、 **xs:date**型、 **xs:time**型、または **xs:dateTime** 型 (またはこれらのサブタイプ) の値を許可する XML スキーマ コレクションを使用していた場合は、その [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以降のバージョンにアタッチすると、以下のアップグレード手順が実行されます。  
  
1.  XML スキーマ コレクションに **xs:anyType**、 **xs:anySimpleType**、 **xs:date** (またはそのサブタイプ)、 **xs:time** (またはそのサブタイプ)、または **xs:dateTime** (またはそのサブタイプ) として型指定されている要素や属性、あるいはこれらの型を含む union 型または list 型の要素や属性が含まれる場合、その XML スキーマ コレクションで型指定されているすべての XML 列で、次の状況が発生します。  
  
    1.  列のすべての XML インデックスが無効になります。  
  
    2.  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] の値はすべて Z タイムゾーンで正規化されているため、引き続き Z タイムゾーンで表されます。  
  
    3.  1 年 1 月 1 日より小さい **xs:date** 値や **xs:dateTime** 値があると、インデックスが再構築されるときや、その値を含む XML データ型に対して XQuery ステートメントや XML-DML ステートメントが実行されるときに、実行時エラーが発生します。  
  
2.  **xs:date** ファセット、 **xs:dateTime** ファセット、または XML スキーマ コレクションの既定値に負の年がある場合は、 **xs:date** 基本型または **xs:dateTime** 基本型で許可されている最も小さな値 (たとえば、 **xs:dateTime**の場合は 0001-01-01T00:00:00.0000000Z) に自動的に更新されます。  
  
 負の年が含まれていても、単純な SQL SELECT ステートメントを使用して XML データ型全体を取得することはできます。 負の年は、新たにサポートされた範囲内の年に置き換えるか、要素や属性の型を **xs:string**に変更することをお勧めします。  
  
## <a name="see-also"></a>関連項目  
 [XML データのインスタンスの作成](create-instances-of-xml-data.md)   
 [xml データ型のメソッド](/sql/t-sql/xml/xml-data-type-methods)   
 [XML データ変更言語 &#40;XML DML&#41;](/sql/t-sql/xml/xml-data-modification-language-xml-dml)   
 [XML Data &#40;SQL Server&#41;](xml-data-sql-server.md)  
  
  
