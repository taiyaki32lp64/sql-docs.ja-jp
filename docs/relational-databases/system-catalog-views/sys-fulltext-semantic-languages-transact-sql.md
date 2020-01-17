---
title: sys.fulltext_semantic_languages (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_semantic_languages
- fulltext_semantic_languages_TSQL
- sys.fulltext_semantic_languages
- sys.fulltext_semantic_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_semantic_languages catalog view
ms.assetid: b42a85e6-1db9-4a22-8a70-014574c95198
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: c060f08ff70e04a22af1eb9de09aeb1e3bf4ff71
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68133778"
---
# <a name="sysfulltext_semantic_languages-transact-sql"></a>sys.fulltext_semantic_languages (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  統計モデルが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに登録されている各言語の行を返します。 言語モデルの登録時に、セマンティック インデックス作成用の言語が有効であります。  
  
 このカタログ ビューに似ています[sys.fulltext_languages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)します。  
    
||||  
|-|-|-|  
|**列名**|**型**|**[説明]**|  
|lcid|int|言語の Microsoft Windows ロケール識別子 (LCID) です。|  
|NAME|sysname|内の別名のいずれかの値は、 [sys.syslanguages &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)の値に対応する**lcid**、または LCID の数値の文字列表現。|  
  
## <a name="general-remarks"></a>全般的な解説  
 詳細については、「 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)」を参照してください。  
  
## <a name="metadata"></a>メタデータ  
 セマンティック インデックス作成をサポートするためにインストールされているセマンティック言語統計データベースに関する詳細については、カタログ ビューに対してクエリ[sys.fulltext_semantic_language_statistics_database &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 カタログ ビューでのメタデータの表示が、ユーザーが所有しているかそのユーザーが権限を許可されている、セキュリティ保護可能なメタデータに制限されます。  
  
## <a name="examples"></a>使用例  
 次の例を照会する方法**sys.fulltext_semantic_languages**の現在のインスタンスでセマンティック インデックス作成の言語モデルが登録されているすべての情報を取得する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
```  
SELECT * FROM sys.fulltext_semantic_languages;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
