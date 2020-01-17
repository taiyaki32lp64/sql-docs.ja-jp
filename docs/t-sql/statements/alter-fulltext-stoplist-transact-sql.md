---
title: ALTER FULLTEXT STOPLIST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER FULLTEXT STOPLIST
- ALTER_FULLTEXT_STOPLIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- ALTER FULLTEXT STOPLIST statement
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: f6ad87d5-6a34-435a-8456-8244947c5c83
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 692f62c6a5b9d6268a27de350a860c0cb58c74bc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067549"
---
# <a name="alter-fulltext-stoplist-transact-sql"></a>ALTER FULLTEXT STOPLIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在のデータベースの既定のフルテキスト ストップリストに対してストップワードを挿入または削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER FULLTEXT STOPLIST stoplist_name  
{   
        ADD [N] 'stopword' LANGUAGE language_term    
  | DROP   
    {  
        'stopword' LANGUAGE language_term   
      | ALL LANGUAGE language_term   
      | ALL  
     }  
;  
```  
  
## <a name="arguments"></a>引数  
 *stoplist_name*  
 変更するストップリストの名前です。 *stoplist_name* には、最大 128 文字まで指定できます。  
  
 **'** *stopword* **'**  
 指定した言語で言語的な意味を持つ単語の場合や言語的な意味のないトークンの場合がある文字列を指定します。 *stopword* の上限は最大トークン長 (64 文字) です。 ストップワードは Unicode 文字列として指定できます。  
  
 LANGUAGE *language_term*  
 追加または削除する *stopword* に関連付ける言語を指定します。  
  
 *language_term* には、次のように、言語のロケール識別子 (LCID) に対応する文字列、整数、または 16 進数の値を指定できます。  
  
|Format|[説明]|  
|------------|-----------------|  
|文字列|*language_term* には、[sys.syslanguages (Transact-SQL)](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) 互換性ビューの **alias** 列の値と同じ値を指定します。 文字列は、 **'***language_term***'** のように引用符 (') で囲む必要があります。|  
|整数|*language_term* には、言語の LCID を指定します。|  
|16 進数|*language_term* には、"0x" の後に LCID の 16 進数の値を指定します。 16 進数の値は、先頭の 0 を含め、8 桁以内で指定してください。 値を 2 バイト文字セット (DBCS) の形式で指定すると、SQL Server で Unicode に変換されます。|  
  
 ADD **'***stopword***'** LANGUAGE *language_term*  
 LANGUAGE *language_term* で指定した言語のストップリストにストップワードを追加します。  
  
 指定したキーワードの組み合わせと言語の LCID 値がストップリスト内で一意でない場合、エラーが返されます。  LCID 値が登録言語に対応していない場合は、エラーが生成されます。  
  
 DROP { **'***stopword***'** LANGUAGE *language_term* | ALL LANGUAGE *language_term* | ALL }  
 ストップ リストからストップ ワードを削除します。  
  
 **'** *stopword* **'** LANGUAGE *language_term*  
 *language_term* で指定した言語の指定したストップ ワードを削除します。  
  
 ALL LANGUAGE *language_term*  
 *language_term* で指定した言語のストップ ワードをすべて削除します。  
  
 ALL  
 ストップリストのストップワードをすべて削除します。  
  
## <a name="remarks"></a>Remarks  
 CREATE FULLTEXT STOPLIST は、互換性レベル 100 以上に対してのみサポートされます。 互換性レベル 80 および 90 の場合は、常にシステム ストップリストがデータベースに割り当てられます。  
  
## <a name="permissions"></a>アクセス許可  
 ストップリストをデータベースの既定のストップリストとして指定するには、ALTER DATABASE 権限が必要です。 それ以外の変更をストップリストに対して行うには、ストップリストの所有者であるか、**db_owner** 固定データベース ロールまたは **db_ddladmin** 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、`CombinedFunctionWordList` というストップリストを変更して、単語 'en' をまずスペイン語用に、次にフランス語用に追加します。  
  
```  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'Spanish';  
ALTER FULLTEXT STOPLIST CombinedFunctionWordList ADD 'en' LANGUAGE 'French';  
```  
  
## <a name="see-also"></a>参照  
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)   
 [フルテキスト検索に使用するストップワードとストップリストの構成と管理](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)   
 [フルテキスト検索に使用するストップワードとストップリストの構成と管理](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)  
  
  
