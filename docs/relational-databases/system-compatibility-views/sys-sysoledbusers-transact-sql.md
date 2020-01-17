---
title: sys.sysoledbusers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysoledbusers
- sys.sysoledbusers_TSQL
- sysoledbusers
- sysoledbusers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysoledbusers system table
- sys.sysoledbusers compatibility view
ms.assetid: fe924c17-9cad-4b2b-8124-1e0fd82931e3
author: rothja
ms.author: jroth
ms.openlocfilehash: d7c8b97a04e8b9898a9d49a412c5c6e5a2aa910c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076532"
---
# <a name="syssysoledbusers-transact-sql"></a>sys.sysoledbusers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!IMPORTANT]  
>  これは、[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]でシステム テーブルが含まれている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]旧バージョンとの互換性を保つのためのビューとして。 使用することをお勧めします。[カタログ ビュー](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)代わりにします。  
  
 指定したリンク サーバーのユーザーとパスワードのマッピングごとに 1 行のデータを格納します。 **sysoledbusers**に格納されている場合は、**マスター**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**rmtsrvid**|**smallint**|サーバーのセキュリティ識別番号 (SID)。|  
|**rmtloginame**|**nvarchar(** 128 **)**|リモート ログインの名前を**loginsid**マップのリンクされた**rmtservid**します。|  
|**rmtpassword**|**nvarchar(** 128 **)**|NULL を返します。|  
|**loginsid**|**varbinary(** 85 **)**|マップするローカル ログインの SID。|  
|**status**|**smallint**|1 の場合、マッピングは、ユーザーの資格情報を使用する必要があります。|  
|**changedate**|**datetime**|マッピング情報が最後に変更された日付。|  
  
## <a name="see-also"></a>関連項目  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
