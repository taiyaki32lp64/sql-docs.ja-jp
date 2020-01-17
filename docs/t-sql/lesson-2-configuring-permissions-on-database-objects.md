---
title: チュートリアル:db オブジェクトに対するアクセス許可の構成
ms.custom: seo-lt-2019
ms.date: 07/31/2018
ms.prod: sql
ms.technology: t-sql
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- database permissions
ms.assetid: f964b66a-ec32-44c2-a185-6a0f173bfa22
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 991bdef702b1ed298bb492172ef65c6d25d5d0ab
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244754"
---
# <a name="lesson-2-configure-permissions-on-database-objects"></a>レッスン 2: データベース オブジェクトに対するアクセス許可の構成
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
データベースへのアクセス権をユーザーに付与するには、次の 3 つの手順があります。 まず、ログインを作成します。 ユーザーはこのログインを使用して、 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]に接続できます。 次に、指定したデータベースでユーザーとしてログインを構成します。 最後に、データベース オブジェクトに対する権限をユーザーに付与します。 このレッスンではこれらの 3 つの手順を紹介し、ビューとストアド プロシージャをオブジェクトとして作成する方法について説明します。  

  >[!NOTE]
  > このレッスンでは、[レッスン 1: データベース オブジェクトの作成](lesson-1-creating-database-objects.md)で作成されたオブジェクトを使用します。 レッスン 2 に進む前に、レッスン 1 を完了してください。 

## <a name="prerequisites"></a>前提条件
このチュートリアルを実行するには、SQL Server Management Studio と SQL Server インスタンスへのアクセスが必要です。 

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールします。

SQL Server インスタンスへのアクセス権を持っていない場合は、次のリンクからプラットフォームを選択します。 SQL 認証を選択する場合は、SQL Server のログイン資格情報を使用します。
- **Windows**:[SQL Server 2017 Developer Edition をダウンロードする](https://www.microsoft.com/sql-server/sql-server-downloads)。
- **macOS**:[Docker で SQL Server 2017 をダウンロードする](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)。

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="create-a-login"></a>ログインを作成します
[!INCLUDE[ssDE](../includes/ssde-md.md)]にアクセスするには、ユーザーのログインが必要です。 ログインは、ユーザーの ID を Windows のアカウントまたは Windows グループのメンバーとして表すか、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のみに存在する [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]ログインを使用することができます。 できるだけ Windows 認証を使用してください。  
  
既定では、コンピューターの管理者には [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]へのフル アクセス権が与えられます。 このレッスンでは、これより特権の少ないユーザーが必要なので、コンピューターに新しいローカルの Windows 認証アカウントを作成します。 そのためには、コンピューターの管理者であることが条件となります。 その後、この新しいユーザーに [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]へのアクセス権を与えます。  
  
### <a name="create-a-new-windows-account"></a>新しい Windows アカウントの作成  
  
1.  **[スタート]** ボタン、 **[ファイル名を指定して実行]** の順にクリックし、 **[名前]** ボックスに「 **%SystemRoot%\system32\compmgmt.msc /s**」と入力して、 **[OK]** をクリックします。コンピューターの管理プログラムが開きます。 
2.  **[システム ツール]** の **[ローカル ユーザーとグループ]** を展開し、 **[ユーザー]** を右クリックして、 **[新しいユーザー]** をクリックします。    
3.  **[ユーザー名]** ボックスに、「 **Mary**」と入力します。    
4.  **[パスワード]** および **[パスワードの確認入力]** ボックスに強力なパスワードを入力し、 **[作成]** をクリックして、新しいローカルの Windows ユーザーを作成します。  
  
### <a name="create-a-sql-login"></a>SQL ログインの作成  

[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]のクエリ エディター ウィンドウで、次のコードを入力して実行します。 `computer_name` は自分のコンピューター名に置き換えます。 `FROM WINDOWS` は Windows がユーザーを認証することを示します。 オプションの `DEFAULT_DATABASE` 引数は、接続文字列で別のデータベースを指定しない限り、 `Mary` を `TestData` データベースに接続します。 このステートメントでは、セミコロンが [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントのオプションの終了文字として使用されています。
  
  ```sql  
  CREATE LOGIN [computer_name\Mary]  
      FROM WINDOWS  
      WITH DEFAULT_DATABASE = [TestData];  
  GO  
  ```  
  
  これでユーザー名 `Mary`が承認され、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のこのインスタンスへのアクセスがコンピューターによって認証されます。 コンピューターに [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスが複数ある場合は、 `Mary` がアクセスする各インスタンスでログインを作成する必要があります。    
  > [!NOTE]  
  > `Mary` はドメインのアカウントではないため、このユーザー名はこのコンピューターでしか認証できません。 


## <a name="grant-access-to-a-database"></a>データベースへのアクセスを許可
これで Mary は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のこのインスタンスにアクセスできますが、データベースにアクセスする権限がありません。 データベースのユーザーとして承認されるまでは、既定の **TestData** データベースにさえアクセスできません。  
  
Mary にアクセス権を与えるには、 **TestData** データベースに切り替えてから CREATE USER ステートメントを使用して、Mary という名のユーザーにそのログインをマップします。  
  
### <a name="to-create-a-user-in-a-database"></a>データベースにユーザーを作成するには  
  
次のステートメントを入力して実行し ( `computer_name` をコンピューターの名前に置き換える)、 `Mary` に `TestData` データベースへのアクセス権を与えます。
  
 ```sql  
 USE [TestData];  
 GO  
 
 CREATE USER [Mary] FOR LOGIN [computer_name\Mary];  
 GO    
 ```  
  
 これで、Mary は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] と `TestData` の両方のデータベースにアクセスできます。  


## <a name="create-views-and-stored-procedures"></a>ビューとストアド プロシージャの作成
管理者は **Products** テーブルおよび **vw_Names** ビューから SELECT を実行し、 **pr_Names** プロシージャを実行できますが、ユーザー Mary は実行できません。 Mary に必要な権限を付与するには、GRANT ステートメントを使用します。  

### <a name="grant-permission-to-stored-procedure"></a>ストアド プロシージャへのアクセス許可の付与  
次のステートメントを実行して、 `Mary` ストアド プロシージャの `EXECUTE` 権限を `pr_Names` に与えます。
  
  ```sql  
  GRANT EXECUTE ON pr_Names TO Mary;  
  GO  
  ```  
  
このシナリオでは、Mary はストアド プロシージャを使用して **Products** テーブルにのみアクセスできます。 Mary がビューに対して SELECT ステートメントを実行できるようにする場合は、 `GRANT SELECT ON vw_Names TO Mary`も実行する必要があります。 データベース オブジェクトへのアクセス権を削除するには、REVOKE ステートメントを使用します。  
  
> [!NOTE]  
> テーブル、ビュー、およびストアド プロシージャが同じスキーマに所有されていない場合は、権限を付与すると、複雑になります。  
  
### <a name="about-grant"></a>GRANT について  
ストアド プロシージャを実行するには、EXECUTE 権限が必要です。 データにアクセスしたり、データを変更するには、SELECT、INSERT、UPDATE、および DELETE 権限が必要です。 GRANT ステートメントは、テーブルを作成する権限など、他の権限にも使用されます。  
  
## <a name="next-steps"></a>次のステップ
次の記事では、他のレッスンで作成されたデータベース オブジェクトを削除する方法について説明します。 

詳細については、次の記事に進んでください
> [!div class="nextstepaction"]
>[次の手順](lesson-3-deleting-database-objects.md)
  
