---
title: sp_fulltext_semantic_register_language_statistics_db (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_semantic_register_language_statistics_db
- sp_fulltext_semantic_register_language_statistics_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_semantic_register_language_statistics_db
ms.assetid: bef1b104-5a44-4327-9ae4-45eae3000f7e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 59cf70574a73827887542221f556e65e46090395
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124209"
---
# <a name="spfulltextsemanticregisterlanguagestatisticsdb-transact-sql"></a>sp_fulltext_semantic_register_language_statistics_db (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の現在のインスタンスで、事前にデータが設定されているセマンティック言語統計データベースを登録します。  
  
 この言語統計データベースをアタッチし、このストアド プロシージャを使用して登録した後にのみ、セマンティックな抽出を開始することができます。 インスタンスごとに 1 回このタスクを実行するだけで済みます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db  
    [ @dbname = ] 'database_name';  
GO  
```  
  
##  <a name="Arguments"></a> 引数  
 [ @dbname = ] '*database_name*'  
 現在のインスタンスに登録するセマンティック言語統計データベースの名前を指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 データベースが既にアタッチされている必要があります。 *database_name*は**sysname**NULL にできない可能性があります。  
  
## <a name="return-code-value"></a>リターン コード値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-set"></a>結果セット  
 [なし] :  
  
## <a name="general-remarks"></a>全般的な解説  
 セマンティック言語統計データベースには、テキスト コンテンツのセマンティックな処理に必要な言語関連の統計情報が含まれています。  
  
 **sp_fulltext_semantic_register_language_statistics_db**は、次の手順を実行します。  
  
1.  確認のインスタンス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]セマンティックな処理をサポートするバージョンです。  
  
2.  確認のインスタンス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]まだ定義されているセマンティック言語統計データベースがないです。  
  
3.  データベースが有効なセマンティック言語統計データベースであることを確認します。  
  
4.  ユーザーがデータベースへのアクセスを制限するセマンティック言語統計データベースのアクセス許可を設定します。  
  
5.  インスタンスのセマンティック言語統計データベースの名前を定義するメタデータを挿入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
6.  インストールされているセマンティック言語統計データベースと内部言語モデル テーブル間のマッピングを定義するメタデータを挿入します。  
  
7.  データベースがすぐに使用できることを確認することを確認します。  
  
 詳細については、「 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)」を参照してください。  
  
## <a name="metadata"></a>メタデータ  
 インスタンスにインストールされているセマンティック言語統計データベースに関する情報の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、カタログ ビューに対してクエリ[sys.fulltext_semantic_language_statistics_database &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)します。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 CONTROL SERVER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、呼び出すことによって、セマンティック言語統計データベースを登録する方法を示しています。 **sp_fulltext_semantic_register_language_statistics_db**します。  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = 'semanticsDb';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
