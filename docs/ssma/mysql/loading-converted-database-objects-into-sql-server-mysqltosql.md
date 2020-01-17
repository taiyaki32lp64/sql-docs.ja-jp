---
title: SQL Server (MySQLToSQL) へのデータベース オブジェクトの変換後の読み込み |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac993a6d-0283-4823-8793-6b217677dfa3
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: a6966209300e6959e7ba9cb1afa11eb42b855d82
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909012"
---
# <a name="loading-converted-database-objects-into-sql-server-mysqltosql"></a>SQL Server への変換されたデータベース オブジェクトの読み込み (MySQLToSQL)
MySQL データベースを変換した後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure には、結果のデータベース オブジェクトを読み込むことができます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 SSMA は、オブジェクトを作成したか、またはオブジェクトをスクリプトし、自分でスクリプトを実行することができます。 SSMA によりの実際の内容で対象のメタデータを更新する、また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure データベース。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同期とスクリプトの選択  
変換されたデータベース オブジェクトを読み込む場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または変更なしの SQL Azure、SSMA を直接作成またはデータベース オブジェクトを再生成ができます。 メソッドを簡単に実行を定義する TRANSACT-SQL コードのカスタマイズは許可されませんが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のオブジェクト。  
  
オブジェクトを作成するために使用する Transact SQL を変更する場合、またはオブジェクトの作成より詳細に制御したい場合は、SSMA を使用してスクリプトを作成します。 これらのスクリプトを変更し、個別に、各オブジェクトを作成しも SQL Server エージェントを使用して、これらのオブジェクトを作成するスケジュールを設定できます。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>SSMA を使用して、SQL server オブジェクトを同期するには  
SSMA を使用して、SQL Server または SQL Azure のデータベース オブジェクトを作成する、内のオブジェクトを選択する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータ エクスプ ローラーを持つオブジェクトの同期をとって[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure、次の手順で示すようにします。 内のオブジェクトに存在する場合、既定で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のかどうかは、SSMA メタデータがいくつかのローカルの変更や更新プログラム、非常にこれらのオブジェクトの定義、SSMA でオブジェクトの定義が変更されます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 編集して、既定の動作を変更する**プロジェクト設定**します。  
  
> [!NOTE]  
> 既存の選択[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure データベース オブジェクトの MySQL データベースからに変換されなかった。 ただし、これらのオブジェクトを再作成またはされません SSMA によって変更します。  
  
##### <a name="to-synchronize-objects-with-sql-server-or-sql-azure"></a>SQL Server または SQL Azure とオブジェクトを同期するには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータ エクスプ ローラーで、上部の展開[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のノードを展開し、**データベース**します。  
  
2.  処理するオブジェクトを選択します。  
  
    -   完全なデータベースを同期するには、データベース名の横にあるチェック ボックスを選択します。  
  
    -   個々 のオブジェクトまたはオブジェクトのカテゴリの省略を同期したり、選択するか、オブジェクトまたはフォルダーの横にあるチェック ボックスをオフにします。  
  
3.  SQL Server または SQL Azure メタデータ エクスプ ローラーで処理するオブジェクトを選択したら右**データベース**、順にクリックします**データベースと同期する**します。  
  
    オブジェクトまたはその親フォルダーを右クリックし、をクリックして、個々 のオブジェクトまたはオブジェクトのカテゴリに分類を同期することも**データベースと同期する**します。  
  
    その後、SSMA が表示されます、**データベースと同期する**ダイアログ ボックスで、2 つの項目のグループを確認できます。 左側にある、SSMA は、ツリーで表される選択されたデータベース オブジェクトを示します。 右側にある、SSMA メタデータ内の同じオブジェクトを表すツリーを表示できます。 ことができます、右または左クリックして、ツリーを展開 ' +' ボタンをクリックします。 同期の方向は、2 つのツリーの間に配置アクション 列に表示されます。  
  
    次の 3 つの状態では、アクションの符号になります。  
  
    -   左矢印は、メタデータの内容は、データベース (既定値) に保存されますを意味します。  
  
    -   右向きの矢印は、データベースの内容は、SSMA メタデータで上書きされますを意味します。  
  
    -   バツ印は、アクションは実行されませんを意味します。  
  
    -   状態を変更するアクションの記号をクリックします。 クリックすると、実際の同期が行われます**OK**のボタン、**データベースと同期する**ダイアログ。  
  
## <a name="scripting-objects"></a>オブジェクトのスクリプト作成  
保存する[!INCLUDE[tsql](../../includes/tsql-md.md)]、変換後のデータベース オブジェクトのオブジェクトの定義を変更し、自分でスクリプトの実行にまたは定義を保存できます変換されたデータベース オブジェクトの定義[!INCLUDE[tsql](../../includes/tsql-md.md)]スクリプト。  
  
**オブジェクトをスクリプトとして保存するには**  
  
1.  スクリプトを保存するオブジェクトを選択したら後で右クリック**データベース**、 をクリックし、**スクリプトとして保存**します。  
  
    また、オブジェクトまたはその親フォルダーを右クリックし、をクリックして個々 のオブジェクトまたはオブジェクトのカテゴリをスクリプト**スクリプトとして保存**します。  
  
2.  **名前を付けて保存** ダイアログ ボックスで、ファイルの名前を入力、スクリプトを保存フォルダーを探して、**ファイル名**ボックスで、し[!INCLUDE[clickOK](../../includes/clickok-md.md)]SSMA は、.sql というファイル名拡張子を追加します。  
  
### <a name="modifying-scripts"></a>スクリプトを変更します。  
スクリプトとして、SQL Server または SQL Azure のオブジェクト定義を保存した後は、スクリプトを変更するのに SQL Server Management Studio を使用することができます。  
  
**スクリプトを変更するには**  
  
1.  Management Studio で**ファイル**メニューで、**オープン**、 をクリックし、**ファイル**。  
  
2.  [開く] ダイアログ ボックスで、検索し、スクリプト ファイルを選択してクリックして**OK**します。  
  
3.  クエリ エディターを使用して、スクリプト ファイルを編集します。クエリ エディターの詳細については、[エディター利便性のためのコマンドと機能] で SQL Server オンライン ブックを参照してください。  
  
4.  [ファイル] メニューに、スクリプトを保存する選択**保存**します。  
  
### <a name="running-scripts"></a>スクリプトを実行します。  
SQL Server Management Studio では、スクリプト、または個々 のステートメントを実行できます。  
  
**スクリプトを実行するには**  
  
1.  SQL Server Management Studio で**ファイル**メニューで、**オープン** をクリックし、**ファイル**します。  
  
2.  [開く] ダイアログ ボックスで、検索し、スクリプト ファイルを選択してクリックして**OK**します。  
  
3.  完全なスクリプトを実行するキーを押して、 **F5**キー。  
  
4.  一連のステートメントを実行するクエリ エディター ウィンドウで、ステートメントを選択し、キーを押します、 **F5**キー。  
  
5.  クエリ エディターを使用してスクリプトを実行する方法の詳細については、「SQL Server Management Studio Transact SQL クエリ」SQL Server オンライン ブックを参照してください。  
  
6.  使用して、コマンドラインからスクリプトを実行することも、 **sqlcmd**ユーティリティ、および SQL Server エージェントから。 詳細については**sqlcmd**、SQL Server オンライン ブックの「"sqlcmd ユーティリティ"を参照してください。 SQL Server エージェントの詳細については、「管理タスクを自動化する (SQL Server エージェント)」で SQL Server オンライン ブックを参照してください。  
  
## <a name="securing-objects-in-sql-server"></a>SQL Server のオブジェクトをセキュリティで保護します。  
変換後のデータベース オブジェクトは、SQL Server に読み込まれるが後、を付与し、これらのオブジェクトに対する権限の拒否できます。 移行する前にそうことをお勧めする SQL Server のデータ。 SQL Server のセキュリティで保護されたオブジェクトを支援する方法については、「セキュリティの考慮事項のデータベースとデータベース アプリケーション」で SQL Server オンライン ブックを参照してください。  
  
## <a name="next-step"></a>次の手順  
移行プロセスでは、次の手順は[MySQL データを SQL Server - Azure SQL DB に移行する&#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
## <a name="see-also"></a>関連項目  
[SQL Server - Azure SQL DB への移行 MySQL データベース&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
