---
title: sp_setapprole (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/12/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_setapprole
- sp_setapprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_setapprole
ms.assetid: cf0901c0-5f90-42d4-9d5b-8772c904062d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: de85505295ceff98f404b2ba4c1effe3946fdbe5
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304962"
---
# <a name="sp_setapprole-transact-sql"></a>sp_setapprole (Transact-sql)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在のデータベースのアプリケーションロールに関連付けられている権限をアクティブにします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  

```sql
sp_setapprole [ @rolename = ] 'role',  
    [ @password = ] { encrypt N'password' }
      |  
        'password' [ , [ @encrypt = ] { 'none' | 'odbc' } ]  
        [ , [ @fCreateCookie = ] true | false ]  
    [ , [ @cookie = ] @cookie OUTPUT ]  
```

## <a name="arguments"></a>引数

`[ @rolename = ] 'role'` は、現在のデータベースで定義されているアプリケーションロールの名前です。 *role*の型は**sysname**で、既定値はありません。 *ロール*は現在のデータベースに存在している必要があります。  
  
`[ @password = ] { encrypt N'password' }` は、アプリケーションロールをアクティブ化するために必要なパスワードです。 *パスワード*は**sysname**,、既定値はありません。 ODBC **encrypt**関数を使用すると、*パスワード*を難読化できます。 **Encrypt**関数を使用する場合は、最初の引用符の前に**N**を配置することで、パスワードを Unicode 文字列に変換する必要があります。  
  
 [暗号化] オプションは、 **SqlClient**を使用している接続ではサポートされていません。  
  
> [!IMPORTANT]  
> ODBC **encrypt**関数では、暗号化は提供されません。 ネットワーク経由で転送されるパスワードを保護するために、この機能に依存しないでください。 この情報がネットワーク経由で送信される場合は、SSL または IPSec を使用します。
  
 **@encrypt = ' none '**  
 暗号化を使用しないことを示します。 パスワードはプレーンテキストとして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に渡されます。 これは既定値です。  
  
 **@encrypt= ' odbc '**  
 Odbc で、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]にパスワードを送信する前に ODBC **encrypt**関数を使用してパスワードを難読化することを指定します。 これは、ODBC クライアントまたは OLE DB Provider for SQL Server のいずれかを使用している場合にのみ指定できます。  
  
`[ @fCreateCookie = ] true | false` クッキーを作成するかどうかを指定します。 **true**は、暗黙的に1に変換されます。 **false**は暗黙的に0に変換されます。  
  
`[ @cookie = ] @cookie OUTPUT` クッキーを格納する出力パラメーターを指定します。 クッキーが生成されるのは、 **\@fCreateCookie**の値が**true**の場合だけです。 **varbinary(8000)**  
  
> [!NOTE]  
> **sp_setapprole** のクッキーの **OUTPUT** パラメーターは現在、適切な最大長である **varbinary(8000)** としてドキュメントに記載されています。 ただし、現在の実装では **varbinary(50)** を返します。 アプリケーションは、今後のリリースでクッキーの戻り値のサイズが増加した場合にアプリケーションが引き続き正常に動作するように、 **varbinary (8000)** を引き続き予約する必要があります。
  
## <a name="return-code-values"></a>リターン コードの値

 0 (成功) と 1 (失敗)  
  
## <a name="remarks"></a>Remarks

 **Sp_setapprole**を使用してアプリケーションロールをアクティブ化した後は、ユーザーがサーバーとの接続を切断するか**sp_unsetapprole**を実行するまで、ロールはアクティブのままになります。 **sp_setapprole**は、直接 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントによってのみ実行できます。 **sp_setapprole**は、別のストアドプロシージャ内、またはユーザー定義のトランザクション内では実行できません。  
  
 アプリケーションロールの概要については、「[アプリケーションロール](../../relational-databases/security/authentication-access/application-roles.md)」を参照してください。  
  
> [!IMPORTANT]  
> ネットワーク経由で転送されるときにアプリケーションロールのパスワードを保護するには、アプリケーションロールを有効にするときに、常に暗号化された接続を使用する必要があります。
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC **encrypt**オプションは、 **SqlClient**ではサポートされていません。 資格情報を格納する必要がある場合は、Crypto API 関数を使用して暗号化します。 パラメーターの*パスワード*は、一方向のハッシュとして格納されます。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]との互換性を維持するために、パスワードの複雑さのポリシーは**sp_addapprole**によって強制されません。 パスワードの複雑さのポリシーを適用するには、[[アプリケーションロールの作成](../../t-sql/statements/create-application-role-transact-sql.md)] を使用します。  
  
## <a name="permissions"></a>アクセス許可

**Public**のメンバーシップと、ロールのパスワードに関する知識が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-activating-an-application-role-without-the-encrypt-option"></a>A. 暗号化オプションを使用せずにアプリケーションロールをアクティブ化する

 次の例では、アプリケーション ロール `SalesAppRole` をアクティブにします。このロールには、プレーンテキストのパスワード `AsDeF00MbXX` が設定されており、現在のユーザーが使用するアプリケーション用に特別に設計された権限が与えられています。

```sql
EXEC sys.sp_setapprole 'SalesApprole', 'AsDeF00MbXX';  
GO
```

### <a name="b-activating-an-application-role-with-a-cookie-and-then-reverting-to-the-original-context"></a>b. Cookie を使用してアプリケーションロールをアクティブ化し、元のコンテキストに戻す

 次の例では、パスワード `Sales11` が設定されているアプリケーション ロール `fdsd896#gfdbfdkjgh700mM` をアクティブ化し、クッキーを作成します。 この例では、現在のユーザーの名前が返されます。その後、`sp_unsetapprole` を実行して元のコンテキストに戻します。  

```sql
DECLARE @cookie varbinary(8000);  
EXEC sys.sp_setapprole 'Sales11', 'fdsd896#gfdbfdkjgh700mM'  
    , @fCreateCookie = true, @cookie = @cookie OUTPUT;  
-- The application role is now active.  
SELECT USER_NAME();  
-- This will return the name of the application role, Sales11.  
EXEC sys.sp_unsetapprole @cookie;  
-- The application role is no longer active.  
-- The original context has now been restored.  
GO  
SELECT USER_NAME();  
-- This will return the name of the original user.
GO
```

## <a name="see-also"></a>参照

 [システムストアドプロシージャ&#40;&#41; transact-sql](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md) [セキュリティストアド&#40;プロシージャ transact-sql の&#41; ](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md) [作成アプリケーション&#40;ロール transact-sql の&#41; ](../../t-sql/statements/create-application-role-transact-sql.md) [DROP application role &#40;&#41; ](../../t-sql/statements/drop-application-role-transact-sql.md) transact-sql [sp_unsetapprole &#40;transact-sql の&#41; ](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md)場合)
