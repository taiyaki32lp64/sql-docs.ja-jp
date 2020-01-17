---
title: FREETEXTTABLE (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- FREETEXTTABLE_TSQL
- FREETEXTTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- search conditions [SQL Server], meaning matches
- meaning matches [full-text search]
- FREETEXTTABLE function (Transact-SQL)
- ranked results [full-text search]
- column searches [full-text search]
ms.assetid: 4523ae15-4260-40a7-a53c-8df15e1fee79
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4ab1797fabd8fb7d77eab85c97604b77e72f25c3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042762"
---
# <a name="freetexttable-transact-sql"></a>FREETEXTTABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  使用される関数、[FROM 句](../../t-sql/queries/from-transact-sql.md)の[!INCLUDE[tsql](../../includes/tsql-md.md)]を実行する SELECT ステートメント、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]フル ・ テキストの全文検索が文字ベースのデータ型を含む列をインデックス付けします。 この関数は 0、1、または複数の行を意味し、正確な表現だけでなく、指定したテキストに一致する値を格納している列のテーブルを返します*freetext_string*します。 FREETEXTTABLE は、通常のテーブル名の場合と同様に参照されます。  
  
 FREETEXTTABLE は、同じ種類と一致するのに便利です、 [FREETEXT &#40;Transact SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)、  
  
 FREETEXTTABLE を使用するクエリでは、ランク付けの値 (RANK) とフルテキスト キー (キー) が行ごとに関連性の高さを返します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされているフルテキスト検索の形式については、「[フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)」を参照してください。  
  
(https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).|  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
FREETEXTTABLE (table , { column_name | (column_list) | * }   
          , 'freetext_string'   
     [ , LANGUAGE language_term ]   
     [ , top_n_by_rank ] )  
```  
  
## <a name="arguments"></a>引数  
 *テーブル*  
 フル ・ テキスト用にマークされているテーブルの名前を照会します。 *テーブル*または*ビュー*1、2、または 3 つのデータベース オブジェクトの名前にすることができます。 ビューに対してクエリを実行する場合は、フルテキスト インデックスが作成されたベース テーブルを 1 つだけ指定できます。  
  
 *テーブル*サーバー名を指定することはできませんし、リンク サーバーに対するクエリでは使用できません。  
  
 *column_name*  
 FROM 句で指定したテーブルのフルテキスト インデックス付きの列の名前を指定します。 列には、**char**、**varchar**、**nchar**、**nvarchar**、**text**、**ntext**、**image**、**xml**、**varbinary**、**varbinary(max)** のいずれかの型を指定できます。  
  
 *column_list*  
 コンマ区切りで複数の列を指定できます。 *column_list* は、かっこで囲む必要があります。 *language_term* を指定しない場合、*column_list* で指定するすべての列の言語は同じにする必要があります。  
  
 \*  
 フルテキスト検索用に登録されているすべての列を使用して、指定した *freetext_string* を検索します。 しない限り、 *language_term*を指定すると、テーブル内のすべてのフルテキスト インデックス付き列の言語は同じである必要があります。  
  
 *freetext_string*  
 *column_name* で検索するテキストです。 単語、フレーズ、文など、あらゆるテキストを入力できます。 用語または一定の形式になっている用語がフルテキスト インデックス内に見つかった場合、一致するものと判断されます。  
  
 異なり、CONTAINS の検索条件であり、キーワードで使用すると*freetext_string*という単語 'と'、ノイズ ワードと見なされますまたは[ストップ ワード](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)、され破棄されます。  
  
 WEIGHT、FORMSOF、ワイルドカード、NEAR、その他の構文は使用できません。 *freetext_string* は単語、語幹に分割され、類義語がチェックされて渡されます。  
  
 LANGUAGE *language_term*  
 クエリにおいて、単語区切り、語幹への分割、類義語のチェック、ストップワードの破棄を行うときに使用する言語リソースの言語を指定します。 このパラメーターは省略可能で、言語のロケール識別子 (LCID) に対応する文字列、整数、または 16 進数の値を指定できます。 *language_term* を指定した場合、その言語は検索条件のすべての要素に適用されます。 値を指定しなかった場合は、列のフルテキストの言語が使用されます。  
  
 1 つの列に言語の異なる複数のドキュメントが BLOB (Binary Large Object) として格納されている場合、そのインデックスの作成に使用される言語は、そのドキュメントのロケール識別子 (LCID) によって決まります。 そのような列に対してクエリを実行する場合は、*LANGUAGE language_term* を指定すると検索結果の一致率が高まります。  
  
 *language_term* を文字列で指定する場合は、[sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 互換性ビューの **alias** 列の値と同じ値を指定します。  文字列の場合は、'*language_term*' のように引用符 (') で囲む必要があります。 *language_term* を整数で指定する場合は、その言語を表す実際の LCID を指定します。 *language_term* を 16 進数の値で指定する場合は、「0x」の後に LCID の 16 進数の値を指定します。 16 進数の値は、先頭の 0 を含め、8 桁以内で指定してください。  
  
 値を 2 バイト文字セット (DBCS) の形式で指定すると、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で Unicode に変換されます。  
  
 指定した言語が無効であるか、その言語に該当するリソースがインストールされていない場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によりエラーが返されます。 ニュートラル言語リソースを使用するには、*language_term* に「0x0」を指定してください。  
  
 *top_n_by_rank*  
 のみを指定します*n*の降順に並べ替え、最上位のランクと一致が返されます。 整数値では場合に、のみ適用されます*n*を指定します。 *top_n_by_rank* を他のパラメーターと組み合わせた場合、クエリから返される行数は、実際にすべての述語に一致する行数より少なくなります。 *top_n_by_rank*最も重要なヒットだけを再度呼び出すことによってクエリのパフォーマンスを向上することができます。  
  
## <a name="remarks"></a>コメント  
 フルテキストの述語と関数の対象は、FROM 述語で示される 1 つのテーブルです。 複数のテーブルを検索するには、FROM 句で結合テーブルを使用して、複数のテーブルが組み合わされた結果セットを検索します。  
  
 FREETEXTTABLE では、FREETEXT 述語と同じ検索条件が使用されます。  
  
 返されたテーブルがという名前の列を作成のような**KEY**と**RANK**、適切な行を取得し、行の値のランク付けを使用するクエリ内で参照されています。  
  
## <a name="permissions"></a>アクセス許可  
 FREETEXTTABLE を呼び出すには、指定されるテーブルまたは参照されるテーブル列に対して適切な SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-simple-example"></a>A. 簡単な例  
 次の例では、作成し、3 つの郡およびそのフラグの色の一覧を表示する 2 つの列の単純なテーブルを入力します。 It では、作成し、テーブルのインデックス、フルテキスト カタログを設定します。 **FREETEXTTABLE**の構文を説明します。  
  
```  
CREATE TABLE Flags (Country nvarchar(30) NOT NULL, FlagColors varchar(200));  
CREATE UNIQUE CLUSTERED INDEX FlagKey ON Flags(Country);  
INSERT Flags VALUES ('France', 'Blue and White and Red');  
INSERT Flags VALUES ('Italy', 'Green and White and Red');  
INSERT Flags VALUES ('Tanzania', 'Green and Yellow and Black and Yellow and Blue');  
SELECT * FROM Flags;  
GO  
  
CREATE FULLTEXT CATALOG TestFTCat;  
CREATE FULLTEXT INDEX ON Flags(FlagColors) KEY INDEX FlagKey ON TestFTCat;  
GO   
  
SELECT * FROM Flags;  
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Blue');  
SELECT * FROM FREETEXTTABLE (Flags, FlagColors, 'Yellow');  
```  
  
### <a name="b-using-freetext-in-an-inner-join"></a>B. FREETEXT を使用して内部結合で  
 次の例の説明と説明の意味と一致するすべての製品の順位を返します`high level of performance`します。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance') AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
### <a name="c-specifying-language-and-highest-ranked-matches"></a>C. 言語および最高順位の一致の指定  
 次の例と同じし、の使用例を示します、 `LANGUAGE` *language_term*と*top_n_by_rank*パラメーター。  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT FT_TBL.Description  
    ,KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL   
    INNER JOIN FREETEXTTABLE(Production.ProductDescription,  
    Description,   
    'high level of performance',  
    LANGUAGE N'English', 2) AS KEY_TBL  
ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY RANK DESC;  
GO  
```  
  
> [!NOTE]
>  言語*language_term*パラメーターを使用する必要はありません、 *top_n_by_rank*パラメーター。  
  
## <a name="see-also"></a>関連項目  
 [フルテキスト検索の概要](../../relational-databases/search/get-started-with-full-text-search.md)   
 [フルテキスト カタログの作成と管理](../../relational-databases/search/create-and-manage-full-text-catalogs.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [フルテキスト インデックスの作成と管理](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [フルテキスト検索でのクエリ](../../relational-databases/search/query-with-full-text-search.md)   
 [フルテキスト検索クエリの作成 &#40;Visual Database Tools&#41;](https://msdn.microsoft.com/library/537fa556-390e-4c88-9b8e-679848d94abc)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [行セット関数 &#40;Transact-SQL&#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [precompute rank サーバー構成オプション](../../database-engine/configure-windows/precompute-rank-server-configuration-option.md)  
  
  
