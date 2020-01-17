---
title: システム管理者がロックアウトされた場合の SQL Server への接続 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- connecting when locked out [SQL Server]
- locked out [SQL Server]
ms.assetid: c0c0082e-b867-480f-a54b-79f2a94ceb67
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ebaa078fc3be919a6114ad275b0ef5ece6f0d0d7
ms.sourcegitcommit: ede04340adbf085e668a2536d4f7114abba14a0c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74761211"
---
# <a name="connect-to-sql-server-when-system-administrators-are-locked-out"></a>システム管理者がロックアウトされた場合の SQL Server への接続
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、システム管理者が [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] へのアクセスを復旧する方法について説明します。 システム管理者は、次のいずれかの理由で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにアクセスできなくなることがあります。  
  
-   sysadmin 固定サーバー ロールのメンバーであるログインがすべて、誤って削除された。  
  
-   sysadmin 固定サーバー ロールのメンバーである Windows グループがすべて、誤って削除された。  
  
-   sysadmin 固定サーバー ロールのメンバーであるログインの使用者が退社したか不在である。  
  
-   sa アカウントが無効になっているか、パスワードが不明である。  
  
 アクセスを復旧する 1 つの方法は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再インストールし、すべてのデータベースを新しいインスタンスにアタッチすることです。 この解決方法は時間がかかるうえ、ログインを復旧するには、バックアップから master データベースを復元する必要が生じる場合があります。 master データベースのバックアップが古いと、一部の情報が含まれていない可能性があります。 master データベースのバックアップが新しいと、以前のインスタンスと同じログインが含まれているために管理者がロックアウトされたままになる可能性があります。  
  
## <a name="resolution"></a>解決策  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -m **オプションまたは** -f **オプションを使用して、** のインスタンスをシングル ユーザー モードで起動します。 これにより、コンピューターのローカル Administrators グループのメンバーがすべて、固定サーバー ロール sysadmin のメンバーとして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに接続できるようになります。  
  
> [!NOTE]  
>  シングル ユーザー モードで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを起動する場合は、まず [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを停止してください。 そうしないと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって先に接続が行われ、2 番目のユーザーとして接続できなくなる場合があります。  
  
 **sqlcmd** または **で** -m [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]オプションを使用すると、接続を特定のクライアント アプリケーションに限定できます。 たとえば、 **-m"sqlcmd"** を使用すると、接続が、 **sqlcmd** クライアント プログラムとして識別される必要がある単一の接続に限定されます。 このオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をシングル ユーザー モードで起動するときに、その唯一の接続を不明なクライアント アプリケーションによって使用されていた場合に使用します。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]のクエリ エディターを使用して接続するには、 **-m"Microsoft SQL Server Management Studio - Query"** を使用します。  
  
> [!IMPORTANT]  
>  このオプションをセキュリティ機能として使用しないでください。 クライアント アプリケーションの名前はクライアント アプリケーションによって接続文字列の一部として指定されるため、本当の名前が指定されるとは限りません。  
  
 シングル ユーザー モードで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を起動する手順の詳細については、「[サーバーのスタートアップ オプションの構成 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)」を参照してください。  
  
## <a name="step-by-step-instructions"></a>詳細な手順  
 次の手順では、Windows 8 以降で実行されている [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] に接続するためのプロセスについて説明します。 以前のバージョンの SQL Server または Windows の場合の若干の調整についても示しています。 ここで示す手順は、ローカルの Administrators グループのメンバーとして Windows にログオンした状態で実行する必要があります。また、この手順では、コンピューターに [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] がインストールされていることを前提としています。  
  
1.  スタート ページで、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を起動します。 **[表示]** メニューの **[登録済みサーバー]** をクリックします (サーバーをまだ登録していない場合は、 **[ローカル サーバー グループ]** を右クリックし、 **[タスク]** をポイントして、 **[ローカル サーバーの登録]** をクリックします)。  
  
2.  [登録済みサーバー] で、サーバーを右クリックし、 **[SQL Server 構成マネージャー]** をクリックします。 管理者として実行してもよいかどうかが確認され、構成マネージャー プログラムが起動します。  
  
3.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]を終了します。  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーの左ペインで、 **[SQL Server のサービス]** を選択します。 右ペインで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスを探します ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスには、コンピューター名の後に **(MSSQLSERVER)** が付いています。 名前付きインスタンスは、[登録済みサーバー] に表示されているものと同じ名前が大文字表記で表示されます)。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[起動時のパラメーター]** タブの **[起動時のパラメーターの指定]** ボックスに、「`-m`」と入力し、 **[追加]** をクリックします (入力文字はダッシュの後に小文字の m です)。  
  
    > [!NOTE]  
    >  以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **[起動時のパラメーター]** タブがない場合があります。その場合は、 **[詳細設定]** タブで、 **[起動時のパラメーター]** をダブルクリックします。 パラメーターが小さいウィンドウに表示されます。 既存のパラメーターは、いずれも変更しないように注意してください。 最後に、新しいパラメーター `;-m` を追加し、 **[OK]** をクリックします (入力文字はセミコロンの後に小文字の m です)。  
  
