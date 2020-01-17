---
title: semantickeyphrasetable (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- semantickeyphrasetable
- semantickeyphrasetable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semantickeyphrasetable function
ms.assetid: d33b973a-2724-4d4b-aaf7-67675929c392
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bfde3ee5d26557759bd881bce34a69b6ecf98dd1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140567"
---
# <a name="semantickeyphrasetable-transact-sql"></a>semantickeyphrasetable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  指定されたテーブル内の指定された列に関連付けられているキー フレーズに対し、0 行、1 行、または複数の行を含むテーブルを返します。  
  
 この行セット関数は、標準のテーブル名のように、SELECT ステートメントの FROM 句で参照できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
SEMANTICKEYPHRASETABLE  
    (  
    table,  
    { column | (column_list) | * }  
     [ , source_key ]  
    )  
```  
  
##  <a name="Arguments"></a> 引数  
 **テーブル**  
 フルテキスト インデックスとセマンティック インデックスが有効になっているテーブルの名前を指定します。  
  
 この名前は、1 部から 4 部の構成の名前にできますが、リモート サーバー名は許可されません。  
  
 **column**  
 結果を返すインデックス付きの列の名前です。 列でセマンティック インデックス作成が有効になっている必要があります。  
  
 **column_list**  
 複数の列を指定します。その際、各列をコンマで区切り、かっこで囲みます。 すべての列でセマンティック インデックス作成が有効になっている必要があります。  
  
 **\***  
 セマンティック インデックスが有効になっているすべての列が含まれていることを示します。  
  
 **source_key**  
 特定の行の結果を要求する、行の一意のキーです。  
  
 このキーは、可能であれば常に、ソース テーブル内の一意なフルテキスト キーの型に暗黙的に変換されます。 キーは定数または変数として指定できますが、式や、スカラー サブクエリの結果にすることはできません。 source_key を省略すると、すべての行の結果が返されます。  
  
## <a name="table-returned"></a>返されるテーブル  
 次の表に、この行セット関数から返されるキー フレーズに関する情報を示します。  
  
|Column_name|型|説明|  
|------------------|----------|-----------------|  
|**column_id**|**int**|現在のキー フレーズが抽出され、インデックスが作成された列の ID です。<br /><br /> 列 ID から列名 (または列名から列 ID) を取得する方法の詳細については、COL_NAME 関数と COLUMNPROPERTY 関数のセクションを参照してください。|  
|**document_key**|**\***<br /><br /> このキーは、ソース テーブル内の一意キーの型と一致します。|現在のキー フレーズのインデックスが作成されたドキュメントまたは行の一意のキー値です。|  
|**keyphrase**|**NVARCHAR**|column_id で識別された列にあり、document_key で指定されたドキュメントに関係付けられるキー フレーズです。|  
|**score**|**REAL**|インデックスが作成された列の同じドキュメントに含まれる他のすべてのキー フレーズとの関係における、このキー フレーズの相対値です。<br /><br /> この値は [0.0, 1.0] の範囲内の小数値です。スコアの値が大きいほど類似性が高く、1.0 は完全に一致することを表します。|  
  
## <a name="general-remarks"></a>全般的な解説  
 詳細については、次を参照してください。[セマンティック検索を使用したドキュメント内のキー フレーズの検索](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md)します。  
  
## <a name="metadata"></a>メタデータ  
 セマンティックなキー フレーズの抽出および生成の詳細と状態については、次の動的管理ビューに対してクエリを実行してください。  
  
-   [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 フルテキストおよびセマンティック インデックスが作成されたベース テーブルに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
###  <a name="HowToTopPhrases"></a> 例 1: 特定のドキュメント内の最上位のキー フレーズを検索します。  
 次の例では、AdventureWorks サンプル データベースの Production.Document テーブルの Document 列にある、@DocumentId 変数で指定されたドキュメントから、上位 10 個のキー フレーズを取得します。 @DocumentId 変数は、フルテキスト インデックスのキー列の値を表します。 **SEMANTICKEYPHRASETABLE** 関数は、テーブル スキャンではなくインデックス シークを使用してこれらの結果を効率的に取得します。 この例では、フルテキストとセマンティック インデックスに対して列が設定されます。  
  
```sql  
SELECT TOP(10) KEYP_TBL.keyphrase  
FROM SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document,  
    @DocumentId  
    ) AS KEYP_TBL  
ORDER BY KEYP_TBL.score DESC;  
  
```  
  
###  <a name="HowToTopDocuments"></a> 例 2: 特定のキー フレーズを含む上位のドキュメントを検索します。  
 次の例では、AdventureWorks サンプル データベースの Production.Document テーブルの Document 列から、キー フレーズ "Bracket" を含む上位 25 個のドキュメントを取得します。 この例では、フルテキストとセマンティック インデックスに対して列が設定されます。  
  
```sql  
SELECT TOP (25) DOC_TBL.DocumentID, DOC_TBL.DocumentSummary  
FROM Production.Document AS DOC_TBL  
    INNER JOIN SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document  
    ) AS KEYP_TBL  
ON DOC_TBL.DocumentID = KEYP_TBL.document_key  
WHERE KEYP_TBL.keyphrase = 'Bracket'  
ORDER BY KEYP_TBL.Score DESC;  
  
```  
  
  
