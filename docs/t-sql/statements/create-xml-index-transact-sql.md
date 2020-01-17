---
title: CREATE XML INDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- XML_TSQL
- CREATE_XML_INDEX_TSQL
- XML INDEX
- CREATE_XML_TSQL
- XML
- CREATE XML
- CREATE XML INDEX
- XML_INDEX_TSQL
- FOR_XML_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE XML INDEX statement
- CREATE INDEX statement
- index creation [SQL Server], XML indexes
- XML indexes [SQL Server], creating
ms.assetid: c510cfbc-68be-4736-b3cc-dc5b7aa51f14
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93571a71662f8d24044b77c2c65dec01778096d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948064"
---
# <a name="create-xml-index-transact-sql"></a>CREATE XML INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定したテーブルに XML インデックスを作成します。 インデックスはテーブル内にデータがなくても作成できます。 データベース名を修飾して指定することにより、他のデータベース内のテーブルに XML インデックスを作成することもできます。  
  
> [!NOTE]  
>  リレーショナル インデックスを作成するには、「[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)」を参照してください。 空間インデックスを作成する方法については、「[CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
Create XML Index   
CREATE [ PRIMARY ] XML INDEX index_name   
    ON <object> ( xml_column_name )  
    [ USING XML INDEX xml_index_name   
        [ FOR { VALUE | PATH | PROPERTY } ] ]  
    [ WITH ( <xml_index_option> [ ,...n ] ) ]  
[ ; ]  
  
<object> ::=  
{ database_name.schema_name.table_name | schema_name.table_name | table_name }
  
<xml_index_option> ::=  
{   
    PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
}  
  
```  
  
## <a name="arguments"></a>引数  
 [PRIMARY] XML  
 指定した **xml** 列に、XML インデックスを作成します。 PRIMARY を指定した場合、クラスター化インデックスは、ユーザー テーブルのクラスター化キーと XML ノード識別子から構成されるクラスター化キーで作成されます。 各テーブルには 249 個までの XML インデックスを作成できます。 XML インデックスを作成するときには、次のことに注意してください。  
  
-   クラスター化インデックスは、ユーザー テーブルの主キー上に存在する必要がある。  
  
-   ユーザー テーブルのクラスター化キーは 15 列に制限されている。  
  
-   テーブル内の各 **xml** 列には、1 つのプライマリ XML インデックスと、複数のセカンダリ XML インデックスを作成できます。  
  
-   列にセカンダリ XML インデックスを作成するには、**xml** 列にプライマリ XML インデックスが存在している必要があります。  
  
-   1 つの XML インデックスは単一の **xml** 列でのみ作成できます。 XML インデックスは **xml** 以外の列には作成できません。またリレーショナル インデックスは **xml** 列には作成できません。  
  
-   ビュー内の **xml** 列、**xml** 列を使用したテーブル値変数、および **xml** 型の変数には、プライマリまたはセカンダリのいずれの XML インデックスも作成できません。  
  
-   **xml** 計算列にプライマリ XML インデックスを作成することはできません。  
  
-   SET オプション設定は、インデックス付きビューおよび計算列インデックスに必要な設定と同じにする必要がある。 特に、XML インデックスを作成し、**xml** 列に値を挿入、削除、更新する場合は、オプション ARITHABORT が ON に設定されている必要があります。  
  
 詳細については、「[XML インデックス &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)」をご覧ください。  
  
 *index_name*  
 インデックスの名前です。 インデックス名は、テーブル内では一意である必要がありますが、データベース内で一意である必要はありません。 インデックス名は、[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従っている必要があります。  
  
 プライマリ XML インデックス名は **#** 、 **##** 、 **@** 、または **@@** で始めることはできません。  
  
 *xml_column_name*  
 インデックスの基準となる **xml** 列を指定します。 単一の XML インデックス定義には、1 つの **xml** 列しか指定できませんが、1 つの **xml** 列には複数のセカンダリ XML インデックスを作成できます。  
  
 USING XML INDEX *xml_index_name*  
 セカンダリ XML インデックスの作成でプライマリ XML インデックスを使用します。  
  
 FOR { VALUE | PATH | PROPERTY }  
 セカンダリ XML インデックスの種類を指定します。  
  
 Value  
 キー列がプライマリ XML インデックス (ノード値とパス) となっている列に、セカンダリ XML インデックスを作成します。  
  
 PATH  
 プライマリ XML インデックスのパス値とノード値に基づく列に、セカンダリ XML インデックスを作成します。 PATH セカンダリ インデックスではパス値とノード値がキー列になり、パスの検索時に効率的にシークできるようになります。  
  
 PROPERTY  
 PK がベース テーブルの主キーとなっているプライマリ XML インデックスの列 (PK、パスおよびノード値) に、セカンダリ XML インデックスを作成します。  
  
 **\<object>::=**  
  
 インデックスを作成するオブジェクトを、完全修飾または完全修飾ではない形式で指定します。  
  
 *database_name*  
 データベースの名前です。  
  
 *schema_name*  
 テーブルが所属するスキーマの名前を指定します。  
  
 *table_name*  
 インデックスを作成するテーブルの名前を指定します。  
  
 **\<xml_index_option> ::=** 
  
 インデックスを作成するときに使用するオプションを指定します。  
  
 PAD_INDEX **=** { ON | **OFF** }  
 インデックスの埋め込みを指定します。 既定値は OFF です。  
  
 ON  
 *fillfactor* で指定される空き領域のパーセンテージが、インデックスの中間レベルのページに適用されます。  
  
 OFF または *fillfactor* の指定なし  
 中間レベルのページはほぼ全容量が使用されます。ただし、中間ページにあるキーのセットを考慮して、インデックスに割り当てることのできる、少なくとも 1 行の最大サイズが収まる分の領域は残されます。  
  
 PAD_INDEX では FILLFACTOR で指定されるパーセンテージが使用されるので、PAD_INDEX オプションは、FILLFACTOR が指定されている場合にのみ有効です。 FILLFACTOR で指定されるパーセンテージで 1 行分のデータを格納できない場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)] では内部的に、最小サイズを格納できるパーセンテージにオーバーライドします。 中間インデックス ページの行数は、*fillfactor* の値がどれだけ小さくなっても 2 未満にはなりません。  
  
 FILLFACTOR **=** _fillfactor_  
 インデックスの作成時または再構築時に、[!INCLUDE[ssDE](../../includes/ssde-md.md)] が各インデックス ページのリーフ レベルをどの程度まで埋めるかを、パーセント値で指定します。 *fillfactor* 値には、1 ～ 100 の整数値を指定してください。 既定値は 0 です。 *fillfactor* が 100 または 0 の場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)] では全容量を使用するリーフ ページでインデックスが作成されます。  
  
> [!NOTE]  
>  FILL FACTOR 値 0 と 100 の機能は、まったく同じです。  
  
 FILLFACTOR 設定は、インデックスが作成または再構築されるときのみ適用されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では、ページ内で指定されたパーセント分の空き領域は動的に保持されません。 FILL FACTOR 設定を表示するには、[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) カタログ ビューを使用します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssDE](../../includes/ssde-md.md)]では、クラスター化インデックスの作成時にデータが再分配されるため、100 未満の FILLFACTOR 値を使ってクラスター化インデックスを作成すると、データ用のストレージ領域のサイズに影響が生じます。  
  
 詳細については、「 [インデックスの FILL FACTOR の指定](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)」を参照してください。  
  
 SORT_IN_TEMPDB **=** { ON | **OFF** }  
 **tempdb** に一時的な並べ替え結果を格納するかどうかを指定します。 既定値は OFF です。  
  
 ON  
 インデックス構築に使用される中間の並べ替え結果が **tempdb** に格納されます。 **tempdb** がユーザー データベースとは異なるディスク セットにある場合は、インデックスの作成に要する時間が削減されます。 インデックスの構築中に使用されるディスク領域のサイズは増加します。  
  
 OFF  
 中間の並べ替え結果はインデックスと同じデータベースに格納されます。  
  
 インデックスを作成するためにユーザー データベース内に必要となる領域の他に、**tempdb** には、並べ替えの中間結果を格納するためにほぼ同じ大きさの追加領域が必要になります。 詳細については、「[インデックスの SORT_IN_TEMPDB オプション](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)」を参照してください。  
  
 IGNORE_DUP_KEY **=OFF**  
 インデックスの種類が一意になることはないので、XML インデックスでは無効です。 このオプションを ON に設定すると、エラーが発生します。  
  
 DROP_EXISTING **=** { ON | **OFF** }  
 名前付きの、既存の XML インデックスを削除および再構築することを指定します。 既定値は OFF です。  
  
 ON  
 既存のインデックスは削除され、再構築されます。 指定するインデックス名は、現在存在するインデックスと同じにする必要がありますが、インデックス定義は変更できます。 たとえば、異なる列、並べ替え順、パーティション構成、またはインデックス オプションを指定できます。  
  
 OFF  
 指定するインデックス名が既に存在する場合、エラーが表示されます。  
  
 DROP_EXISTING を使用してインデックスの種類を変更することはできません。 また、プライマリ XML インデックスをセカンダリ XML インデックスに、またはその逆に再定義することもできません。  
  
 ONLINE **=OFF**  
 インデックス操作中に、基となるテーブルとそれに関連する各インデックスに対してクエリやデータ変更を行えないことを指定します。 このバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、XML インデックスに対するオンラインのインデックス構築操作はサポートされていません。 XML インデックスに対してこのオプションを ON に設定すると、エラーが発生します。 ONLINE オプションを省略するか、ONLINE を OFF に設定してください。  
  
 オフラインのインデックス操作で、XML インデックスの作成、再構築、または削除を行う場合は、テーブルで Sch-M (スキーマ修正) ロックが取得されます。 このため、操作中は、すべてのユーザーは基になるテーブルにアクセスできません。  
  
> [!NOTE]
>  オンラインでのインデックス操作は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各エディションでサポートされる機能の一覧については、「[Editions and Supported Features for SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)」 (SQL Server 2016 のエディションとサポートされる機能) を参照してください。  
  
 ALLOW_ROW_LOCKS **=** { **ON** | OFF }  
 行ロックを許可するかどうかを指定します。 既定値は ON です。  
  
 ON  
 インデックスにアクセスするとき、行ロックが許可されます。 いつ行ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって決定されます。  
  
 OFF  
 行ロックは使用されません。  
  
 ALLOW_PAGE_LOCKS **=** { **ON** | OFF }  
 ページ ロックを許可するかどうかを指定します。 既定値は ON です。  
  
 ON  
 ページにアクセスするとき、行ロックが許可されます。 いつページ ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)] によって決定されます。  
  
 OFF  
 ページ ロックは使用されません。  
  
 MAXDOP **=** _max_degree_of_parallelism_  
 インデックス操作の間、[max degree of parallelism サーバー構成オプション](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)更新オプションをオーバーライドします。 並列プランの実行で使用されるプロセッサ数を制限するには、MAXDOP を使用します。 最大数は 64 プロセッサです。  
  
> [!IMPORTANT]  
>  MAXDOP オプションはすべての XML インデックスで構文的にサポートされていますが、プライマリ XML インデックスの場合、CREATE XML INDEX では単一のプロセッサのみが使用されます。  
  
 *max_degree_of_parallelism* は次のように指定できます。  
  
 1  
 並列プラン生成を抑制します。  
  
 \>1  
 現在のシステム ワークロードに基づいて、並列インデックス操作で使用される最大プロセッサ数を指定の数以下に制限します。  
  
 0 (既定値)  
 現在のシステム ワークロードに基づいて、実際の数以下のプロセッサを使用します。  
  
 詳細については、「 [並列インデックス操作の構成](../../relational-databases/indexes/configure-parallel-index-operations.md)」を参照してください。  
  
> [!NOTE]
>  並列インデックス操作は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各エディションでサポートされる機能の一覧については、「[Editions and Supported Features for SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)」 (SQL Server 2016 のエディションとサポートされる機能) を参照してください。  
  
## <a name="remarks"></a>Remarks  
 計算列のデータ型をインデックス キー列または非キー列として使用できる限り、**xml** データ型から派生した計算列は、キー列または非キー列としてインデックスを設定できます。 **xml** 計算列にプライマリ XML インデックスを作成することはできません。  
  
 XML インデックスについての情報を表示するには、[sys.xml_indexes](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md) カタログ ビューを使用します。  
  
 XML インデックスの詳細については、「[XML インデックス &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)」を参照してください。  
  
## <a name="additional-remarks-on-index-creation"></a>インデックス作成に関する詳細説明  
 インデックスの作成の詳細については、「[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)」の「解説」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-primary-xml-index"></a>A. プライマリ XML インデックスを作成する  
 次の例では、`CatalogDescription` テーブルの `Production.ProductModel` 列にプライマリ XML インデックスを作成します。  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT * FROM sys.indexes  
            WHERE name = N'PXML_ProductModel_CatalogDescription')  
    DROP INDEX PXML_ProductModel_CatalogDescription   
        ON Production.ProductModel;  
GO  
CREATE PRIMARY XML INDEX PXML_ProductModel_CatalogDescription  
    ON Production.ProductModel (CatalogDescription);  
GO  
```  
  
### <a name="b-creating-a-secondary-xml-index"></a>B. セカンダリ XML インデックスを作成する  
 次の例では、`CatalogDescription` テーブルの `Production.ProductModel` 列にセカンダリ XML インデックスを作成します。  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.indexes  
            WHERE name = N'IXML_ProductModel_CatalogDescription_Path')  
    DROP INDEX IXML_ProductModel_CatalogDescription_Path  
        ON Production.ProductModel;  
GO  
CREATE XML INDEX IXML_ProductModel_CatalogDescription_Path   
    ON Production.ProductModel (CatalogDescription)  
    USING XML INDEX PXML_ProductModel_CatalogDescription FOR PATH ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)   
 [XML インデックス &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.xml_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [XML インデックス &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  

