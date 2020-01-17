---
title: 新しい登録済みサーバーの作成 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.registerserver.general.sqlce.f1
- sql13.swb.registerserver.general.sqlserver.f1
helpviewer_keywords:
- Registered Servers [SQL Server], creating new registered servers
ms.assetid: 716ea070-a3b5-4514-9de2-82ce8a96514b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2fd57edd00e2e5cd6a8921f324b1de20260bfa9f
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267792"
---
# <a name="create-a-new-registered-server-sql-server-management-studio"></a>新しい登録済みサーバーの作成 (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  このトピックでは、サーバーを [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の 登録済みサーバー コンポーネントに登録することによって、頻繁にアクセスするサーバーの接続情報を保存する方法について説明します。 サーバーの登録は、接続する前か、またはオブジェクト エクスプローラーから接続するときに実行できます。 ローカル コンピューターのサーバー インスタンスを登録するには、特殊なメニュー オプションを使用します。  
  
 登録済みサーバーには、次の 2 種類があります。  
  
-   ローカル サーバー グループ  
  
     ローカル サーバー グループを使用すると、管理頻度の高いサーバーに簡単に接続できます。 ローカル サーバーとローカル以外のサーバーは、どちらもローカル サーバー グループに登録されます。 ローカル サーバー グループは各ユーザーに固有です。 登録済みサーバーの情報を共有する方法については、「 [登録済みサーバー情報のエクスポート &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/export-registered-server-information-sql-server-management-studio.md) 」および「 [登録済みサーバー情報のインポート &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/import-registered-server-information-sql-server-management-studio.md)の 登録済みサーバー コンポーネントに登録することによって、頻繁にアクセスするサーバーの接続情報を保存する方法について説明します。  
  
    > [!NOTE]  
    >  可能な限り Windows 認証を使用することをお勧めします。  
  
-   中央管理サーバー  
  
     サーバー登録は、ファイル システムではなく中央管理サーバーに保存されます。 中央管理サーバーおよび従属登録済みサーバーは、Windows 認証を使用しないと登録できません。 中央管理サーバーを登録すると、そのサーバーに関連する登録済みサーバーが自動的に表示されます。 中央管理サーバーの詳細については、「 [中央管理サーバーを使用した複数のサーバーの管理](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)」を参照してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] よりも前のバージョンの [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] では、中央管理サーバーを指定できません。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-automatically-register-the-local-server-instances"></a>ローカル サーバー インスタンスを自動的に登録するには  
  
-   [登録済みサーバー] で、[登録済みサーバー] ツリーの任意のノードを右クリックし、 **[ローカル サーバーの登録情報を更新]** をクリックします。  
  
#### <a name="to-create-a-new-registered-server"></a>新しい登録済みサーバーを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で [登録済みサーバー] が表示されていない場合は、 **[表示]** メニューの **[登録済みサーバー]** をクリックします。  
  
     **サーバーの種類**  
     [登録済みサーバー] を使用してサーバーを登録する場合、 **[サーバーの種類]** ボックスは読み取り専用になり、[登録済みサーバー] ペインに表示されているサーバーの種類と一致する値が表示されます。 別の種類のサーバーを登録するには、新しいサーバーの登録を開始する前に、 **[登録済みサーバー]** ツール バーの **[データベース エンジン]** 、 **[分析サーバー]** 、 **[Reporting Services]** 、または **[Integration Services]** をクリックします。  
  
     **サーバー名**  
     登録するサーバー インスタンスを、 *\<servername>* [\\ *\<instancename>* ] という形式で選択します。  
  
     **[認証]**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続する際には、2 つの認証モードのいずれかを選択します。  
  
     **[Windows 認証]**  
     Windows 認証モードを使用すると、ユーザーは [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ユーザー アカウントを使用して接続できます。  
  
     **SQL Server 認証 (SQL Server Authentication)**  
     指定されたログイン名とパスワードを使用して、信頼関係の低い接続から接続した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン アカウントが設定されているかどうか、指定されたパスワードが以前に記録されたパスワードと一致しているかどうかを確認することで認証を行います。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にログイン アカウントが設定されていない場合、認証は失敗し、エラー メッセージが返されます。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)] 詳細については、「 [認証モードの選択](../../relational-databases/security/choose-an-authentication-mode.md)」を参照してください。  
  
     **User name**  
     接続に使用されている、現在のユーザー名を表示します。 この読み取り専用オプションは、Windows 認証を使用した接続が指定されている場合にのみ使用できます。 **[ユーザー名]** を変更するには、別のユーザーとしてコンピューターにログインします。  
  
     **Login**  
     接続に使用するログインを入力します。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用した接続を選択した場合にのみ使用できます。  
  
     **パスワード**  
     ログインのパスワードを入力します。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用した接続を選択した場合にのみ編集できます。  
  
     **[パスワードを保存する]**  
     入力したパスワードを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で暗号化して保存する場合に選択します。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用した接続を選択した場合にのみ表示されます。  
  
    > [!NOTE]  
    >  パスワードの保存を止めるには、このチェック ボックスをオフにして **[保存]** をクリックします。  
  
     **[登録済みサーバーの名前]**  
     [登録済みサーバー] に表示する名前です。 この名前は、 **[サーバー名]** ボックスの名前と一致する必要はありません。  
  
     **[登録済みサーバーの説明]**  
     サーバーの説明をオプションで入力します。  
  
     **テスト**  
     クリックすると、 **[サーバー名]** で選択されたサーバーへの接続をテストします。  
  
     **[保存]**  
     クリックすると、登録済みサーバーの設定を保存します。  
  
## <a name="multiserver-queries"></a>マルチサーバー クエリ  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のクエリ エディター ウィンドウを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンスに同時に接続してクエリを実行できます。 クエリから返された結果は、マージして 1 つの結果ペインに表示することも、別々の結果ペインに表示することもできます。 クエリ エディターには、各行を生成したサーバーの名前と、各行を提供したサーバーへの接続に使用されたログインを表示する列をオプションで追加できます。 マルチサーバー クエリを実行する方法については、「[複数のサーバーに対してステートメントを同時に実行する方法 &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/execute-statements-against-multiple-servers-simultaneously.md)」を参照してください。  
  
 ローカル サーバー グループ内のすべてのサーバーに対してクエリを実行するには、サーバー グループを右クリックし、 **[接続]** をポイントして、 **[新しいクエリ]** をクリックします。 新しいクエリ エディター ウィンドウで実行したクエリは、ユーザー認証コンテキストなど保存されている接続情報を使用して、グループ内のすべてのサーバーに対して実行されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して登録されていても、パスワードが保存されていないサーバーは接続できません。  
  
 中央管理サーバーに登録されているすべてのサーバーに対してクエリを実行するには、中央管理サーバーを展開し、サーバー グループを右クリックして、 **[接続]** をポイントし、 **[新しいクエリ]** をクリックします。 新しいクエリ エディター ウィンドウで実行したクエリは、保存されている接続情報およびユーザーの Windows 認証コンテキストを使用して、サーバー グループ内のすべてのサーバーに対して実行されます。  
  
## <a name="see-also"></a>参照  
 [オブジェクト エクスプローラーのシステム オブジェクトの非表示](../object/hide-system-objects-in-object-explorer.md)   
 [登録済みサーバー情報のエクスポート &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/export-registered-server-information-sql-server-management-studio.md)   
 [登録済みサーバー情報のインポート &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/import-registered-server-information-sql-server-management-studio.md)  
  
  