6.  **[OK]** をクリックし、再起動するためのメッセージが表示されたら、サーバー名を右クリックし、 **[再起動]** をクリックします。  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動すると、サーバーはシングル ユーザー モードになります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行されていないことを確認します。 起動した場合、それが唯一の接続となります。  
  
8.  Windows 8 のスタート画面で、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]のアイコンを右クリックします。 画面の下部で、 **[管理者として実行]** を選択します (これにより、管理者資格情報が SSMS に渡されます)。  
  
    > [!NOTE]  
    >  以前のバージョンの Windows では、 **[管理者として実行]** オプションはサブメニューとして表示されます。  
  
     構成によっては、SSMS が複数の接続の確立を試みます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はシングル ユーザー モードなので、複数の接続は失敗します。 次のいずれかの操作を選択して実行できます。 次のいずれかの操作を行います。  
  
    1.  Windows 認証 (管理者の資格情報を含む) を使用してオブジェクト エクスプローラーと接続します。 **[セキュリティ]** 、 **[ログイン]** の順に展開し、自身のログインをダブルクリックします。 **[サーバー ロール]** ページで、 **[sysadmin]** を選択し、 **[OK]** をクリックします。  
  
    2.  オブジェクト エクスプローラーではなく、Windows 認証 (管理者の資格情報を含む) を使用してクエリ ウィンドウと接続します (この方法で接続できるのは、オブジェクト エクスプローラーと接続していない場合のみです)。**sysadmin** 固定サーバー ロールのメンバーである新しい Windows 認証ログインを追加するには、次のようなコードを実行します。 次の例では、`CONTOSO\PatK` という名前のドメイン ユーザーを追加します。  
  
        ```  
        CREATE LOGIN [CONTOSO\PatK] FROM WINDOWS;  
        ALTER SERVER ROLE sysadmin ADD MEMBER [CONTOSO\PatK];  
        ```  
  
    3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を混合認証モードで実行している場合、Windows 認証 (管理者の資格情報を含む) を使用してクエリ ウィンドウと接続します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin **固定サーバー ロールのメンバーである新しい** 認証ログインを作成するには、次のようなコードを実行します。  
  
        ```  
        CREATE LOGIN TempLogin WITH PASSWORD = '************';  
        ALTER SERVER ROLE sysadmin ADD MEMBER TempLogin;  
        ```  
  
        > [!WARNING]  
        >  ************ は強力なパスワードと置き換えてください。  
  
    4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を混合認証モードで実行していて、 **sa** アカウントのパスワードをリセットする場合、Windows 認証 (管理者の資格情報を含む) を使用してクエリ ウィンドウと接続します。 次の構文を使用して、 **sa** アカウントのパスワードを変更します。  
  
        ```  
        ALTER LOGIN sa WITH PASSWORD = '************';  
        ```  
  
        > [!WARNING]  
        >  ************ は強力なパスワードと置き換えてください。  
  
9. 次の手順では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をマルチユーザー モードに戻します。 SSMS を閉じます。  
  
10. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーの左ペインで、 **[SQL Server のサービス]** を選択します。 右ペインで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスを右クリックし、 **[プロパティ]** をクリックします。  
  
11. **[起動時のパラメーター]** タブの **[既存のパラメーター]** ボックスで、[ `-m` ] を選択し、 **[削除]** をクリックします。  
  
    > [!NOTE]  
    >  以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **[起動時のパラメーター]** タブがない場合があります。その場合は、 **[詳細設定]** タブで、 **[起動時のパラメーター]** をダブルクリックします。 パラメーターが小さいウィンドウに表示されます。 前の手順で追加した `;-m` を削除し、 **[OK]** をクリックします。  
  
12. サーバー名を右クリックし、 **[再起動]** をクリックします。 必ずもう一度 SQL Server エージェントを起動します。
  
 これで、 **sysadmin** 固定サーバー ロールのメンバーであるアカウントの 1 つを使用して正常に接続できます。  
  
## <a name="see-also"></a>参照  
 [シングル ユーザー モードでの SQL Server の起動](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)   
 [データベース エンジン サービスのスタートアップ オプション](../../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
