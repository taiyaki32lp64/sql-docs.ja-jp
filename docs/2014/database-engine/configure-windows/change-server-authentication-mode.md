---
title: サーバーの認証モードの変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- authentication [SQL Server], changing modes
- server authentication mode [SQL Server]
- modifying server authentication mode
ms.assetid: 79babcf8-19fd-4495-b8eb-453dc575cac0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 43919e335700a23a4174eb1bdf42c36c0c08fe2f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62812301"
---
# <a name="change-server-authentication-mode"></a>サーバーの認証モードの変更
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、サーバーの認証モードを変更する方法について説明します。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] はインストール中に、 **[Windows 認証モード]** または **[SQL Server 認証モードと Windows 認証モード]** のいずれかに設定されます。 インストール後は、認証モードをいつでも変更できます。  
  
 インストール中に **[Windows 認証モード]** を選択した場合、sa ログインは無効となり、パスワードはセットアップによって割り当てられます。 後で認証モードを **[SQL Server 認証モードと Windows 認証モード]** に変更しても、sa ログインは無効のままです。 sa ログインを使用するには、ALTER LOGIN ステートメントを使用して、sa ログインを有効にし、新しいパスワードを割り当ててください。 sa ログインは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用しないとサーバーに接続できません。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **サーバーの認証モードを変更する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
 sa アカウントは、よく知られた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントで、悪意のあるユーザーの攻撃対象となることが少なくありません。 sa アカウントは、アプリケーションで必要とならない限り、有効にしないでください。 sa ログインには、複雑なパスワードを使用することが非常に重要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-change-security-authentication-mode"></a>セキュリティ認証モードを変更するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[セキュリティ]** ページの **[サーバー認証]** で、新しいサーバーの認証モードを選択し、 **[OK]** をクリックします。  
  
3.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の再起動が必要であることを示す **のダイアログ ボックスで、** [OK] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をクリックします。  
  
4.  オブジェクト エクスプローラーでサーバーを右クリックし、 **[再起動]** をクリックします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントも再起動する必要があります (実行されている場合)。  
  
#### <a name="to-enable-the-sa-login"></a>sa ログインを有効にするには  
  
1.  オブジェクト エクスプ ローラーで、**セキュリティ**、ログインを展開し、右クリック`sa`、 をクリックし、**プロパティ**します。  
  
2.  **[全般]** ページで、ログインのパスワード作成と確認が必要になる場合があります。  
  
3.  **[状態]** ページで、 **[ログイン]** の **[有効]** をクリックし、 **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **sa ログインを有効にするには**  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 次の例では、sa ログインを有効にし、新しいパスワードを設定します。  
  
    ```  
    ALTER LOGIN sa ENABLE ;  
    GO  
    ALTER LOGIN sa WITH PASSWORD = '<enterStrongPasswordHere>' ;  
    GO  
  
    ```  
  
## <a name="see-also"></a>参照  
 [強力なパスワード](../../relational-databases/security/strong-passwords.md)   
 [SQL Server インストールにおけるセキュリティの考慮事項](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)   
 [システム管理者がロックアウトされた場合の SQL Server への接続](connect-to-sql-server-when-system-administrators-are-locked-out.md)  
  
  
