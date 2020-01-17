---
title: sys.sp_rda_set_rpo_duration (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_rpo_duration
- sys.sp_rda_set_rpo_duration_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_rpo_duration stored procedure
ms.assetid: 95c80c5b-9252-4612-9ea7-544c48834fd2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 12d703b03483e1ea4641a822291106de3598f05e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905008"
---
# <a name="syssprdasetrpoduration-transact-sql"></a>sys.sp_rda_set_rpo_duration (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  ポイントイン タイム リストアが必要な場合、リモート Azure データベースの完全復元をことを確認するためにステージング テーブルでは、SQL Server を保持する移行されたデータの時間数を設定します。    
    
 詳細については、次を参照してください。 [Stretch Database は、移行済みの行を一時的に保持して、Azure のデータのデータ損失のリスクを軽減](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md#stretchRPO)します。  
   
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
     
## <a name="syntax"></a>構文    
    
```    
    
sp_rda_set_rpo_duration [ @duration_hrs = ] duration_hrs    
    
```    
    
## <a name="arguments"></a>引数    
 [ @duration_hrs = ] *duration_hrs*    
 時間数です (null 以外の整数値) の現在の Stretch 対応データベースを保持する SQL Server に必要なデータを移行します。 既定値と最小値は、8 時間です。    
 
 > [!NOTE]
 > 大きい値には、SQL Server の記憶領域が必要です。
    
## <a name="permissions"></a>アクセス許可    
 Db_owner アクセス許可が必要です。    
    
## <a name="remarks"></a>コメント    
 実行して、現在の値を取得[sys.sp_rda_get_rpo_duration &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)します。    
    
## <a name="see-also"></a>参照    
 [sys.sp_rda_get_rpo_duration &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-get-rpo-duration-transact-sql.md)     
 [Stretch 対応データベース (Stretch Database) の復元します。](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)     
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)    
    
  
