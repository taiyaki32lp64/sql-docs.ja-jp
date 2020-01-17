---
title: SQL Server (DB2ToSQL) へのデータベース オブジェクトの変換後の読み込み |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 7af5566094c9cc4c40ba2aa33f27e79bae1c7445
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141033"
---
# <a name="loading-converted-database-objects-into-sql-server-db2tosql"></a>SQL Server (DB2ToSQL) へのデータベース オブジェクトの変換後の読み込み
DB2 スキーマに変換した後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]には、結果のデータベース オブジェクトを読み込むことができます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 SSMA は、オブジェクトを作成したか、またはオブジェクトをスクリプトし、自分でスクリプトを実行することができます。 SSMA によりの実際の内容で対象のメタデータを更新する、また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同期とスクリプトの選択  
変換されたデータベース オブジェクトを読み込む場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]する変更を加えなければ、SSMA を直接作成またはデータベース オブジェクトを作成し直すことができます。 メソッドは、迅速かつ簡単がのカスタマイズを許可しておらず、[!INCLUDE[tsql](../../includes/tsql-md.md)]を定義するコード、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ストアド プロシージャ以外のオブジェクト。  
  
変更する場合、[!INCLUDE[tsql](../../includes/tsql-md.md)]オブジェクトを作成またはオブジェクトの作成より詳細に制御する場合は、SSMA を使用して、スクリプトを作成するに使用されます。 これらのスクリプトを変更して、個別に、各オブジェクトを作成しを使用しても[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントをこれらのオブジェクトを作成するスケジュールを設定します。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>SSMA を使用して、SQL server オブジェクトを同期するには  
SSMA を使用して作成する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内のオブジェクトを選択したデータベースのオブジェクト[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーを使用してオブジェクトの同期をとって[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]次の手順で示すように、します。 内のオブジェクトに存在する場合、既定で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、SSMA メタデータが内のオブジェクトよりも新しい場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、SSMA でオブジェクトの定義が変更されます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 編集して、既定の動作を変更する**プロジェクト設定**します。  
  
> [!NOTE]  
> 既存を選択する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース DB2 データベースから変換されたオブジェクト。 ただし、これらのオブジェクトを再作成またはされません SSMA によって変更します。  
  
**SQL server オブジェクトを同期するには**  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーで、上部の展開[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ノードを順に展開**データベース**。  
  
2.  処理するオブジェクトを選択します。  
  
    -   完全なデータベースを同期するには、データベース名の横にあるチェック ボックスを選択します。  
  
    -   個々 のオブジェクトまたはオブジェクトのカテゴリの省略を同期したり、選択するか、オブジェクトまたはフォルダーの横にあるチェック ボックスをオフにします。  
  
3.  後で処理するオブジェクトを選択したら[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータ エクスプ ローラーを右クリックして**データベース**、順にクリックします**データベースと同期する**します。  
  
    オブジェクトまたはその親フォルダーを右クリックし、をクリックして、個々 のオブジェクトまたはオブジェクトのカテゴリに分類を同期することも**データベースと同期する**します。  
  
    その後、SSMA が表示されます、**データベースと同期する**ダイアログ ボックスで、2 つの項目のグループを確認できます。 左側にある、SSMA は、ツリーで表される選択されたデータベース オブジェクトを示します。 右側にある、SSMA メタデータ内の同じオブジェクトを表すツリーを表示できます。 ことができます、右または左クリックして、ツリーを展開 ' +' ボタンをクリックします。 同期の方向は、2 つのツリーの間に配置アクション 列に表示されます。  
  
    3 つの状態では、アクションの符号になります。  
  
    -   左矢印は、メタデータの内容は、データベース (既定値) に保存されますを意味します。  
  
    -   右向きの矢印は、データベースの内容は、SSMA メタデータで上書きされますを意味します。  
  
    -   バツ印は、アクションは実行されませんを意味します。  
  
状態を変更するアクションの記号をクリックします。 クリックすると、実際の同期が行われます**OK**のボタン、**データベースと同期する**ダイアログ。  
  
## <a name="scripting-objects"></a>オブジェクトのスクリプト作成  
保存する[!INCLUDE[tsql](../../includes/tsql-md.md)]、変換後のデータベース オブジェクトのオブジェクトの定義を変更し、自分でスクリプトの実行にまたは定義を保存できます変換されたデータベース オブジェクトの定義[!INCLUDE[tsql](../../includes/tsql-md.md)]スクリプト。  
  
**オブジェクトをスクリプトとして保存するには**  
  
1.  スクリプトを保存するオブジェクトを選択したら後で右クリック**データベース**、 をクリックし、**スクリプトとして保存**します。  
  
    また、オブジェクトまたはその親フォルダーを右クリックし、をクリックして個々 のオブジェクトまたはオブジェクトのカテゴリをスクリプト**スクリプトとして保存**します。  
  
2.  **名前を付けて保存** ダイアログ ボックスで、ファイルの名前を入力、スクリプトを保存フォルダーを探して、**ファイル名**ボックスで、し[!INCLUDE[clickOK](../../includes/clickok-md.md)]します。 SSMA は、.sql というファイル名拡張子を追加します。  
  
### <a name="modifying-scripts"></a>スクリプトを変更します。  
保存した後、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用する 1 つまたは複数のスクリプトとしてオブジェクトの定義、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を表示したり、スクリプトを変更します。  
  
**スクリプトを変更するには**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **ファイル**メニューで、**オープン**、 をクリックし、**ファイル**。  
  
2.  **オープン**ダイアログ ボックスで、スクリプト ファイルを選択して [ok] をクリックします。
  
3.  クエリ エディターを使用して、スクリプト ファイルを編集します。  
  
    クエリ エディターの詳細についてを参照してください"エディター便利なコマンドと機能"[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
4.  ファイル メニューの スクリプトを保存する**保存**します。  
  
### <a name="running-scripts"></a>スクリプトを実行します。  
スクリプト、または個々 のステートメントを実行できる[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]します。  
  
**スクリプトを実行するには**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **ファイル**メニューで、**オープン**、 をクリックし、**ファイル**。  
  
2.  **オープン** ダイアログ ボックスで、スクリプト ファイルを選択し、 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  完全なスクリプトを実行するキーを押して、 **F5**キー。  
  
4.  一連のステートメントを実行するクエリ エディター ウィンドウで、ステートメントを選択し、キーを押します、 **F5**キー。  
  
クエリ エディターを使用してスクリプトを実行する方法の詳細については、次を参照してください。" [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]クエリ"で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
使用して、コマンドラインからスクリプトを実行することも、 **sqlcmd**ユーティリティとの間、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント。 詳細については**sqlcmd**、"sqlcmd ユーティリティ"を参照してください[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。 詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントを参照してください"管理タスクを自動化する ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント)"で[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
## <a name="securing-objects-in-sql-server"></a>SQL Server のオブジェクトをセキュリティで保護します。  
変換されたデータベース オブジェクトを読み込んだ後[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を付与し、それらのオブジェクトに対する権限の拒否できます。 移行する前にそうことをお勧めするデータ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 オブジェクトをセキュリティで保護する方法については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、「セキュリティの考慮事項のデータベースとデータベース アプリケーション」を参照してください[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順が、 [SQL Server への DB2 データの移行](https://msdn.microsoft.com/86cbd39f-6dac-409a-9ce1-7dd54403f84b)します。  
  
## <a name="see-also"></a>参照  
[DB2 のデータを SQL Server に移行する&#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
  
