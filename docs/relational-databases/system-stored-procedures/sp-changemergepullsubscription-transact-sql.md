---
title: sp_changemergepullsubscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergepullsubscription
- sp_changemergepullsubscription_TSQL
helpviewer_keywords:
- sp_changemergepullsubscription
ms.assetid: 5e0d04f2-6175-44a2-ad96-a8e2986ce4c9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8771d7c821a82733b0664f09c5dadf2128baf877
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090847"
---
# <a name="spchangemergepullsubscription-transact-sql"></a>sp_changemergepullsubscription (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  マージ プル サブスクリプションのプロパティを変更します。 このストアド プロシージャは、サブスクライバーのサブスクリプション データベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changemergepullsubscription [ [ @publication= ] 'publication' ]  
    [ , [ @publisher= ] 'publisher' ]  
    [ , [ @publisher_db= ] 'publisher_db' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前です。 *パブリケーション*は**sysname**、既定値は % です。  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前です。 *パブリッシャー*は**sysname**、既定値は % です。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシャー データベースの名前です。 *publisher_db*は**sysname**、既定値は % です。  
  
`[ @property = ] 'property'` 変更するプロパティの名前です。 *プロパティ*は**sysname**テーブル内の値のいずれかを指定できます。  
  
`[ @value = ] 'value'` 指定したプロパティの新しい値です。 *値*は**nvarchar (255)** テーブル内の値のいずれかを指定できます。  
  
|プロパティ|値|説明|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||スナップショット フォルダーの場合は、場所は以外、またはさらに、既定の場所に格納される場所。|  
|**description**||このマージ プル サブスクリプションの説明です。|  
|**ディストリビューター**||ディストリビューターの名前。|  
|**distributor_login**||ディストリビューターで使用されたログイン ID[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証|  
|**distributor_password**||ディストリビューターで使用するパスワード (暗号化)[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。|  
|**distributor_security_mode**|**1**|ディストリビューターに接続するときに、Windows 認証を使用します。|  
||**0**|使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ディストリビューターに接続するときに認証します。|  
|**dynamic_snapshot_location**||スナップショット ファイルが保存されるフォルダーへのパスです。|  
|**ftp_address**||旧バージョンとの互換性のためにだけ使用できます。 ディストリビューター用ファイル転送プロトコル (FTP) サービスのネットワーク アドレスです。|  
|**ftp_login**||旧バージョンとの互換性のためにだけ使用できます。 FTP サービスに接続するときに使用するユーザー名です。|  
|**ftp_password**||旧バージョンとの互換性のためにだけ使用できます。 FTP サービスに接続するときに使用するユーザー パスワードです。|  
|**ftp_port**||旧バージョンとの互換性のためにだけ使用できます。 ディストリビューター用の FTP サービスのポート番号です。|  
|**ホスト名**||指定します、この関数は、結合フィルターまたは論理レコード リレーションシップの WHERE 句で使用される場合の HOST_NAME() の値。|  
|**internet_login**||基本認証を使用して Web 同期をホストしている Web サーバーに接続するときに、マージ エージェントを使用してログインします。|  
|**internet_password**||マージ エージェントが基本認証を使用して Web 同期をホストしている Web サーバーに接続するときに使用するログインのパスワードです。|  
|**internet_security_mode**|**1**|Web 同期をホストしている Web サーバーに接続するときは、Windows 認証を使用します。|  
||**0**|Web 同期をホストしている Web サーバーに接続するときは、基本認証を使用します。|  
|**internet_timeout**||Web 同期要求の有効期限が切れるまでの秒数で、時間の長さ。|  
|**internet_url**||Web 同期レプリケーション リスナーの位置を表す URL です。|  
|**merge_job_login**||エージェントを実行する Windows アカウントにログインします。|  
|**merge_job_password**||エージェントを実行する Windows アカウントのパスワード。|  
|**priority**||旧バージョンとの互換性だけです。実行[sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)パブリッシャー側で代わりに、サブスクリプションの優先度を変更します。|  
|**publisher_login**||パブリッシャーで使用されたログイン ID[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。|  
|**publisher_password**||パブリッシャーで使用するパスワード (暗号化)[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。|  
|**publisher_security_mode**|**0**|使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーに接続するときに認証します。|  
||**1**|パブリッシャーに接続するときに Windows 認証を使用。|  
||**2**|同期のトリガーを使用して、静的な**sysservers**でリモート プロシージャ コール (RPC)、およびパブリッシャーを実行するエントリを定義する必要があります、 **sysservers**リモート サーバーまたはリンク サーバーとしてのテーブル。|  
|**sync_type**|**自動**|スキーマと初期データのパブリッシュされたテーブルの」は最初に、サブスクライバーに転送されます。|  
||**none**|スキーマと初期データのパブリッシュされたテーブル以外のサブスクライバーに既に存在します。システム テーブルとデータは常に転送します。|  
|**use_ftp**|**true**|一般的なプロトコルの代わりに FTP を使用して、スナップショットを取得します。|  
||**false**|スナップショットを取得するのにには、一般的なプロトコルを使用します。|  
|**use_web_sync**|**true**|サブスクリプションは、HTTP 経由で同期できます。|  
||**false**|サブスクリプションは HTTP 上で同期できません。|  
|**use_interactive_resolver**|**true**|調整時にインタラクティブ競合回避モジュールを使用します。|  
||**false**|インタラクティブ競合回避モジュールには使用されません。|  
|**working_directory**||ディレクトリへの完全修飾パスが、そのオプションを指定した場合は、FTP を使用してスナップショット ファイルを転送します。|  
|NULL (既定値)||サポートされている値の一覧を返します*プロパティ*します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_changemergepullsubscription**はマージ レプリケーションで使用します。  
  
 現在のサーバーがサブスクライバー、現在のデータベースがサブスクライバー データベースであると解釈されます。  
  
 エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーのみ、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロールが実行できる**sp_changemergepullsubscription**します。  
  
## <a name="see-also"></a>関連項目  
 [プル サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [sp_addmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
