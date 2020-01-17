---
title: sys.sysdevices (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdevices
- sysdevices_TSQL
- sys.sysdevices
- sys.sysdevices_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysdevices compatibility view
- sysdevices system table
ms.assetid: ac5bcaf4-8fb6-4855-8856-d7643f469361
author: rothja
ms.author: jroth
ms.openlocfilehash: 9cbd14a7ce8dd1cfb1571874a83a615065200014
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053523"
---
# <a name="syssysdevices-transact-sql"></a>sys.sysdevices (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ディスク バックアップ ファイル、テープ バックアップ ファイル、およびデータベース ファイルの 1 つの行が含まれています。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|バックアップ ファイルまたはデータベース ファイルの論理名。|  
|**size**|**int**|2 キロバイト (KB) のページで、ファイルのサイズ。|  
|**low**|**int**|旧バージョンとの互換性のためにだけ用意されています。|  
|**high**|**int**|旧バージョンとの互換性のためにだけ用意されています。|  
|**status**|**smallint**|デバイスの種類を示すビットマップ。<br /><br /> 1 = 既定のディスク<br /><br /> 2 = 物理ディスク<br /><br /> 4 = 論理ディスク<br /><br /> 8 = ヘッダーをスキップ<br /><br /> 16 = バックアップ ファイル<br /><br /> 32 = シリアル書き込み<br /><br /> 4096 = 読み取り専用|  
|**cntrltype**|**smallint**|コント ローラーの種類:<br /><br /> 0 = データベース ファイルの非 CD-ROM<br /><br /> 2 = ディスク バックアップ ファイル<br /><br /> 3-4 = フロッピー ディスク バックアップ ファイル<br /><br /> 5 = テープ バックアップ ファイル<br /><br /> 6 = 名前付きパイプ ファイル|  
|**phyname**|**nvarchar(260)**|物理ファイルの名前。|  
  
## <a name="see-also"></a>関連項目  
 [システム ビューへのシステム テーブルのマッピング&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
