---
title: semanticsimilaritydetailstable (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- semanticsimilaritydetailstable
- semanticsimilaritydetailstable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semanticsimilaritydetailstable function
ms.assetid: 038d751a-fca5-4b4c-9129-cba741a4e173
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 34473e6eb173a0aabc5c2067e50aeeec27ce5636
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067737"
---
# <a name="semanticsimilaritydetailstable-transact-sql"></a>semanticsimilaritydetailstable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  意味が似たコンテンツを持つ 2 つのドキュメント (ソース ドキュメントと一致するドキュメント) に共通するキー フレーズの 0 行、1 行、または複数の行から成るテーブルを返します。  
  
 この行セット関数は、SELECT ステートメントの FROM 句で参照できます。 
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
SEMANTICSIMILARITYDETAILSTABLE  
    (  
    table,  
    source_column,  
    source_key,  
    matched_column,  
    matched_key  
    )  
```  
  
##  <a name="Arguments"></a> 引数  
 **テーブル**  
 フルテキスト インデックスとセマンティック インデックスが有効になっているテーブルの名前を指定します。  
  
 この名前は、1 部から 4 部の構成の名前にできますが、リモート サーバー名は許可されません。  
  
 **source_column**  
 類似性を比較されるコンテンツを含んだソース行の列の名前。  
  
 **source_key**  
 ソース ドキュメントの行を表す一意のキー。  
  
 このキーは、可能であれば常に、ソース テーブル内の一意なフルテキスト キーの型に、暗黙的に変換されます。 キーは定数または変数として指定できますが、式や、スカラー サブクエリの結果にすることはできません。 無効なキーが指定された場合、行は返されません。  
  
 **matched_column**  
 類似性を比較されるコンテンツを含んだ一致行の列の名前。  
  
 **matched_key**  
 一致ドキュメントの行を表す一意のキー。  
  
 このキーは、可能であれば常に、ソース テーブル内の一意なフルテキスト キーの型に、暗黙的に変換されます。 キーは定数または変数として指定できますが、式や、スカラー サブクエリの結果にすることはできません。  
  
## <a name="table-returned"></a>返されるテーブル  
 次の表に、この行セット関数から返されるキー フレーズに関する情報を示します。  
  
|Column_name|型|説明|  
|------------------|----------|-----------------|  
|**keyphrase**|**NVARCHAR**|ソース ドキュメントと一致したドキュメント間の類似性に関係があるキー フレーズ。|  
|**score**|**REAL**|類似した 2 つのドキュメントの関連性における、その他のすべてのキー フレーズとこのキー フレーズの相対値。<br /><br /> この値は [0.0, 1.0] の範囲内の小数値です。スコアの値が大きいほど類似性が高く、1.0 は完全に一致することを表します。|  
  
## <a name="general-remarks"></a>全般的な解説  
 詳細については、次を参照してください。[類似および関連ドキュメント セマンティック検索による](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md)します。  
  
## <a name="metadata"></a>メタデータ  
 セマンティックな類似性の抽出および作成の詳細と状態については、次の動的管理ビューに対してクエリを実行してください。  
  
-   [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 フルテキストおよびセマンティック インデックスが作成されたベース テーブルに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例で指定された候補間で最も類似スコアが 5 つのキー フレーズを取得する**HumanResources.JobCandidate** AdventureWorks2012 サンプル データベースのテーブル。 @CandidateIdと@MatchedID変数は、フルテキスト インデックスのキー列から値を表します。  
  
```sql  
SELECT TOP(5) KEY_TBL.keyphrase, KEY_TBL.score  
FROMSEMANTICSIMILARITYDETAILSTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume, @CandidateID,  
    Resume, @MatchedID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
  
```  
  
  
