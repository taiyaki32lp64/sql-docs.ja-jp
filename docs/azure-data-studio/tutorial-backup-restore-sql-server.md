---
title: データベースをバックアップし、復元する
titleSuffix: Azure Data Studio
description: Azure Data Studio を使用してデータベースをバックアップし、復元する方法について説明します。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 11/04/2019
ms.openlocfilehash: bdf3bb3151cfac9f68a9765a2c59232b9fb59f56
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532473"
---
# <a name="backup-and-restore-databases-using-includename-sosincludesname-sos-shortmd"></a>[!INCLUDE[name-sos](../includes/name-sos-short.md)] を使用してデータベースをバックアップし、復元する

このチュートリアルでは、次の目的で [!INCLUDE[name-sos](../includes/name-sos-short.md)] を使用する方法について学習します。
> [!div class="checklist"]
> * データベースをバックアップする 
> * バックアップ状態を表示する
> * バックアップを実行するために使用するスクリプトを生成する
> * データベースを復元する
> * 復元タスクの状態を表示する

## <a name="prerequisites"></a>Prerequisites

このチュートリアルには、SQL Server *TutorialDB* が必要です。 *TutorialDB* データベースを作成するには、次のクイックスタートのいずれかを実行します。

* [[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] を使用して SQL Server に接続し、クエリを実行する](quickstart-sql-server.md)

このチュートリアルでは、SQL Server データベースに接続する必要があります。 Azure SQL Database には自動バックアップがあるため、Azure Data Studio では Azure SQL Database のバックアップと復元が実行されません。 詳細は、[自動 SQL Database バックアップ](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups)に関するページを参照してください。

## <a name="back-up-a-database"></a>データベースをバックアップする

1. TutorialDB データベースダッシュボードを開きます ( **[サーバー]** サイドバーを開き (**Ctrl + G**)、 **[データベース]** を展開し、 **[TutorialDB]** を右クリック、 **[管理]** を選択します)。

2. **[データベースのバックアップ]** ダイアログを開きます ( **[タスク]** ウィジェットで **[バックアップ]** をクリックします)。

   ![タスク ウィジェット](./media/tutorial-backup-restore-sql-server/tasks.png)

3. このチュートリアルでは、既定のバックアップ オプションが使用されています。そのため、 **[バックアップ]** をクリックします。
   ![バックアップ ダイアログ](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

**[バックアップ]** をクリックすると、 **[データベースのバックアップ]** ダイアログボックスが消え、バックアップ プロセスが開始されます。

## <a name="view-the-backup-status-and-view-the-backup-script"></a>バックアップの状態を表示し、バックアップ スクリプトを表示する

1. **[タスク履歴]** ペインが表示されるか、**CTRL + T** キーを押します。

   ![タスクの履歴](./media/tutorial-backup-restore-sql-server/task-history.png)

2. エディターでバックアップ スクリプトを表示するには、 **[Backup Database succeeded]\(データベース バックアップに成功しました\)** を右クリックし、 **[スクリプト]** を選択します。

   ![バックアップ スクリプト](./media/tutorial-backup-restore-sql-server/task-script.png)

## <a name="restore-a-database-from-a-backup-file"></a>データベースをバックアップ ファイルから復元する

1. **[サーバー]** サイドバーを開き (**Ctrl + G**)、サーバーを右クリックし、 **[管理]** を選択します。

2. **[データベースの復元]** ダイアログを開きます ( **[タスク]** ウィジェットで **[復元]** をクリックします)。

   ![復元タスク](media/tutorial-backup-restore-sql-server/tasks-restore.png)

3. **[復元元]** フィールドで **[バックアップ ファイル]** を選択します。

4. **[バックアップ ファイル パス]** フィールドの省略記号 (...) をクリックし、*TutorialDB* の最新バックアップ ファイルを選択します。

5. **[Destination]\(復元先\)** セクションの **[Target database]\(復元先データベース\)** フィールドに「**TutorialDB_Restored**」と入力すると、バックアップ ファイルが新しいデータベースに復元されます。 次に、 **[復元]** を選択します。

   ![復元 (restore)](./media/tutorial-backup-restore-sql-server/restore.png)

6. 復元操作の状態を表示するには、**Ctrl + T** キーを押して **[タスク履歴]** を開きます。

   ![復元 (restore)](./media/tutorial-backup-restore-sql-server/task-history-restore.png)