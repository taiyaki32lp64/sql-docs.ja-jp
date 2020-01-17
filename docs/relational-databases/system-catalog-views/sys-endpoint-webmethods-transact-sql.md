---
title: sys.endpoint_webmethods (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.endpoint_webmethods_TSQL
- sys.endpoint_webmethods
- endpoint_webmethods_TSQL
- sys.http_soap_methods_TSQL
- endpoint_webmethods
- sys.http_soap_methods
dev_langs:
- TSQL
helpviewer_keywords:
- sys.endpoint_webmethods catalog view
ms.assetid: 7dad0cf6-eafa-47cf-98cc-75ba8d3c7959
author: stevestein
ms.author: sstein
ms.openlocfilehash: 14e3534671cc36d8c2cac46f627d158056f985e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079253"
---
# <a name="sysendpoint_webmethods-transact-sql"></a>sys.endpoint_webmethods (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 SOAP 対応 HTTP エンドポイントで定義された FOR EACH SOAP メソッドの行が含まれています。 Endpoint_id と名前空間列の組み合わせは一意にです。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|endpoint_id|**int**|Web メソッドが定義されているエンドポイントの ID です。|  
|namespace|**nvarchar(384)**|Web メソッドの Namespace です。|  
|method_alias|**nvarchar(64)**|メソッドの別名です。<br /><br /> 注:[!INCLUDE[tsql](../../includes/tsql-md.md)]識別子は、WSDL メソッド名では無効な文字を許可します。<br /><br /> 実際の基になるエンドポイントの WSDL の説明で公開されている名前にマップするエイリアスが使用される[!INCLUDE[tsql](../../includes/tsql-md.md)]web メソッドが呼び出されたときに呼び出される実行可能オブジェクト。|  
|object_name|**nvarchar(776)**|NAME = オプションで指定された、Web メソッドのリダイレクト先のオブジェクト名です。 名前の部分がピリオド (.) で区切られ、角かっこを使用して区切られた`[``]`します。<br /><br /> オブジェクト名は WSDL オプションで指定されている、3 つの部分から成る名前でなければなりません。|  
|result_schema|**tinyint**|XSD (ある場合) を応答と共に返送するかどうかを指定するオプションです。<br /><br /> 0 = なし<br /><br /> 1 = 標準<br /><br /> 2 = 既定値|  
|result_schema_desc|**nvarchar(60)**|XSD (ある場合) を応答と共に返送するかどうかを指定するオプションの説明です。<br /><br /> なし<br /><br /> STANDARD<br /><br /> DEFAULT|  
|result_format|**tinyint**|応答において結果をどのようにフォーマットするかを指定するオプションです。<br /><br /> 1 = ALL_RESULTS<br /><br /> 2 = ROWSETS_ONLY<br /><br /> 3 = なし|  
|result_format_desc|**nvarchar(60)**|応答において結果をフォーマットする方法を決定するオプションの説明です。<br /><br /> ALL_RESULTS<br /><br /> ROWSETS_ONLY<br /><br /> なし|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [エンドポイントのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
