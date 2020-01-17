---
title: sys.remote_logins (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.remote_logins_TSQL
- remote_logins
- remote_logins_TSQL
- sys.remote_logins
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_logins catalog view
ms.assetid: 38477e91-d084-4df7-b1de-b930c5580189
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 371f8e2bf9a5d67d68e9c1d48502bf3fa2f81db6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904576"
---
# <a name="sysremotelogins-transact-sql"></a>sys.remote_logins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  リモート ログイン マッピングごとに 1 行のデータを返します。 このカタログ ビューは、対応するサーバーから送信されてきたと称する受信ローカル ログインを、実際のローカル ログインにマップするために使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|内のサーバーの ID **sys.servers**します。 この名前は、「リモート」サーバーからの接続によって提供されます。|  
|**remote_name**|**sysname**|マップへの接続を提供するログイン名です。 NULL の場合、接続で指定されているログイン名が使用されます。|  
|**local_principal_id**|**int**|ログインがマップ先のサーバー プリンシパルの ID。 0 の場合、リモート ログインは、同じ名前のログインにマップされます。|  
|**modify_date**|**datetime**|リンク ログインが最後に変更された日付。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [リンク サーバーのカタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
