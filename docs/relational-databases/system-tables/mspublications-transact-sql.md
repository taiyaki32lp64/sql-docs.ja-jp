---
title: MSpublications (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpublications
- MSpublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublications system table
ms.assetid: 7a0b3457-7265-4f24-a255-7f055d908f20
author: stevestein
ms.author: sstein
ms.openlocfilehash: de4970e82155454b3d05d6200bc7413baca97aef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939010"
---
# <a name="mspublications-transact-sql"></a>MSpublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpublications**テーブルには、パブリッシャーによってレプリケートされるパブリケーションごとに 1 つの行が含まれています。 このテーブルは、ディストリビューション データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|パブリッシャーの ID。|  
|**publisher_db**|**sysname**|パブリッシャー データベースの名前。|  
|**publication**|**sysname**|パブリケーションの名前を指定します。|  
|**publication_id**|**int**|パブリケーションの ID。|  
|**publication_type**|**int**|パブリケーションの種類:<br /><br /> **0** = トランザクション。<br /><br /> **1** = スナップショット。<br /><br /> **2** = マージします。|  
|**thirdparty_flag**|**bit**|パブリケーションがかどうかを示す、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。<br /><br /> **0** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **1**以外のデータ ソースを =[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。|  
|**independent_agent**|**bit**|このパブリケーションに対して、スタンドアロンのディストリビューション エージェントがあるかどうかを示します。|  
|**immediate_sync**|**bit**|同期ファイルが作成またはスナップショット エージェントを実行するたびに再作成するかどうかを示します。|  
|**allow_push**|**bit**|指定したパブリケーションに対してプッシュ サブスクリプションを作成できるかどうかを示します。|  
|**allow_pull**|**bit**|指定したパブリケーションに対してプル サブスクリプションを作成できるかどうかを示します。|  
|**allow_anonymous**|**bit**|指定されたパブリケーションに対して匿名サブスクリプションを作成できるかどうかを示します。|  
|**description**|**nvarchar (255)**|パブリケーションの説明です。|  
|**vendor_name**|**nvarchar(100)**|パブリッシャーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のデータベースの場合の製造元の名前です。|  
|**保有期間**|**int**|パブリケーションの保有期間 (時間) です。|  
|**sync_method**|**int**|同期方法:<br /><br /> **0** = ネイティブ (すべてのテーブルのネイティブ モードの一括コピー出力を生成します)。<br /><br /> **1** = 文字 (すべてのテーブルのキャラクター モードの一括コピー出力を生成します)。<br /><br /> **3** = 同時実行 (すべてのネイティブ モードの一括コピー出力テーブルは、スナップショット時に、テーブルをロックしませんが生成されます)。<br /><br /> **4** = Concurrent_c (すべてのキャラクター モードの一括コピー出力テーブルは、スナップショット時に、テーブルをロックしませんが生成されます)<br /><br /> 値**3**と**4**が使用可能なトランザクション レプリケーションおよびマージ レプリケーションの場合、スナップショット レプリケーションではなく。|  
|**allow_subscription_copy**|**bit**|有効またはこのパブリケーションにサブスクライブするサブスクリプション データベースをコピーする機能を無効にします。 **0**コピーが無効である、ことを意味し、 **1**有効になっていることを意味します。|  
|**thirdparty_options**|**int**|指定するかどうか、パブリケーションのレプリケーション フォルダー内の表示[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]は抑制されます。<br /><br /> **0** = レプリケーション フォルダーに異種パブリケーションを表示[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]します。<br /><br /> **1** = 表示しないレプリケーション フォルダー内に異種パブリケーション[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]します。|  
|**allow_queued_tran**|**bit**|パブリケーションがキュー更新を許可するかどうかを指定します。<br /><br /> **0 =** パブリケーションはキューに置かれた非。<br /><br /> **1** = パブリケーションはキューに配置します。|  
|**options**|**int**|このリリースに関する情報はありません。|  
  
## <a name="see-also"></a>関連項目  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
