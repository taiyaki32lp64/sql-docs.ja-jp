---
title: sys.linked_logins (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.linked_logins
- sys.linked_logins_TSQL
- linked_logins_TSQL
- linked_logins
dev_langs:
- TSQL
helpviewer_keywords:
- sys.linked_logins catalog view
ms.assetid: af57bf0c-a265-410f-9bab-63b78569b4a6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: dfde20205de71a302c7ba8151fc6171cecc05a08
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140680"
---
# <a name="syslinkedlogins-transact-sql"></a>sys.linked_logins (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  RPC と対応するリンク サーバーにローカル サーバーからの分散クエリで使用するためのリンク サーバー ログイン マッピングごとに 1 行を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|内のサーバーの ID **sys.servers**します。|  
|**local_principal_id**|**int**|マッピングが適用されるサーバー プリンシパル。<br /><br /> 0 = ワイルドカードまたは public。|  
|**uses_self_credential**|**bit**|1 の場合、マッピングはセッションは独自の資格情報を使用する必要がありますを示しますそれ以外の場合、0 では、セッションで提供される名前とパスワードを使用することを示します。|  
|**remote_name**|**sysname**|接続時に使用するリモート ユーザー名。 パスワードも格納されているがカタログ ビューのインターフェイスでは公開されません。|  
|**modify_date**|**datetime**|リンク ログインが最後に変更された日付。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [リンク サーバーのカタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)  
  
  
