---
title: 'レッスン 1: データベース エンジンへの接続 | Microsoft Docs'
ms.custom: ''
ms.date: 02/05/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: quickstart
ms.assetid: e8db82f0-50ed-4531-9209-940006ed34cb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1bc950a7d0a576338bea9a614193ab3edaee7c96
ms.sourcegitcommit: 82b70c39550402a2b0b327db32bf5ecf88b50d3c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73032997"
---
# <a name="lesson-1-connecting-to-the-database-engine"></a>レッスン 1:データベース エンジンへの接続
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]のインストール時に一緒にインストールされるツールは、エディションとセットアップによって異なります。 このレッスンでは、主要なツールについて確認し、接続して基本機能を実行する方法について学習します。これで、さらに多くのユーザーを認証することができます。  

このレッスンの内容は次のとおりです。  
- [作業開始のためのツール](#tools)  
- [Management Studio を使用した接続](#connect)  
- [追加接続の認証](#additional) 

## <a name="tools">作業開始のためのツール</a> 
- [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] にはさまざまなツールが付属しています。 このトピックでは、作業に必要なツールを選択するときの参考となるよう、最初に必要となるツールについて説明します。 すべてのツールには、 **[スタート]** メニューからアクセスできます。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]など、一部のツールは既定ではインストールされません。 インストールするには、セットアップ中に、クライアント コンポーネントの一部としてツールを選択する必要があります。 以下のツールの詳細については、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オンライン ブックで検索してください。 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] には、これらのツールのサブセットのみが付属しています。  

### <a name="basic-tools"></a>基本ツール
- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) は、 [!INCLUDE[ssDE](../includes/ssde-md.md)] を管理し、 [!INCLUDE[tsql](../includes/tsql-md.md)] コードを記述するための主要なツールです。 このツールは、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] シェルでホストされます。 SSMS は、 [Microsoft ダウンロード センター](https://msdn.microsoft.com/library/mt238290.aspx)から無料でダウンロードできます。 最新バージョンを以前のバージョンの [!INCLUDE[ssDE_md](../includes/ssde-md.md)]で使用できます。  

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] およびクライアント ツールと共にインストールされます。 このツールを使用すると、サーバー プロトコルを有効化したり、TCP ポートなどのプロトコル オプション、サーバー サービスの自動開始、指定の方法によるクライアント コンピューターの接続などを構成することができます。 このツールはより詳細な接続要素を構成しますが、機能は有効にしません。  

### <a name="sample-database"></a>サンプル データベース
サンプル データベースとサンプルは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に付属していません。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オンライン ブックで説明されているほとんどの例では、 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] サンプル データベースを使用しています。  

##### <a name="to-start-sql-server-management-studio"></a>SQL Server Management Studio を起動するには
- 現在のバージョンの Windows では、 **スタート** ページで「SSMS」と入力し、 **[Microsoft SQL Server Management Studio]** をクリックします。  
- 以前のバージョンの Windows では、 **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]] の順にポイントして、 **[SQL Server Management Studio]** をクリックします。  

##### <a name="to-start-sql-server-configuration-manager"></a>SQL Server 構成マネージャーを起動するには  
- 現在のバージョンの Windows では、 **[スタート]** ページで「 **Configuration Manager**] の順にポイントして、 **[SQL Server *&lt;バージョン&gt;* Configuration Manager**から無料でダウンロードできます。   
- 以前のバージョンの Windows では、 **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  

## <a name="connect"></a>Management Studio を使用した接続  
- インスタンスの名前がわかり、ローカルの Administrators グループのメンバーとしてコンピューターにログインしていれば、同じコンピューターで実行されているツールから [!INCLUDE[ssDE](../includes/ssde-md.md)] に簡単に接続できます。 次の手順は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]をホストしている同じコンピューター上で実行する必要があります。  

> [!NOTE]  
> このトピックでは、オンプレミスの SQL Server への接続について説明します。 Azure SQL Database に接続するには、「 [SQL Server Management Studio を使用して SQL Database に接続し、T-SQL サンプル クエリを実行する](https://azure.microsoft.com/documentation/articles/sql-database-connect-query-ssms/)」を参照してください。  

##### <a name="to-determine-the-name-of-the-instance-of-the-database-engine"></a>データベース エンジン インスタンスの名前を確認するには  

1.  Administrators グループのメンバーとして Windows にログインし、 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]を起動します。  
2.  **[サーバーへの接続]** ダイアログ ボックスで、 **[キャンセル]** をクリックします。  
3.  [登録済みサーバー] が表示されていない場合は、 **[表示]** メニューの **[登録済みサーバー]** をクリックします。
4.  [登録済みサーバー] ツール バーで **[データベース エンジン]** を選択した状態で、 **[データベース エンジン]** を展開して **[ローカル サーバー グループ]** を右クリックし、 **[タスク]** をポイントして **[ローカル サーバーの登録]** をクリックします。 **[ローカル サーバー グループ]** を展開し、表示されているコンピューターにインストールされている [!INCLUDE[ssDE](../includes/ssde-md.md)] のすべてのインスタンスを表示します。 既定のインスタンスには名前がなく、コンピューター名で表示されます。 名前付きインスタンスは、コンピューター名の後に円記号 (\\)、その後にインスタンスの名前が続く形式で表示されます。 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] の場合は、セットアップ中に変更されない限り、インスタンス名は *<computer_name>* \sqlexpress の形式になります。  

##### <a name="to-verify-that-the-database-engine-is-running"></a>データベース エンジンが実行されていることを確認するには

