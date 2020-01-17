---
title: sp_addlinkedsrvlogin (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addlinkedsrvlogin_TSQL
- sp_addlinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlinkedsrvlogin
ms.assetid: eb69f303-1adf-4602-b6ab-f62e028ed9f6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1bf39a9a1262f30e3c0bbd6fd2ea5892a55540dd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072669"
---
# <a name="spaddlinkedsrvlogin-transact-sql"></a>sp_addlinkedsrvlogin (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  作成または更新のローカル インスタンス上のログインの間のマッピング[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]とリモート サーバー上のセキュリティ アカウント。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_addlinkedsrvlogin [ @rmtsrvname = ] 'rmtsrvname'   
     [ , [ @useself = ] { 'TRUE' | 'FALSE' | NULL } ]   
     [ , [ @locallogin = ] 'locallogin' ]   
     [ , [ @rmtuser = ] 'rmtuser' ]   
     [ , [ @rmtpassword = ] 'rmtpassword' ]   
```  
  
## <a name="arguments"></a>引数  
 `[ @rmtsrvname = ] 'rmtsrvname'`  
 ログイン マッピングを適用するリンク サーバーの名前です。 *rmtsrvname*は**sysname**、既定値はありません。  
  
 `[ @useself = ] { 'TRUE' | 'FALSE' | NULL }'`  
 接続するかどうかを判断します*rmtsrvname*ローカル ログインの権限を借用または明示的にログインとパスワードを送信します。 データ型は**varchar (** 8 **)** 、既定値は TRUE。  
  
 TRUE の値は、ログインがへの接続に自身の資格情報を使用することを指定します*rmtsrvname*で、 *rmtuser*と*rmtpassword*引数は無視されます。 FALSE を指定する、 *rmtuser*と*rmtpassword*引数がへの接続に使用される*rmtsrvname* 、指定された*locallogin*. 場合*rmtuser*と*rmtpassword*も NULL でないログインまたはパスワードに設定を使用して、リンク サーバーに接続します。  
  
 `[ @locallogin = ] 'locallogin'`  
 ローカル サーバー上のログインです。 *locallogin*は**sysname**、既定値は NULL です。 NULL では、このエントリに接続するすべてのローカル ログインに適用されることを示す*rmtsrvname*します。 NULL 以外の場合*locallogin*できます、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインまたは Windows ログインします。 Windows ログインが与えられているへのアクセス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]いずれかを直接または Windows グループのメンバーシップを介してアクセスを許可します。  
  
 `[ @rmtuser = ] 'rmtuser'`  
 接続するために使用するリモート ログイン*rmtsrvname*とき@useselfは FALSE です。 インスタンスがリモート サーバーの場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Windows 認証を使用しない*rmtuser*は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインします。 *rmtuser*は**sysname**、既定値は NULL です。  
  
 `[ @rmtpassword = ] 'rmtpassword'`  
 パスワードに関連付けられている*rmtuser*します。 *rmtpassword*は**sysname**、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>コメント  
 ユーザーは、ローカル サーバーにログオンし、リンク サーバー上のテーブルにアクセスする分散クエリを実行、すると、ローカル サーバーはそのテーブルにアクセスするユーザーの代理として、リンク サーバーにログオンする必要があります。 sp_addlinkedsrvlogin を使用して、ローカル サーバーがリンク サーバーへのログインに使用するログイン資格情報を指定します。  
  
