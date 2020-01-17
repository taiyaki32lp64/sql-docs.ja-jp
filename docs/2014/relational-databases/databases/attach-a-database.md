---
title: データベースのインポート | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.attachdatabase.f1
helpviewer_keywords:
- database attaching [SQL Server]
- attaching databases [SQL Server]
ms.assetid: b4efb0ae-cfe6-4d81-a4b4-6e4916885caa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b4c9a3160224078b908059c3902e66ef59608bac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62872252"
---
# <a name="attach-a-database"></a>データベースのインポート
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]のデータベースをアタッチする方法について説明します。 この機能は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのコピー、移動、またはアップグレードに使用できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [前提条件](#Prerequisites)  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **使用してデータベースのアタッチ。**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [データベースのアップグレード後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件  
  
-   最初にデータベースをデタッチする必要があります。 デタッチされていないデータベースをアタッチしようとすると、エラーが返されます。 詳細については、「 [データベースのデタッチ](detach-a-database.md)」を参照してください。  
  
-   データベースをアタッチするときは、すべてのデータ ファイル (MDF ファイルおよび LDF ファイル) を利用できる状態にする必要があります。 データベースを最初に作成したときか最後にアタッチしたときとデータ ファイルのパスが異なる場合、ファイルの現在のパスを指定する必要があります。  
  
-   データベースをアタッチするときに、MDF ファイルと LDF ファイルが異なるディレクトリに配置されており、いずれかのパスに \\\\?\GlobalRoot が含まれている場合は、操作は失敗します。  
  
###  <a name="Recommendations"></a> 推奨事項  
使用してデータベースを移動することをお勧め、`ALTER DATABASE`使用する代わりに、計画的再配置手順のデタッチし、アタッチします。 詳細については、「 [ユーザー データベースの移動](move-user-databases.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
ファイル アクセス許可は、データベースのデタッチやアタッチなど、さまざまなデータベース操作中に設定されます。 データベースをデタッチおよびアタッチするたびに設定されるファイル権限の詳細については、 [オンライン ブックの「](https://technet.microsoft.com/library/ms189128.aspx) データ ファイルとログ ファイルのセキュリティ保護 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 」を参照してください。  
  
不明なソースや信頼されていないソースからデータベースをアタッチまたは復元しないことをお勧めします。 こうしたデータベースには、意図しない [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを実行したり、スキーマまたは物理データベース構造を変更してエラーを発生させるような、悪意のあるコードが含まれている可能性があります。 不明または信頼できないソースのデータベースを使用する前に、運用サーバー以外のサーバーでそのデータベースに対し [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) を実行し、さらに、そのデータベースのストアド プロシージャやその他のユーザー定義コードなどのコードを調べます。 データベースのアタッチ、およびデータベースのアタッチ時にメタデータに対して行われる変更の詳細については、「[データベースのデタッチとアタッチ &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)」を参照してください。  
  
####  <a name="Permissions"></a> Permissions  
`CREATE DATABASE`、`CREATE ANY DATABASE`、または `ALTER ANY DATABASE` アクセス許可が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
### <a name="to-attach-a-database"></a>データベースをアタッチするには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] オブジェクト エクスプローラーで、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を右クリックし、 **[アタッチ]** をクリックします。  
  
3.  アタッチするデータベースを指定するには、 **[データベースのインポート]** ダイアログ ボックスで **[追加]** をクリックし、 **[データベース ファイルの検索]** ダイアログ ボックスで目的のデータベースが常駐するディスク ドライブを選択します。次に、そのディレクトリ ツリーを展開し、そのデータベースの .mdf ファイルを選択します。たとえば、次のように指定します。  
  
     `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\AdventureWorks2012_Data.mdf`  
  
    > [!IMPORTANT]  
    > 既にアタッチされているデータベースを選択しようとすると、エラーが発生します。  
  
     **[アタッチするデータベース]**  
     選択されたデータベースに関する情報を表示します。  
  
     \<空白の列ヘッダー>  
     アタッチ操作の状態を示すアイコンが表示されます。 表示されるアイコンの種類は、下の **[状態]** の説明に示します。  
  
     **[MDF ファイルの場所]**  
     選択した MDF ファイルのパスとファイル名が表示されます。  
  
     **データベース名**  
     データベースの名前が表示されます。  
  
     **[次の名前でアタッチ]**  
     データベースを別の名前でアタッチする場合に、その名前を指定します。  
  
     **[所有者]**  
     データベースの所有者のドロップダウン リストです。これを使用して、必要に応じて別の所有者を選択できます。  
  
     **ステータス**  
     次の表に示すように、データベースの状態を表示します。  
  
    |アイコン|状態テキスト|説明|  
    |----------|-----------------|-----------------|  
    |(アイコンなし)|(テキストなし)|このオブジェクトのアタッチ操作が開始されていないか、保留されています。 これは、ダイアログ ボックスを開いたときの既定の状態です。|  
    |緑の右向き三角形|[実行中]|アタッチ操作が開始されましたが、完了していません。|  
    |緑のチェック マーク|成功|オブジェクトは正常にアタッチされました。|  
    |赤い丸の中に白い×印|[エラー]|アタッチ操作でエラーが発生し、正常に完了しませんでした。|  
    |4 つに区切られた丸印 (左右の領域が黒、上下の領域が白)|停止|ユーザーがアタッチ操作を停止したため、正常に完了しませんでした。|  
    |丸の中に反時計回りの矢印|[ロールバックされました]|アタッチ操作は正常に完了しましたが、他のオブジェクトのアタッチ中にエラーが発生したため、ロールバックされました。|  
  
     **メッセージ**  
     空白のメッセージ、または "ファイルが見つかりません" のハイパーリンクが表示されます。  
  
     **[追加]**  
     主な必須データベース ファイルを検索します。 ユーザーが .mdf ファイルを選択した場合、 **[アタッチするデータベース]** グリッドの対応するフィールドに、対応する情報が自動的に入力されます。  
  
     **[削除]**  
     選択したファイルを **[アタッチするデータベース]** グリッドから削除します。  
  
     **"** *<database_name>* **" データベースの詳細**  
     デタッチするファイルの名前を表示します。 ファイルのパス名を確認または変更するには、**参照**ボタン ( **[...]** ) をクリックしてください。  
  
    > [!NOTE]  
    > ファイルが存在しなかった場合、 **[メッセージ]** 列に "見つかりませんでした" と表示されます。 ログ ファイルが見つからない場合は、ログ ファイルが別のディレクトリに置かれているか、削除されています。 **[データベースの詳細]** グリッドでファイル パスを更新し、正しい場所を指定するか、そのログ ファイルをグリッドから削除します。 .ndf データ ファイルが見つからない場合、グリッドのパスを更新して、正しい場所を指定する必要があります。  
  
     **[元のファイル名]**  
     データベースに属している、アタッチされたファイルの名前が表示されます。  
  
     **[ファイルの種類]**  
     ファイルの種類を表します。 **[データ]** または **[ログ]** になります。  
  
     **[現在のファイル パス]**  
     選択されているデータベース ファイルのパスを表示します。 このパスは手作業で編集できます。  
  
     **メッセージ**  
     空白のメッセージ、または **"ファイルが見つかりません"** ハイパーリンクが表示されます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
### <a name="to-attach-a-database"></a>データベースをアタッチするには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  使用して、 [CREATE DATABASE](/sql/t-sql/statements/create-database-sql-server-transact-sql)ステートメントを`FOR ATTACH`を閉じます。  
  
     次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースのファイルをアタッチし、データベースの名前を `MyAdventureWorks`に変更します。  
  
    ```sql  
    CREATE DATABASE MyAdventureWorks   
        ON (FILENAME = 'C:\MySQLServer\AdventureWorks_Data.mdf'),   
        (FILENAME = 'C:\MySQLServer\AdventureWorks_Log.ldf')   
        FOR ATTACH;  
    ```  
  
    > [!NOTE]  
    > また、 [sp_attach_db](/sql/relational-databases/system-stored-procedures/sp-attach-db-transact-sql) ストアド プロシージャまたは [sp_attach_single_file_db](/sql/relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql) ストアド プロシージャを使用することもできます。 ただし、これらのプロシージャは、Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の今後のバージョンでは削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 CREATE DATABASE を使用することをお勧めしています.FOR ATTACH を使用することをお勧めします  
  
##  <a name="FollowUp"></a>補足情報: SQL Server データベースのアップグレード後  
 attach メソッドを使用してデータベースをアップグレードする導入後、データベースはすぐに使用可能になります、自動的にアップグレードします。 データベースにフルテキスト インデックスがある場合、アップグレード プロセスでは、 **"フルテキスト アップグレード オプション"** サーバー プロパティの設定に応じて、インポート、リセット、または再構築が行われます。 アップグレード オプションが **[インポート]** または **[再構築]** に設定されている場合、アップグレード中はフルテキスト インデックスを使用できなくなります。 インデックスを作成するデータ量によって、インポートには数時間、再構築には最大でその 10 倍の時間がかかることがあります。 なお、アップグレード オプションが **[インポート]** に設定されており、フルテキスト カタログが使用できない場合は、関連付けられたフルテキスト インデックスが再構築されます。  
  
アップグレード前のユーザー データベースの互換性レベルが 100 以上の場合は、アップグレード後も互換性レベルは変わりません。 アップグレード前の互換性レベルが 90 の場合、アップグレードされたデータベースの互換性レベルは 100 に設定されます。これは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] でサポートされている下限の互換性レベルです。 詳細については、「[ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [データベースのデタッチ](detach-a-database.md)  
  
  
