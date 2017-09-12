---
title: "ログインを作成する |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- creating a login
ms.assetid: a2512310-bdb6-41dc-858a-e866b2b58afc
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c8d1edc92b209fc73eb85af703058cc329a775cb
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-2-1---creating-a-login"></a>レッスン 2-1-ログインを作成します。
[!INCLUDE[ssDE](../includes/ssde-md.md)]にアクセスするには、ユーザーのログインが必要です。 ログインは、ユーザーの ID を Windows のアカウントまたは Windows グループのメンバーとして表すか、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のみに存在する [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]ログインを使用することができます。 できるだけ Windows 認証を使用してください。  
  
既定では、コンピューターの管理者には [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]へのフル アクセス権が与えられます。 このレッスンでは、これより特権の少ないユーザーが必要なので、コンピューターに新しいローカルの Windows 認証アカウントを作成します。 そのためには、コンピューターの管理者であることが条件となります。 その後、この新しいユーザーに [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]へのアクセス権を与えます。  
  
### <a name="to-create-a-new-windows-account"></a>新しい Windows アカウントを作成するには  
  
1.  [ **スタート**] ボタン、[ **ファイル名を指定して実行**] の順にクリックし、[ **名前** ] ボックスに「 **%SystemRoot%\system32\compmgmt.msc /s**」と入力して、[ **OK** ] をクリックします。コンピューターの管理プログラムが開きます。  
  
2.  [ **システム ツール**] の [ **ローカル ユーザーとグループ**] を展開し、[ **ユーザー**] を右クリックして、[ **新しいユーザー**] をクリックします。  
  
3.  [ **ユーザー名** ] ボックスに、「 **Mary**」と入力します。  
  
4.  [ **パスワード** ] および [ **パスワードの確認入力** ] ボックスに強力なパスワードを入力し、[ **作成** ] をクリックして、新しいローカルの Windows ユーザーを作成します。  
  
### <a name="to-create-a-login"></a>ログインを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]のクエリ エディター ウィンドウで、次のコードを入力して実行します。 `computer_name` は自分のコンピューター名に置き換えます。 `FROM WINDOWS` は Windows がユーザーを認証することを示します。 オプションの `DEFAULT_DATABASE` 引数は、接続文字列で別のデータベースを指定しない限り、 `Mary` を `TestData` データベースに接続します。 このステートメントでは、セミコロンが [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントのオプションの終了文字として使用されています。  
  
    ```  
    CREATE LOGIN [computer_name\Mary]  
        FROM WINDOWS  
        WITH DEFAULT_DATABASE = [TestData];  
    GO  
    ```  
  
    これでユーザー名 `Mary`が承認され、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のこのインスタンスへのアクセスがコンピューターによって認証されます。 コンピューターに [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスが複数ある場合は、 `Mary` がアクセスする各インスタンスでログインを作成する必要があります。  
  
    > [!NOTE]  
    > `Mary` はドメインのアカウントではないため、このユーザー名はこのコンピューターでしか認証できません。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
[データベースへのアクセス権の付与](../t-sql/lesson-2-2-granting-access-to-a-database.md)  
  
## <a name="see-also"></a>参照  
[CREATE LOGIN &#40;Transact-SQL&#41;](../t-sql/statements/create-login-transact-sql.md)  
[認証モードの選択](../relational-databases/security/choose-an-authentication-mode.md)  
  
  
  