> [!NOTE]  
>  リンク サーバーでテーブルを使用している場合は、最適なクエリ プランを作成するには、リンク サーバーのデータの分布統計情報がクエリ プロセッサに必要です。 ユーザー テーブルの列に対するアクセス許可が制限されている便利なすべての統計を取得する可能性があります効率の悪いクエリ プランを受信し、パフォーマンスが低下のための十分な権限がありません。 リンク サーバーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスである場合、利用可能な統計情報をすべて取得するには、ユーザーがテーブルを所有しているか、リンク サーバーの固定サーバー ロール sysadmin、固定データベース ロール db_owner、または固定データベース ロール db_ddladmin のメンバーである必要があります。 SQL Server 2012 SP1 では、統計を取得するための権限の制限が変更され、SELECT 権限を持つユーザーは DBCC SHOW_STATISTICS で入手可能な統計にアクセスできます。 詳細については、アクセス許可のセクションを参照してください。 [DBCC SHOW_STATISTICS &#40;TRANSACT-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)します。  
  
 すべてのローカル サーバー上のログインとリンク サーバー上のリモート ログインの既定のマッピングは、sp_addlinkedserver を実行することによって自動的に作成されます。 既定のマッピングでは、ことを示す[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログインの代わりに、リンク サーバーに接続するときに、ローカル ログインのユーザーの資格情報を使用します。 Sp_addlinkedsrvlogin を実行するのと同じ@useself設定 **true** ローカル ユーザー名を指定せず、リンク サーバー。 既定のマッピングを変更するときや、特定のローカル ログインに対応する新しいマッピングを追加するときだけ sp_addlinkedsrvlogin を使用します。 既定のマッピングまたはその他のマッピングを削除するには、sp_droplinkedsrvlogin を使用します。  
  
 次のすべての条件が成立する場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、sp_addlinkedsrvlogin を使用してあらかじめ決められたログイン マッピングを作成する代わりに、クエリを実行するユーザーの Windows セキュリティ資格情報 (Windows のログイン名とパスワード) を自動的に使用して、リンク サーバーに接続できます。  
  
-   ユーザーが接続されている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Windows 認証モードを使用しています。  
  
-   セキュリティ アカウントの委任は、クライアントと送信側サーバーで使用できます。  
  
-   たとえば Windows 上で実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のように、プロバイダーが Windows 認証モードをサポートしている。  
  
> [!NOTE]  
>  委任がシングル ホップのシナリオで有効にする必要はありませんが、複数のホップ シナリオの必須。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカル インスタンス上で sp_addlinkedsrvlogin を実行して定義されたマッピングを、リンク サーバーが使用して認証を行った後は、ローカル サーバーではなく、リンク サーバーがリモート データベース内の個々のオブジェクトに対する権限を規定します。  
  
 ユーザー定義のトランザクション内から sp_addlinkedsrvlogin を実行することはできません。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する ALTER ANY LOGIN 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-connecting-all-local-logins-to-the-linked-server-by-using-their-own-user-credentials"></a>A. 自分のユーザー資格情報を使用してすべてのローカル ログインをリンク サーバーに接続  
 次の例では、ローカル サーバーにすべてのログインをリンク サーバーに接続を確認するマッピングを作成する`Accounts`自身のユーザー資格情報を使用しています。  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts';  
```  
  
 または  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'true';  
```  
  
> [!NOTE]  
>  個別のログイン用に作成された明示的なマッピングがある場合よりも優先どのグローバル マッピングが存在するリンク サーバーにします。  
  
### <a name="b-connecting-a-specific-login-to-the-linked-server-by-using-different-user-credentials"></a>B. 特定のログインをリンク サーバーに別のユーザーの資格情報を使用して接続します。  
 次の例では、ことを確認するマッピングを作成する Windows ユーザー`Domain\Mary`をリンク サーバー経由で接続`Accounts`、ログインを使用して`MaryP`とパスワード`d89q3w4u`します。  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'false', 'Domain\Mary', 'MaryP', 'd89q3w4u';  
```  
  
> [!IMPORTANT]  
>  この例では、Windows 認証は使用しません。 暗号化されていないパスワードが送信されます。 パスワードは、ディスク、バックアップ、およびログファイルに保存されたデータ ソース定義やスクリプトで参照できます。 この種類の接続では、システム管理者のパスワードを使用しないでください。 セキュリティのガイダンスについては、環境に合わせたネットワーク管理者に問い合わせてください。  
  
## <a name="see-also"></a>関連項目  
 [リンク サーバーのカタログ ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
