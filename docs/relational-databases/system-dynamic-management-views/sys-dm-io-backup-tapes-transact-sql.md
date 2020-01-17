---
title: sys.dm_io_backup_tapes (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_io_backup_tapes
- dm_io_backup_tapes_TSQL
- sys.dm_io_backup_tapes_TSQL
- dm_io_backup_tapes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_backup_tapes dynamic management view
ms.assetid: 2e27489e-cf69-4a89-9036-77723ac3de66
author: stevestein
ms.author: sstein
ms.openlocfilehash: 98902f096bb960436d764416e2563af5056f00dd
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874154"
---
# <a name="sysdm_io_backup_tapes-transact-sql"></a>sys.dm_io_backup_tapes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  テープ デバイスの一覧、およびバックアップのマウント要求の状態を返します。   
 
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**physical_device_name**|**nvarchar(520)**|バックアップを実行できる実際の物理デバイスの名前。 NULL 値は許可されません。|  
|**logical_device_name**|**nvarchar (256)**|ドライブのユーザー指定の名前 ( **sys. backup_devices**)。 ユーザー指定の名前が使用できない場合は NULL です。 NULL 値が許可されます。|  
|**ステータス**|**int**|テープの状態。<br /><br /> 1 = オープン、使用可能<br /><br /> 2 = マウント保留<br /><br /> 3 = 使用中<br /><br /> 4 = 読み込み中<br /><br /> **注:** テープが読み込まれている間 (**status = 4**)、メディアラベルはまだ読み取られていません。 **Media_sequence_number**など、メディアラベルの値をコピーする列には、予測される値が表示されます。これは、テープの実際の値とは異なる場合があります。 ラベルが読み取られた後**status**への変更**3** (使用) 中、メディア ラベル列が読み込まれている実際のテープを反映します。<br /><br /> NULL 値は許可されません。|  
|**status_desc**|**nvarchar(520)**|テープの状態の説明。<br /><br /> AVAILABLE<br /><br /> マウントが保留中です<br /><br /> IN USE<br /><br /> LOADING MEDIA<br /><br /> NULL 値は許可されません。|  
|**mount_request_time**|**datetime**|マウントが要求された時刻。 保留中マウントがない場合は NULL (**status! = 2**)。 NULL 値が許可されます。|  
|**mount_expiration_time**|**datetime**|マウント要求の有効期限が切れる時刻 (タイムアウト)。 保留中マウントがない場合は NULL (**status! = 2**)。 NULL 値が許可されます。|  
|**database_name**|**nvarchar (256)**|このデバイスにバックアップされるデータベース。 NULL 値が許可されます。|  
|**spid**|**int**|セッション ID。 これにより、テープのユーザーが識別されます。 NULL 値が許可されます。|  
|**command**|**int**|バックアップを実行するコマンド。 NULL 値が許可されます。|  
|**command_desc**|**nvarchar(120)**|コマンドの説明です。 NULL 値が許可されます。|  
|**media_family_id**|**int**|メディアファミリのインデックス (1. *..n*)、 *n*は、メディアセット内のメディアファミリの数です。 NULL 値が許可されます。|  
|**media_set_name**|**nvarchar (256)**|メディアセットが作成されたときに、MEDIANAME オプションで指定されたメディアセットの名前 (存在する場合)。 NULL 値が許可されます。|  
|**media_set_guid**|**uniqueidentifier**|メディアセットを一意に識別する識別子。 NULL 値が許可されます。|  
|**media_sequence_number**|**int**|メディアファミリ内のボリュームのインデックス (1. *..n*)。 NULL 値が許可されます。|  
|**tape_operation**|**int**|実行中のテープ操作:<br /><br /> 1 = 読み取り<br /><br /> 2 = 形式<br /><br /> 3 = 初期化<br /><br /> 4 = 追加<br /><br /> NULL 値が許可されます。|  
|**tape_operation_desc**|**nvarchar(120)**|実行中のテープ操作:<br /><br /> READ<br /><br /> FORMAT<br /><br /> INIT<br /><br /> 追記<br /><br /> NULL 値が許可されます。|  
|**mount_request_type**|**int**|マウント要求の種類:<br /><br /> 1 = 特定のテープ。 **Media\*** フィールドで識別されるテープが必要です。<br /><br /> 2 = 次のメディアファミリ。 まだ復元されていない次のメディアファミリが要求されます。 これは、メディアファミリの数よりも多くのデバイスから復元する場合に使用します。<br /><br /> 3 = 後続テープ。 メディア ファミリが拡張され、後続テープが要求されています。<br /><br /> NULL 値が許可されます。|  
|**mount_request_type_desc**|**nvarchar(120)**|マウント要求の種類:<br /><br /> SPECIFIC TAPE<br /><br /> NEXT MEDIA FAMILY<br /><br /> CONTINUATION VOLUME<br /><br /> NULL 値が許可されます。|  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーは、サーバーに対する VIEW SERVER STATE 権限を持っている必要があります。  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [I/O 関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

