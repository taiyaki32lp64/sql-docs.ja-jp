---
title: リモート サーバー | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- server management [SQL Server], remote servers
- remote servers [SQL Server], configuring
- remote servers [SQL Server]
- servers [SQL Server], remote
- remote access option
ms.assetid: abf0fa24-f199-4273-9a1a-e8787ac9bee1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2b3c4937d87d166d87711389be7acd0c4ae0f8ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938183"
---
# <a name="remote-servers"></a>リモート サーバー
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、旧バージョンとの互換性を保つ目的でのみ、リモート サーバーがサポートされています。 新しいアプリケーションでは、リモート サーバーではなく、リンク サーバーを使用してください。 詳しくは、「 [リンク サーバー &#40;データベース エンジン&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)」を参照してください。  
  
 リモート サーバーを構成することによって、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続しているクライアントは、新たに接続を確立することなく、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の別のインスタンスでストアド プロシージャを実行できます。 クライアントが接続するサーバーは、クライアントからの要求を受け、この要求をクライアントの代わりにリモート サーバーに送信します。 リモート サーバーが、要求を処理し、要求を行ったサーバーに結果を返します。 結果を受け取ったサーバーは、結果をクライアントに渡します。 リモート サーバーを構成する場合は、セキュリティをどのように確立するかを検討する必要もあります。  
  
 サーバー構成を設定して、別のサーバー上のストアド プロシージャを実行できるようにする場合に、まだリモート サーバーを構成していない場合は、リモート サーバーの代わりにリンク サーバーを使用してください。 リンク サーバーではストアド プロシージャと分散クエリの両方を使用できます。これに対して、リモート サーバーで使用できるのはストアド プロシージャだけです。  
  
## <a name="remote-server-details"></a>リモート サーバーの詳細  
 リモート サーバーは、組で設定します。 1 組のリモート サーバーを設定するには、両方のサーバーが相互にリモート サーバーとして認識できるように構成します。  
  
 通常は、リモート サーバーの構成オプションを設定する必要はありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって、ローカル コンピューターとリモート コンピューターの両方にリモート サーバー接続を可能にする既定値が設定されます。  
  
 リモート サーバー アクセスが機能するには、ローカルとリモートの両方のコンピューターで **remote access** 構成オプションが 1 に設定されている必要があります。 (これは既定の設定です)。**remote access** は、リモート サーバーからのログインを制御するオプションです。 この構成オプションを再設定するには、[!INCLUDE[tsql](../../includes/tsql-md.md)] **sp_configure** ストアド プロシージャまたは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用します。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してこのオプションを設定する場合は、 **[サーバーのプロパティ]** の [接続] ページで **[このサーバーへのリモート接続を許可する]** チェック ボックスをオンにします。 **[サーバーのプロパティ]** の [接続] ページにアクセスするには、オブジェクト エクスプローラーでサーバー名を右クリックし、 **[プロパティ]** をクリックします。 **[サーバーのプロパティ]** ページで、 **[接続]** ページをクリックします。  
  
 ローカル サーバーからリモート サーバー構成を無効にすると、組になっているリモート サーバー上のユーザーはそのローカル サーバーにアクセスできなくなります。  
  
## <a name="security-for-remote-servers"></a>リモート サーバーのセキュリティ  
 リモート サーバーに対する RPC (リモート プロシージャ コール) を有効にするには、そのリモート サーバーでログイン マッピングを設定する必要があります。場合によっては、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを実行しているローカル サーバーでの設定も必要になります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、RPC は既定で無効になっています。 この構成により、攻撃可能な領域を減らしてサーバーのセキュリティを強化できます。 RPC を使用する場合は、事前にこの機能を有効にする必要があります。 詳細については、「 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)」を参照してください。  
  
