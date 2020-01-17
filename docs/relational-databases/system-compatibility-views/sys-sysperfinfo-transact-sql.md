---
title: sys.sysperfinfo (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysperfinfo_TSQL
- sys.sysperfinfo_TSQL
- sys.sysperfinfo
- sysperfinfo
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysperfinfo compatibility view
- sysperfinfo system table
ms.assetid: e22a81cd-27de-4690-9443-6aad6393bd3c
author: rothja
ms.author: jroth
ms.openlocfilehash: e6ce86e7be7d54e95c2336691b53ea12ff0d8575
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076505"
---
# <a name="syssysperfinfo-transact-sql"></a>sys.sysperfinfo (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  含まれています、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] Windows システム モニターで表示できる内部パフォーマンス カウンターの表現。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|パフォーマンス オブジェクト名など**SQLServer:LockManager**または**SQLServer:BufferManager**します。|  
|**counter_name**|**nchar(128)**|オブジェクト内のパフォーマンス カウンターの名前など**ページ要求**または**Locks Requested**します。|  
|**instance_name**|**nchar(128)**|カウンターの名前付きインスタンス。 たとえばなど、ロックの種類ごとに保持されるカウンターは**テーブル**、**ページ**、**キー**など。 類似したカウンターはインスタンス名で区別されます。|  
|**cntr_value**|**bigint**|実際のカウンター値。 多くの場合、これは、インスタンス イベントの発生数を表すレベルまたは単純増加のカウンターになります。|  
|**cntr_type**|**int**|Windows パフォーマンス アーキテクチャによって定義されているカウンターのタイプします。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビューへのシステム テーブルのマッピング&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
