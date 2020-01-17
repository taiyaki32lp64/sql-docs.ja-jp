---
title: sp_helpmergepullsubscription (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepullsubscription
- sp_helpmergepullsubscription_TSQL
helpviewer_keywords:
- sp_helpmergepullsubscription
ms.assetid: 6f3125f3-0dfa-40bd-b725-8aa1591234f6
author: stevestein
ms.author: sstein
ms.openlocfilehash: c92ea8e2f172d9cb5b40559c2a7b77a60153065b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68137712"
---
# <a name="sp_helpmergepullsubscription-transact-sql"></a>sp_helpmergepullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  サブスクライバーに存在するプル サブスクリプションに関する情報を返します。 このストアド プロシージャは、サブスクライバーのサブスクリプション データベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpmergepullsubscription [ [ @publication=] 'publication']  
    [ , [ @publisher=] 'publisher']  
    [ , [ @publisher_db=] 'publisher_db']  
    [ , [ @subscription_type=] 'subscription_type']  
```  
  
## <a name="argument"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前です。 *パブリケーション*は**sysname**、既定値は **%** します。 場合*パブリケーション*は **%** 、すべてのマージ パブリケーションと、現在のデータベース内のサブスクリプションに関する情報が返されます。  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前です。 *パブリッシャー*は**sysname**、既定値は **%** します。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシャー データベースの名前です。 *publisher_db*は**sysname**、既定値は **%** します。  
  
`[ @subscription_type = ] 'subscription_type'` プル サブスクリプションを表示するかどうかです。 *subscription_type*は**nvarchar (10)** 、既定値は **'pull'** します。 有効な値は **'push'** 、 **'pull'** 、または **'both'** します。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**nvarchar(1000)**|サブスクリプションの名前。|  
|**publication**|**sysname**|パブリケーションの名前。|  
|**publisher**|**sysname**|パブリッシャーの名前。|  
|**publisher_db**|**sysname**|パブリッシャー データベースの名前です。|  
|**subscriber**|**sysname**|サブスクライバーの名前。|  
|**subscription_db**|**sysname**|サブスクリプション データベースの名前。|  
|**status**|**int**|サブスクリプションの状態:<br /><br /> **0** = 非アクティブなサブスクリプション<br /><br /> **1** = アクティブなサブスクリプション<br /><br /> **2** = 削除されたサブスクリプション<br /><br /> **3** = デタッチされたサブスクリプション<br /><br /> **4** = アタッチされたサブスクリプション<br /><br /> **5** = アップロードと共に再初期化のマークされているサブスクリプション<br /><br /> **6** = 失敗したサブスクリプションのアタッチ<br /><br /> **7** = バックアップから復元されたサブスクリプション|  
|**subscriber_type**|**int**|サブスクライバーの種類。<br /><br /> **1** = グローバル<br /><br /> **2** = ローカル<br /><br /> **3** = 匿名|  
|**subscription_type**|**int**|サブスクリプションの種類。<br /><br /> **0**プッシュを =<br /><br /> **1** = プル<br /><br /> **2** = 匿名|  
|**priority**|**float(8)**|サブスクリプションの優先度。 値がある必要がありますより小さい**100.00**します。|  
|**sync_type**|**tinyint**|サブスクリプションの同期の種類:<br /><br /> **1** = 自動<br /><br /> **2** = スナップショットは使用されません。|  
|**description**|**nvarchar (255)**|プル サブスクリプションの簡単な説明。|  
|**merge_jobid**|**binary(16)**|マージ エージェントのジョブ ID。|  
|**enabled_for_syncmgr**|**int**|サブスクリプションを介した同期が可能かどうか、[!INCLUDE[msCoName](../../includes/msconame-md.md)]同期マネージャーです。|  
|**last_updated**|**nvarchar(26)**|マージ エージェントが最後に成功時に、サブスクリプションが同期されます。|  
|**publisher_login**|**sysname**|パブリッシャーのログイン名。|  
|**publisher_password**|**sysname**|パブリッシャーのパスワード。|  
|**publisher_security_mode**|**int**|パブリッシャーのセキュリティ モードを指定します。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証<br /><br /> **1** = Windows 認証|  
|**distributor**|**sysname**|ディストリビューターの名前。|  
|**distributor_login**|**sysname**|ディストリビューターのログイン名。|  
|**distributor_password**|**sysname**|ディストリビューターのパスワード。|  
|**distributor_security_mode**|**int**|ディストリビューターのセキュリティ モードを指定します。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証<br /><br /> **1** = Windows 認証|  
|**ftp_address**|**sysname**|旧バージョンとの互換性のためにだけ使用できます。 ディストリビューター用ファイル転送プロトコル (FTP) サービスのネットワーク アドレスです。|  
|**ftp_port**|**int**|旧バージョンとの互換性のためにだけ使用できます。 ディストリビューター用の FTP サービスのポート番号です。|  
|**ftp_login**|**sysname**|旧バージョンとの互換性のためにだけ使用できます。 FTP サービスに接続するときに使用するユーザー名です。|  
|**ftp_password**|**sysname**|旧バージョンとの互換性のためにだけ使用できます。 FTP サービスに接続するときに使用するユーザー パスワードです。|  
|**alt_snapshot_folder**|**nvarchar (255)**|スナップショット フォルダーの場合は、場所は以外、またはさらに、既定の場所に格納される場所。|  
|**working_directory**|**nvarchar (255)**|ディレクトリへの完全修飾パスが、そのオプションを指定した場合は、FTP を使用してスナップショット ファイルを転送します。|  
|**use_ftp**|**bit**|インターネット経由でサブスクリプションがパブリケーションにサブスクライブして、FTP アドレス プロパティが構成されます。 場合**0**サブスクリプションは FTP を使用していません。 場合**1**サブスクリプションは FTP を使用しています。|  
|**offload_agent**|**bit**|エージェントのアクティブ化し、リモート実行かどうかを指定します。 場合**0**エージェントをリモートでアクティブにできません。|  
|**offload_server**|**sysname**|リモートから起動するときに使用するサーバーの名前です。|  
|**use_interactive_resolver**|**int**|調整時に対話型の競合回避モジュールを使用するかどうかを示します。 場合**0**、インタラクティブ競合回避のモジュールは使用されません。|  
|**subid**|**uniqueidentifier**|サブスクライバーの ID。|  
|**dynamic_snapshot_location**|**nvarchar (255)**|スナップショット ファイルが保存されるフォルダーへのパス。|  
|**last_sync_status**|**int**|同期の状態:<br /><br /> **1** = 起動中<br /><br /> **2** = に成功しました<br /><br /> **3** = 実行中<br /><br /> **4** = アイドル状態<br /><br /> **5**失敗後再試行を =<br /><br /> **6** = に失敗しました<br /><br /> **7** = 検証失敗<br /><br /> **8** = 検証合格<br /><br /> **9**シャット ダウンの要求を =|  
|**last_sync_summary**|**sysname**|最後の同期の結果の説明です。|  
|**use_web_sync**|**bit**|HTTPS 経由でサブスクリプションを同期することができるかどうかの値が指定**1**この機能が有効になっていることを意味します。|  
|**internet_url**|**nvarchar(260)**|Web 同期レプリケーション リスナーの位置を表す URL です。|  
|**internet_login**|**nvarchar(128)**|基本認証を使用して Web 同期をホストしている Web サーバーに接続するときに、マージ エージェントを使用してログインします。|  
|**internet_password**|**nvarchar(524)**|マージ エージェントが基本認証を使用して Web 同期をホストしている Web サーバーに接続するときに使用するログインのパスワードです。|  
|**internet_security_mode**|**int**|Web 同期をホストしている Web サーバーに接続するときに使用する認証モードです。 値**1** 、Windows 認証を示し、値の**0**意味[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。|  
|**internet_timeout**|**int**|Web 同期要求の有効期限が切れるまでの秒数で、時間の長さ。|  
|**hostname**|**nvarchar(128)**|オーバー ロードの値を指定します[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)パラメーター化された行フィルターの WHERE 句でこの関数を使用する場合。|  
|**job_login**|**nvarchar(512)**|形式で返される、マージ エージェントを実行する Windows アカウントは、*ドメイン*\\*username*します。|  
|**job_password**|**sysname**|セキュリティ上の理由の値" **\*\*\*\*\*\*\*\*\*\*** "が常に返されます。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helpmergepullsubscription**はマージ レプリケーションで使用します。 結果セットで返される日付で**last_updated**としてフォーマットされている*YYYYMMDD hh:mm:ss.fff*します。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールおよび**db_owner**固定データベース ロールが実行できる**sp_helpmergepullsubscription**します。  
  
## <a name="see-also"></a>関連項目  
 [sp_addmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
