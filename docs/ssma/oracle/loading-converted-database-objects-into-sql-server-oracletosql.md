---
title: SQL Server (OracleToSQL) へのデータベース オブジェクトの変換後の読み込み |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Synchronization, Securing Objects in SQL Server
- Synchronization,Scripting Objects
ms.assetid: a8ae33b2-1883-4785-922b-ea0e31c0b37a
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 97c34beb0cbe27e8d3c88b922690dc369fb7103b
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262989"
---
# <a name="loading-converted-database-objects-into-sql-server-oracletosql"></a>SQL Server への変換されたデータベース オブジェクトの読み込み (OracleToSQL)
Oracle スキーマを SQL Server に変換した後は、SQL Server に結果のデータベース オブジェクトを読み込むことができます。 SSMA は、オブジェクトを作成したか、またはオブジェクトをスクリプトし、自分でスクリプトを実行することができます。 また、SSMA には、SQL Server データベースの実際の内容で対象のメタデータを更新することができます。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同期とスクリプトの選択  
SQL Server に変更しなくても、変換後のデータベース オブジェクトを読み込む場合は、SSMA を直接作成またはデータベース オブジェクトを再作成してもかまいません。 メソッドは、簡単ですのカスタマイズは許可されません、[!INCLUDE[tsql](../../includes/tsql-md.md)]ストアド プロシージャ以外の SQL Server オブジェクトを定義するコードです。  
  
変更する場合、[!INCLUDE[tsql](../../includes/tsql-md.md)]オブジェクトを作成またはオブジェクトの作成より詳細に制御する場合は、SSMA を使用して、スクリプトを作成するに使用されます。 これらのスクリプトを変更し、個別に、各オブジェクトを作成しも SQL Server エージェントを使用して、それらのオブジェクトを作成するスケジュールを設定できます。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>SSMA を使用して、SQL server オブジェクトを同期するには  
SSMA を使用して SQL Server データベース オブジェクトを作成するには、SQL Server メタデータ エクスプ ローラーでオブジェクトを選択し、次の手順で示すように SQL server でのオブジェクトを同期します。 既定では、SSMA メタデータが、SQL Server 内のオブジェクトよりも新しい場合は、オブジェクトは、SQL Server で既に存在する場合、SSMA によって変わることで SQL Server オブジェクトの定義。 編集して、既定の動作を変更する**プロジェクト設定**します。  
  
> [!NOTE]  
> Oracle データベースから変換されなかった既存の SQL Server データベース オブジェクトを選択することができます。 ただし、これらのオブジェクトを再作成またはされません SSMA によって変更します。  
  
**SQL server オブジェクトを同期するには**  
  
1.  SQL Server メタデータ エクスプ ローラーで最上位の SQL Server ノードを展開し、展開**データベース**します。  
  
2.  処理するオブジェクトを選択します。  
  
    -   完全なデータベースを同期するには、データベース名の横にあるチェック ボックスを選択します。  
  
    -   個々 のオブジェクトまたはオブジェクトのカテゴリの省略を同期したり、選択するか、オブジェクトまたはフォルダーの横にあるチェック ボックスをオフにします。  
  
3.  SQL Server メタデータ エクスプ ローラーで処理するオブジェクトを選択したら右**データベース**、順にクリックします**データベースと同期する**します。  
  
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
  
2.  **名前を付けて保存** ダイアログ ボックスで、ファイルの名前を入力、スクリプトを保存フォルダーを探して、**ファイル名**ボックスし、順にクリックします ok の SSMA は、.sql というファイル名拡張子を追加します。  
  
### <a name="modifying-scripts"></a>スクリプトを変更します。  
使用することができます、1 つ以上のスクリプトの SQL Server オブジェクトの定義を保存した後[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を表示したり、スクリプトを変更します。  
  
**スクリプトを変更するには**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **ファイル**メニューで、**オープン**、 をクリックし、**ファイル**。  
  
2.  **オープン**ダイアログ ボックスでは、スクリプト ファイルを選択し、[ok] をクリックします。
  
3.  クエリ エディターを使用して、スクリプト ファイルを編集します。  
  
    クエリ エディターの詳細については、[エディター利便性のためのコマンドと機能] で SQL Server オンライン ブックを参照してください。  
  
4.  ファイル メニューの スクリプトを保存する**保存**します。  
  
### <a name="running-scripts"></a>スクリプトを実行します。  
スクリプト、または個々 のステートメントを実行できる[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]します。  
  
**スクリプトを実行するには**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **ファイル**メニューで、**オープン**、 をクリックし、**ファイル**。  
  
2.  **オープン**ダイアログ ボックスで、スクリプト ファイルを選択して [ok] をクリックして  
  
3.  完全なスクリプトを実行するキーを押して、 **F5**キー。  
  
4.  一連のステートメントを実行するクエリ エディター ウィンドウで、ステートメントを選択し、キーを押します、 **F5**キー。  
  
クエリ エディターを使用してスクリプトを実行する方法の詳細については、次を参照してください。" [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]クエリ"SQL Server オンライン ブックの「します。  
  
使用して、コマンドラインからスクリプトを実行することも、 **sqlcmd**ユーティリティ、および SQL Server エージェントから。 詳細については**sqlcmd**、SQL Server オンライン ブックの「"sqlcmd ユーティリティ"を参照してください。 SQL Server エージェントの詳細については、「管理タスクを自動化する (SQL Server エージェント)」で SQL Server オンライン ブックを参照してください。  
  
## <a name="securing-objects-in-sql-server"></a>SQL Server のオブジェクトをセキュリティで保護します。  
変換後のデータベース オブジェクトは、SQL Server に読み込まれるが後、を付与し、それらのオブジェクトに対する権限の拒否できます。 移行する前にそうことをお勧めする SQL Server のデータ。 SQL Server のセキュリティで保護されたオブジェクトを支援する方法については、「セキュリティの考慮事項のデータベースとデータベース アプリケーション」で SQL Server オンライン ブックを参照してください。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順が、[データを SQL Server に移行](migrating-oracle-data-into-sql-server-oracletosql.md)します。  
  
## <a name="see-also"></a>参照  
[SQL Server にデータベースを移行する Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
