---
title: SQL Server (AccessToSQL) へのデータベース オブジェクトの変換後の読み込み |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, loading converted objects into SQL Azure
- Access databases, loading converted objects into SQL Server
- data, securing
- loading objects into SQL Azure
- loading objects into SQL Server
- migrating objects into SQL Azure
- migrating objects into SQL Server
- moving objects into SQL Azure
- moving objects into SQL Server
- schemas, loading into SQL Azure
- schemas, loading into SQL Server
- scripting converted objects
- securing data
- SQL Azure, loading objects into
- SQL Server, loading objects into
- synchronizing metadata with SQL Azure
- synchronizing metadata with SQL Server
- uploading objects into SQL Azure
- uploading objects into SQL Server
ms.assetid: 4e854eee-b10c-4f0b-9d9e-d92416e6f2ba
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7effaa973b7a39df6fc0b9385a5cfde4fdad18d4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67986313"
---
# <a name="loading-converted-database-objects-into-sql-server-accesstosql"></a>SQL Server (AccessToSQL) へのデータベース オブジェクトの変換後の読み込み
Access データベースのオブジェクトに変換した後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure には、結果のデータベース オブジェクトを読み込むことができます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 SSMA は、オブジェクトを作成したか、またはオブジェクトをスクリプトし、自分でスクリプトを実行することができます。 SSMA によりの実際の内容で対象のメタデータを更新する、また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure データベース。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同期とスクリプトの選択  
変換されたデータベース オブジェクトを読み込む場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または変更なしの SQL Azure、SSMA を直接作成またはデータベース オブジェクトを再生成ができます。 メソッドは、迅速かつ簡単がのカスタマイズを許可しておらず、[!INCLUDE[tsql](../../includes/tsql-md.md)]を定義するコード、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]またはストアド プロシージャ以外の SQL Azure のオブジェクト。  
  
