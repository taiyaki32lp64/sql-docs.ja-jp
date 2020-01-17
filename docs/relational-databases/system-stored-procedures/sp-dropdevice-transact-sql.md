---
title: sp_dropdevice (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropdevice_TSQL
- sp_dropdevice
dev_langs:
- TSQL
helpviewer_keywords:
- backup devices [SQL Server], deleting
- sp_dropdevice
ms.assetid: c8b07189-7c35-414b-acc1-45bd6e7e17c3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 998794fd2e5fe5521587ebbb2a88c61c80cff39e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927823"
---
# <a name="spdropdevice-transact-sql"></a>sp_dropdevice (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  インスタンスからデータベース デバイスまたはバックアップ デバイスを削除、[!INCLUDE[ssDEversion2005](../../includes/ssdeversion2005-md.md)]からエントリを削除して**master.dbo.sysdevices**します。  
   
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dropdevice [ @logicalname = ] 'device'   
    [ , [ @delfile = ] 'delfile' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @logicalname = ] 'device'` 記載されているデータベース デバイスまたはバックアップ デバイスの論理名は、 **master.dbo.sysdevices.name**します。 *デバイス*は**sysname**、既定値はありません。  
  
`[ @delfile = ] 'delfile'` 物理バックアップ デバイス ファイルを削除するかどうかを指定します。 *delfile*は**varchar (7)** します。 として指定されている場合**DELFILE**、物理バックアップ デバイス ディスク ファイルは削除されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 **sp_dropdevice**トランザクション内で使用することはできません。  
  
## <a name="permissions"></a>アクセス許可  
 **diskadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、テープ ダンプ デバイス `tapedump1` を[!INCLUDE[ssDE](../../includes/ssde-md.md)]から削除します。  
  
```  
EXEC sp_dropdevice 'tapedump1';  
```  
  
## <a name="see-also"></a>関連項目  
 [バックアップ デバイス &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [バックアップ デバイスの削除&#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_helpdb &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helpdevice &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdevice-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
