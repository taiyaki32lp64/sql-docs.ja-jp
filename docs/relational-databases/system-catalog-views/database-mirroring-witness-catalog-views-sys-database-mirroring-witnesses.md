---
title: sys.database_mirroring_witnesses (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring_witnesses
- sys.database_mirroring_witnesses_TSQL
- database_mirroring_witnesses
- database_mirroring_witnesses_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], catalog views
- sys.database_mirroring_witnesses catalog view
- witness [SQL Server], sys.database_mirroring_witnesses catalog view
ms.assetid: 0dd5b794-733b-4a3c-b5a4-62f9f1f0f22d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 10fbd3ac410ee5b6944ffe7b32285008f8b11776
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033081"
---
# <a name="database-mirroring-witness-catalog-views---sysdatabasemirroringwitnesses"></a>データベース ミラーリング監視サーバーのカタログ ビュー - sys.database_mirroring_witnesses
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  サーバーがデータベース ミラーリング パートナーシップで果たすすべてのミラーリング監視ロールの行を格納します。 
  
  データベース ミラーリング セッションで、自動フェールオーバーを行うには、ミラーリング監視サーバーが必要です。 理想的には、ミラーリング監視サーバーは、プリンシパルとミラーの両方のサーバーから別のコンピューターに存在します。 ミラーリング監視サーバーには、データベースを操作は行いません。 代わりに、プリンシパルとミラー サーバーの状態を監視します。 プリンシパル サーバーが失敗した場合、ミラーリング監視サーバーがミラー サーバーへの自動フェールオーバーを開始できます。 
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|データベース ミラーリング セッションで、データベースの 2 つのコピーの名前です。|  
|**principal_server_name**|**sysname**|現在データベースのコピーがプリンシパル データベースとなっているパートナー サーバーの名前。|  
|**mirror_server_name**|**sysname**|データベースのコピーがミラー データベースでは現在、パートナー サーバーの名前です。|  
|**safety_level**|**tinyint**|ミラー データベースの更新に関するトランザクションの安全性設定:<br /><br /> 0 = 状態不明<br /><br /> 1 = オフ (非同期)<br /><br /> 2 = 完全 (同期)<br /><br /> 自動フェールオーバーに対してミラーリング監視サーバーを使用する場合は、トランザクションの安全性が「完全」であること必要です。また、「完全」は既定の設定になっています。|  
|**safety_level_desc**|**nvarchar(60)**|安全性の説明は、ミラー データベースで更新プログラムの保証します。<br /><br /> UNKNOWN<br /><br /> OFF<br /><br /> FULL|  
|**safety_sequence_number**|**int**|更新シーケンス番号の変更を**safety_level**します。|  
|**role_sequence_number**|**int**|ミラーリング パートナーによって実行されるプリンシパル/ミラー ロールには、変更のシーケンス番号を更新します。|  
|**mirroring_guid**|**uniqueidentifier**|ミラーリング パートナーシップの識別子です。|  
|**family_guid**|**uniqueidentifier**|データベースのバックアップ ファミリの識別子です。 一致する復元状態を検出するために使用します。|  
|**is_suspended**|**bit**|データベース ミラーリングが一時中断していることを示す値。|  
|**is_suspended_sequence_number**|**int**|設定のシーケンス番号**is_suspended**します。|  
|**partner_sync_state**|**tinyint**|ミラーリング セッションの同期状態:<br /><br /> 5 = パートナーが同期されています。 フェールオーバーは、可能性のある可能性があります。 フェールオーバーでは、「要件について[ロールの切り替え中にデータベース ミラーリング セッション&#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)します。<br /><br /> 6 = パートナーが同期されていません。 フェールオーバーは不可能なようになりました。|  
|**partner_sync_state_desc**|**nvarchar(60)**|ミラーリング セッションの同期状態の説明 :<br /><br /> SYNCHRONIZED<br /><br /> 同期されていません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [データベース ミラーリング監視サーバー](../../database-engine/database-mirroring/database-mirroring-witness.md)   
 [sys.database_mirroring &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよくあるご質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
