---
title: sp_attachsubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_attachsubscription
- sp_attachsubscription_TSQL
helpviewer_keywords:
- sp_attachsubscription
ms.assetid: b9bbda36-a46a-4327-a01e-9cd632e4791b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2e059b78a886735ce53b86de77effa43b03136df
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768966"
---
# <a name="spattachsubscription-transact-sql"></a>sp_attachsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  既存のサブスクリプション データベースを任意のサブスクライバーにアタッチします。 このストアドプロシージャは、master データベースの新しいサブスクライバーで実行されます。  
  
> [!IMPORTANT]  
>  この機能は非推奨とされており、今後のリリースでは削除されます。 新しい開発作業では、この機能を使用しないでください。 パラメーター化されたフィルターを使用してパーティション分割されたマージ パブリケーションでは、パーティション スナップショットの新しい機能を使用することをお勧めします。この機能を使用すると、多数のサブスクリプションの初期化を簡単に実行できます。 詳しくは、「 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」をご覧ください。 パーティション分割されていないパブリケーションの場合は、バックアップを使用してサブスクリプションを初期化できます。 詳細については、「[スナップショットを使用しないトランザクション サブスクリプションの初期化](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_attachsubscription [ @dbname = ] 'dbname'  
        , [ @filename = ] 'filename'  
    [ , [ @subscriber_security_mode = ] 'subscriber_security_mode' ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @distributor_security_mode = ] distributor_security_mode ]   
    [ , [ @distributor_login = ] 'distributor_login' ]   
    [ , [ @distributor_password = ] 'distributor_password' ]   
    [ , [ @publisher_security_mode = ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @db_master_key_password = ] 'db_master_key_password' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @dbname = ] 'dbname'`宛先サブスクリプションデータベースを名前で指定する文字列を指定します。 *dbname*は**sysname**,、既定値はありません。  
  
`[ @filename = ] 'filename'`プライマリ MDF (**master**データファイル) の名前と物理的な場所を指定します。 *ファイル名*は**nvarchar (260)** ,、既定値はありません。  
  
`[ @subscriber_security_mode = ] 'subscriber_security_mode'`サブスクライバーが同期時に接続するときに使用する、サブスクライバーのセキュリティモードを示します。 *subscriber_security_mode*は**int**,、既定値は NULL です。  
  
> [!NOTE]  
>  Windows 認証を使用する必要があります。 *Subscriber_security_mode*が**1** (Windows 認証) でない場合は、エラーが返されます。  
  
`[ @subscriber_login = ] 'subscriber_login'`同期時にサブスクライバーに接続するときに使用するサブスクライバーのログイン名を指定します。 *subscriber_login* は **sysname** 、既定値は NULL です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のみを維持しています。 *Subscriber_security_mode*が**1**ではなく、 *subscriber_login*が指定されている場合は、エラーが返されます。  
  
`[ @subscriber_password = ] 'subscriber_password'`サブスクライバーパスワードを入力します。 *subscriber_password* は **sysname** 、既定値は NULL です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のみを維持しています。 *Subscriber_security_mode*が**1**ではなく、 *subscriber_password*が指定されている場合は、エラーが返されます。  
  
`[ @distributor_security_mode = ] distributor_security_mode`は、同期時にディストリビューターに接続するときに使用するセキュリティモードです。 *distributor_security_mode*は**int**,、既定値は**0**です。 **0**は[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証を指定します。 **1** Windows 認証を指定します。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @distributor_login = ] 'distributor_login'`ディストリビューターへの接続時に、同期時に使用するディストリビューターログインを示します。 *distributor_login* 場合は必須です *distributor_security_mode* に設定されている **0** します。 *distributor_login* は **sysname** 、既定値は NULL です。  
  
`[ @distributor_password = ] 'distributor_password'`ディストリビューターパスワードを入力します。 *distributor_password* 場合は必須です *distributor_security_mode* に設定されている **0** します。 *distributor_password* は **sysname** 、既定値は NULL です。 *Distributor_password*の値は 120 Unicode 文字未満である必要があります。  
  
> [!IMPORTANT]  
>  空白のパスワードは使用しないでください。 強力なパスワードを使用してください。 可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
`[ @publisher_security_mode = ] publisher_security_mode`同期時にパブリッシャーに接続するときに使用するセキュリティモードを示します。 *publisher_security_mode*は**int**,、既定値は**1**です。 **0**の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証を指定します。 **1**の場合、Windows 認証を指定します。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'`同期時にパブリッシャーに接続するときに使用するログインを示します。 *publisher_login* は **sysname** 、既定値は NULL です。  
  
`[ @publisher_password = ] 'publisher_password'`パブリッシャーに接続するときに使用するパスワードを入力します。 *publisher_password* は **sysname** 、既定値は NULL です。 *Publisher_password*の値は 120 Unicode 文字未満である必要があります。  
  
> [!IMPORTANT]  
>  空白のパスワードは使用しないでください。 強力なパスワードを使用してください。 可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
`[ @job_login = ] 'job_login'`エージェントを実行する Windows アカウントのログインを指定します。 *job_login*は**nvarchar (257)** ,、既定値はありません。 この Windows アカウントは、ディストリビューターへのエージェント接続に常に使用されます。  
  
`[ @job_password = ] 'job_password'`エージェントを実行する Windows アカウントのパスワードを指定します。 *job_password* は **sysname** 、既定値はありません。 *Job_password*の値は 120 Unicode 文字未満である必要があります。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
`[ @db_master_key_password = ] 'db_master_key_password'`ユーザー定義のデータベースマスターキーのパスワードを指定します。 *db_master_key_password*は**nvarchar (524)** ,、既定の値は NULL です。 *Db_master_key_password*が指定されていない場合は、既存のデータベースマスターキーが削除され、再作成されます。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_attachsubscription**は、スナップショットレプリケーション、トランザクションレプリケーション、およびマージレプリケーションで使用します。  
  
 パブリケーションの保有期間が終了している場合、サブスクリプションをパブリケーションにアタッチすることはできません。 保有期間が経過したサブスクリプションが指定されている場合、サブスクリプションがアタッチされているか、最初に同期されたときに、エラーが発生します。 パブリケーションの保有期間が**0** (期限切れにならない) のパブリケーションは無視されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_attachsubscription**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
