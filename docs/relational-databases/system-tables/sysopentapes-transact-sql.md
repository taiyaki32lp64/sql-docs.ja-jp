---
title: sysopentapes (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysopentapes
- sysopentapes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], sysopentapes system table
- sysopentapes system table
ms.assetid: c066ca9b-9cfd-46b1-90a3-5c8dc9e7b6ae
author: stevestein
ms.author: sstein
ms.openlocfilehash: 813592ffa5b67a4926dff611c2ba0e0faf36d273
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029799"
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在開いているテープ デバイスごとに 1 行のデータを格納します。 このビューは、**マスター**データベース。  
  
> [!IMPORTANT]  
>  このシステム テーブルは、旧バージョンとの互換性のためのビューとして用意されています。 代わりに、使用、 [sys.dm_io_backup_tapes &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md)動的管理ビュー。  
  
> [!NOTE]  
>  削除することはできません、 **sysopentapes**ビュー。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**openTape**|**nvarchar(64)**|開いているテープ デバイスの物理ファイル名。 開くおよびテープ デバイスを解放の詳細については、次を参照してください。[バックアップ&#40;TRANSACT-SQL&#41; ](../../t-sql/statements/backup-transact-sql.md)と[復元&#40;TRANSACT-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)します。|  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーには、サーバーに対する VIEW SERVER STATE 権限が必要があります。  
  
  
