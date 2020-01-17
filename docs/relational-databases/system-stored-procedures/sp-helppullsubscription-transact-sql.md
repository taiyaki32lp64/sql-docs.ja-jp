---
title: sp_helppullsubscription (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppullsubscription_TSQL
- sp_helppullsubscription
helpviewer_keywords:
- sp_helppullsubscription
ms.assetid: a0d9c3f1-1fe9-497c-8e2f-5b74f47a7346
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1ab2afba10ff754b5bd99d36df02d642cc5c6bb0
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771443"
---
# <a name="sp_helppullsubscription-transact-sql"></a>sp_helppullsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  サブスクライバーの1つ以上のサブスクリプションに関する情報を表示します。 このストアドプロシージャは、サブスクライバー側のサブスクリプションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helppullsubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @show_push = ] 'show_push' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'`リモートサーバーの名前を指定します。 *publisher*のデータ型は**sysname**で、 **%** 既定値はです。これにより、すべてのパブリッシャーの情報が返されます。  
  
`[ @publisher_db = ] 'publisher_db'`パブリッシャーデータベースの名前を指定します。 *publisher_db*は**sysname**,、既定値 **%** は、すべてのパブリッシャーデータベースを返します。  
  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *パブリケーション*は**sysname**で、既定値 **%** はです。これにより、すべてのパブリケーションが返されます。 このパラメーターが ALL と等しい場合は、independent_agent = **0**のプルサブスクリプションのみが返されます。  
  
`[ @show_push = ] 'show_push'`すべてのプッシュサブスクリプションを返すかどうかを指定します。 *show_push*は**nvarchar (5)** ,、既定値は FALSE の場合、プッシュサブスクリプションは返されません。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|パブリッシャーの名前。|  
|**publisher database**|**sysname**|パブリッシャーデータベースの名前。|  
|**publication**|**sysname**|パブリケーションの名前。|  
|**independent_agent**|**bit**|このパブリケーションに対してスタンドアロンのディストリビューションエージェントがあるかどうかを示します。|  
|**subscription type**|**int**|パブリケーションへのサブスクリプションの種類。|  
|**distribution agent**|**nvarchar(100)**|サブスクリプションを処理ディストリビューションエージェント。|  
|**publication description**|**nvarchar (255)**|パブリケーションの説明です。|  
|**last updating time**|**date**|サブスクリプション情報が更新された時刻。 ISO 日付 (114) + ODBC 時刻 (121) の UNICODE 文字列です。 形式は yyyymmdd hh: mi: sss. mmm です。 ' yyyy ' は年、' mm ' は月、' dd ' は日、' hh ' は時間、' mi ' は分、' sss ' は秒、' mmm ' はミリ秒です。|  
|**subscription name**|**varchar(386)**|サブスクリプションの名前。|  
|**last transaction timestamp**|**varbinary(16)**|最後にレプリケートされたトランザクションのタイムスタンプ。|  
|**update mode**|**tinyint**|許可される更新の種類。|  
|**distribution agent job_id**|**int**|ディストリビューション エージェントのジョブ ID。|  
|**enabled_for_synmgr**|**int**|同期マネージャーを[!INCLUDE[msCoName](../../includes/msconame-md.md)]使用してサブスクリプションを同期できるかどうかを指定します。|  
|**subscription guid**|**binary(16)**|パブリケーションのサブスクリプションのバージョンのグローバル識別子。|  
|**subid**|**binary(16)**|匿名サブスクリプションのグローバル識別子。|  
|**immediate_sync**|**bit**|スナップショット エージェントを実行するたびに、同期ファイルを作成または再作成するかどうかを示します。|  
|**publisher login**|**sysname**|パブリッシャーで認証に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用されるログイン ID。|  
|**publisher password**|**nvarchar(524)**|認証のため[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にパブリッシャーで使用されるパスワード (暗号化)。|  
|**publisher security_mode**|**int**|パブリッシャーで実装されているセキュリティ モード。<br /><br /> **0**  = 認証[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> **1** = Windows 認証<br /><br /> **2** = 同期トリガーは、静的な**sysservers**エントリを使用してリモートプロシージャコール (RPC) を実行します。また、*パブリッシャー*は、 **sysservers**テーブルのリモートサーバーまたはリンクサーバーとして定義されている必要があります。|  
|**distributor**|**sysname**|ディストリビューターの名前。|  
|**distributor_login**|**sysname**|ディストリビューターで認証に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用されるログイン ID。|  
|**distributor_password**|**nvarchar(524)**|認証のために[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ディストリビューターで使用されるパスワード (暗号化)。|  
|**distributor_security_mode**|**int**|ディストリビューターで実装されているセキュリティモード:<br /><br /> **0**  = 認証[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> **1** = Windows 認証|  
|**ftp_address**|**sysname**|これは旧バージョンとの互換性のためにだけ用意されています。|  
|**ftp_port**|**int**|これは旧バージョンとの互換性のためにだけ用意されています。|  
|**ftp_login**|**sysname**|これは旧バージョンとの互換性のためにだけ用意されています。|  
|**ftp_password**|**nvarchar(524)**|これは旧バージョンとの互換性のためにだけ用意されています。|  
|**alt_snapshot_folder**|**nvarchar (255)**|場所が既定の場所に加えてまたは以外の場合に、スナップショットフォルダーが格納される場所。|  
|**working_directory**|**nvarchar (255)**|該当するオプションが指定され、ファイル転送プロトコル (FTP) を使ってスナップショット ファイルを転送する場合の、転送先ディレクトリの完全修飾パス。|  
|**use_ftp**|**bit**|サブスクリプションは、インターネット経由でパブリケーションをサブスクライブしています。また、FTP アドレスのプロパティが構成されています。 **0**の場合、サブスクリプションは FTP を使用していません。 **1**の場合、サブスクリプションは FTP を使用しています。|  
|**publication_type**|**int**|パブリケーションのレプリケーションの種類。<br /><br /> **0** = トランザクションレプリケーション<br /><br /> **1** = スナップショットレプリケーション<br /><br /> **2** = マージレプリケーション|  
|**dts_package_name**|**sysname**|データ変換サービス (DTS) パッケージの名前を指定します。|  
|**dts_package_location**|**int**|DTS パッケージが格納されている場所:<br /><br /> **0** = ディストリビューター<br /><br /> **1** = サブスクライバー|  
|**offload_agent**|**bit**|エージェントをリモートでアクティブ化できるかどうかを指定します。 **0**の場合、エージェントをリモートでアクティブにすることはできません。|  
|**offload_server**|**sysname**|リモートからのアクティブ化に使用するサーバーのネットワーク名を指定します。|  
|**last_sync_status**|**int**|サブスクリプションの状態:<br /><br /> **0** = すべてのジョブが開始を待機しています<br /><br /> **1** = 1 つ以上のジョブが開始されています<br /><br /> **2** = すべてのジョブが正常に実行されました<br /><br /> **3** = 少なくとも1つのジョブが実行されています<br /><br /> **4** = すべてのジョブがスケジュールされ、アイドル状態になっている<br /><br /> **5** = 少なくとも1つのジョブが前回のエラーの発生後に実行しようとしています<br /><br /> **6** = 少なくとも1つのジョブを正常に実行できませんでした|  
|**last_sync_summary**|**sysname**|前回の同期の結果の説明。|  
|**last_sync_time**|**datetime**|サブスクリプション情報が更新された時刻。 ISO 日付 (114) + ODBC 時刻 (121) の UNICODE 文字列です。 形式は yyyymmdd hh: mi: sss. mmm です。 ' yyyy ' は年、' mm ' は月、' dd ' は日、' hh ' は時間、' mi ' は分、' sss ' は秒、' mmm ' はミリ秒です。|  
|**job_login**|**nvarchar(512)**|ディストリビューションエージェントを実行する Windows アカウントを指定します。このアカウントは、*ドメイン*\\*ユーザー名*の形式で返されます。|  
|**job_password**|**sysname**|セキュリティ上の理由から、値 " **\*\*\*\*\*"は\*常に返されます。\*\*\*\***|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helppullsubscription**は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helppullsubscription**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_droppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
