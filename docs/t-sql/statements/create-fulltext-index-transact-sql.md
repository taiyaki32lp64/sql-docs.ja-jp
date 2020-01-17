---
title: CREATE FULLTEXT INDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FULLTEXT_INDEX_TSQL
- CREATE_FULLTEXT_INDEX_TSQL
- CREATE FULLTEXT INDEX
- FULLTEXT INDEX
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], creating
- index creation [SQL Server], CREATE FULLTEXT INDEX statement
- CREATE FULLTEXT INDEX statement
ms.assetid: 8b80390f-5f8b-4e66-9bcc-cabd653c19fd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5d51385ff820155d805803773265f39cd8598df6
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981892"
---
# <a name="create-fulltext-index-transact-sql"></a>CREATE FULLTEXT INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベース内のテーブルまたはインデックス付きビューで、フルテキスト インデックスを作成します。 テーブルまたはインデックス付きビューごとに 1 つのフルテキスト インデックスのみ使用でき、各フルテキスト インデックスは 1 つのテーブルまたはインデックス付きビューに適用されます。 フルテキスト インデックスには、1,024 列まで格納できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
CREATE FULLTEXT INDEX ON table_name  
   [ ( { column_name   
             [ TYPE COLUMN type_column_name ]  
             [ LANGUAGE language_term ]   
             [ STATISTICAL_SEMANTICS ]  
        } [ ,...n]   
      ) ]  
    KEY INDEX index_name   
    [ ON <catalog_filegroup_option> ]  
    [ WITH [ ( ] <with_option> [ ,...n] [ ) ] ]  
[;]  
  
<catalog_filegroup_option>::=  
 {  
    fulltext_catalog_name   
 | ( fulltext_catalog_name, FILEGROUP filegroup_name )  
 | ( FILEGROUP filegroup_name, fulltext_catalog_name )  
 | ( FILEGROUP filegroup_name )  
 }  
  
<with_option>::=  
 {  
   CHANGE_TRACKING [ = ] { MANUAL | AUTO | OFF [, NO POPULATION ] }   
 | STOPLIST [ = ] { OFF | SYSTEM | stoplist_name }  
 | SEARCH PROPERTY LIST [ = ] property_list_name   
 }  
