---
title: Ssma for MySQL (MySQLToSQL) 作業の開始 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Getting started, MySQL metadata explorer
- Getting started, SQL Server or SQL Azure metadata explorer
- Getting started,Installing and licensing
ms.assetid: 8ebfa061-be6f-4a07-923f-8dc832a82f70
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5a1adb6d9354dc870c11fab0a68f6c92e704ebfb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67984537"
---
# <a name="getting-started-with-ssma-for-mysql-mysqltosql"></a>SSMA for MySQL 入門 (MySQLToSQL)
SQL Server Migration Assistant (SSMA) for MySQL では、迅速に MySQL データベースのスキーマを SQL Server または Azure SQL DB のスキーマに変換、SQL Server または Azure SQL DB に結果のスキーマをアップロードおよび MySQL から SQL Server または Azure SQL DB にデータを移行することができます。  
  
このトピックでは、インストール プロセスを紹介し、SSMA ユーザー インターフェイスを理解し、支援します。  
  
## <a name="installing-ssma"></a>SSMA のインストール  
SSMA を使用するには、最初にする必要があります、プログラムのインストール SSMA クライアント ソースの MySQL データベースと SQL Server または Azure SQL DB のターゲット インスタンスの両方にアクセスできるコンピューターにします。 次に、SSMA クライアント プログラムを実行しているコンピューターに MySQL プロバイダー (MySQL ODBC 5.1 ドライバー (信頼されている)) をインストールします。 インストール手順については、次を参照してください[SSMA for MySQL をインストールする&#40;MySqlToSql。&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
  
SSMA を起動するには、クリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**SQL Server Migration Assistant for MySQL**、順にクリックします**SQL Server の移行Assistant for MySQL**します。  
  
## <a name="ssma-for-mysql-user-interface"></a>SSMA for MySQL のユーザー インターフェイス  
SSMA は、インストールして、ライセンス認証は後、は、SQL Server または Azure SQL DB に MySQL データベースを移行するのに SSMA を使用できます。 これは、開始する前に SSMA ユーザー インターフェイスを理解するのに役立ちます。 次の図では、SSMA、メタデータ エクスプ ローラー、メタデータ、ツールバー、出力ウィンドウで、エラー一覧 ウィンドウなどのユーザー インターフェイスを示しています。  
  
![SSMA for MySql のグラフィカル ユーザー インターフェイス](../../ssma/mysql/media/ssmaformysqlgui.gif "SSMA for MySql のグラフィカル ユーザー インターフェイス")  
  
移行を開始するには、次の必要があります。  
  
1.  新しいプロジェクトを作成します。  
  
2.  MySQL データベースに接続します。  
  
3.  接続に成功した後は、MySQL スキーマは、MySQL メタデータ エクスプ ローラーに表示されます。 などのタスクを実行する MySQL メタデータ エクスプ ローラーで右クリックしてオブジェクトでは、SQL Server または Azure SQL DB への変換の評価レポートを作成します。  
  
ツールバーとメニューを使用して、これらのタスクを実行することもできます。  
  
SQL Server のインスタンスに接続することも必要があります。 接続に成功した後は、SQL Server データベースの階層は、SQL Server メタデータ エクスプ ローラーに表示されます。 MySQL スキーマを SQL Server スキーマに変換した後は、SQL Server メタデータ エクスプ ローラーでこれらの変換されたスキーマを選択し、スキーマを SQL Server と同期します。  
  
新しいプロジェクト ダイアログ ボックスのドロップダウン リストに、移行から Azure SQL DB を選択した場合は、Azure SQL DB に接続する必要があります。 接続に成功した後は、Azure SQL DB データベースの階層は、Azure SQL DB メタデータ エクスプ ローラーに表示されます。 MySQL スキーマを Azure SQL DB のスキーマに変換した後は、Azure SQL DB メタデータ エクスプ ローラーでこれらの変換されたスキーマを選択し、Azure SQL DB では、スキーマを同期します。  
  
SQL Server または Azure SQL DB に変換されたスキーマを同期した後は、MySQL メタデータ エクスプ ローラーに戻るし、MySQL スキーマから SQL Server または Azure SQL DB データベースにデータを移行します。  
  
これらのタスクとその実行方法の詳細については、次を参照してください。 [SQL Server - Azure SQL DB への MySQL データベースの移行&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)します。  
  
次のセクションでは、SSMA ユーザー インターフェイスの機能について説明します。  
  
### <a name="metadata-explorers"></a>メタデータ エクスプ ローラー  
SSMA には、参照し、MySQL および SQL Server データベースで操作を実行する 2 つのメタデータ エクスプ ローラーが含まれています。  
  
### <a name="mysql-metadata-explorer"></a>MySQL メタデータ エクスプ ローラー  
MySQL メタデータ エクスプ ローラーでは、MySQL スキーマについての情報が表示されます。 MySQL メタデータ エクスプ ローラーを使用すると、次のタスクを実行できます。  
  
-   各スキーマ内のオブジェクトを参照します。  
  
-   変換でオブジェクトを選択し、SQL Server の構文にオブジェクトを変換します。 詳細については、次を参照してください[MySQL データベースを変換する&#40;MySQLToSQL。&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
-   データ移行のためのテーブルを選択し、それらのテーブルからデータを SQL Server に移行します。 詳細については、次を参照してください[MySQL データを SQL Server - Azure SQL DB に移行する&#40;MySQLToSQL。&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server または Azure SQL DB メタデータ エクスプ ローラー  
SQL Server または Azure SQL DB メタデータ エクスプ ローラーには、SQL Server または Azure SQL DB のインスタンスに関する情報が表示されます。 SQL Server または Azure SQL DB のインスタンスに接続するときに SSMA はそのインスタンスに関するメタデータを取得し、プロジェクト ファイルに格納します。  
  
このメタデータ エクスプ ローラーを使用して、変換後の MySQL データベースのオブジェクトを選択し、SQL Server または Azure SQL DB のインスタンスでこれらのオブジェクトを同期できます。  
  
詳細については、次を参照してください[同期 (SQL Server への MySQL または Azure SQL DB)。](https://msdn.microsoft.com/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
### <a name="metadata"></a>メタデータ  
各メタデータ エクスプ ローラーの右側には、選択したオブジェクトを記述するタブが。 たとえば、MySQL メタデータ エクスプ ローラーでテーブルを選択する場合は、9 つのタブが表示されます。**テーブル**、 **SQL**、**の種類のマッピング**、**データ**、**設定**、 **Charset マッピング**、**SQL モード**、**プロパティ**、および**レポート**します。 **レポート** タブには、選択したオブジェクトを格納しているレポートを作成した後にのみ情報が含まれます。 SQL Server メタデータ エクスプ ローラーでテーブルを選択する場合は、3 つのタブが表示されます。**テーブル**、 **SQL**と**データ**します。  
  
ほとんどのメタデータの設定とは、読み取り専用です。 ただし、次のメタデータを変更できます。  
  
-   MySQL メタデータ エクスプ ローラーでは、型のマッピング、文字セットのマッピングを SQL モードを変更できます。 変更された型のマッピングまたは文字セットのマッピングまたは SQL モードに変換するには、スキーマを変換する前に、変更を加えます。  
  
-   SQL Server メタデータ エクスプ ローラーで、[テーブル] タブでテーブルとインデックスのプロパティを変更できます。SQL Server でこれらの変更を表示するには、スキーマを SQL Server に読み込む前にこれらの変更を行います。  
  
メタデータ エクスプ ローラーで行われた変更は、ソースまたはターゲット データベースではなく、プロジェクトのメタデータに反映されます。  
  
### <a name="toolbars"></a>[ツール バー]  
SSMA は 2 つのツールバー: プロジェクト ツールバー、および移行ツールバー。  
  
### <a name="the-project-toolbar"></a>プロジェクトのツールバー  
プロジェクトのツールバーには、プロジェクトでの作業、MySQL への接続、および SQL Server または Azure SQL DB に接続するためのボタンが含まれています。 これらのボタンで、コマンドのように、**ファイル**メニュー。  
  
### <a name="migration-toolbar"></a>移行のツールバー  
次の表は、ツールバーのコマンドを移行には。  
  
|||  
|-|-|  
|**Button**|**関数**|  
|**レポートを作成します。**|SQL Server または Azure SQL DB のオブジェクトを選択した MySQL オブジェクトに変換し、どのように成功して、変換を示すレポートを作成します。<br /><br />MySQL メタデータ エクスプ ローラーでオブジェクトが選択されていない場合は、このコマンドが無効です。|  
|**スキーマを変換します。**|選択した MySQL オブジェクトを SQL Server または Azure SQL DB のオブジェクトに変換します。<br /><br />MySQL メタデータ エクスプ ローラーでオブジェクトが選択されていない場合は、このコマンドが無効です。|  
|**データを移行します。**|MySQL データベースからデータを SQL Server または Azure SQL DB に移行します。 このコマンドを実行する前に、MySQL スキーマを SQL Server または Azure SQL DB のスキーマに変換し、SQL Server または Azure SQL DB にオブジェクトを読み込む必要があります。<br /><br />MySQL メタデータ エクスプ ローラーでオブジェクトが選択されていない場合は、このコマンドが無効です。|  
|**[停止]**|現在のプロセスを停止します。|  
  
### <a name="menus"></a>メニュー  
次の表では、SSMA メニューを示します。  
  
|||  
|-|-|  
|**Menu**|**[説明]**|  
|**[最近使ったファイル]**|プロジェクトでの作業、MySQL への接続、および SQL Server または Azure SQL DB に接続するためのコマンドが含まれています。|  
|**[編集]**|検索と詳細ページのテキストを扱うのためのコマンドが含まれています。 開くには**ブックマークの管理** ダイアログの編集 メニューの ブックマークの管理 をクリックします。 ダイアログ ボックスで、既存のブックマークの一覧が表示されます。 ダイアログ ボックスの右側にあるボタンを使用するには、ブックマークを管理します。|  
|**[表示]**|含まれています、**メタデータ エクスプ ローラーの同期**コマンド。 MySQL メタデータ エクスプ ローラーと SQL Server または Azure SQL DB メタデータ エクスプ ローラーの間のオブジェクトを同期するとします。 表示し、非表示にするためのコマンドも含まれています、**出力**と**エラー一覧**ペインおよびオプション**レイアウト**レイアウトを管理します。|  
|**ツール**|レポートを作成、スキーマの変換、データベースからの更新、オブジェクトとデータの移行、およびスクリプトとして保存するためのコマンドが含まれています。 アクセスできます、**グローバル設定、プロジェクト設定の既定の**と**プロジェクト設定** ダイアログ ボックス。|  
|**ヘルプ**|SSMA のヘルプにアクセスを提供します、**について** ダイアログ ボックス。|  
  
### <a name="output-pane-and-error-list-pane"></a>出力ウィンドウおよびエラー一覧 ウィンドウ  
**ビュー**メニュー コマンドの出力ウィンドウおよびエラー一覧 ウィンドウの表示を切り替えるには。  
  
-   [出力] ペインは、SSMA からオブジェクトへの変換、オブジェクトの同期、およびデータの移行中にステータス メッセージを示します。  
  
-   エラー一覧ウィンドウには、並べ替え可能なリストでのエラー、警告、および情報メッセージが表示されます。  
  
## <a name="see-also"></a>参照  
[ユーザー インターフェイス リファレンス&#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
[SQL Server - Azure SQL DB への MySQL データの移行&#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
