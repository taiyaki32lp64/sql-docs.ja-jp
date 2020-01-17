---
title: MySQL データベース (MySQLToSQL) の変換 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac21850b-fb32-4704-9985-5759b7c688c7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1ad4cbbdf80422f87c850c44e47f82899de4c82a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103050"
---
# <a name="converting-mysql-databases-mysqltosql"></a>MySQL データベースの変換 (MySQLToSQL)
MySQL に接続すると後に、接続されている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に MySQL データベースのオブジェクトを変換できる SQL Azure、およびプロジェクトの設定とデータ マッピング オプション、または[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure データベースのオブジェクト。  
  
## <a name="the-conversion-process"></a>変換プロセス  
MySQL からオブジェクトの定義は、データベース オブジェクトの変換と同様に変換して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure オブジェクト、および SSMA メタデータにこの情報を読み込みます。 インスタンスに情報は読み込まれません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 使用して、オブジェクトとそのプロパティを表示することができますし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータ エクスプ ローラー。  
  
変換中は、SSMA は、出力ウィンドウに出力メッセージとエラー一覧 ウィンドウにエラー メッセージを出力します。 出力とエラー情報を使用して、MySQL データベースまたは必要な変換の結果を得るため、変換プロセスを変更しているかどうかを確認します。  
  
## <a name="setting-conversion-options"></a>変換オプションの設定  
オブジェクトを変換する前に、プロジェクトの変換オプションを確認して、**プロジェクト設定** ダイアログ ボックス。 このダイアログ ボックスを使用すると、SSMA がテーブルとインデックスに変換する方法を設定できます。 詳細については、「[プロジェクト設定&#40;変換&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
  
## <a name="conversion-results"></a>変換結果  
次の表は、変換、MySQL のオブジェクトし、その結果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクト。  
  
|||  
|-|-|  
|**MySQL のオブジェクト**|**SQL Server オブジェクトの結果として得られる**|  
|インデックスなどの依存オブジェクトを持つテーブル|SSMA は、依存オブジェクトをテーブルを作成します。 テーブルは、すべてのインデックスと制約に変換されます。 インデックスは、個別に変換されます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクト。<br /><br />**空間データ型マッピング**テーブル ノード レベルでのみ実行できます。<br /><br />テーブルの変換の設定の詳細については、次を参照してください[変換の設定。](conversion-settings-mysqltosql.md)|  
|関数|関数は、TRANSACT-SQL に直接変換できる、SSMA は、関数を作成します。 場合によっては、関数は、ストアド プロシージャに変換する必要があります。 これを使用して行うことができます**関数の変換**プロジェクトの設定にします。 この場合は、SSMA では、ストアド プロシージャおよびストアド プロシージャを呼び出す関数を作成します。<br /><br />**指定されたオプション:**<br /><br />プロジェクトの設定に従って変換します。<br /><br />関数への変換します。<br /><br />ストアド プロシージャへの変換します。<br /><br />関数の変換の設定の詳細については、次を参照してください[変換の設定。](conversion-settings-mysqltosql.md)|  
|手順|プロシージャは、TRANSACT-SQL に直接変換できる、SSMA は、ストアド プロシージャを作成します。 場合によっては、自律的なトランザクションでストアド プロシージャを呼び出す必要があります。 この場合は、SSMA が 2 つのストアド プロシージャを作成します: ストアド プロシージャのいずれかの手順と、実装を呼び出すために使用する別の実装します。|  
|データベースの変換|MySQL オブジェクトとしてのデータベースは直接変換されませんによって SSMA for MySQL。 MySQL データベースをスキーマ名のようにより処理され、物理的なすべてのパラメーターは変換中に失われます。 SSMA for MySQL を使用して[MySQL データベースを SQL Server スキーマへのマッピング&#40;MySQLToSQL&#41; ](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)に適切な SQL Server データベース/スキーマのペアに MySQL データベースからオブジェクトをマップします。|  
|トリガーの変換|**SSMA では、次の規則に基づくトリガーが作成されます。**<br /><br />トリガーが INSTEAD OF T-SQL トリガーに変換される前に<br /><br />AFTER トリガーは、行ごとのイテレーションの有無の後に T-SQL トリガーに変換されます。|  
|ビューの変換|SSMA は、依存オブジェクトでビューを作成します|  
|ステートメントの変換|-各 SQL ステートメントのオブジェクトが (DDL、DML、およびその他の種類のステートメント) などの 1 つの MySQL ステートメントを含めることができますか、開始しています.終了ブロック。<br />-   **複数ステートメントの変換: 開始しています.ブロックの変換終了**SQL ステートメントでは、BEGIN を含めることができますもしています.プロシージャ、関数、またはトリガーの定義でいずれかのような終了ブロック。 それらのブロックには、同様の MySQL の 1 つのステートメント オブジェクトの変換を変換する必要があります。|  
  
## <a name="converting-mysql-database-objects"></a>MySQL データベース オブジェクトの変換  
MySQL データベースのオブジェクトを変換するには、こと、変換するオブジェクトを選択し、SSMA 変換を実行します。 変換中に出力メッセージを表示する、**ビュー**メニューの **出力**します。  
  
**MySQL のオブジェクトを SQL Server または SQL Azure の構文に変換するには**  
  
1.  MySQL メタデータ エクスプ ローラーで、MySQL サーバーを展開し、展開**データベース**します。  
  
2.  変換するオブジェクトを選択します。  
  
    -   すべてのスキーマを変換する場合は、横にチェック ボックスを選択します**データベース**します。  
  
    -   変換またはデータベースの省略は、データベース名の横にあるチェック ボックスを選択します。  
  
    -   変換またはオブジェクトのカテゴリの省略は、スキーマを展開し、オンまたはカテゴリの横にあるチェック ボックスをオフにします。  
  
    -   変換または個々 のオブジェクトの省略は、カテゴリ フォルダーを展開し、オンまたはオブジェクトの横にチェック ボックスをオフにします。  
  
3.  右クリックし、選択したすべてのオブジェクトを変換する**データベース**選択**スキーマの変換**します。  
  
    オブジェクトまたはその親フォルダーを右クリックして選択し、個々 のオブジェクトまたはオブジェクトのカテゴリを変換することも**スキーマの変換**します。  
  
## <a name="viewing-conversion-problems"></a>変換の問題を表示します。  
MySQL の一部のオブジェクトを変換できません可能性があります。 変換の概要レポートを表示することによってコンバージョンの成功率を指定できます。  
  
**概要レポートを表示するには**  
  
1.  MySQL メタデータ エクスプ ローラーで選択**データベース**します。  
  
2.  右側のウィンドウで、選択、**レポート**タブ。  
  
    このレポートには、変換または評価されているすべてのデータベース オブジェクトの評価の概要レポートが表示されます。 個々 のオブジェクトの概要レポートを表示することもできます。  
  
    -   個々 のスキーマのレポートを表示するには、MySQL メタデータ エクスプ ローラーでデータベースを選択します。  
  
    -   個々 のオブジェクトのレポートを表示するには、MySQL メタデータ エクスプ ローラーで、オブジェクトを選択します。 変換の問題のあるオブジェクトは赤いエラー アイコンがあります。  
  
オブジェクトの変換に失敗した場合は、変換エラーを発生させた構文を表示することができます。  
  
**個々 の変換の問題を表示するには**  
  
1.  MySQL メタデータ エクスプ ローラーで、**データベース**します。  
  
2.  赤いエラー アイコンが表示されるデータベースを展開します。  
  
3.  データベースの下に赤いエラー アイコンが付いているフォルダーを展開します。  
  
4.  赤いエラー アイコンを含むオブジェクトを選択します。  
  
5.  右側のウィンドウでをクリックして、**レポート**タブ。  
  
6.  上部にある、**レポート** タブは、ドロップダウン リスト。 一覧表示されている場合**統計**、選択範囲を変更**ソース**します。  
  
    SSMA は、ソース コードとコードのすぐ上のいくつかのボタンに表示されます。  
  
7.  をクリックして、**次の問題**ボタンをクリックします。 これは、右向き矢印の付いた赤いエラー アイコンです。  
  
    SSMA は、現在のオブジェクトで見つかった最初の問題のあるソース コードを強調表示されます。  
  
変換できなかった項目ごとにそのオブジェクトを決定する必要があります。  
  
-   削除または問題のあるコードを変更するには MySQL データベース内のオブジェクトを変更することができます。 SSMA に更新されたコードを読み込むには、メタデータを更新する必要があります。 詳細については、次を参照してください[MySQL に接続する&#40;MySQLToSQL。&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   オブジェクトは、移行から除外できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータ エクスプ ローラーと MySQL メタデータ エクスプ ローラーにオブジェクトを読み込む前に、項目の横にあるチェック ボックスをオフに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure と MySQL からデータを移行します。  
  
## <a name="next-step"></a>次の手順  
移行プロセスでは、次の手順は[を SQL Server に変換されたデータベース オブジェクトの読み込み&#40;MySQLToSQL&#41;](../../ssma/mysql/loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>関連項目  
[SQL Server - Azure SQL DB への移行 MySQL データベース&#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