### <a name="setting-up-the-remote-server"></a>リモート サーバーのセットアップ  
 リモート ログインのマッピングは、リモート サーバーで設定する必要があります。 リモート サーバーはこれらのマッピングを使用して、指定のサーバーから RPC 接続用に受信したログインをローカル ログインにマップします。 リモート ログインのマッピングは、リモート サーバーで **sp_addremotelogin** ストアド プロシージャを使用して設定できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **sp_remoteoption** の **trusted** オプションがサポートされていません。  
  
### <a name="setting-up-the-local-server"></a>ローカル サーバーのセットアップ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のローカル ログインの場合、ローカル サーバーでログインのマッピングを設定する必要はありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって、リモート サーバーへの接続にローカル ログインとパスワードが使用されます。 Windows 認証のログインの場合は、ローカル ログインのマッピングをローカル サーバーで設定します。このマッピングでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスがリモート サーバーに RPC 接続する際に使用するログインとパスワードを定義します。  
  
 Windows 認証で作成されたログインの場合は、 **sp_addlinkedservlogin** ストアド プロシージャを使用して、ログイン名とパスワードへのマッピングを作成する必要があります。 このログイン名とパスワードは、 **sp_addremotelogin**によって作成され、リモート サーバーが予期していた受信ログイン名とパスワードに一致している必要があります。  
  
> [!NOTE]  
>  可能な場合は、Windows 認証を使用します。  
  
### <a name="remote-server-security-example"></a>リモート サーバーのセキュリティの例  
 **serverSend** と **serverReceive** という [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールがあるとします。 **serverReceive** は、 **Sales_Mary**という **serverSend**からの受信ログインを、 **serverReceive** の **Alice** という [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のログインにマップするように構成されています。 **serverSend**からの **Joe**という別の受信ログインは、 **serverReceive**_の_ **Joe** という[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のログインにマップされます。  
  
 次の Transact-SQL コードの例では、 `serverSend` に対して RPC を実行するように `serverReceive`を構成しています。  
  
```  
--Create remote server entry for RPCs   
--from serverSend in serverReceive.  
EXEC sp_addserver 'serverSend';  
GO  
  
--Create remote login mapping for login 'Sales_Mary' from serverSend  
--to Alice.  
EXEC sp_addremotelogin 'serverSend', 'Alice', 'Sales_Mary';  
GO  
--Create remote login mapping for login Joe from serverReceive   
--to same login.  
--Assumes same password for Joe in both servers.  
EXEC sp_addremotelogin 'serverSend', 'Joe', 'Joe';  
GO  
```  
  
 `serverSend`では、Windows 認証のログイン `Sales\Mary` をログイン `Sales_Mary`に変換するようにローカル ログインのマッピングが作成されます。 `Joe`には `serverReceive` に対するマッピングがあり、既定では同じログイン名とパスワードが使用されるので、 `Joe`のローカル マッピングは不要です。  
  
```  
--Create a remote server entry for RPCs from serverReceive.  
EXEC sp_addserver 'serverReceive';  
GO  
--Create a local login mapping for the Windows authenticated login.  
--Sales\Mary to Sales_Mary. The password should match the  
--password for the login Sales_Mary in serverReceive.  
EXEC sp_addlinkedsrvlogin 'serverReceive', false, 'Sales\Mary',  
   'Sales_Mary', '430[fj%dk';  
GO  
```  
  
## <a name="viewing-local-or-remote-server-properties"></a>ローカル サーバーまたはリモート サーバーのプロパティの表示  
 **xp_msver** 拡張ストアド プロシージャを使用すると、ローカル サーバーまたはリモート サーバーのサーバー属性を確認できます。 これらの属性には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のバージョン番号、コンピューターのプロセッサの種類と数、およびオペレーティング システムのバージョンが格納されています。 リモート サーバーのデータベース、ファイル、ログイン、およびツールを、ローカル サーバーで表示できます。 詳細については、「[xp_msver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-msver-transact-sql.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 [リンク サーバー &#40;データベース エンジン&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
 [remote access サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)  
  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
