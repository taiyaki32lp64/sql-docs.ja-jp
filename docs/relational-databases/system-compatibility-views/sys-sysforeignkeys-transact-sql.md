---
title: sys.sysforeignkeys (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysforeignkeys
- sys.sysforeignkeys
- sys.sysforeignkeys_TSQL
- sysforeignkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysforeignkeys system table
- sys.sysforeignkeys compatibility view
ms.assetid: 41544236-1c46-4501-be88-18c06963b6e8
author: rothja
ms.author: jroth
ms.openlocfilehash: acbf543abeb8e35adb506e1fb381d2fa2018f113
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053452"
---
# <a name="syssysforeignkeys-transact-sql"></a>sys.sysforeignkeys (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  データベース中のテーブルの定義内にある、FOREIGN KEY 制約に関する情報を保持します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|FOREIGN KEY 制約の ID。|  
|**fkeyid**|**int**|FOREIGN KEY 制約を持つテーブルのオブジェクト ID。|  
|**rkeyid**|**int**|FOREIGN KEY 制約で参照されるテーブルのオブジェクト ID。|  
|**fkey**|**smallint**|参照元の列の ID。|  
|**rkey**|**smallint**|参照先の列の ID。|  
|**keyno**|**smallint**|参照列リスト内の列の位置。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビューへのシステム テーブルのマッピング&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
