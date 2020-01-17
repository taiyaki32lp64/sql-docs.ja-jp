---
title: sys.edge_constraints (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.edge_constraints
- edge_constraints
- SQL Graph
- edge_constraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.edge_constraints catalog view
ms.assetid: 0f782d2f-7126-46ab-85b7-bcba44862231
author: shkale-msft
ms.author: shkale
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5dc2e47c49dc9d639489426fceab0b848c9def3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079323"
---
# <a name="sysedgeconstraints-transact-sql"></a>sys.edge_constraints (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

エッジの制約のあるオブジェクトごとに 1 行が含まれています。 
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<Sys.objects から継承された列 >**||このビューが継承する列の一覧は、次を参照してください。 [sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)します。|  
|**is_disabled**|**bit**|1 = 制約が無効なエッジ。<br /><br /> 0 = エッジの制約が有効にします。|  
|**is_not_trusted**|**bit**|1 = エッジの制約がシステムによって検証されていません。<br /><br /> 0 = エッジの制約がシステムによって確認されました。|  
|**delete_referential_action**|**tinyint**|このエッジの制約で定義された参照操作。<br /><br />0 = no Action です。|  
|**delete_referential_action_desc**|**nvarchar(60)**|このエッジの制約で定義された参照操作の説明です。<br /><br />NO_ACTION|  
|**is_system_named**|**bit**|1 = エッジの制約名は、システムによって生成されました。<br /><br />0 = エッジの制約名は、ユーザーが指定されました。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよくあるご質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
