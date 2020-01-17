---
title: SSMS を使用したデータベース バックアップの復元 | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.locatebackupfileazure.f1
- sql13.swb.specifybackup.f1
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: 24b3311d-5ce0-4581-9a05-5c7c726c7b21
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7cd893c9556b1dd45e2206ce73740e253af98ed3
ms.sourcegitcommit: 26715b4dbef95d99abf2ab7198a00e6e2c550243
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70278767"
---
# <a name="restore-a-database-backup-using-ssms"></a>SSMS を使用してデータベース バックアップを復元する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックでは、SQL Server Management Studio を使用して、データベースの完全バックアップを復元する方法について説明します。    
       
### <a name="important"></a>重要:    
完全復旧モデルまたは一括ログ復旧モデルでデータベースを復旧する前に、アクティブ トランザクション ログ ( [ログの末尾](tail-log-backups-sql-server.md)と呼ばれる) をバックアップする必要がある場合があります。 詳細については、「 [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)」を参照してください。  

別のインスタンスからデータベースを復元するときは、「 [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 (SQL Server)](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)」の情報を考慮してください。   
    
暗号化されたデータベースを復元するには、データベースを暗号化するために使用した証明書や非対称キーにアクセスする必要があります。 証明書または非対称キーがないと、データベースを復元することはできません。 バックアップを保存する必要がある間は、データベースの暗号化キーの暗号化に使用した証明書を保持する必要があります。 詳細については、「 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)」をご覧ください。    
    
