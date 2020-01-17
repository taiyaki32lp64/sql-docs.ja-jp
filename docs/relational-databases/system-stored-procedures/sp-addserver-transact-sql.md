---
title: sp_addserver (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addserver
- sp_addserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addserver
- renaming servers
- machine names [SQL Server]
- computer names
ms.assetid: 160a6b29-5e80-44ab-80ec-77d4280f627c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8924a2a5c0960137eb5fe2a78d2ea7f3521b3929
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381716"
---
# <a name="sp_addserver-transact-sql"></a>sp_addserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のローカル インスタンスの名前を定義します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をホストしているコンピューターの名前が変更された場合は、 **sp_addserver**を使用して、新しいコンピューター名の [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] をインスタンスに通知します。 このプロシージャは、コンピューターでホストされている、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のすべてのインスタンスで実行する必要があります。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスの名前は変更できません。 名前付きインスタンスのインスタンス名を変更するには、指定した名前で新しいインスタンスをインストールし、古いインスタンスからデータベース ファイルをデタッチし、新しいインスタンスにデータベースをアタッチして古いインスタンスをドロップします。 または、クライアント コンピューター上でクライアント別名を作成して、サーバー コンピューター上のインスタンス名を変更せずに、接続を別のサーバーとインスタンス名か **サーバー:ポート** の組み合せにリダイレクトできます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addserver [ @server = ] 'server' ,  
     [ @local = ] 'local'   
     [ , [ @duplicate_ok = ] 'duplicate_OK' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @server = ] 'server'` はサーバーの名前です。 サーバー名は一意で、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows のコンピューター名の規則に従っている必要があります。ただし、スペースは使用できません。 *server* のデータ型は **sysname**で、既定値はありません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンスがコンピューターにインストールされている場合、インスタンスは別のサーバー上にあるように動作します。 *サーバー*を*servername\instancename*として参照し、名前付きインスタンスを指定します。  
  
`[ @local = ] 'LOCAL'` は、ローカルサーバーとして追加されるサーバーを指定します。 **\@ローカル**は**varchar (10)** ,、既定値は NULL です。 ローカルとして **\@local**を指定すると、ローカルサーバーの名前として **\@server** **が定義さ**れ、@@SERVERNAME 関数によって*サーバー*の値が返されます。  
  
 インストール中、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップによってこの変数がコンピューター名に設定されます。 既定では、追加構成を行うことなく、ユーザーはこのコンピューター名を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続できます。  
  
 ローカル定義は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] を再起動した後に有効になります。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の各インスタンスでは、1 つのローカル サーバーだけを定義できます。  
  
`[ @duplicate_ok = ] 'duplicate_OK'`、重複するサーバー名を許可するかどうかを指定します。 **\@duplicate_OK**は**varchar (13)** ,、既定値は NULL です。 **\@duplicate_OK**には**DUPLICATE_OK**または NULL のみを指定できます。 **Duplicate_OK**が指定されていて、追加されるサーバー名が既に存在する場合、エラーは発生しません。 名前付きパラメーターを使用しない場合は、 **\@local**を指定する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>Remarks  
 サーバーオプションを設定またはクリアするには、 **sp_serveroption**を使用します。  
  
 **sp_addserver**は、ユーザー定義のトランザクション内では使用できません。  
  
 リモートサーバーを追加するために**sp_addserver**を使用することは廃止されました。 代わりに [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) を使用してください。  
  
## <a name="permissions"></a>アクセス許可  
 **setupadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] をホストしているコンピューターの名前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エントリを `ACCOUNTS`に変更します。  
  
```  
sp_addserver 'ACCOUNTS', 'local';  
```  
  
## <a name="see-also"></a>参照  
 [SQL Server のスタンドアロンインスタンスをホストするコンピューターの名前を変更](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [transact-sql &#40;  の&#41; sp_dropserver](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)  
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
