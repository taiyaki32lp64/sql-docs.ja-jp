---
title: sp_fulltext_semantic_unregister_language_statistics_db (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_semantic_unregister_language_statistics_db_TSQL
- sp_fulltext_semantic_unregister_language_statistics_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_semantic_unregister_language_statistics_db
ms.assetid: 1426ca4a-9a76-489e-98da-8f6d13ff9732
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d6952d245dfc9083c7cfa6e6d36ad991ffd24654
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909137"
---
# <a name="sp_fulltext_semantic_unregister_language_statistics_db-transact-sql"></a>sp_fulltext_semantic_unregister_language_statistics_db (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の現在のインスタンスから既存のセマンティック言語統計データベースの登録を解除し、関連付けられているメタデータを削除します。  
  
 このステートメントでは、データベースをデタッチしたり、ファイルシステムから物理データベースファイルを削除したりすることはありません。 データベースの登録の解除後は、それをデタッチし、物理的なデータベース ファイルを削除することができます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
##  <a name="Arguments"></a> 引数  
 このプロシージャは、引数を必要としません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにはセマンティック言語統計データベースが1つしかないため、データベースを識別する必要はありません。  
  
## <a name="return-code-value"></a>リターン コード値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-set"></a>結果セット  
 [なし] :  
  
## <a name="general-remarks"></a>全般的な解説  
 セマンティック言語統計データベースの登録が解除されると、それに関連付けられているすべてのメタデータも削除されます。  
  
 **sp_fulltext_semantic_unregister_language_statistics_db**は、次の手順を実行します。  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の現在のインスタンスに対して実行中のセマンティック作成がないことを確認します。  
  
2.  指定されたセマンティック言語統計データベースに関連付けられているすべてのメタデータを削除します。  

 詳細については、「 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)」を参照してください。  
  
## <a name="metadata"></a>[ブラウザー]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスにインストールされているセマンティック言語統計データベースの詳細については、カタログビュー [fulltext_semantic_language_statistics_database &#40;&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)にクエリを実行してください。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>Permissions  
 CONTROL SERVER 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、 **sp_fulltext_semantic_unregister_language_statistics_db**を呼び出して、セマンティック言語統計データベースの登録を解除する方法を示します。  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
## <a name="see-also"></a>「  
 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
