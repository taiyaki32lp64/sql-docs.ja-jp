---
title: restorehistory (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- restorehistory
- restorehistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restorehistory system table
ms.assetid: 9140ecc1-d912-4d76-ae70-e2a857da6d44
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1565adfedca53dfe6e9ddf66af559adff23337d7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910148"
---
# <a name="restorehistory-transact-sql"></a>restorehistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  復元操作ごとに 1 行のデータを格納します。 このテーブルに格納されます、 **msdb**データベース。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|各復元操作を識別する一意の識別番号。 ID、主キー。|  
|**restore_date**|**datetime**|復元操作の開始の日時。 NULL にすることができます。|  
|**destination_database_name**|**nvarchar(128)**|復元操作の転送先データベースの名前。 NULL にすることができます。|  
|**user_name**|**nvarchar(128)**|復元操作を実行したユーザーの名前です。 NULL にすることができます。|  
|**backup_set_id**|**int**|復元されるバックアップ セットを識別する一意な識別番号。 参照**backupset (backup_set_id)** します。|  
|**restore_type**|**char(1)**|復元操作の種類。<br /><br /> D = データベース<br /><br /> F = ファイル<br /><br /> G = ファイル グループ<br /><br /> I = 差分<br /><br /> L = ログ<br /><br /> V = Verifyonly<br /><br /> NULL にすることができます。|  
|**replace**|**bit**|復元操作に REPLACE オプションが指定されているかどうかを示します。<br /><br /> 1 = 指定しました。<br /><br /> 0 = 指定なし<br /><br /> NULL にすることができます。<br /><br /> データベースは、データベース スナップショットに戻す、ときに 0 が唯一のオプションを使用します。|  
|**復旧 (recovery)**|**bit**|復元操作に RECOVERY または NORECOVERY オプションが指定されたかどうか。<br /><br /> 1 = 回復<br /><br /> NULL にすることができます。<br /><br /> データベースは、データベース スナップショットに戻す、ときに 1、唯一のオプションです。<br /><br /> 0 = NORECOVERY|  
|**restart**|**bit**|復元操作に RESTART オプションが指定されたかどうかを示します。<br /><br /> 1 = 指定しました。<br /><br /> 0 = 指定なし<br /><br /> NULL にすることができます。<br /><br /> データベースは、データベース スナップショットに戻す、ときに 0 が唯一のオプションを使用します。|  
|**stop_at**|**datetime**|データベースの復旧時間にポイントします。 NULL にすることができます。|  
|**device_count**|**tinyint**|復元操作に関係したデバイスの数。 この数には、バックアップのメディア ファミリ数よりも少ないを指定できます。 NULL にすることができます。<br /><br /> データベースは、データベース スナップショットに戻す、ときに、数は常に 1 にします。|  
|**stop_at_mark_name**|**nvarchar(128)**|名前付きマークを含むトランザクションへの復旧。 NULL にすることができます。<br /><br /> データベースをデータベース スナップショットに戻す場合、この値は NULL になります。|  
|**stop_before**|**bit**|名前付きマークを含むトランザクションが復旧に含まれていたかどうかを示します。<br /><br /> 0 = マーク付きトランザクションの前に、で復旧中止します。<br /><br /> 1 = マーク付きのトランザクションも復旧された。<br /><br /> NULL にすることができます。<br /><br /> データベースをデータベース スナップショットに戻す場合、この値は NULL になります。|  
  
## <a name="remarks"></a>コメント  
 このテーブルおよびその他のバックアップと履歴テーブルの行の数を減らすためには、実行、 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)ストアド プロシージャ。  
  
## <a name="see-also"></a>参照  
 [バックアップし、復元テーブル&#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefile &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/restorefile-transact-sql.md)   
 [restorefilegroup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [システム テーブル &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
