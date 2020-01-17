---
title: managed_backup.fn_is_master_switch_on (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_is_master_switch_on
- fn_is_master_switch_on_TSQL
- smart_admin.fn_is_master_switch_on
- smart_admin.fn_is_master_switch_on_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_is_master_switch_on
- fn_is_master_switch_on
ms.assetid: e8c2108d-b104-46cb-9645-a15f46112c86
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 044cdc1b334732a0730cd2c223d5690e4089a0cf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140644"
---
# <a name="managedbackupfnismasterswitchon-transact-sql"></a>managed_backup.fn_is_master_switch_on (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  SQL Server のインスタンスにおける [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]操作の状態を返します。  
  
 この関数を使用すると、[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の現在の状態を取得できます。  
  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
managed_backup.fn_is_master_switch_on ()  
```  
  
##  <a name="Arguments"></a> 引数  
 なし  
  
## <a name="return-type"></a>戻り値の型  
 **BIT**  
  
 1 = [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]はアクティブです。0 = [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]は一時停止しています。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 この関数に対する SELECT 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [Microsoft Azure への SQL Server マネージド バックアップ](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