1.  登録済みサーバーで、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスの名前の隣に白い矢印付きの緑色のドットが表示されていれば、 [!INCLUDE[ssDE](../includes/ssde-md.md)] は実行されています。それ以上の操作は必要ありません。  

2.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスの名前の隣に白い正方形の付いた赤いドットが表示されている場合、 [!INCLUDE[ssDE](../includes/ssde-md.md)] は停止しています。 [!INCLUDE[ssDE](../includes/ssde-md.md)]の名前を右クリックし、 **[サービス コントロール]** をクリックしてから **[開始]** をクリックします。 確認のダイアログ ボックスが表示された後に [!INCLUDE[ssDE](../includes/ssde-md.md)] が起動し、丸印が白い矢印付きの緑色に変わります。  

##### <a name="to-connect-to-the-database-engine"></a>データベース エンジンに接続するには  

[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] をインストールしたときに、少なくとも 1 人の管理者アカウントが選択されています。 管理者として Windows にログインした状態で、次の手順を実行します。

1.  [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]の **[ファイル]** メニューの **[オブジェクト エクスプローラーを接続]** をクリックします。 
- **[サーバーへの接続]** ダイアログ ボックスが開きます。 **[サーバーの種類]** ボックスに、最後に使用したコンポーネントの種類が表示されます。  

2.  **[データベース エンジン]** を選択します。

![オブジェクト エクスプ ローラー](../relational-databases/media/object-explorer.png)

3.  **[サーバー名]** ボックスに、 [!INCLUDE[ssDE](../includes/ssde-md.md)]インスタンスの名前を入力します。 SQL Server の既定のインスタンスでは、サーバー名はコンピューター名です。 SQL Server の名前付きインスタンスでは、サーバー名は _\<computer_name\>_ **\\** _\<instance_name\>_ となります (**ACCTG_SRVR\SQLEXPRESS** など)。 次のスクリーン ショットは、"PracticeComputer" という名前のコンピューター上の、既定の (名前のない) [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]インスタンスへの接続を示しています。 Windows にログオンしているユーザーは、Contoso ドメインの Mary です。 Windows 認証を使用する場合は、ユーザー名を変更することはできません。 

![connect-to-server](../relational-databases/media/connect-to-server.png)

4.  **[接続]** をクリックします。

> [!NOTE]
> このチュートリアルでは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を初めて使用し、接続時に特別な問題がないことを想定しています。 このような前提はほとんどのユーザーにとって十分であり、このチュートリアルが単純であるのはこのためです。 詳細なトラブルシューティングの手順については、「 [SQL Server データベース エンジンへの接続のトラブルシューティング](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)」を参照してください。 

## <a name="additional"></a>追加接続の認証  
ここまでの作業で、管理者として [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に接続できました。次に行う最初の作業の 1 つに、他のユーザーの接続の認証があります。 これには、ログインを作成し、そのログインに対し、ユーザーとしてデータベースにアクセスすることを認証します。 ログインは Windows 認証ログインまたは SQL Server 認証ログインです。Windows 認証ログインには Windows の資格情報が使用されます。SQL Server 認証ログインは Windows の資格情報に依存せず、認証情報は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に保存されます。 可能であれば、Windows 認証を使用します。

> [!TIP]
> ほとんどの組織では、ドメイン ユーザーが採用されており、Windows 認証が使用されます。 コンピューター上の他のローカル ユーザーを作成することで、自分で試してみることができます。 ローカル ユーザーは、コンピューターによって認証されるため、ドメインはコンピューター名です。 たとえば、ユーザーのコンピューター名が `MyComputer` であり、`Test` という名前のユーザーを作成する場合、Windows ではこのユーザーは `Mycomputer\Test` と表されます。  

##### <a name="create-a-windows-authentication-login"></a>Windows 認証ログインを作成するには 

1.  前の作業で、 [!INCLUDE[ssDE](../includes/ssde-md.md)] を使用して [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]に接続しました。 次に、オブジェクト エクスプローラーでサーバー インスタンスを開き、 **[セキュリティ]** を展開して **[ログイン]** を右クリックし、 **[新しいログイン]** をクリックします。 **[ログイン - 新規作成]** ダイアログ ボックスが表示されます。  

2.  **[全般]** ページの **[ログイン名]** ボックスに、次の形式で Windows ログインを入力します。 `<domain>\\<login>`

![new-login](../relational-databases/media/new-login.png)

3.  **[既定のデータベース]** ボックスで、[ [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] ] が有効な場合はこれを選択します。 有効でない場合は **[master]** を選択します。  
4.  **[サーバー ロール]** ページで、新しいログインを管理者として設定する場合は **[sysadmin]** をクリックします。管理者として設定しない場合は空白にします。  
5.  **[ユーザー マッピング]** ページで、 **データベースが有効な場合はこのデータベースに対し** [Map] [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] を選択します。 有効でない場合は **[master]** を選択します。 ここで、 **[ユーザー]** ボックスにログインが表示されたことに注目してください。 ダイアログ ボックスを閉じると、データベースにこのユーザーが作成されます。  
6.  **[既定のスキーマ]** ボックスに「 **dbo** 」と入力し、ログインをデータベース所有者スキーマにマップします。   
7.  **[セキュリティ保護可能なリソース]** ボックスと **[状態]** ボックスには既定の設定をそのまま使用します。 **[OK]** をクリックするとログインが作成されます。  

> [!IMPORTANT]  
> 上記は開始するための基本的な情報です。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では優れたセキュリティ環境が提供されます。セキュリティはデータベース操作において明らかに重要な要素です。  

## <a name="next-lesson"></a>次のレッスン  
[レッスン 2:別のコンピューターからの接続](../relational-databases/lesson-2-connecting-from-another-computer.md)    
  