以前のバージョンのデータベースを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] に復元すると、データベースは自動的に [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードされます。 これにより、データベースが古いバージョンの [!INCLUDE[ssde_md](../../includes/ssde_md.md)] で使用されるのを防ぎます。 ただし、これはメタデータのアップグレードに関係し、[データベースの互換性レベル](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)には影響しません。 アップグレード前のユーザー データベースの互換性レベルが 100 以上の場合は、アップグレード後も互換性レベルは変わりません。 アップグレード前の互換性レベルが 90 の場合、アップグレードされたデータベースの互換性レベルは 100 に設定されます。これは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] でサポートされている下限の互換性レベルです。 詳細については、「[ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」を参照してください。  
  
通常、データベースは直ちに使用可能になります。 ただし、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースにフルテキスト インデックスがある場合、アップグレード プロセスでは、 **[フルテキストのアップグレード オプション]** サーバー プロパティの設定に応じて、インデックスのインポート、リセット、または再構築が行われます。 アップグレード オプションが **[インポート]** または **[再構築]** に設定されている場合、アップグレード中はフルテキスト インデックスを使用できません。 インデックスを作成するデータ量によって、インポートには数時間かかる場合があります。再構築には、最大でその 10 倍の時間がかかります。     
    
アップグレード オプションが **[インポート]** に設定されているときに、フルテキスト カタログが使用できない場合は、関連付けられたフルテキスト インデックスが再構築されます。 **フルテキスト アップグレード オプション** プロパティの設定の表示と変更については、「 [サーバー インスタンスでのフルテキスト検索の管理と監視](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)」を参照してください。    

Microsoft Azure BLOB ストレージ サービスからの SQL Server の復元については、「 [Microsoft Azure BLOB ストレージ サービスを使用した SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」をご覧ください。

## <a name="examples"></a>使用例
    
### <a name="a-restore-a-full-database-backup"></a>A. データベースの完全バックアップを復元する   
    
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
    
2.  **[データベース]** を右クリックして、 **[データベースの復元...]** を選択します。    
    
3.  **[全般]** ページの **復元元**のセクションを使用して、復元するバックアップ セットの復元元ファイルと場所を指定します。 以下のオプションの 1 つを選択します。    
    
    -   **[データベース]**    
    
         復元するデータベースをドロップダウン リストから選択します。 このリストには、 **msdb** バックアップ履歴に従ってバックアップされたデータベースのみが含まれます。    
    
        > [!NOTE]
        > 別のサーバーで作成されたバックアップの場合、復元先のサーバーには指定されたデータベースのバックアップ履歴情報が存在しません。 この場合、 **[デバイス]** をクリックして、復元するファイルまたはデバイスを手動で指定します。 
    
    -   **[デバイス]**    
    
         参照ボタン (**[...]**) をクリックし、 **[バックアップ デバイスの選択]** ダイアログ ボックスを開きます。 
         
        -   **[バックアップ デバイスの選択]** ダイアログ ボックス  
        
            **バックアップ メディアの種類**  
         **[バックアップ メディアの種類]** ドロップダウン リストからメディアの種類を選択します。  注:**[テープ]** オプションは、テープ ドライブがコンピューターにセットされている場合だけ表示されます。また、**[バックアップ デバイス]** オプションは、1 つ以上のバックアップ デバイスが存在する場合だけ表示されます。

            **[追加]**  
            **[追加]** をクリックすると、 **[バックアップ メディアの種類]** ドロップダウン リストで選択したメディアの種類に応じて、次のダイアログ ボックスのいずれかが開きます。 ( **[バックアップ メディア]** ボックスの一覧がいっぱいの場合、 **[追加]** ボタンは使用できません)。

            |メディアの種類|ダイアログ ボックス|Description|    
            |----------------|----------------|-----------------|    
            |**[最近使ったファイル]**|**[バックアップ ファイルの検索]**|このダイアログ ボックスでは、ツリーからローカル ファイルを選択するか、完全修飾の汎用名前付け規則 (UNC) 名を使用したリモート ファイルを指定できます。 詳細については、「 [バックアップ デバイス &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)の別のインスタンスで作成された場合、これは必須です。|    
            |**[デバイス]**|**[バックアップ デバイスの選択]**|このダイアログ ボックスでは、サーバー インスタンスで定義された論理バックアップ デバイスの一覧から選択できます。|    
            |**[テープ]**|**[バックアップ テープの選択]**|このダイアログ ボックスでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスが動作しているコンピューターに物理的に接続されているテープ ドライブの一覧から選択できます。|    
            |**[URL]**|**[バックアップ ファイルの場所を選択]**|このダイアログ ボックスで、既存の SQL Server 資格情報/Azure ストレージ コンテナーを選択し、共有アクセス署名で新しい Azure ストレージ コンテナーを追加するか、共有アクセス署名と既存のストレージ コンテナーの SQL Server 資格情報を生成します。  「 [Connect to a Microsoft Azure Subscription](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md)」 (Microsoft Azure サブスクリプションへの接続) もご覧ください。|  
         
             **[削除]**    
             選択されている 1 つまたは複数のファイル、テープ、または論理バックアップ デバイスを削除します。    
                 
             **目次**    
            選択されているファイル、テープ、または論理バックアップ デバイスのメディアの内容を表示します。  メディアの種類が **[URL]** の場合、このボタンは機能しない場合があります。  

             **[バックアップ メディア]**   
             選択したメディアを一覧します。
    
             **[バックアップ メディア]** ボックスに目的のデバイスを追加したら、 **[OK]** をクリックして、 **[全般]** ページに戻ります。    
    
         **[ソース: デバイス: データベース]** リスト ボックスで、復元するデータベースの名前を選択します。    
    
         > [!NOTE]
         > この一覧は **[デバイス]** を選択した場合にのみ使用できます。 選択されたデバイスにバックアップを持つデータベースのみが使用できるようになります。    
     
4.  **復元先のセクション**の **[データベース]** ボックスに、復元するデータベースの名前が自動的に表示されます。 データベースの名前を変更するには、 **[データベース]** ボックスに新しい名前を入力します。    
    
5.  **[復元先]** ボックスで、既定値の **[最後に作成されたバックアップ]** のままにするか、 **[タイムライン]** をクリックして、 **[バックアップのタイムライン]** ダイアログ ボックスにアクセスし、具体的にどの時点で復旧アクションを停止するかを手動で選択します。 特定の時点を指定する方法の詳細については、「 [バックアップ タイムライン](../../relational-databases/backup-restore/backup-timeline.md)」をご覧ください。    
    
6.  **[復元するバックアップ セット]** グリッドで、復元するバックアップを選択します。 このグリッドには、指定された場所に対して使用可能なバックアップが表示されます。 既定では、復旧計画が推奨されています。 推奨された復元計画を変更するには、グリッドの選択を変更します。 以前のバックアップの選択を解除すると、以前のバックアップの復元に依存するバックアップは自動的に選択が解除されます。 **[復元するバックアップ セット]** グリッドの列の詳細については、「[データベースの復元 &#40;[全般] ページ&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)」を参照してください。    
    
7.  必要に応じて、**[ページの選択]** ペインの **[ファイル]** をクリックして、**[ファイル]** ダイアログ ボックスにアクセスします。 このダイアログ ボックスでは、**[次のデータベース ファイルに復元]** グリッド内の各ファイルに新しい復元先を指定することで、新しい場所にデータベースを復元できます。 このグリッドの詳細については、「[データベースの復元 &#40;[ファイル] ページ&#41;](../../relational-databases/backup-restore/restore-database-files-page.md)」を参照してください。    
    
8. 拡張オプションを表示または選択するには、**[オプション]** ページの **[復元オプション]** パネルを使用します。状況に応じて、次の任意のオプションを選択できます。    

   1. **WITH** オプション (必須ではありません):    
    
     - **[既存のデータベースを上書きする (WITH REPLACE)]**    
    
     - **[レプリケーションの設定を保存する (WITH KEEP_REPLICATION)]**    
    
     - **[復元するデータベースへのアクセスを制限する (WITH RESTRICTED_USER)]**    
    
   2. **[復旧状態]** ボックスのオプションを選択します。 このボックスの選択内容により、復元操作後のデータベースの状態が決まります。    
    
     - **[RESTORE WITH RECOVERY]** : コミットされていないトランザクションをロールバックして、データベースを使用可能な状態にします。これが既定の動作です。 別のトランザクション ログは復元できません。 このオプションは、必要なバックアップをすべて復元する場合に選択します。    
    
     - **[RESTORE WITH NORECOVERY]** : データベースは操作不可状態のままとなり、コミットされていないトランザクションはロールバックされません。 別のトランザクション ログは復元できます データベースは、復旧されるまで使用できません。    
    
     - **[RESTORE WITH STANDBY]** : データベースを読み取り専用モードにします。 コミットされていないトランザクションは元に戻されますが、復旧結果を元に戻せるように元に戻す操作をスタンバイ ファイルに保存します。    
    
   3. **復元の前にログ末尾のバックアップを実行します。** ログ末尾のバックアップは、すべての復元シナリオで必要となるわけではありません。  詳細については、「 **ログ末尾のバックアップ (SQL Server)** 」の「 [ログ末尾のバックアップが必要となるシナリオ](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)」を参照してください。
  
   4. データベースへのアクティブな接続がある場合、復元操作は失敗する可能性があります。 **とデータベース間のすべてのアクティブな接続を閉じるには、** [既存の接続を閉じる] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] オプションをオンにします。 このチェック ボックスをオンにすると、データベースは復元操作の実行前にシングル ユーザー モードに設定され、復元操作の完了後にマルチユーザー モードに設定されます。    
  
   5. 復元操作と復元操作の間に、その都度、確認のメッセージを表示するには、 **[各バックアップを復元する前に確認する]** をオンにします。 通常は、その必要はありません。データベースが大きく、復元操作のステータスを監視する必要がある場合にのみ使用します。    
    
これらの復元オプションの詳細については、「[データベースの復元 &#40;[オプション] ページ&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)」をご覧ください。    
    
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="b-restore-an-earlier-disk-backup-over-an-existing-database"></a>B. 既存のデータベースに以前のディスク バックアップを復元する
次の例では、`Sales` の以前のディスク バックアップを復元し、既存の `Sales` データベースを上書きします。

1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
2.  **[データベース]** を右クリックして、 **[データベースの復元...]** を選択します。  
3.  **[全般]** ページで、 **[ソース]** セクションの **[デバイス]** を選択します。
4.  参照ボタン (**[...]**) をクリックし、 **[バックアップ デバイスの選択]** ダイアログ ボックスを開きます。 **[追加]** をクリックし、バックアップに移動します。 ディスク バックアップ ファイルを選択してから **[OK]** をクリックします。
5.  **[OK]** をクリックして、 **[全般]** ページに戻ります。
6.  **[ページの選択]** ペインの **[オプション]** をクリックします。
7.  **[復元オプション]** パネルで、 **[既存のデータベースを上書きする (WITH REPLACE)]** チェック ボックスをオンにします。

    > [!NOTE]
    > このオプションをオンにしない場合、次のエラー メッセージが表示されることがあります。"System.Data.SqlClient.SqlError:バックアップ セットは、既存のデータベース '`Sales`' 以外のデータベースのバックアップを保持しています。 (Microsoft.SqlServer.SmoExtended)"

8.  **[ログ末尾のバックアップ]** セクションで、**[復元の前にログ末尾のバックアップを実行する]** チェック ボックスをオフにします。

    > [!NOTE]
    > ログ末尾のバックアップは、すべての復元シナリオで必要となるわけではありません。 復旧ポイントが、それより前のログ バックアップに含まれているのであれば、ログ末尾のバックアップは不要です。 また、データベースを移動するか置き換えて (上書きして) いる場合、ログ末尾のバックアップは不要であり、最新のバックアップ以降の特定の時点に復元する必要もありません。 詳細については、「 [ログ末尾のバックアップ (SQL Server)](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)」を参照してください。

    このオプションは、単純復旧モデルのデータベースには使用できません。

9.  **[サーバー接続]** セクションで、 **[接続先データベースへの既存の接続を閉じる]** チェック ボックスをオンにします。

    > [!NOTE]
    > このオプションをオンにしない場合、次のエラー メッセージが表示されることがあります。"System.Data.SqlClient.SqlError:データベースは使用中なので、排他アクセスを獲得できませんでした。 (Microsoft.SqlServer.SmoExtended)"
    
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="c--restore-an-earlier-disk-backup-with-a-new-database-name-where-the-original-database-still-exists"></a>C.  元のデータベースが存在する新しいデータベース名で以前のディスク バックアップを復元する
次の例では、`Sales` の以前のディスク バックアップを復元し、`SalesTest` という新しいデータベースを作成します。  元のデータベース ( `Sales`) はサーバーに存在しています。

1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
2.  **[データベース]** を右クリックして、 **[データベースの復元...]** を選択します。  
3.  **[全般]** ページで、 **[ソース]** セクションの **[デバイス]** を選択します。
4.  参照ボタン (**[...]**) をクリックし、 **[バックアップ デバイスの選択]** ダイアログ ボックスを開きます。 **[追加]** をクリックし、バックアップに移動します。 ディスク バックアップ ファイルを選択してから **[OK]** をクリックします。
5.  **[OK]** をクリックして、 **[全般]** ページに戻ります。
6.  **復元先のセクション**の **[データベース]** ボックスに、復元するデータベースの名前が自動的に表示されます。 データベースの名前を変更するには、 **[データベース]** ボックスに新しい名前を入力します。
7.  **[ページの選択]** ペインの **[オプション]** をクリックします。
8.  **[ログ末尾のバックアップ]** セクションで、**[復元の前にログ末尾のバックアップを実行する]** チェック ボックスをオフにします。

    > [!IMPORTANT]
    > このオプションをオフにすると、既存のデータベース ( `Sales`) は復元中の状態に変更されます。

9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

    > [!NOTE]
    > 次のエラー メッセージが表示された場合:      
    > "System.Data.SqlClient.SqlError:データベース "`Sales`" のログの末尾がバックアップされませんでした。 この部分の作業を保存しておく場合は `BACKUP LOG WITH NORECOVERY` を使用してログをバックアップしてください。 ログのコンテンツを上書きするだけの場合は、`RESTORE` ステートメントで `WITH REPLACE` 句または `WITH STOPAT` 句を使用してください。 (Microsoft.SqlServer.SmoExtended)"。      
    > 上記の手順 6 で新しいデータベース名を入力していない可能性があります。 通常、復元により、誤ってデータベースを別のデータベースで上書きしてしまうのを防ぐことができます。 `RESTORE` ステートメントで指定したデータベースが現在のサーバーに既に存在し、指定したデータベースのファミリ GUID がバックアップ セットに記録されているデータベースのファミリ GUID と異なる場合、そのデータベースは復元されません。 これは重要な保護機能です。

### <a name="d--restore-earlier-disk-backups-to-a-point-in-time"></a>D.  特定の時点に以前のディスク バックアップを復元する
次の例では、データベースを `1:23:17 PM` `May 30, 2016` の状態に復元し、複数のログ バックアップが関連する復元操作を行います。 現在、データベースはサーバーに存在しません。

1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
2.  **[データベース]** を右クリックして、 **[データベースの復元...]** を選択します。  
3.  **[全般]** ページで、 **[ソース]** セクションの **[デバイス]** を選択します。
4.  参照ボタン (**[...]**) をクリックし、 **[バックアップ デバイスの選択]** ダイアログ ボックスを開きます。 **[追加]** をクリックし、完全バックアップとすべての関連するトランザクション ログのバックアップに移動します。  ディスク バックアップ ファイルを選択してから **[OK]** をクリックします。
5.  **[OK]** をクリックして、 **[全般]** ページに戻ります。
6.  **[復元先]** ボックスで、 **[タイムライン]** をクリックして、 **[バックアップのタイムライン]** ダイアログ ボックスにアクセスし、どの時点で復旧アクションを停止するかを手動で選択します。
7.  **[特定の日付と時刻]** を選択します。  
8.  ドロップダウン ボックスで **[タイムライン間隔]** を **[時間]** に変更します (省略可能)。  
9.  目的の時間にスライダーを移動します。
10. **[OK]** をクリックして、[全般] ページに戻ります。
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="e--restore-a-backup-from-the-microsoft-azure-storage-service"></a>E.  Microsoft Azure Storage サービスからバックアップを復元する

#### <a name="common-steps"></a>一般的な手順
次の 2 つの例では、Microsoft Azure Storage サービスに置かれているバックアップから `Sales` の復元を実行します。  ストレージ アカウント名は `mystorageaccount`です。  コンテナーは `myfirstcontainer`と呼ばれます。  簡潔にするため、最初の 6 つの手順をここに一度だけリストし、例はすべて **手順 7**から始めます。
1.  **オブジェクト エクスプローラー**で、SQL Server データベース エンジンのインスタンスに接続し、そのインスタンスを展開します。
2.  **[データベース]** を右クリックして、 **[データベースの復元...]** を選択します。
3.  **[全般]** ページで、 **[ソース]** セクションの **[デバイス]** を選択します。
4.  参照ボタン ([...]) をクリックし、 **[バックアップ デバイスの選択]** ダイアログ ボックスを開きます。    
5.  **[バックアップ メディアの種類:]** ドロップダウン リストから **[URL]** を選択します。
6.  **[追加]** をクリックすると、**[バックアップ ファイルの場所を選択]** ダイアログ ボックスが開きます。

#### <a name="e1---restore-a-striped-backup-over-an-existing-database-and-a-shared-access-signature-exists"></a>E1.   既存のデータベース上にストライプ バックアップを復元し、共有アクセス署名が存在する場合
保存されたアクセス ポリシーは読み取り、書き込み、削除および一覧表示権で作成されています。  保存されたアクセス ポリシーに関連付けられている Shared Access Signature は、コンテナー `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`用に作成されています。  SQL Server 資格情報が既に存在する場合、手順はほとんど同じです。  現在、 `Sales` データベースはサーバーに存在しています。  バックアップ ファイルは、 `Sales_stripe1of2_20160601.bak` と `Sales_stripe2of2_20160601.bak`です。  

1.  SQL Server 資格情報が既に存在する場合、 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` [Azure ストレージ コンテナー:] **ドロップダウン リストから [** ] を選択します。それ以外の場合は、手動でコンテナーの名前 ( `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`) を入力します。 
1. **[Shared Access Signature:]** リッチ テキスト ボックス に Shared Access Signature を入力します。
1. **[OK]** をクリックすると、 **[Microsoft Azure でのバックアップ ファイルの位置指定]** ダイアログ ボックスが開きます。
1. **[コンテナー]** を展開して、 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`に移動します。
1. Ctrl キーを押しながらファイル `Sales_stripe1of2_20160601.bak` と `Sales_stripe2of2_20160601.bak`を選択します。
1. [**OK**] をクリックします。
1. **[OK]** をクリックして、 **[全般]** ページに戻ります。
1. **[ページの選択]** ペインの **[オプション]** をクリックします。
1. **[復元オプション]** パネルで、 **[既存のデータベースを上書きする (WITH REPLACE)]** チェック ボックスをオンにします。
1. **[ログ末尾のバックアップ]** セクションで、 **[復元の前にログ末尾のバックアップを実行する]** チェック ボックスをオフにします。
1. **[サーバー接続]** セクションで、 **[接続先データベースへの既存の接続を閉じる]** チェック ボックスをオンにします。
1. [**OK**] をクリックします。

#### <a name="e2---a-shared-access-signature-does-not-exist"></a>E2.   Shared Access Signature が存在しない場合
この例では、現在、`Sales` データベースはサーバーに存在しません。
1. **[追加]** をクリックすると、 **[Microsoft サブスクリプションへの接続]** ダイアログ ボックスが開きます。  
1. **[Microsoft サブスクリプションへの接続]** ダイアログ ボックスに入力し、 **[OK]** をクリックして **[バックアップ ファイルの場所を選択]** ダイアログ ボックスに戻ります。  詳細については、「 [Microsoft Azure サブスクリプションへの接続](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md) 」をご覧ください。
1. **[バックアップ ファイルの場所を選択]** ダイアログ ボックスで **[OK]** をクリックして、 **[Microsoft Azure でのバックアップ ファイルの位置指定]** ダイアログ ボックスを開きます。
1. **[コンテナー]** を展開して、 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`に移動します。
1. バックアップ ファイルを選択して、 **[OK]** をクリックします。
1. **[OK]** をクリックして、 **[全般]** ページに戻ります。
1. [**OK**] をクリックします。

#### <a name="f-restore-local-backup-to-microsoft-azure-storage-url"></a>F. Microsoft Azure Storage (URL) のローカルのバックアップを復元する
`Sales` データベースは、`E:\MSSQL\BAK` に置かれたバックアップから Microsoft Azure ストレージ コンテナー `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` に復元されます。  Azure コンテナーの SQL Server 資格情報は、既に作成されています。  復元先コンテナーの SQL Server 資格情報は、 **[復元]** タスク中に作成できないので、既に存在している必要があります。  現在、 `Sales` データベースはサーバーに存在しません。
1.  **オブジェクト エクスプローラー**で、SQL Server データベース エンジンのインスタンスに接続し、そのインスタンスを展開します。
2.  **[データベース]** を右クリックして、 **[データベースの復元...]** を選択します。
3.  **[全般]** ページで、 **[ソース]** セクションの **[デバイス]** を選択します。
4.  参照ボタン ([...]) をクリックし、 **[バックアップ デバイスの選択]** ダイアログ ボックスを開きます。  
5.  **[バックアップ メディアの種類:]** ドロップダウン リストから **[ファイル]** を選択します。
6.  **[追加]** をクリックすると、 **[バックアップ ファイルの検索]** ダイアログ ボックスが開きます。
7.  `E:\MSSQL\BAK`を移動し、バックアップ ファイルを選択して **[OK]** をクリックします。
8.  **[OK]** をクリックして、 **[全般]** ページに戻ります。
9.  **[ページの選択]** ペインの **[ファイル]** をクリックします。
10. **[すべてのファイルをフォルダーに移動]** チェック ボックスをオンにします。
11. `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`[データ ファイル フォルダー:] **と** [ログ ファイルのフォルダ:] **のテキスト ボックスで、コンテナー (**) を入力します。
12. [**OK**] をクリックします。

## <a name="see-also"></a>参照    
 [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)     
 [データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)     
 [データベースを新しい場所に復元する &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)     
 [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)     
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)     
 [[データベースの復元] &#40;[オプション] ページ&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)     
 [[データベースの復元] &#40;[全般] ページ&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)    
    
  
