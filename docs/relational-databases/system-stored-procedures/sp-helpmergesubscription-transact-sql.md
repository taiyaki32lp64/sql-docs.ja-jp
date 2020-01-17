---
title: sp_helpmergesubscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergesubscription
- sp_helpmergesubscription_TSQL
helpviewer_keywords:
- sp_helpmergesubscription
ms.assetid: da564112-f769-4e67-9251-5699823e8c86
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0e5f044482d3e46e4e20279a437b8d9459d1d3bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002644"
---
# <a name="sp_helpmergesubscription-transact-sql"></a>sp_helpmergesubscription (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  情報を返します、マージ パブリケーションに対するサブスクリプションでは、プッシュし、プルの両方。 このストアド プロシージャは、パブリッシャー、パブリケーション データベースに対して、またはサブスクリプション データベースに対して再パブリッシュ サブスクライバーで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpmergesubscription [ [ @publication=] 'publication']  
    [ , [ @subscriber=] 'subscriber']  
    [ , [ @subscriber_db=] 'subscriber_db']  
    [ , [ @publisher=] 'publisher']  
    [ , [ @publisher_db=] 'publisher_db']  
    [ , [ @subscription_type=] 'subscription_type']  
    [ , [ @found=] 'found' OUTPUT]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前です。 *パブリケーション*は**sysname**、既定値は **%** します。 パブリケーションは既に存在し、識別子の規則に準拠している必要があります。 NULL の場合、または **%** 、すべてのマージ パブリケーションと、現在のデータベース内のサブスクリプションに関する情報が返されます。  
  
`[ @subscriber = ] 'subscriber'` サブスクライバーの名前です。 *サブスクライバー*は**sysname**、既定値は **%** します。 場合は NULL または %、指定したパブリケーションへのすべてのサブスクリプションに関する情報が返されます。  
  
`[ @subscriber_db = ] 'subscriber_db'` サブスクリプション データベースの名前です。 *subscriber_db*は **sysname**、既定値は **%** 、すべてのサブスクリプション データベースに関する情報が返されます。  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前です。 パブリッシャーは、有効なサーバーである必要があります。 *パブリッシャー*は**sysname**、既定値は **%** 、すべてのパブリッシャーに関する情報が返されます。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシャー データベースの名前です。 *publisher_db*は**sysname**、既定値は **%** 、すべてのパブリッシャー データベースに関する情報が返されます。  
  
`[ @subscription_type = ] 'subscription_type'` サブスクリプションの種類です。 *subscription_type*は**nvarchar (15)** 、これらの値のいずれかを指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**push**(既定値)|プッシュ サブスクリプション|  
|**pull**|プル サブスクリプション|  
|**both**|プッシュおよびプル サブスクリプションの両方|  
  
`[ @found = ] 'found'OUTPUT` 行を返すことを示すフラグ。 *見つかった*は**int**は出力パラメーター、既定値は NULL です。 **1**パブリケーションが見つかったことを示します。 **0**パブリケーションが見つからないことを示します。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**sysname**|サブスクリプションの名前。|  
|**publication**|**sysname**|パブリケーションの名前。|  
|**publisher**|**sysname**|パブリッシャーの名前。|  
|**publisher_db**|**sysname**|パブリッシャー データベースの名前です。|  
|**subscriber**|**sysname**|サブスクライバーの名前。|  
|**subscriber_db**|**sysname**|サブスクリプション データベースの名前。|  
|**status**|**int**|サブスクリプションの状態:<br /><br /> **0** = すべてのジョブが起動待ち<br /><br /> **1** = 1 つ以上のジョブが起動中<br /><br /> **2** = すべてのジョブが正常に実行されました<br /><br /> **3** = 少なくとも 1 つジョブが実行中<br /><br /> **4** = すべてのジョブがスケジュールされ、アイドル状態<br /><br /> **5** = 少なくとも 1 つジョブが前回のエラーの後に実行しようとしています<br /><br /> **6** = 少なくとも 1 つが正常に実行するジョブが失敗しました|  
|**subscriber_type**|**int**|サブスクライバーの種類。|  
|**subscription_type**|**int**|サブスクリプションの種類。<br /><br /> **0**プッシュを =<br /><br /> **1** = プル<br /><br /> **2** = 両方|  
|**priority**|**float(8)**|サブスクリプションの優先度を示す数値です。|  
|**sync_type**|**tinyint**|サブスクリプションの同期の種類。|  
|**description**|**nvarchar (255)**|マージ サブスクリプションの簡単な説明。|  
|**merge_jobid**|**binary(16)**|マージ エージェントのジョブ ID。|  
|**full_publication**|**tinyint**|完全またはフィルター選択されたパブリケーション サブスクリプションであるかどうか。|  
|**offload_enabled**|**bit**|レプリケーション エージェントのオフロードするために、サブスクライバーで実行設定されているかどうかを指定します。 NULL の場合、パブリッシャー側で実行されます。|  
|**offload_server**|**sysname**|エージェントが動作しているサーバーの名前。|  
|**use_interactive_resolver**|**int**|調整時に対話型の競合回避モジュールを使用するかどうかを示します。 場合**0**、インタラクティブ競合回避モジュールを使用しません。|  
|**hostname**|**sysname**|値によってサブスクリプションがフィルター選択するときに指定された値、 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)関数。|  
|**subscriber_security_mode**|**smallint**|セキュリティ モードをサブスクライバーで、場所**1** Windows 認証では、ことを意味と**0**意味[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。|  
|**subscriber_login**|**sysname**|サブスクライバーのログイン名です。|  
|**subscriber_password**|**sysname**|実際のサブスクライバー パスワードは返されません。 によってマスクされる結果は、" **\*\*\*\*\*\*** "文字列。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helpmergesubscription**パブリッシャーまたは再パブリッシュ サブスクライバーで格納されているサブスクリプション情報を返すためにマージ レプリケーションで使用します。  
  
 匿名サブスクリプションの場合、 *subscription_type*値は常に**1** (プル) します。 ただし、実行する必要があります[sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)匿名サブスクリプションに関する情報は、サブスクライバーでします。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロール、 **db_owner**固定データベース ロールまたはサブスクリプションが属しているパブリケーションのパブリケーション アクセス リストが実行できる**sp _helpmergesubscription**します。  
  
## <a name="see-also"></a>関連項目  
 [sp_addmergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
