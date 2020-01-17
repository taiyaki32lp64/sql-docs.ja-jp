---
title: backupmediaset (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupmediaset
- backupmediaset_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], backupmediaset system table
- backupmediaset system table
ms.assetid: d9c18a93-cab9-4db8-ae09-c6bd8145ab8f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1dbaf429acb94334540f0e147eae2808e1655309
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119354"
---
# <a name="backupmediaset-transact-sql"></a>backupmediaset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  バックアップ メディア セットごとに 1 行のデータを格納します。 このテーブルに格納されます、 **msdb**データベース。  
 
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|一意なメディア セット識別番号です。 ID、主キー。|  
|**media_uuid**|**uniqueidentifier**|メディア セットの UUID。 すべて[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メディア セットは UUID があります。<br /><br /> 以前のバージョンの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、ただし、メディア セットには、1 つだけのメディア ファミリが含まれている場合、 **media_uuid**列は NULL になります (**media_family_count**は 1)。|  
|**media_family_count**|**tinyint**|メディア セット内のメディア ファミリの数。 NULL にすることができます。|  
|**name**|**nvarchar(128)**|メディア セットの名前。 NULL にすることができます。<br /><br /> 詳細についてを参照してください MEDIANAME と MEDIADESCRIPTION[バックアップ&#40;TRANSACT-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)します。|  
|**description**|**nvarchar (255)**|メディア セットの説明。 NULL にすることができます。<br /><br /> 詳細についてを参照してください MEDIANAME と MEDIADESCRIPTION[バックアップ&#40;TRANSACT-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)します。|  
|**software_name**|**nvarchar(128)**|メディア ラベルを作成したバックアップ ソフトウェアの名前。 NULL にすることができます。|  
|**software_vendor_id**|**int**|バックアップ メディア ラベルを記述したソフトウェア ベンダーの識別番号。 NULL にすることができます。<br /><br /> 値は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は 16 進数の 0x1200 です。|  
|**MTF_major_version**|**tinyint**|メジャー バージョン番号の[!INCLUDE[msCoName](../../includes/msconame-md.md)]Tape Format は、このメディア セットの生成に使用します。 NULL にすることができます。|  
|**mirror_count**|**tinyint**|メディア セット内のミラーの数。|  
|**is_password_protected**|**bit**|メディアはパスワードで保護を設定します。<br /><br /> 0 = 保護されていない<br /><br /> 1 = 保護されている|  
|**is_compressed**|**bit**|バックアップが圧縮されているかどうか。<br /><br /> 0 = 非圧縮<br /><br /> 1 = 圧縮<br /><br /> 中に、 **msdb**アップグレードすると、この値は NULL に設定するされます。 これは圧縮されていないバックアップを示します。|  
|**is_encrypted**|**Bit**|バックアップが暗号化されているかどうか。<br /><br /> 0 = 暗号化なし<br /><br /> 1 = 暗号化|  
  
## <a name="remarks"></a>コメント  
 RESTORE VERIFYONLY FROM *backup_device* WITH LOADHISTORY の列に設定、 **backupmediaset**メディア セット ヘッダーから適切な値を持つテーブル。  
  
 このテーブルおよびその他のバックアップと履歴テーブルの行の数を減らすためには、実行、 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)ストアド プロシージャ。  
  
## <a name="see-also"></a>参照  
 [バックアップし、復元テーブル&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [システム テーブル &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
