---
title: パーティション テーブルとパーティション インデックスの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.createpartition.progress.f1
- sql13.swb.createpartition.partitioncolumn.f1
- sql13.swb.createpartition.createjob.f1
- sql13.swb.createpartition.finish.f1
- sql13.swb.createpartition.selectoutput.f1
- sql13.swb.createpartition.partitionfunction.f1
- sql13.swb.createpartition.partitionscheme.f1
- sql13.swb.createpartition.getstart.f1
- sql13.swb.createpartition.mappartition.f1
- sql13.swb.createpartition.summary.f1
helpviewer_keywords:
- partitioned indexes [SQL Server], creating
- partition schemes [SQL Server], creating
- partition functions [SQL Server], creating
- partitioned tables [SQL Server], creating
- partition functions [SQL Server]
- partition schemes [SQL Server]
ms.assetid: 7641df10-1921-42a7-ba6e-4cb03b3ba9c8
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 046ce79c989fdfb24c6615968e6bad951aeb7280
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024903"
---
# <a name="create-partitioned-tables-and-indexes"></a>パーティション テーブルとパーティション インデックスの作成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、パーティション テーブルまたはパーティション インデックスを作成できます。 パーティション テーブルとパーティション インデックスのデータは、データベース内の複数のファイル グループに分散できるように、行方向に複数の単位に分割されています。 パーティション分割により、大規模なテーブルとインデックスの管理の可能性と拡張性が向上します。  
  
 一般に、パーティション テーブルまたはパーティション インデックスの作成は、次の 4 つの操作で構成されます。  
  
1.  ファイル グループと、パーティション構成で指定されたパーティションを保持する対応するファイルを作成します。  
  
2.  テーブルまたはインデックスの行を指定された列の値に基づいてパーティションにマップするパーティション関数を作成します。  
  
3.  パーティション テーブルまたはパーティション インデックスのパーティションを新しいファイル グループにマップするパーティション構成を作成します。  
  
4.  テーブルまたはインデックスを作成または変更し、格納場所としてそのパーティション構成を指定します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用してパーティション テーブルまたはパーティション インデックスを作成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   パーティション関数および構成のスコープは、それが作成されたデータベースに制限されます。 データベース内では、パーティション関数は他の関数とは別の名前空間に配置されます。  
  
-   パーティション関数内のいずれかの行に null 値を持つパーティション分割列がある場合、これらの行は左端のパーティションに割り当てられます。 ただし、NULL が境界値として指定され、RIGHT が指定されている場合、NULL 値は左端のパーティションを空にしたまま 2 番目のパーティションに配置されます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 パーティション テーブルを作成するには、データベースでの CREATE TABLE 権限と、テーブルを作成する構成に対する ALTER 権限が必要です。 パーティション インデックスを作成するには、インデックスを作成するテーブルまたはビューに対する ALTER 権限が必要です。 パーティション テーブルまたはパーティション インデックスを作成するには、次の追加の権限のいずれかが必要です。  
  
-   ALTER ANY DATASPACE 権限。 この権限は、既定では **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、および **db_ddladmin** 固定データベース ロールのメンバーに与えられています。  
  
-   パーティション関数およびパーティション構成を作成するデータベースに対する CONTROL 権限または ALTER 権限。  
  
-   パーティション関数およびパーティション構成を作成するデータベースのサーバーに対する CONTROL SERVER 権限または ALTER ANY DATABASE 権限。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 次の手順を実行して、1 つまたは複数のファイル グループ、対応するファイルと、およびテーブルを作成します。 これらのオブジェクトは、次の手順でパーティション テーブルを作成するときに参照します。  
  
#### <a name="to-create-new-filegroups-for-a-partitioned-table"></a>パーティション テーブルの新しいファイル グループを作成するには  
  
1.  オブジェクト エクスプローラーで、パーティション テーブルを作成するデータベースを右クリックし、 **[プロパティ]** を選択します。  
  
2.  **[データベースのプロパティ -** *database_name]* ダイアログ ボックスの **[ページの選択]** で、 **[ファイル グループ]** を選択します。  
  