```  
  
## <a name="arguments"></a>引数
*table_name*       
フルテキスト インデックスに含まれている列を格納するテーブルまたはインデックス付きビューの名前を指定します。  
  
*column_name*       
フルテキスト インデックスに含める列の名前を指定します。 フルテキスト検索用にインデックスを作成できるのは、型が **char**、**varchar**、**nchar**、**nvarchar**、**text**、**ntext**、**image**、**xml**、**varbinary(max)** の列だけです。 複数の列を指定するには、次のように *column_name* 句を繰り返します。  
  
CREATE FULLTEXT INDEX ON *table_name* (*column_name1* [...], *column_name2* [...]) ...  
  
TYPE COLUMN *type_column_name*       
**varbinary(max)** または **image** ドキュメントのドキュメント型を保持するために使用されているテーブル列 *type_column_name* の名前を指定します。 型列と呼ばれるこの列には、ユーザー指定のファイル拡張子 (.doc、.pdf、.xls など) が格納されます。 型列は、 **char**型、 **nchar**型、 **varchar**型、 **nvarchar**型にする必要があります。  
  
TYPE COLUMN *type_column_name* を指定できるのは、*column_name* で、データがバイナリ データとして格納される **varbinary(max)** または **image** 列を指定した場合のみです。それ以外の場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではエラーが返されます。  
  
> [!NOTE]  
> Full-Text Engine は、インデックスを作成する際に、各テーブル行の型列の省略形を使用して、*column_name* でドキュメントに使用するフルテキスト検索フィルターを特定します。 フィルターはドキュメントをバイナリ ストリームとして読み込み、書式設定情報を削除し、ドキュメントからワード ブレーカー コンポーネントへテキストを送信します。 詳細については、「 [検索用フィルターの構成と管理](../../relational-databases/search/configure-and-manage-filters-for-search.md)」を参照してください。  
  
LANGUAGE *language_term*       
*column_name* に格納されているデータの言語です。  
  
*language_term* は省略可能で、言語のロケール識別子 (LCID) に対応する文字列、整数、または 16 進数の値を指定できます。 値を指定しなかった場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの既定の言語が使用されます。  
  
*language_term* を指定すると、それが表す言語が、**char**、**nchar**、**varchar**、**nvarchar**、**text**、**ntext** 列のデータのインデックス付けに使われます。 クエリ実行時に、列に対するフルテキスト述語の一部として *language_term* を指定しない場合は、ここで指定した言語がクエリでの既定の言語になります。  
  
*language_term* を文字列で指定する場合は、syslanguages システム テーブルの alias 列の値と同じ値を指定します。 文字列は、 **'** _language\_term_ **'** のように引用符 (') で囲む必要があります。 *language_term* を整数で指定する場合は、その言語を表す実際の LCID を指定します。 *language_term* を 16 進数値で指定する場合は、「0x」の後に LCID の 16 進数値を指定します。 16 進数の値は、先頭の 0 を含め、8 桁以内で指定してください。  
  
値を 2 バイト文字セット (DBCS) の形式で指定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で Unicode に変換されます。  
  
*language_term* で指定した言語に対しては、単語区切りや語幹検索などのリソースが有効になっている必要があります。 指定した言語でこれらのリソースがサポートされていない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではエラーが返されます。  
  
[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの既定のフルテキスト言語に関する情報を取得するには、sp_configure ストアド プロシージャを使用します。 詳細については、「 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)」を参照してください。  
  
列のデータ型が BLOB および XML 以外で、複数の言語のテキスト データが含まれている場合や、列に格納されているテキストの言語が不明な場合は、ニュートラル (0x0) 言語リソースを使用することもできます。 ただしその前に、ニュートラル (0x0) 言語リソースを使用した場合にどのような結果が起こりうるのかを理解しておく必要があります。 ニュートラル (0x0) 言語リソースの使用について考えられる解決策と起こりうる結果については、「[フルテキスト インデックス作成時の言語の選択](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)」を参照してください。  
  
データ型が XML または BLOB の列に格納されているドキュメントに対しては、そのドキュメントの言語のエンコードがインデックス作成時に使用されます。 たとえば、データ型が XML の列では、XML ドキュメントの属性 **xml:lang** によって言語が決定されます。 クエリ時には、フルテキスト クエリ内で *language_term* を指定しない限り、前回 *language_term* に指定された値がフルテキスト クエリの既定の言語になります。  
  
STATISTICAL_SEMANTICS       
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降)。 
  
キー フレーズを追加で作成し、統計的セマンティック インデックス作成の一部である類似性のインデックスを記録します。 詳細については、「[セマンティック検索 &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md)」を参照してください。  
  
KEY INDEX *index_name*       
*table_name* の一意キー インデックスの名前を指定します。 KEY INDEX は、一意で、単一のキーを含む、NULL 値を許容しない列であることが必要です。 フルテキストの一意キーには、一番小さな一意キー インデックスを選択します。  最適なパフォーマンスが得られるように、フルテキスト キーには整数データ型を使用することをお勧めします。  
  
*fulltext_catalog_name*       
フルテキスト インデックスに使用するフルテキスト カタログを指定します。 このカタログはデータベース内に存在する必要があります。 この句は省略可能です。 指定しない場合は、既定のカタログが使用されます。 既定のカタログが存在しない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではエラーが返されます。  
  
FILEGROUP *filegroup_name*       
指定したファイル グループに、指定したフルテキスト インデックスを作成します。 ファイル グループは既に存在している必要があります。 FILEGROUP 句を指定しなかった場合、フルテキスト インデックスは、非パーティション テーブルの場合にはベース テーブルまたはベース ビューと同じファイル グループに、パーティション テーブルの場合にはプライマリ ファイル グループに配置されます。  
  
 CHANGE_TRACKING [ = ] { MANUAL | **AUTO** | OFF [ , NO POPULATION ] }       
 フルテキスト インデックスの対象となるテーブル列の変更 (更新、削除、または挿入) が、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってフルテキスト インデックスに反映されるかどうかを指定します。 WRITETEXT および UPDATETEXT によるデータの変更は、フルテキスト インデックスには反映されず、変更の監視でも取得されません。  
  
MANUAL       
ALTER FULLTEXT INDEX ... START UPDATE POPULATION [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの呼び出しによって手動で行うこと ("*手動作成*") を指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用すると、この [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを定期的に呼び出すことができます。  
  
**AUTO**       
ベース テーブルでデータが変更されたときに、追跡された変更を自動的に反映すること ("*自動作成*") を指定します。 この場合、フルテキスト インデックスに対して変更は自動的に反映されますが、反映までに少し時間がかかることがあります。 AUTO は既定値です。  
  
OFF [ `,` NO POPULATION]       
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、インデックスの対象となるデータに対して行われた変更の一覧を保持しません。 NO POPULATION を指定しない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、インデックスの作成後にインデックスへの値が完全に設定されます。  
  
NO POPULATION オプションは、CHANGE_TRACKING が OFF の場合にだけ使用できます。 NO POPULATION を指定した場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではインデックスの作成後、インデックスに対して値は設定されません。 この場合、ユーザーが START FULL POPULATION 句または START INCREMENTAL POPULATION 句を指定して ALTER FULLTEXT INDEX コマンドを実行した後でなければ、インデックスは作成されません。  
  
STOPLIST [ = ] { OFF | **SYSTEM** | *stoplist_name* }       
フルテキスト ストップリストをインデックスに関連付けます。 インデックスには、指定したストップリストの一部であるトークンは設定されません。 STOPLIST を指定しない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってシステム フルテキスト ストップリストがインデックスに関連付けられます。  
  
OFF       
フルテキスト インデックスにストップリストを関連付けないことを指定します。  
  
**SYSTEM**       
このフルテキスト インデックスに対して既定のフルテキスト システム ストップリストを使用することを指定します。  
  
*stoplist_name*       
フルテキスト インデックスに関連付けるストップリストの名前を指定します。  
  
SEARCH PROPERTY LIST [ = ] *property_list_name*       
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降)。  
  
検索プロパティ リストとインデックスを関連付けます。  
 
OFF       
フルテキスト インデックスにプロパティ リストを関連付けないことを指定します。  
  
*property_list_name*       
フルテキスト インデックスに関連付ける検索プロパティ リストの名前を指定します。  
  
## <a name="remarks"></a>Remarks  
フルテキスト インデックスについて詳しくは、「[フルテキスト インデックスの作成と管理](../../relational-databases/search/create-and-manage-full-text-indexes.md)」をご覧ください。  
  
**xml** 列にフルテキスト インデックスを作成して XML 要素のコンテンツにインデックスを設定できますが、XML マークアップは無視されます。 属性値には、数値でない限り、フルテキスト インデックスが設定されます。 要素タグはトークンの境界として使用されます。 複数言語を含む整形式の XML または HTML ドキュメントやフラグメントはサポートされます。 詳細については、「 [XML 列でのフルテキスト検索の使用](../../relational-databases/xml/use-full-text-search-with-xml-columns.md)」を参照してください。  
  
インデックス キー列は整数データ型にすることをお勧めします。 整数データ型にすると、クエリの実行が最適化されます。  
  
## <a name="interactions-of-change-tracking-and-no-population-parameter"></a>変更の追跡と NO POPULATION パラメーターの相関関係  
 フルテキスト インデックスが作成されるかどうかは、変更の追跡が有効になっているかどうかと、ALTER FULLTEXT INDEX ステートメントで WITH NO POPULATION が指定されているかどうかによって決まります。 次の表は、その相関関係の結果をまとめたものです。  
  
|変更の追跡|WITH NO POPULATION|結果|  
|---------------------|------------------------|------------|  
|有効ではない|指定なし|インデックスで完全作成が実行されます。|  
|有効ではない|[Specified]|ALTER FULLTEXT INDEX...START POPULATION ステートメントが実行されるまで、インデックスの作成は行われません。|  
|有効|指定あり|エラーが発生し、インデックスは変更されません。|  
|有効|指定なし|インデックスで完全作成が実行されます。|  
  
 フルテキスト インデックスの作成について詳しくは、「[フルテキスト インデックスの作成](../../relational-databases/search/populate-full-text-indexes.md)」をご覧ください。  
  
## <a name="permissions"></a>アクセス許可  
 フルテキスト カタログに対する `REFERENCES` 権限とテーブルまたはインデックス付きビューに対する `ALTER` 権限を持っているか、`sysadmin` 固定サーバー ロール、`db_owner` 固定データベース ロール、または `db_ddladmin` 固定データベース ロールのメンバーであることが必要です。  
  
`SET STOPLIST` を指定した場合は、ユーザーが指定のストップリストに対する REFERENCES 権限を持っている必要があります。 ストップリストの所有者がこの権限を許可できます。  
  
> [!NOTE]  
> public には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に含まれる既定のストップリストに対する REFERENCE 権限が許可されています。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-unique-index-a-full-text-catalog-and-a-full-text-index"></a>A. 一意のインデックス、フルテキスト カタログ、およびフルテキスト インデックスを作成する  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] サンプル データベースの `HumanResources.JobCandidate` テーブルの `JobCandidateID` 列に一意のインデックスを作成します。 その後、既定のフルテキスト カタログ、`ft` を作成します。 そして最後に、`Resume` カタログおよびシステム ストップリストを使用して `ft` 列にフルテキスト インデックスを作成します。  
  
```sql  
CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
CREATE FULLTEXT CATALOG ft AS DEFAULT;  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
   KEY INDEX ui_ukJobCand   
   WITH STOPLIST = SYSTEM;  
