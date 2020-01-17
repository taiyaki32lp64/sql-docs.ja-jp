---
title: sys.soap_endpoints (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- soap_endpoints_TSQL
- sys.soap_endpoints
- soap_endpoints
- sys.soap_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.soap_endpoints catalog view
ms.assetid: f50dcbfc-02ed-4a19-9c07-c78a5a1b3224
author: stevestein
ms.author: sstein
ms.openlocfilehash: f7081d96d996d33bbabedd13201d7b0fa2547563
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078669"
---
# <a name="syssoapendpoints-transact-sql"></a>sys.soap_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 SOAP 型ペイロードを扱うサーバーのエンドポイントごとに 1 行のデータを格納します。 このビューですべての行については、同じ行に対応**endpoint_id**で、 **sys.http_endpoints**カタログ ビューに、HTTP 構成メタデータが含まれます。  
  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**< 継承された列 >**||このビューが継承する列の一覧は、次を参照してください。 [sys.endpoints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)します。|  
|**is_sql_language_enabled**|**bit**|1 は、BATCHES = ENABLED オプションが指定されていることを示します。エンドポイントでアドホック SQL バッチが許可されます。|  
|**wsdl_generator_procedure**|**nvarchar(776)**|このメソッドを実装するストアド プロシージャの、3 つの要素で構成される名前。<br /><br /> メソッドの名前は、3 つの要素で構成する必要があります。 1 つの要素、2 つの要素、または 4 つの要素で構成される名前は許可されません。|  
|**default_database**|**sysname**|DATABASE = オプションで指定される、既定のデータベースの名前。<br /><br /> NULL = DEFAULT が指定されています。|  
|**default_namespace**|**nvarchar(384)**|名前空間で指定された既定の名前空間 = オプション、または`https://tempuri.org`既定値が代わりに指定されている場合。|  
|**default_result_schema**|**tinyint**|SCHEMA = オプションの既定値。<br /><br /> 0 = NONE<br /><br /> 1 = STANDARD|  
|**default_result_schema_desc**|**nvarchar(60)**|SCHEMA = オプションの既定値の説明。<br /><br /> なし<br /><br /> STANDARD|  
|**is_xml_charset_enforced**|**bit**|0 は、CHARACTER_SET = SQL オプションが指定されていることを示します。<br /><br /> 1 は、CHARACTER_SET = XML オプションが指定されていることを示します。|  
|**is_session_enabled**|**bit**|0 は、SESSION = DISABLE オプションが指定されていることを示します。<br /><br /> 1 は、SESSION = ENABLED オプションが指定されていることを示します。|  
|**session_timeout**|**int**|SESSION_TIMEOUT オプションで指定された値。|  
|**login_type**|**nvarchar(60)**|エンドポイントで許可される認証の種類。<br /><br /> WINDOWS<br /><br /> MIXED|  
|**header_limit**|**int**|SOAP ヘッダーの最大許容サイズ。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エンドポイントのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
