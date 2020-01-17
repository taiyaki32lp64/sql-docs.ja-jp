---
title: MSreplication_options (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSreplication_options
- MSreplication_options_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_options system table
ms.assetid: 23cf10d7-8bc1-4368-b5eb-e5576421e776
author: stevestein
ms.author: sstein
ms.openlocfilehash: c48a57b876cde41d6bb514c522bcaa241eec11fd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063004"
---
# <a name="msreplication_options-transact-sql"></a>MSreplication_options (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]


  **MSreplication_options** テーブルには、レプリケーションで内部的に使用されるメタデータが格納されます。 このテーブルは **master** データベースに保存されます。

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|内部使用のみです。|  
|**value**|**bit**|内部使用のみです。|  
|**major_version**|**int**|内部使用のみです。|  
|**minor_version**|**int**|内部使用のみです。|  
|**revision**|**int**|内部使用のみです。|  
|**install_failures**|**int**|内部使用のみです。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
