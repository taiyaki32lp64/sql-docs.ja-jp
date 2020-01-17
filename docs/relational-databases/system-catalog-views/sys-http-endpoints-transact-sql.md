---
title: sys.http_endpoints (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.http_endpoints
- http_endpoints
- sys.http_endpoints_TSQL
- http_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.http_endpoints catalog view
ms.assetid: 16f59695-ecd9-457e-8874-055af63f8ea7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 41ca717399a3cd86f2137de6ae474d89e3eb819e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122732"
---
# <a name="syshttp_endpoints-transact-sql"></a>sys.http_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  HTTP プロトコルを使用するサーバー内で作成されたエンドポイントごとに 1 行のデータを保持します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**< 継承された列 >**||列を継承[sys.endpoints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)します。|  
|**site**|**nvarchar(128)**|サイトのホスト コンピューターの名前、サイトで指定されているオプションを = です。|  
|**url_path**|**nvarchar (4000)**|この HTTP エンドポイントの URL のパスのみの部分のパスで指定されたオプションを = です。|  
|**is_clear_port_enabled**|**bit**|1 = クリア ポートはポートを使用して有効になっている = CLEAR オプション。|  
|**clear_port**|**int**|CLEAR PORT = オプションで指定されたポート番号です。<br /><br /> NULL = 指定されていません。|  
|**is_ssl_port_enabled**|**bit**|1 = SSL ポートはポートを使用して有効になっている = SSL オプション。|  
|**ssl_port**|**int**|SSL PORT = オプションで指定されたポート番号値です。<br /><br /> NULL = 指定されていません。|  
|**is_anonymous_enabled**|**bit**|1 = 匿名アクセスは、認証を使用して有効になっている = 匿名オプション。|  
|**is_basic_auth_enabled**|**bit**|1 = basic 認証は、認証を使用して有効になっている = BASIC オプション。|  
|**is_digest_auth_enabled**|**bit**|1 = ダイジェスト認証は、AUTHENTICATION = DIGEST オプションを使用して有効になっています。|  
|**is_kerberos_auth_enabled**|**bit**|1 = 統合認証は、AUTHENTICATION = KERBEROS オプションを使用して有効になっています。|  
|**is_ntlm_auth_enabled**|**bit**|1 = 統合認証の認証を使用して有効になっている = NTLM オプション。|  
|**is_integrated_auth_enabled**|**bit**|1 = 統合認証は、認証を使用して有効になっている = INTEGRATED オプション。|  
|**authorization_realm**|**nvarchar(128)**|HTTP DIGEST 認証の試行の一部としてクライアントに返されるヒントです。 AUTH REALM オプションの値です。<br /><br /> 指定されていない場合、または DIGEST 認証が有効になっていない場合、NULL です。|  
|**default_logon_domain**|**nvarchar(128)**|既定のログイン ドメイン基本認証を有効にした場合。 DEFAULT LOGON DOMAIN オプションの値です。<br /><br /> 指定されていない場合は NULL または基本認証が有効でないかどうかです。|  
|**is_compression_enabled**|**bit**|1 = COMPRESSION = ENABLED オプションが設定されています。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [エンドポイントのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  
  
  