3.  **[行]** で、 **[追加]** をクリックします。 新しい行に、ファイル グループ名を入力します。  
  
    > [!WARNING]  
    >  パーティションを作成するときは常に、境界値に指定されたファイル グループの数より 1 つ多い数のファイル グループが必要です。  
  
4.  行の追加を繰り返して、パーティション テーブルのすべてのファイル グループを作成します。  
  
5.  **[OK]** をクリックします。  
  
6.  **[ページの選択]** で、 **[ファイル]** を選択します。  
  
7.  **[行]** で、 **[追加]** をクリックします。 新しい行にファイル名を入力し、ファイル グループを選択します。  
  
8.  行の追加を繰り返して、各ファイル グループに少なくとも 1 つのファイルを作成します。  
  
9. **[テーブル]** フォルダーを展開し、通常と同じようにテーブルを作成します。 詳しくは、「[テーブルの作成 &#40;データベース エンジン&#41;](../../relational-databases/tables/create-tables-database-engine.md)」をご覧ください。 または、次の手順で既存のテーブルを指定することもできます。  
  
#### <a name="to-create-a-partitioned-table"></a>パーティション テーブルを作成するには  
  
1.  パーティション分割するテーブルを右クリックし、 **[ストレージ]** をポイントします。次に、 **[パーティションの作成]** をクリックします。  
  
2.  **パーティションの作成ウィザード**の **[パーティションの作成ウィザードへようこそ]** ページで、 **[次へ]** をクリックします。  
  
3.  **[パーティション分割列の選択]** ページの **[使用可能なパーティション分割列]** グリッドで、テーブルのパーティション分割に使用する列を選択します。 **[使用可能なパーティション分割列]** グリッドには、データのパーティション分割に使用できるデータ型の列だけが表示されます。 計算列をパーティション分割列として選択する場合は、列を PERSISTED として指定する必要があります。  
  
     パーティション分割列とその値の範囲の選択肢は、主に、データをどの程度論理的にグループ化できるかによって決まります。 たとえば、月や四半期に基づいてデータを論理グループに分割することができます。 この論理グループがテーブル パーティションの管理に適しているかどうかは、データに対してどのようなクエリを実行する予定かによって決まります。 すべてのデータ型は、 **text**、 **ntext**、 **image**、 **xml**、 **timestamp**、 **varchar(max)** 、 **nvarchar(max)** 、 **varbinary(max)** 、別名データ型、または CLR ユーザー定義データ型を除いて、列を分割して使用することができます。  
  
     このページで使用できる他のオプションを次に示します。  
  
     **[このテーブルを選択したパーティション テーブルに併置する]**  
     パーティション分割列でこのテーブルと連結する関連データが含まれている、パーティション テーブルを選択できます。 通常、テーブルのパーティションをパーティション分割列で連結すると、クエリの効率が向上します。  
  
     **[一意でないインデックスと一意のインデックスをインデックス付きパーティション列にストレージ固定]**  
     同じパーティション構成でパーティション分割されたテーブルのすべてのインデックスを固定します。 テーブルとインデックスを固定すると、データが同じアルゴリズムでパーティション分割されるため、パーティションをパーティション テーブル内外に効果的に移動できるようになります。  
  
     パーティション分割列とその他のオプションを選択したら、 **[次へ]** をクリックします。  
  
4.  **[パーティション関数の選択]** ページの **[パーティション関数の選択**] で、 **[新しいパーティション関数]** または **[既存のパーティション関数]** をクリックします。 **[新しいパーティション関数]** を選択した場合は、関数の名前を入力します。 **[既存のパーティション関数]** を選択した場合は、使用する関数の名前を一覧から選択します。 データベースに他のパーティション関数がない場合、 **[既存のパーティション関数]** オプションは使用できません。  
  
     このページを完了したら、 **[次へ]** をクリックします。  
  
5.  **[パーティション構成の選択]** ページの **[パーティション構成の選択]** で、 **[新しいパーティション構成]** または **[既存のパーティション構成]** をクリックします。 **[新しいパーティション構成]** を選択した場合は、構成の名前を入力します。 **[既存のパーティション構成]** を選択した場合は、使用する構成の名前を一覧から選択します。 データベースに他のパーティション構成がない場合、 **[既存のパーティション構成]** オプションは使用できません。  
  
     このページを完了したら、 **[次へ]** をクリックします。  
  
6.  **[パーティションのマップ]** ページの **[範囲]** で、 **[左側の境界]** または **[右側の境界]** を選択して、作成する各ファイル グループ内に最大または最小の境界値を含めるかどうかを指定します。 パーティションを作成するときは常に、境界値に指定されたファイル グループの数に 1 つ余分なファイル グループを足した数を入力する必要があります。  
  
     **[ファイル グループを選択して境界値を指定します]** グリッドの **[ファイル グループ]** で、データをパーティション分割するファイル グループを選択します。 **[境界]** で、各ファイル グループの境界値を入力します。 境界値を空にした場合、パーティション関数は、パーティション関数名を使用して、テーブルまたはインデックス全体を単一のパーティションにマップします。  
  
     このページで使用できる他のオプションを次に示します。  
  
     **[境界の設定]**  
     **[境界値の設定]** ダイアログ ボックスを開き、パーティションの境界値と日付範囲を選択します。 このオプションは、 **date**、 **datetime**、 **smalldatetime**、 **datetime2**、または **datetimeoffset**のいずれかのデータ型を含むパーティション分割列を選択した場合にのみ使用できます。  
  
     **[ストレージの推定]**  
     パーティションに指定された各ファイル グループのストレージの行数、必要な領域、および使用できる領域を推定します。 これらの値は、読み取り専用の値としてグリッドに表示されます。  
  
     **[境界値の設定]** ダイアログ ボックスでは、次の追加オプションを設定できます。  
  
     **開始日**  
     パーティションの範囲値の開始日を選択します。  
  
     **終了日**  
     パーティションの範囲値の終了日を選択します。 **[パーティションのマップ]** ページで **[左側の境界]** を選択した場合、この日付は、各ファイル グループまたはパーティションの最後の値になります。 **[パーティションのマップ]** ページで **[右側の境界]** を選択した場合、この日付は、最後から 2 番目のファイル グループの最初の値になります。  
  
     **日付範囲**  
     各パーティションの日付粒度または範囲値の増分を選択します。  
  
     このページを完了したら、 **[次へ]** をクリックします。  
  
7.  **[出力オプションの選択]** ページで、パーティション テーブルを完了する方法を指定します。 ウィザードの前のページに基づいて SQL スクリプトを作成するには、 **[スクリプトの作成]** を選択します。 ウィザードの残りのすべてのページが完了した後に新しいパーティション テーブルを作成するには、 **[すぐに実行する]** を選択します。 事前に定義した時刻に新しいパーティション テーブルを作成するには、 **[スケジュール]** を選択します。  
  
     **[スクリプトの作成]** を選択した場合、 **[スクリプト オプション]** で次のオプションを使用できます。  
  
     **[スクリプトをファイルに保存]**  
     スクリプトを .sql ファイルとして生成します。 **[ファイル名]** ボックスにファイルの名前と場所を入力するか、または **[参照]** をクリックして **[スクリプト ファイルの場所]** ダイアログ ボックスを開きます。 **[名前を付けて保存]** で、 **[Unicode テキスト]** または **[ANSI テキスト]** を選択します。  
  
     **[スクリプトをクリップボードに保存]**  
     スクリプトをクリップボードに保存します。  
  
     **[スクリプトを新しいクエリ ウィンドウに保存]**  
     新しいクエリ エディター ウィンドウにスクリプトを生成します。 これは既定値です。  
  
     **[スケジュール]** を選択した場合は、 **[スケジュールの変更]** をクリックします。  
  
    1.  **[新しいジョブ スケジュール]** ダイアログ ボックスで、 **[名前]** ボックスに、ジョブのスケジュールの名前を入力します。  
  
    2.  **[スケジュールの種類]** ボックスで、スケジュールの種類を選択します。  
  
        -   **[SQL Server エージェントの開始時に自動的に開始]**  
  
        -   **[CPU がアイドル状態になったときに開始]**  
  
        -   **[定期的]** 。 新しいパーティション テーブルを新しい情報で定期的に更新するには、このオプションを選択します。  
  
        -   **[指定日時]** 。 これは既定値です。  
  
    3.  **[有効]** チェック ボックスをオンまたはオフにして、スケジュールを有効または無効にします。  
  
    4.  **[定期的]** を選択した場合:  
  
        1.  **[頻度]** の **[実行]** ボックスの一覧で、実行の頻度を指定します。  
  
            -   **[日単位]** を選択した場合は、 **[間隔]** ボックスに、ジョブ スケジュールを繰り返す頻度を日単位で入力します。  
  
            -   **[週単位]** を選択した場合は、 **[間隔]** ボックスに、ジョブ スケジュールを繰り返す頻度を週単位で入力します。 ジョブ スケジュールを実行する曜日を選択します。  
  
            -   **[月単位]** を選択した場合は、 **[日]** または **[曜日]** を選択します。  
  
                -   **[日]** を選択した場合は、ジョブ スケジュールを実行する日付と、ジョブ スケジュールを繰り返す頻度を月単位で指定します。 たとえば、隔月の 15 日にジョブ スケジュールを実行する場合は、 **[日]** を選択し、1 番目のボックスに「15」と入力し、2 番目のボックスに「2」と入力します。 2 番目のボックスで使用できる最大の値は "99" であることに注意してください。  
  
                -   **[曜日]** を選択した場合は、ジョブ スケジュールを実行する曜日と、ジョブ スケジュールを繰り返す頻度を月単位で指定します。 たとえば、隔月の最後の平日にジョブ スケジュールを実行する場合は、 **[日]** を選択し、リストから **[最終]** を選択します。次に 2 番目のリストから **[平日]** を選択し、最後のボックスに「2」と入力します。 **[第 1]** 、 **[第 2]** 、 **[第 3]** 、または **[第 4]** も、特定の平日 (たとえば、日曜日や水曜日) に加えて、最初の 2 つのリストから選択できます。 最後のボックスで使用できる最大の値は "99" であることに注意してください。  
  
        2.  **[一日のうちの頻度]** で、頻度、ジョブ スケジュールを実行する当日にジョブ スケジュールを繰り返す頻度を指定します。  
  
            -   **[1 回]** を選択した場合は、ジョブ スケジュールを実行する特定の時刻を **[1 回]** ボックスに入力します。 間、分、秒に加え、午前か午後かを入力します。  
  
            -   **[間隔]** を選択した場合は、 **[頻度]** で選択した日にジョブ スケジュールを実行する頻度を指定します。 たとえば、ジョブ スケジュールを実行する当日に 2 時間おきにジョブ スケジュールを実行する場合は、 **[間隔]** を選択し、1 番目のボックスに「2」と入力してから、 **[時間]** を選択します。 このリストでは、 **[分]** と **[秒]** を選択することもできます。 1 番目のボックスで使用できる最大の値は "100" であることに注意してください。  
  
                 **[開始]** ボックスに、ジョブ スケジュールの実行を開始する時刻を入力します。 **[終了]** ボックスに、ジョブ スケジュールの実行を終了する時刻を入力します。 間、分、秒に加え、午前か午後かを入力します。  
  
        3.  **[期間]** で、 **[開始日]** に、ジョブ スケジュールの実行を開始する日付を入力します。 **[終了日]** を選択します。ジョブ スケジュールの実行を停止するタイミングを指定しない場合は、 **[終了日なし]** を選択します。 **[終了日]** を選択した場合は、ジョブ スケジュールの実行を停止する日付を入力します。  
  
    5.  **[指定日時]** を選択した場合は、 **[指定日時に発生]** の **[日付]** ボックスに、ジョブ スケジュールを実行する日付を入力します。 **[時刻]** ボックスに、ジョブ スケジュールを実行する時刻を入力します。 間、分、秒に加え、午前か午後かを入力します。  
  
    6.  **[概要]** の **[説明]** で、すべてのジョブ スケジュール設定が適切であることを確認します。  
  
    7.  **[OK]** をクリックします。  
  
     このページを完了したら、 **[次へ]** をクリックします。  
  
8.  **[概要の確認]** ページの **[選択内容の確認]** で、使用可能なすべてのオプションを展開し、すべてのパーティション設定が適切であることを確認します。 すべての設定が適切であることを確認したら、 **[完了]** をクリックします。  
  
9. **[パーティションの作成ウィザードの進行状況]** ページで、パーティションの作成ウィザードの操作に関する状態情報を監視します。 ウィザードで選択したオプションに応じて、[進行状況] ページに 1 つまたは複数のアクションが含まれる可能性があります。 上部のボックスには、ウィザードの全体的な状態と受信した状態メッセージ、エラー メッセージ、および警告メッセージの数が表示されます。  
  
     **[パーティションの作成ウィザードの進行状況]** ページでは、次のオプションを使用できます。  
  
     **詳細**  
     アクション、状態、およびウィザードで実行したアクションから返されたメッセージが提供されます。  
  
     **操作**  
     各アクションの種類と名前を指定します。  
  
     **ステータス**  
     全体としてウィザードのアクションが **[成功]** または **[失敗]** のいずれの値を返したかを示します。  
  
     **メッセージ**  
     プロセスから返されたすべてのエラー メッセージまたは警告メッセージを提供します。  
  
     **レポート**  
     パーティションの作成ウィザードの結果を含むレポートを作成します。 **[レポートの表示]** 、 **[レポートをファイルに保存]** 、 **[レポートをクリップボードにコピー]** 、 **[レポートを電子メールとして送信]** の各オプションがあります。  
  
     **[レポートの表示]**  
     パーティションの作成ウィザードの進行状況に関するテキスト レポートを表示する **[レポートの表示]** ダイアログ ボックスを開きます。  
  
     **[レポートをファイルに保存]**  
     **[レポートに名前を付けて保存]** ダイアログ ボックスを開きます。  
  
     **[レポートをクリップボードにコピー]**  
     ウィザードの進行状況レポートの結果をクリップボードにコピーします。  
  
     **[レポートを電子メールとして送信]**  
     ウィザードの進行状況レポートの結果を電子メール メッセージにコピーします。  
  
     完了したら、 **[閉じる]** をクリックします。  
  
 パーティションの作成ウィザードによってパーティション関数とパーティション構成が作成され、指定したテーブルにパーティション分割が適用されます。 テーブル パーティション分割を検証するには、オブジェクト エクスプローラーでテーブルを右クリックし、 **[プロパティ]** をクリックします。 **[ストレージ]** ページをクリックします。 このページには、パーティション関数の名前および構成やパーティションの数などの情報が表示されます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-partitioned-table"></a>パーティション テーブルを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、新しいファイル グループ、パーティション関数とパーティション構成を作成します。 パーティション構成を格納場所として指定した新しいテーブルが作成されます。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Adds four new filegroups to the AdventureWorks2012 database  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test1fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test2fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test3fg;  
    GO  
    ALTER DATABASE AdventureWorks2012  
    ADD FILEGROUP test4fg;   
  
    -- Adds one file for each filegroup.  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test1dat1,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t1dat1.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test1fg;  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test2dat2,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t2dat2.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test2fg;  
    GO  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test3dat3,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t3dat3.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test3fg;  
    GO  
    ALTER DATABASE AdventureWorks2012   
    ADD FILE   
    (  
        NAME = test4dat4,  
        FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\t4dat4.ndf',  
        SIZE = 5MB,  
        MAXSIZE = 100MB,  
        FILEGROWTH = 5MB  
    )  
    TO FILEGROUP test4fg;  
    GO  
    -- Creates a partition function called myRangePF1 that will partition a table into four partitions  
    CREATE PARTITION FUNCTION myRangePF1 (int)  
        AS RANGE LEFT FOR VALUES (1, 100, 1000) ;  
    GO  
    -- Creates a partition scheme called myRangePS1 that applies myRangePF1 to the four filegroups created above  
    CREATE PARTITION SCHEME myRangePS1  
        AS PARTITION myRangePF1  
        TO (test1fg, test2fg, test3fg, test4fg) ;  
    GO  
    -- Creates a partitioned table called PartitionTable that uses myRangePS1 to partition col1  
    CREATE TABLE PartitionTable (col1 int PRIMARY KEY, col2 char(10))  
        ON myRangePS1 (col1) ;  
    GO  
    ```  
  
#### <a name="to-determine-if-a-table-is-partitioned"></a>テーブルがパーティション分割されているかどうかを調べるには  
  
1.  次のクエリでは、テーブル `PartitionTable` がパーティション分割されている場合、1 つ以上の行が返されます。 テーブルがパーティション分割されていない場合は、行が返されません。  
  
    ```  
    SELECT *   
    FROM sys.tables AS t   
    JOIN sys.indexes AS i   
        ON t.[object_id] = i.[object_id]   
        AND i.[type] IN (0,1)   
    JOIN sys.partition_schemes ps   
        ON i.data_space_id = ps.data_space_id   
    WHERE t.name = 'PartitionTable';   
    GO  
    ```  
  
#### <a name="to-determine-the-boundary-values-for-a-partitioned-table"></a>パーティション テーブルの境界値を調べるには  
  
1.  次のクエリでは、 `PartitionTable` テーブルの各パーティションの境界値を返します。  
  
    ```  
    SELECT t.name AS TableName, i.name AS IndexName, p.partition_number, p.partition_id, i.data_space_id, f.function_id, f.type_desc, r.boundary_id, r.value AS BoundaryValue   
    FROM sys.tables AS t  
    JOIN sys.indexes AS i  
        ON t.object_id = i.object_id  
    JOIN sys.partitions AS p  
        ON i.object_id = p.object_id AND i.index_id = p.index_id   
    JOIN  sys.partition_schemes AS s   
        ON i.data_space_id = s.data_space_id  
    JOIN sys.partition_functions AS f   
        ON s.function_id = f.function_id  
    LEFT JOIN sys.partition_range_values AS r   
        ON f.function_id = r.function_id and r.boundary_id = p.partition_number  
    WHERE t.name = 'PartitionTable' AND i.type <= 1  
    ORDER BY p.partition_number;  
    ```  
  
#### <a name="to-determine-the-partition-column-for-a-partitioned-table"></a>パーティション テーブルのパーティション列を調べるには  
  
1.  次のクエリでは、テーブルのパーティション分割列の名前を返します。 `PartitionTable`を使用して、パーティション テーブルまたはパーティション インデックスを作成できます。  
  
    ```  
    SELECT   
        t.[object_id] AS ObjectID   
        , t.name AS TableName   
        , ic.column_id AS PartitioningColumnID   
        , c.name AS PartitioningColumnName   
    FROM sys.tables AS t   
    JOIN sys.indexes AS i   
        ON t.[object_id] = i.[object_id]   
        AND i.[type] <= 1 -- clustered index or a heap   
    JOIN sys.partition_schemes AS ps   
        ON ps.data_space_id = i.data_space_id   
    JOIN sys.index_columns AS ic   
        ON ic.[object_id] = i.[object_id]   
        AND ic.index_id = i.index_id   
        AND ic.partition_ordinal >= 1 -- because 0 = non-partitioning column   
    JOIN sys.columns AS c   
        ON t.[object_id] = c.[object_id]   
        AND ic.column_id = c.column_id   
    WHERE t.name = 'PartitionTable' ;   
    GO  
    ```  
  
 詳細については、以下をご覧ください。  
  
-   [ALTER DATABASE の File および Filegroup オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
  
-   [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)  
  
-   [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)  
  
-   [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
  
  