GO  
```  
  
### <a name="b-creating-a-full-text-index-on-several-table-columns"></a>B. 複数のテーブル列にフルテキスト インデックスを作成する  
 次の例では、`production_catalog` サンプル データベースにフルテキスト カタログ、`AdventureWorks` を作成します。 その後、この新しいカタログを使用するフルテキスト インデックスを作成します。 フルテキスト インデックスは、`ReviewerName` の `EmailAddress`、`Comments`、および `Production.ProductReview` 列にあります。 各列に、列のデータの言語である英語の LCID、`1033` を指定します。 このフルテキスト インデックスは、既存の一意なキー インデックス、`PK_ProductReview_ProductReviewID` を使用します。 推奨されているように、このインデックス キーは整数列、`ProductReviewID` にあります。  
  
```sql  
CREATE FULLTEXT CATALOG production_catalog;  
GO  
CREATE FULLTEXT INDEX ON Production.ProductReview  
 (   
  ReviewerName  
     Language 1033,  
  EmailAddress  
     Language 1033,  
  Comments   
     Language 1033       
 )   
  KEY INDEX PK_ProductReview_ProductReviewID   
      ON production_catalog;   
GO  
```  
  
### <a name="c-creating-a-full-text-index-with-a-search-property-list-without-populating-it"></a>C. インデックスの値を設定せずに、検索プロパティ リストのフルテキスト インデックスを作成する  
 次の例では、`Title` テーブルの `DocumentSummary`、`Document`、および `Production.Document` の各列にフルテキスト インデックスを作成します。 この例では、列のデータの言語である英語の LCID、`1033` を指定します。 このフルテキスト インデックスは、既定のフルテキスト カタログおよび既存の一意なキー インデックス、`PK_Document_DocumentID` を使用します。 推奨されているように、このインデックス キーは整数列、`DocumentID` にあります。  
  
 この例では、ストップリストとして SYSTEM を指定します。 また、検索プロパティ リストとして `DocumentPropertyList` も指定します。このプロパティ リストを作成する例については、「[CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)」を参照してください。  
  
 この例では、変更の追跡が OFF で、NO POPULATION を指定しています。 代わりに、ALTER FULLTEXT INDEX ステートメントを指定して、後のピーク タイム以外の時間に新しいインデックスの完全作成を開始し、自動変更追跡を有効にしています。  
  
```sql  
CREATE FULLTEXT INDEX ON Production.Document  
  (   
  Title  
      Language 1033,   
  DocumentSummary  
      Language 1033,   
  Document   
      TYPE COLUMN FileExtension  
      Language 1033   
  )  
  KEY INDEX PK_Document_DocumentID  
          WITH STOPLIST = SYSTEM, SEARCH PROPERTY LIST = DocumentPropertyList, CHANGE_TRACKING OFF, NO POPULATION;  
   GO  
```  
  
 後のピーク タイム以外の時間にインデックスを作成  
  
```sql  
ALTER FULLTEXT INDEX ON Production.Document SET CHANGE_TRACKING AUTO;  
GO  
```  
  
## <a name="see-also"></a>参照  
[フルテキスト インデックスの作成と管理](../../relational-databases/search/create-and-manage-full-text-indexes.md)       
[ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)       
[DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)       
[フルテキスト検索](../../relational-databases/search/full-text-search.md)       
[GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)       
[sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)       
[検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)       
  
  