変更する場合、[!INCLUDE[tsql](../../includes/tsql-md.md)]オブジェクトを作成またはオブジェクトの作成より詳細に制御する場合は、SSMA を使用して、スクリプトを作成するに使用されます。 これらのスクリプトを変更して、個別に、各オブジェクトを作成しを使用しても[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントをこれらのオブジェクトを作成するスケジュールを設定します。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>SSMA を使用して、SQL server オブジェクトを同期するには  
SSMA を使用して作成する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure データベースのオブジェクト内のオブジェクトを選択する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータ エクスプ ローラーを持つオブジェクトの同期をとって[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure、次の手順で示すようにします。 内のオブジェクトに存在する場合、既定で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のかどうかは、SSMA メタデータがいくつかのローカルの変更や更新プログラム、非常にこれらのオブジェクトの定義、SSMA でオブジェクトの定義が変更されます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure です。 編集して、既定の動作を変更する**プロジェクト設定**します。  
  
> [!NOTE]  
> 既存の選択[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Access データベースから変換されなかった SQL Azure データベースのオブジェクト。 ただし、SSMA が再作成しない、またはそれらのオブジェクトが変更されます。  
  
**SQL Server または SQL Azure とオブジェクトを同期するには**  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータ エクスプ ローラーで、上部の展開[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure のノードを展開し、**データベース**します。  
  
2.  処理するオブジェクトを選択します。  
  
    -   完全なデータベースを同期するには、データベース名の横にあるチェック ボックスを選択します。  
  
    -   個々 のオブジェクトまたはオブジェクトのカテゴリの省略を同期したり、選択するか、オブジェクトまたはフォルダーの横にあるチェック ボックスをオフにします。  
  
3.  後で処理するオブジェクトを選択したら[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータ エクスプ ローラーで、右クリックして**データベース**、順にクリックします**データベースと同期する**します。  
  
    オブジェクトまたはその親フォルダーを右クリックし、をクリックして、個々 のオブジェクトまたはオブジェクトのカテゴリに分類を同期することも**データベースと同期する**します。  
  
    その後、SSMA が表示されます、**データベースと同期する**ダイアログ ボックスで、2 つの項目のグループを確認できます。 左側にある、SSMA は、ツリーで表される選択されたデータベース オブジェクトを示します。 右側にある、SSMA メタデータ内の同じオブジェクトを表すツリーを表示できます。 ことができます、右または左クリックして、ツリーを展開 ' +' ボタンをクリックします。 同期の方向は、2 つのツリーの間に配置アクション 列に表示されます。  
  
    3 つの状態では、アクションの符号になります。  
  
    -   左矢印は、メタデータの内容は、データベース (既定値) に保存されますを意味します。  
  
    -   右向きの矢印は、データベースの内容は、SSMA メタデータで上書きされますを意味します。  
  
    -   バツ印は、アクションは実行されませんを意味します。  
  
    状態を変更するアクションの記号をクリックします。 クリックすると、実際の同期が行われます**OK**のボタン、**データベースと同期する**ダイアログ。  
  
## <a name="scripting-objects"></a>オブジェクトのスクリプト作成  
保存する場合[!INCLUDE[tsql](../../includes/tsql-md.md)]オブジェクトの定義を変更するか、変換後のデータベース オブジェクトの定義と実行スクリプトを自分で、オブジェクトの定義を変換後のデータベースに保存する[!INCLUDE[tsql](../../includes/tsql-md.md)]スクリプト。  
  
**スクリプトに 1 つまたは複数のオブジェクトを保存するには**  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーは、最上位ノード (サーバー名) を展開し、展開**データベース**します。  
  
2.  次の 1 つ以上の操作を行います。  
  
    -   完全なデータベースをスクリプト化するには、データベース名の横にあるチェック ボックスを選択します。  
  
    -   スクリプトまたは個々 のビューの省略は、データベースを展開し、**ビュー**、選択するか、ビューの横にあるチェック ボックスをオフにします。  
  
    -   スクリプトまたは個々 のテーブルの省略は、データベースを展開し、**テーブル**、選択するか、テーブルの横にあるチェック ボックスをオフにします。  
  
    -   スクリプトまたはテーブルの個々 のインデックスの省略は、テーブルを展開し、**インデックス**、選択するか、インデックスをオフにします。  
  
3.  右クリック**データベース**選択**スクリプトとして保存**します。  
  
    個々 のオブジェクトをスクリプトすることもできます。 オブジェクトの選択に関係なく、オブジェクトのスクリプト オブジェクトを右クリックし、選択**スクリプトとして保存**します。  
  
4.  **名前を付けて保存** ダイアログ ボックスで、ファイルの名前を入力、スクリプトを保存フォルダーを探して、**ファイル名**ボックスをクリックして**OK**。  
  
    SSMA は、.sql というファイル名拡張子を追加します。  
  
### <a name="modifying-scripts"></a>スクリプトを変更します。  
保存した後、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用するスクリプトとして、オブジェクトの定義を SQL Azure、または[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]スクリプトを変更します。  
  
**スクリプトを変更するには**  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **ファイル**メニューで、**オープン**、 をクリックし、**ファイル**。  
  
2.  **オープン**ダイアログ ボックスで、検索し、スクリプト ファイルを選択し、順にクリックします**OK**します。  
  
3.  クエリ エディターを使用して、スクリプト ファイルを編集します。  
  
    クエリ エディターの詳細についてを参照してください"エディター便利なコマンドと機能"[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
4.  [ファイル] メニューに、スクリプトを保存する選択**保存**します。  
  
### <a name="running-scripts"></a>スクリプトを実行します。  
スクリプト、または個々 のステートメントを実行できる[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]します。  
  
**スクリプトを実行するには**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **ファイル**メニューで、**オープン**順にクリックします**ファイル**します。  
  
2.  **オープン**ダイアログ ボックスで、検索し、スクリプト ファイルを選択し、順にクリックします**OK**します。  
  
3.  完全なスクリプトを実行するキーを押して、 **F5**キー。  
  
4.  一連のステートメントを実行するクエリ エディター ウィンドウで、ステートメントを選択し、キーを押します、 **F5**キー。  
  
クエリ エディターを使用してスクリプトを実行する方法の詳細については、次を参照してください。" [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]クエリ"で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
使用して、コマンドラインからスクリプトを実行することも、 **sqlcmd**ユーティリティ、およびから[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント。 詳細については**sqlcmd**、"sqlcmd ユーティリティ"を参照してください[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。 詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントを参照してください"管理タスクを自動化する ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント)"で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
## <a name="securing-objects-in-sql-server"></a>SQL Server のオブジェクトをセキュリティで保護します。  
変換されたデータベース オブジェクトを読み込んだ後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を付与し、それらのオブジェクトに対する権限の拒否できます。 移行する前にそうことをお勧めするデータ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 オブジェクトをセキュリティで保護する方法については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、「セキュリティの考慮事項のデータベースとデータベース アプリケーション」を参照してください[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
## <a name="next-step"></a>次の手順  
移行プロセスでは、次の手順は[データを SQL Server に移行](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)します。  
  
## <a name="see-also"></a>参照  
[SQL Server へのアクセス データベースの移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
