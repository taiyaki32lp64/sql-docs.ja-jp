---
title: sp_change_subscription_properties (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_change_subscription_properties_TSQL
- sp_change_subscription_properties
helpviewer_keywords:
- sp_change_subscription_properties
ms.assetid: cf8137f9-f346-4aa1-ae35-91a2d3c16f17
author: stevestein
ms.author: sstein
ms.openlocfilehash: cfc42dbf08b6718e72970a703f56fb0bfff850f4
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771409"
---
# <a name="spchangesubscriptionproperties-transact-sql"></a>sp_change_subscription_properties (Transact-sql)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  プル サブスクリプションの情報を更新します。 このストアドプロシージャは、サブスクライバー側のサブスクリプションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_change_subscription_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @property = ] 'property'  
        , [ @value = ] 'value'  
    [ , [ @publication_type = ] publication_type ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'`パブリッシャーの名前を指定します。 *パブリッシャー* は **sysname** 、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'`パブリッシャーデータベースの名前を指定します。 *publisher_db* は **sysname** 、既定値はありません。  
  
`[ @publication = ] 'publication'`パブリケーションの名前を指定します。 *パブリケーション* は **sysname** 、既定値はありません。  
  
`[ @property = ] 'property'`変更するプロパティを指定します。 *プロパティ*は**sysname**です。  
  
`[ @value = ] 'value'`は、プロパティの新しい値です。 *値*は**nvarchar (1000)** ,、既定値はありません。  
  
`[ @publication_type = ] publication_type`パブリケーションのレプリケーションの種類を指定します。 *publication_type*は**int**,、これらの値のいずれかを指定することができます。  
  
|値|パブリケーションの種類|  
|-----------|----------------------|  
|**0**|トランザクション|  
|**1**|スナップショット|  
|**2**|Merge|  
|NULL (既定値)|レプリケーションでは、パブリケーションの種類を決定します。 このストアド プロシージャでは複数のテーブルを検索する必要があるため、このオプションを指定すると、パブリケーションの種類を直接指定したときに比べて動作が遅くなります。|  
  
 次の表では、アーティクルのプロパティとそれらのプロパティの値について説明します。  
  
|プロパティ|値|説明|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||スナップショットの代替フォルダーの場所を指定します。 NULL に設定した場合、スナップショットファイルはパブリッシャーによって指定された既定の場所から取得されます。|  
|**distrib_job_login**||エージェントを実行する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントのログイン。|  
|**distrib_job_password**||エージェントを実行する Windows アカウントのパスワード。|  
|**distributor_login**||ディストリビューターログイン。|  
|**distributor_password**||ディストリビューター パスワード。|  
|**distributor_security_mode**|**1**|ディストリビューターへの接続時に Windows 認証を使用します。|  
||**0**|ディストリビューター [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]への接続時に認証を使用します。|  
|**dts_package_name**||SQL Server 2000 データ変換サービス (DTS) パッケージの名前。 この値は、パブリケーションがトランザクションまたはスナップショットの場合にのみ指定できます。|  
|**dts_package_password**||パッケージのパスワードを指定します。 *dts_package_password*は**sysname**既定値は NULL です。これは、password プロパティを変更せずに残すことを指定します。<br /><br /> 注:DTS パッケージには、パスワードが必要です。<br /><br /> この値は、パブリケーションがトランザクションまたはスナップショットの場合にのみ指定できます。|  
|**dts_package_location**||DTS パッケージが格納されている場所。 この値は、パブリケーションがトランザクションまたはスナップショットの場合にのみ指定できます。|  
|**dynamic_snapshot_location**||スナップショットファイルを保存するフォルダーへのパスを指定します。 この値は、パブリケーションがマージパブリケーションである場合にのみ指定できます。|  
|**ftp_address**||これは旧バージョンとの互換性のためにだけ用意されています。|  
|**ftp_login**||これは旧バージョンとの互換性のためにだけ用意されています。|  
|**ftp_password**||これは旧バージョンとの互換性のためにだけ用意されています。|  
|**ftp_port**||これは旧バージョンとの互換性のためにだけ用意されています。|  
|**名**||パブリッシャーに接続するときに使用されるホスト名。|  
|**internet_login**||基本認証を使用して Web 同期をホストしている Web サーバーに接続するときにマージエージェントが使用するログインです。|  
|**internet_password**||基本認証を使用して Web 同期をホストしている Web サーバーに接続するときにマージエージェントが使用するパスワード。|  
|**internet_security_mode**|**1**|Web 同期に Windows 統合認証を使用します。 Web 同期で基本認証を使用することをお勧めします。 詳しくは、「 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)」をご覧ください。|  
||**0**|Web 同期に基本認証を使用。<br /><br /> 注:Web 同期には、Web サーバーへの SSL 接続が必要です。|  
|**internet_timeout**||Web 同期要求が期限切れになるまでの時間の長さ (秒単位)。|  
|**internet_url**||Web 同期用のレプリケーションリスナーの場所を表す URL。|  
|**merge_job_login**||エージェントを実行する Windows アカウントのログイン。|  
|**merge_job_password**||エージェントを実行する Windows アカウントのパスワード。|  
|**publisher_login**||パブリッシャーログイン。 *Publisher_login*の変更は、マージパブリケーションに対するサブスクリプションでのみサポートされています。|  
|**publisher_password**||パブリッシャーのパスワード。 *Publisher_password*の変更は、マージパブリケーションに対するサブスクリプションでのみサポートされています。|  
|**publisher_security_mode**|**1**|パブリッシャーに接続するときに Windows 認証を使用。 *Publisher_security_mode*の変更は、マージパブリケーションに対するサブスクリプションでのみサポートされています。|  
||**0**|パブリッシャー [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続するときに認証を使用します。|  
|**use_ftp**|**true**|スナップショットを取得するには、通常のプロトコルの代わりに FTP を使用します。|  
||**false**|標準のプロトコルを使用してスナップショットを取得。|  
|**use_web_sync**|**true**|Web 同期を有効にします。|  
||**false**|Web 同期を無効にします。|  
|**working_directory**||ファイル転送プロトコル (FTP) を使用してスナップショットファイルを転送するときに、パブリケーションのデータとスキーマファイルを一時的に格納するために使用する作業ディレクトリの名前。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_change_subscription_properties**は、すべての種類のレプリケーションで使用されます。  
  
 **sp_change_subscription_properties**はプルサブスクリプションに使用します。  
  
 Oracle パブリッシャーの場合、Oracle ではサーバーのインスタンスごとに1つのデータベースしか許可されないため、 *publisher_db*の値は無視されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_change_subscription_properties**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [プル サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [sp_addmergepullsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_addmergepullsubscription_agent &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_addpullsubscription &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_addpullsubscription_agent &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
