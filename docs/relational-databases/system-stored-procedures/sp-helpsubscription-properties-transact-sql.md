---
title: sp_helpsubscription_properties (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscription_properties
- sp_helpsubscription_properties_TSQL
helpviewer_keywords:
- sp_helpsubscription_properties
ms.assetid: 7a76a645-97eb-47ac-b3ea-e2d75012cbed
author: stevestein
ms.author: sstein
ms.openlocfilehash: 28305f4676c9323b364703feb0b668615a159e6b
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771564"
---
# <a name="sp_helpsubscription_properties-transact-sql"></a>sp_helpsubscription_properties (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)テーブルからセキュリティ情報を取得します。 このストアドプロシージャは、サブスクライバー側で実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpsubscription_properties [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db =] 'publisher_db' ]   
    [ , [ @publication =] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'`パブリッシャーの名前を指定します。 *publisher*のデータ型は**sysname**で、 **%** 既定値はです。これにより、すべてのパブリッシャーに関する情報が返されます。  
  
`[ @publisher_db = ] 'publisher_db'`パブリッシャーデータベースの名前を指定します。 *publisher_db*のデータ型は**sysname**で、 **%** 既定値はで、すべてのパブリッシャーデータベースに関する情報を返します。  
  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *publication*のデータ型は**sysname**で、 **%** 既定値はです。これにより、すべてのパブリケーションに関する情報が返されます。  
  
`[ @publication_type = ] publication_type`パブリケーションの種類を示します。*publication_type*は**int**,、既定値は NULL です。 指定する場合、 *publication_type*には次のいずれかの値を指定する必要があります。  
  
|[値]|説明|  
|-----------|-----------------|  
|**0**|トランザクション パブリケーション|  
|**1**|スナップショット パブリケーション|  
|**2**|マージ パブリケーション|  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|パブリッシャーの名前。|  
|**publisher_db**|**sysname**|パブリッシャーデータベースの名前。|  
|**publication**|**sysname**|パブリケーションの名前。|  
|**publication_type**|**int**|パブリケーションの種類です。<br /><br /> **0** = トランザクション<br /><br /> **1** = スナップショット<br /><br /> **2** = マージ|  
|**publisher_login**|**sysname**|パブリッシャーで認証に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用されるログイン ID。|  
|**publisher_password**|**nvarchar(524)**|パブリッシャーで認証 (暗号化) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のために使用されるパスワード。|  
|**publisher_security_mode**|**int**|パブリッシャーで使用されているセキュリティ モードです。<br /><br /> **0**  = 認証[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> **1** = Windows 認証|  
|**distributor**|**sysname**|ディストリビューターの名前。|  
|**distributor_login**|**sysname**|ディストリビューターログイン。|  
|**distributor_password**|**nvarchar(524)**|ディストリビューターパスワード (暗号化)。|  
|**distributor_security_mode**|**int**|ディストリビューターで使用されるセキュリティモード:<br /><br /> **0**  = 認証[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> **1** = Windows 認証|  
|**ftp_address**|**sysname**|これは旧バージョンとの互換性のためにだけ用意されています。 ディストリビューターのファイル転送プロトコル (FTP) サービスのネットワークアドレス。|  
|**ftp_port**|**int**|これは旧バージョンとの互換性のためにだけ用意されています。 ディストリビューター用 FTP サービスのポート番号。|  
|**ftp_login**|**sysname**|これは旧バージョンとの互換性のためにだけ用意されています。 FTP サービスへの接続に使用するユーザー名。|  
|**ftp_password**|**nvarchar(524)**|これは旧バージョンとの互換性のためにだけ用意されています。 FTP サービスへの接続に使用するユーザーパスワード。|  
|**alt_snapshot_folder**|**nvarchar (255)**|スナップショットの代替フォルダーの場所を指定します。|  
|**working_directory**|**nvarchar (255)**|データ ファイルとスキーマ ファイルを保存するために使用する作業ディレクトリ名です。|  
|**use_ftp**|**bit**|スナップショットを取得するために通常のプロトコルではなく FTP を使用することを指定します。 **1**の場合、FTP が使用されます。|  
|**dts_package_name**|**sysame**|データ変換サービス (DTS) パッケージの名前を指定します。|  
|**dts_package_password**|**nvarchar(524)**|パッケージのパスワードを指定します (存在する場合)。|  
|**dts_package_location**|**int**|DTS パッケージが格納されている場所。<br /><br /> **0** = パッケージの場所はディストリビューターです。<br /><br /> **1** = パッケージの場所はサブスクライバーです。|  
|**offload_agent**|**bit**|エージェントをリモートでアクティブ化できるかどうかを指定します。 **0**の場合、エージェントをリモートでアクティブにすることはできません。|  
|**offload_server**|**sysname**|リモートからのアクティブ化に使用するサーバーのネットワーク名を指定します。|  
|**dynamic_snapshot_location**|**nvarchar (255)**|スナップショットファイルを保存するフォルダーへのパスを指定します。|  
|**use_web_sync**|**bit**|サブスクリプションを HTTPS で同期できるかどうかを指定します。値**1**は、この機能が有効になっていることを意味します。|  
|**internet_url**|**nvarchar(260)**|Web 同期用のレプリケーションリスナーの場所を表す URL。|  
|**internet_login**|**nvarchar(128)**|基本認証を使用して Web 同期をホストしている Web サーバーに接続するときにマージエージェントが使用するログインです。|  
|**internet_password**|**nvarchar(524)**|基本認証を使用して Web 同期をホストしている Web サーバーに接続するときにマージエージェントが使用するログインのパスワード。|  
|**internet_security_mode**|**int**|Web 同期をホストしている Web サーバーに接続するときに使用される認証モード。値**1**は Windows 認証を意味し、値**0**は基本認証を意味します。|  
|**internet_timeout**|**int**|Web 同期要求が期限切れになるまでの時間の長さ (秒単位)。|  
|**hostname**|**nvarchar(128)**|この関数が WHERE 句のパラメーター化された行フィルターで使用される場合の HOST_NAME () の値を指定します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helpsubscription_properties**は、スナップショットレプリケーション、トランザクションレプリケーション、およびマージレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helpsubscription_properties**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
