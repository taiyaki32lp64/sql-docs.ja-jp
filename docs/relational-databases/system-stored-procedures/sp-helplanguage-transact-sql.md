---
title: sp_helplanguage (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helplanguage
- sp_helplanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplanguage
- default languages
ms.assetid: 8c4651a5-7dbc-49c5-8691-dc72103c2dfa
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d46e178fc1872a84bb573f16629803c59f2fb6c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122509"
---
# <a name="sphelplanguage-transact-sql"></a>sp_helplanguage (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] での特定の代替言語、またはすべての言語に関する情報を報告します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helplanguage [ [ @language = ] 'language' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @language = ] 'language'` 情報を表示する代替言語の名前です。 *言語*は**sysname**、既定値は NULL です。 場合*言語*が指定すると、指定した言語に関する情報が返されます。 言語が指定されていない場合は、すべての言語については、 **sys.syslanguages**互換性ビューが返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**langid**|**smallint**|言語 ID 番号です。|  
|**dateformat**|**nchar(3)**|日付の形式です。|  
|**datefirst**|**tinyint**|週の最初の曜日:1 は月曜、7 の日曜日、火曜日の場合は 2 です。|  
|**upgrade**|**int**|この言語を使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の最新アップグレード バージョンです。|  
|**name**|**sysname**|言語の名前。|  
|**alias**|**sysname**|言語の別名です。|  
|**months**|**nvarchar(372)**|月の名前。|  
|**shortmonths**|**nvarchar(132)**|月の短縮名です。|  
|**days**|**nvarchar(217)**|曜日です。|  
|**lcid**|**int**|言語の Windows ロケール ID。|  
|**msglangid**|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メッセージ グループ id。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-information-about-a-single-language"></a>A. 1 つの言語に関する情報を返す  
 次の例では、代替言語に関する情報を表示する`French`します。  
  
```  
sp_helplanguage French;  
```  
  
### <a name="b-returning-information-about-all-languages"></a>B. すべての言語に関する情報を返す  
 次の例では、インストールされているすべての代替言語に関する情報を表示します。  
  
```  
sp_helplanguage;  
```  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジン ストアド プロシージャ&#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [SET LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
