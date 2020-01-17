---
title: データベース メール プロファイルの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], public profiles
- profiles [SQL Server], Database Mail
- public profiles [Database Mail]
ms.assetid: 58ae749d-6ada-4f9c-bf00-de7c7a992a2d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 55eab0bbfacdde17ff69dd36a0641561695bc14d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62872208"
---
# <a name="create-a-database-mail-profile"></a>データベース メール プロファイルの作成
  **データベース メール構成ウィザード** または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、データベース メールのパブリック プロファイルとプライベート プロファイルを作成します。  
  

  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件  
 プロファイルに対応する 1 つ以上のデータベース メール アカウントを作成します。 データベース メール アカウントの作成方法については、「 [データベース メール アカウントの作成](create-a-database-mail-account.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
 パブリック プロファイルにより、 **msdb** データベースにアクセスできるすべてのユーザーが、このプロファイルを使用して電子メールを送信できます。 プライベート プロファイルを使用できるのは、ユーザーまたはロールです。 プロファイルにロールのアクセス権を付与すると、保守が簡単なアーキテクチャを作成できます。 メールを送信するには、 **msdb** データベースの **DatabaseMailUserRole** のメンバーであることに加えて、少なくとも 1 つのデータベース メール プロファイルへのアクセス許可が必要です。  
  
####  <a name="Permissions"></a> Permissions  
 プロファイル アカウントを作成し、ストアド プロシージャを実行するユーザーは、sysadmin 固定サーバー ロールのメンバーである必要があります。  
  

  
##  <a name="SSMSProcedure"></a> データベース メール構成ウィザードの使用  
 **データベース メール プロファイルを作成するには**  
  
-   オブジェクト エクスプローラーで、データベース メールを構成する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続し、サーバー ツリーを展開します。  
  
-   **[管理]** ノードを展開します。  
  
-   [データベース メール] をダブルクリックして、データベース メール構成ウィザードを開きます。  
  
-   **[構成タスクの選択]** ページで、 **[データベース メール アカウントおよびプロファイルを管理する]** オプションを選択して、 **[次へ]** をクリックします。  
  
-   **[プロファイルとアカウントの管理]** ページで、 **[新しいプロファイルを作成する]** オプションを選択し、 **[次へ]** をクリックします。  
  
-   **[新しいプロファイル]** ページで、プロファイル名と説明を指定し、プロファイルに含めるアカウントを追加して、 **[次へ]** をクリックします。  
  
-   **[ウィザードの完了]** ページで、実行される動作を確認し、 **[完了]** をクリックして、新しいプロファイルの作成を完了します。  
  
-   **データベース メールのプライベート プロファイルを構成するには**  
  
    -   データベース メール構成ウィザードを開きます。  
  
    -   **[構成タスクの選択]** ページで、 **[データベース メール アカウントおよびプロファイルを管理する]** オプションを選択して、 **[次へ]** をクリックします。  
  
    -   **[プロファイルとアカウントの管理]** ページで、 **[プロファイル セキュリティの管理]** オプションを選択し、 **[次へ]** をクリックします。  
  
    -   **[プライベート プロファイル]** タブで、構成するプロファイルのチェック ボックスをオンにし、 **[次へ]** をクリックします。  
  
    -   **[ウィザードの完了]** ページで、実行される動作を確認し、 **[完了]** をクリックして、プロファイルの構成を完了します。  
  
-   **データベース メールのパブリック プロファイルを構成するには**  
  
    -   データベース メール構成ウィザードを開きます。  
  
    -   **[構成タスクの選択]** ページで、 **[データベース メール アカウントおよびプロファイルを管理する]** オプションを選択して、 **[次へ]** をクリックします。  
  
    -   **[プロファイルとアカウントの管理]** ページで、 **[プロファイル セキュリティの管理]** オプションを選択し、 **[次へ]** をクリックします。  
  
    -   **[パブリック プロファイル]** タブで、構成するプロファイルのチェック ボックスをオンにし、 **[次へ]** をクリックします。  
  
    -   **[ウィザードの完了]** ページで、実行される動作を確認し、 **[完了]** をクリックして、プロファイルの構成を完了します。  
  

  
## <a name="using-transact-sql"></a>Transact-SQL の使用  
  
###  <a name="PrivateProfile"></a> データベース メールのプライベート プロファイルを作成するには  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続します。  
  
-   新しいプロファイルを作成するには、システム ストアド プロシージャ [sysmail_add_profile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql) を次のように実行します。  
  
     **EXECUTEmsdb.dbo.sysmail_add_profile_sp**  
  
     *@profile_name* = '*Profile Name*'  
  
     *@description* = '*Desciption*'  
  
     *@profile_name* はプロファイルの名前です。 *@description* はプロファイルの説明です。 このパラメーターはオプションです。  
  
-   アカウントごとに、ストアド プロシージャ [sysmail_add_profileaccount_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql) を次のように実行します。  
  
     **EXECUTEmsdb.dbo.sysmail_add_profileaccount_sp**  
  
     *@profile_name* = '*Name of the profile*'  
  
     *@account_name* = '*Name of the account*'  
  
     *@sequence_number* = '*sequence number of the account within the profile.* '  
  
     *@profile_name* はプロファイルの名前です。 *@account_name* は、プロファイルに追加するアカウントの名前です。 *@sequence_number* は、プロファイル内のアカウントが使用される順序を決定します。  
  
-   このプロファイルを使用してメールを送信する各データベース ロールまたはユーザーについて、プロファイルへのアクセス権を付与します。 そのためには、ストアド プロシージャ [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql) を次のように実行します。  
  
     **EXECUTEmsdb.sysmail_add_principalprofile_sp**  
  
     *@profile_name* = '*Name of the profile*'  
  
     *@ principal_name* = '*Name of the database user or role*'  
  
     *@is_default* = '*Default Profile status* '  
  
     *@profile_name* はプロファイルの名前です。 *@principal_name* はデータベース ユーザーまたはロールの名前です。 *@is_default* は、このプロファイルが、データベース ユーザーまたはロールの既定のプロファイルであるかどうかを決定します。  
  
 次の例ではまず、データベース メール アカウントを作成し、データベース メールのプライベート プロファイルを作成します。その後、アカウントをプロファイルに追加し、そのプロファイルへのアクセス権を、 **msdb** データベースの **DBMailUsers** データベース ロールに与えます。  
  
```  
-- Create a Database Mail account  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @replyto_address = 'danw@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
  
-- Create a Database Mail profile  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @description = 'Profile used for administrative mail.' ;  
  
-- Add the account to the profile  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @account_name = 'AdventureWorks Administrator',  
    @sequence_number =1 ;  
  
-- Grant access to the profile to the DBMailUsers role  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @principal_name = 'ApplicationUser',  
    @is_default = 1 ;  
```  
  
 
  
###  <a name="PublicProfile"></a> データベース メールのパブリック プロファイルを作成するには  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続します。  
  
-   新しいプロファイルを作成するには、システム ストアド プロシージャ [sysmail_add_profile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql) を次のように実行します。  
  
     **EXECUTEmsdb.dbo.sysmail_add_profile_sp**  
  
     *@profile_name* = '*Profile Name*'  
  
     *@description* = '*Desciption*'  
  
     *@profile_name* はプロファイルの名前です。 *@description* はプロファイルの説明です。 このパラメーターはオプションです。  
  
-   アカウントごとに、ストアド プロシージャ [sysmail_add_profileaccount_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql) を次のように実行します。  
  
     **EXECUTEmsdb.dbo.sysmail_add_profileaccount_sp**  
  
     *@profile_name* = '*Name of the profile*'  
  
     *@account_name* = '*Name of the account*'  
  
     *@sequence_number* = '*sequence number of the account within the profile.* '  
  
     *@profile_name* はプロファイルの名前です。 *@account_name* は、プロファイルに追加するアカウントの名前です。 *@sequence_number* は、プロファイル内のアカウントが使用される順序を決定します。  
  
-   パブリック アクセス権を付与するには、ストアド プロシージャ [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql) を次のように実行します。  
  
     **EXECUTEmsdb.sysmail_add_principalprofile_sp**  
  
     *@profile_name* = '*Name of the profile*'  
  
     *@ principal_name* = '**public** or **0**'  
  
     *@is_default* = '*Default Profile status* '  
  
     *@profile_name* はプロファイルの名前です。 *@principal_name* は、このプロファイルがパブリック プロファイルであることを示します。 *@is_default* は、このプロファイルが、データベース ユーザーまたはロールの既定のプロファイルであるかどうかを決定します。  
  
 次の例ではまず、データベース メール アカウントを作成し、データベース メールのプライベート プロファイルを作成します。その後、アカウントをプロファイルに追加し、そのプロファイルへのパブリック アクセス権を与えます。  
  
```  
-- Create a Database Mail account  
  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Public Account',  
    @description = 'Mail account for use by all database users.',  
    @email_address = 'db_users@Adventure-Works.com',  
    @replyto_address = 'danw@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
  
-- Create a Database Mail profile  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @description = 'Profile used for administrative mail.' ;  
  
-- Add the account to the profile  
  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @account_name = 'AdventureWorks Public Account',  
    @sequence_number =1 ;  
  
-- Grant access to the profile to all users in the msdb database  
  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @principal_name = 'public',  
    @is_default = 1 ;  
```  
  

  
  
