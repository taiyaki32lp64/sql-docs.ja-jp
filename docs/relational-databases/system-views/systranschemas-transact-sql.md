---
title: systranschemas (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- systranschemas
- systranschemas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- systranschemas system table
ms.assetid: 864c3966-cb61-4f2b-8939-ccda112de853
author: stevestein
ms.author: sstein
ms.openlocfilehash: e2a80729738986d69f2eb78b16d119072d6e9e11
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094755"
---
# <a name="systranschemas-transact-sql"></a>systranschemas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Systranschemas**トランザクションまたはスナップショット パブリケーションでパブリッシュされたアーティクルのスキーマ変更を追跡するテーブルを使用します。 このテーブルは、publication データベースと subscription データベースの両方に保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**tabid**|**int**|スキーマの変更が発生したテーブル アーティクルを識別します。|  
|**startlsn**|**binary**|スキーマ変更開始時の LSN 値です。|  
|**endlsn**|**binary**|スキーマ変更の最後の LSN 値です。|  
|**typeid**|**int**|スキーマ変更のタイプです。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
