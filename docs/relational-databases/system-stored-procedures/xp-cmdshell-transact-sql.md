---
title: xp_cmdshell (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 12/01/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_cmdshell
- xp_cmdshell_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_cmdshell
ms.assetid: 18935cf4-b320-4954-b6c1-e007fcefe358
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: be1b7bc97a46282e0adae2fb5679cfff0cd11dd1
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2019
ms.locfileid: "74687319"
---
# <a name="xp_cmdshell-transact-sql"></a>xp_cmdshell (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Windows のコマンド シェルを起動し、実行用の文字列に渡します。 出力は、テキストの行として返されます。  
  
 ![トピックリンクアイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-sql 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
xp_cmdshell { 'command_string' } [ , no_output ]  
```  
  
## <a name="arguments"></a>引数  
 **'** *command_string* **'**  
 オペレーティングシステムに渡すコマンドを含む文字列を指定します。 *command_string*は**varchar (8000)** または**nvarchar (4000)**,、既定値はありません。 *command_string*には、2つ以上の二重引用符を含めることはできません。 *Command_string*で参照されているファイルパスまたはプログラム名にスペースがある場合は、1組の引用符が必要です。 埋め込みスペースで問題が発生した場合は、回避策として FAT 8.3 ファイル名を使用することを検討してください。  
  
 **no_output**  
 は省略可能なパラメーターであり、クライアントに出力を返さないことを指定します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 次の `xp_cmdshell` ステートメントを実行すると、現在のディレクトリの一覧が返されます。  
  
```  
EXEC xp_cmdshell 'dir *.exe';  
GO  
```  
  
 行は、 **nvarchar (255)** 列で返されます。 **No_output**オプションを使用すると、次のものだけが返されます。  
  
```  
The command(s) completed successfully.  
```  
  
## <a name="remarks"></a>コメント  
 **Xp_cmdshell**によって生成される Windows プロセスには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サービスアカウントと同じセキュリティ権限が与えられます。  
  
 **xp_cmdshell**は同期的に動作します。 コマンドシェルのコマンドが完了するまで、コントロールは呼び出し元に返されません。  
  
 **xp_cmdshell**を有効または無効にするには、ポリシーベースの管理を使用するか、 **sp_configure**を実行します。 詳細については、「[セキュリティ構成](../../relational-databases/security/surface-area-configuration.md)」および「 [Xp_cmdshell サーバー構成オプション](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)」を参照してください。  
  
> [!IMPORTANT]
>  バッチ内で**xp_cmdshell**が実行され、エラーが返された場合、バッチは失敗します。 これは動作の変更です。 以前のバージョンの[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、バッチは引き続き実行されます。  
  
## <a name="xp_cmdshell-proxy-account"></a>xp_cmdshell プロキシアカウント  
 **Sysadmin**固定サーバーロールのメンバーではないユーザーによって呼び出された場合、 **xp_cmdshell**は、" **# #xp_cmdshell_proxy_account # #**" という名前の資格情報に格納されているアカウント名とパスワードを使用して Windows に接続します。 このプロキシ資格情報が存在しない場合、 **xp_cmdshell**は失敗します。  
  
 プロキシアカウントの資格情報を作成するには**sp_xp_cmdshell_proxy_account**を実行します。 このストアド プロシージャは、Windows のユーザー名とパスワードを引数にとります。 たとえば、次のコマンドは、windows パスワード`SHIPPING\KobeR` `sdfh%dkc93vcMt0`を持つ windows ドメインユーザー用のプロキシ資格情報を作成します。  
  
```  
EXEC sp_xp_cmdshell_proxy_account 'SHIPPING\KobeR','sdfh%dkc93vcMt0';  
```  
  
 詳細については、「 [sp_xp_cmdshell_proxy_account &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 悪意のあるユーザーが**xp_cmdshell**を使用して特権を昇格しようとすることがあるため、 **xp_cmdshell**は既定で無効になっています。 **Sp_configure**または**ポリシーベースの管理**を使用して有効にします。 詳細については、「 [xp_cmdshell サーバー構成オプション](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)」を参照してください。  
  
 最初に有効にした場合、 **xp_cmdshell**は CONTROL SERVER 権限を実行する必要があり、 **xp_cmdshell**によって作成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]された Windows プロセスは、サービスアカウントと同じセキュリティコンテキストを持ちます。 多く[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の場合、サービスアカウントには、 **xp_cmdshell**によって作成されたプロセスによって実行される作業に必要な権限よりも多くのアクセス許可があります。 セキュリティを強化するには、 **xp_cmdshell**へのアクセスを高い特権を持つユーザーに制限する必要があります。  
  
 非管理者が**xp_cmdshell**を使用できるようにし[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、が低い特権のアカウントのセキュリティトークンを使用して子プロセスを作成できるようにするには、次の手順を実行します。  
  
1.  プロセスに必要な最小限の特権で、Windows ローカルユーザーアカウントまたはドメインアカウントを作成およびカスタマイズします。  
  
2.  **Sp_xp_cmdshell_proxy_account**システムプロシージャを使用して、その最小特権のアカウントを使用するように**xp_cmdshell**を構成します。  
  
    > [!NOTE]  
    >  また、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]オブジェクトエクスプローラーでサーバー名の**プロパティ**を右クリックし、[**サーバープロキシアカウント**] セクションの [**セキュリティ**] タブを使用して、このプロキシアカウントを構成することもできます。  
  
3.  で[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]は、master データベースを使用して`GRANT exec ON xp_cmdshell TO N'<some_user>';` 、ステートメントを実行し、特定の非**sysadmin**ユーザーに**xp_cmdshell**を実行する権限を与えます。 指定されたユーザーは、master データベースに存在している必要があります。  
  
 管理者以外のユーザーは**xp_cmdshell**でオペレーティングシステムプロセスを起動できるようになりました。これらのプロセスは、構成したプロキシアカウントのアクセス許可で実行されます。 CONTROL SERVER 権限を持つユーザー ( **sysadmin**固定サーバーロールのメンバー) は、 **xp_cmdshell**によって起動さ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]れる子プロセスのサービスアカウントのアクセス許可を引き続き受け取ります。  
  
 オペレーティングシステムプロセスを起動するときに**xp_cmdshell**によって使用されている Windows アカウントを特定するには、次のステートメントを実行します。  
  
```  
xp_cmdshell 'whoami.exe'  
  
```  
  
 別のログインのセキュリティ コンテキストを確認するには、次のコマンドを実行します。  
  
```  
EXECUTE AS LOGIN = '<other_login>' ;  
GO  
xp_cmdshell 'whoami.exe' ;  
REVERT ;  
  
```  
  
## <a name="examples"></a>例  
  
### <a name="a-returning-a-list-of-executable-files"></a>A. 実行可能ファイルの一覧を返す  
 次の例では、ディレクトリ コマンドを実行する `xp_cmdshell` 拡張ストアド プロシージャを示します。  
  
```  
EXEC master..xp_cmdshell 'dir *.exe''  
```  
  
### <a name="b-returning-no-output"></a>B. 出力を返さない  
 次の例で`xp_cmdshell`は、を使用して、クライアントに出力を返さずにコマンド文字列を実行します。  
  
```  
USE master;  
  
EXEC xp_cmdshell 'copy c:\SQLbcks\AdvWorks.bck  
    \\server2\backups\SQLbcks, NO_OUTPUT';  
GO  
```  
  
### <a name="c-using-return-status"></a>C. リターンステータスの使用  
 次の例では、 `xp_cmdshell`拡張ストアドプロシージャによって戻り値の状態も提案されます。 リターンコード値は変数`@result`に格納されます。  
  
```  
DECLARE @result int;  
EXEC @result = xp_cmdshell 'dir *.exe';  
IF (@result = 0)  
   PRINT 'Success'  
ELSE  
   PRINT 'Failure';  
```  
  
### <a name="d-writing-variable-contents-to-a-file"></a>D. 変数の内容をファイルに書き込む  
 次の例では、`@var` 変数の内容を、現在のサーバー ディレクトリにある `var_out.txt` というファイルに書き込みます。  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'Hello world';  
SET @cmd = 'echo ' + @var + ' > var_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
### <a name="e-capturing-the-result-of-a-command-to-a-file"></a>E. コマンドの結果をファイルにキャプチャする  
 次の例では、現在のディレクトリの内容を、現在`dir_out.txt`のサーバーディレクトリ内のという名前のファイルに書き込みます。  
  
```  
DECLARE @cmd sysname, @var sysname;  
SET @var = 'dir/p';  
SET @cmd = @var + ' > dir_out.txt';  
EXEC master..xp_cmdshell @cmd;  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;の一般的な拡張ストアドプロシージャ](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_cmdshell サーバー構成オプション](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md)   
 [セキュリティ構成](../../relational-databases/security/surface-area-configuration.md)   
 [sp_xp_cmdshell_proxy_account &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md)  
  
  
