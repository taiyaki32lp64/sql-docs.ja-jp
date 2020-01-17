---
title: sys.fulltext_semantic_language_statistics_database (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_semantic_language_statistics_database_TSQL
- fulltext_semantic_language_statistics_database_TSQL
- fulltext_semantic_language_statistics_database
- sys.fulltext_semantic_language_statistics_database
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_semantic_language_statistics_database catalog view
ms.assetid: 32e95614-ed88-4068-8c37-1e21544717bc
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: e1d2e60ce41cd3c57af209123471696cf02a03ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133789"
---
# <a name="sysfulltextsemanticlanguagestatisticsdatabase-transact-sql"></a>sys.fulltext_semantic_language_statistics_database (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のインスタンスにインストールされているセマンティック言語統計データベースに関する行を返します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
 セマンティックな処理に必要なセマンティック言語統計コンポーネントについて確認するには、このビューを照会できます。  
   
  
||||  
|-|-|-|  
|**列名**|**型**|**[説明]**|  
|**database_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内で一意のデータベースの ID です。|  
|**register_date**|**datetime**|セマンティックな処理、データベースが登録された日付。|  
|**registered_by**|**int**|セマンティックな処理のデータベースを登録したサーバー プリンシパルの ID。|  
|**version**|**nvarchar(128)**|最新バージョンに固有の情報、セマンティック言語統計データベース。|  
  
## <a name="general-remarks"></a>全般的な解説  
 詳細については、「 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)」を参照してください。  
  
## <a name="metadata"></a>メタデータ  
 セマンティック インデックス作成はサポートされている言語については、カタログ ビューに対してクエリ[sys.fulltext_semantic_languages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md)します。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 カタログ ビューでのメタデータの表示が、ユーザーが所有しているかそのユーザーが権限を許可されている、セキュリティ保護可能なメタデータに制限されます。  
  
## <a name="examples"></a>使用例  
 次の例を照会する方法**sys.fulltext_semantic_language_statistics_database**の現在のインスタンスに登録されているセマンティック言語統計データベースに関する情報を取得する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
```  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
