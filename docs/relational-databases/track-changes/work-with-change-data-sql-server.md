---
title: 変更データの処理
ms.custom: seo-dt-2019
ms.date: 01/02/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data [SQL Server]
- change data capture [SQL Server], query function scenarios
- change data capture [SQL Server], LSN boundaries
- change data capture [SQL Server], query functions
ms.assetid: 5346b852-1af8-4080-b278-12efb9b735eb
author: rothja
ms.author: jroth
ms.openlocfilehash: f68227bb3f88996ee8a4f5ea60c9cdd88f4f765a
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095403"
---
# <a name="work-with-change-data-sql-server"></a>変更データの処理 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
  変更データ キャプチャのコンシューマーは、テーブル値関数 (TVF) を使用することによって変更データを利用できるようになります。 これらの関数のすべてのクエリには、ログ シーケンス番号 (LSN) の範囲を定義する 2 つのパラメーターが必要です。これらのパラメーターは、返される結果セットを開発する際に検討の対象になります。 期間の両端を示す LSN の上限値と下限値は、期間内に含まれると見なされます。  
  
 TVF のクエリで使用する適切な LSN 値を特定するための関数がいくつか用意されています。 [sys.fn_cdc_get_min_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md) 関数は、キャプチャ インスタンスの有効期間に関連付けられた最小の LSN を返します。 この有効期間は、現在キャプチャ インスタンスが変更データを利用できる期間です。 [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) 関数は、有効期間内の最大の LSN を返します。 [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) 関数と [sys.fn_cdc_map_lsn_to_time](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md) 関数は、LSN 値を従来のタイムラインに配置する場合に使用できます。 変更データ キャプチャでは両端の値を含む閉区間のクエリ範囲が使用されるため、連続したクエリ ウィンドウで変更が重複しないようにするためにシーケンス内の次の LSN 値を生成することが必要になる場合があります。 [sys.fn_cdc_increment_lsn](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md) 関数と [sys.fn_cdc_decrement_lsn](../../relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql.md) 関数は、LSN 値の増分の調整が必要な場合に役立ちます。  
  
##  <a name="LSN"></a> LSN の下限と上限の検証  
 TVF クエリで使用する LSN の下限と上限は、使用前に検証することをお勧めします。 下限または上限が Null の場合やキャプチャ インスタンスの有効期間から外れている場合、変更データ キャプチャの TVF からエラーが返されます。  
  
 たとえば、すべての変更のクエリで、クエリ範囲の定義に使用されたパラメーターが無効または範囲外である場合や、行フィルター オプションが無効である場合は、次のエラーが返されます。  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_all_changes_ ...`  
  
 **net changes** のクエリに対して返される対応するエラーは次のとおりです。  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_net_changes_ ...`  
  
> [!NOTE]  
>  メッセージ 313 のメッセージは誤解を招き、エラーの実際の原因を伝えていないことが確認されています。 このメッセージが不適切に使用されている原因は、TVF 内から明示的なエラーを返せないことから生じています。 ただし、不正確ではあっても認識可能なエラーを返す方が、空の結果セットを返すよりは役立つと考えられます。 空の結果セットでは、有効なクエリが変更を返さなかった場合と区別できないためです。  
  
 すべての変更のクエリを実行したときに承認エラーが発生した場合は、次のような情報が返されます。  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object 'fn_cdc_get_all_changes_...', database 'MyDB', schema 'cdc'.`  
  
 これは、差分変更のクエリを実行した場合も同じです。  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object fn_cdc_get_net_changes_...', database 'MyDB', schema 'cdc'.`  
  
 これらの既知の TVF エラーを受け取り、そのエラーに関する有益情報を返す例については、"TRY CATCH を使用した差分変更の列挙" テンプレートを参照してください。  
  
> [!NOTE]  
>  SQL Server Management Studio で変更データ キャプチャ テンプレートを見つけるには、 **[表示]** メニューの **[テンプレート エクスプローラー]** をクリックし、 **[SQL Server テンプレート]** を展開し、 **[変更データ キャプチャ]** フォルダーを展開します。  
  
##  <a name="Functions"></a> クエリ関数  
 追跡されているソース テーブルの特性とそのキャプチャ インスタンスの構成方法に応じて、変更データのクエリのための TVF が 1 つまたは 2 つ生成されます。  
  
-   [cdc.fn_cdc_get_all_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) 関数は、指定した期間に発生したすべての変更を返します。 この関数は常に生成されます。 エントリは、必ず並べ替えて返されます。まず変更のトランザクション コミット LSN で並べ替えられ、次にそのトランザクション内の変更のシーケンス値で並べ替えられます。 選択した行フィルター オプションに応じて、更新について最後の行が返される (行フィルター オプションが "all" の場合) か、新しい値と古い値の両方が返されます (行フィルター オプションが "all update old" の場合)。  
  
-   [cdc.fn_cdc_get_net_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) 関数は、ソース テーブルが有効である場合に @supports_net_changes パラメーターが 1 に設定されていると生成されます。  
  
    > [!NOTE]  
    >  このオプションは、ソース テーブルで主キーが定義されている場合、または @index_name パラメーターを使用して一意のインデックスが特定されている場合にのみサポートされます。  
  
     **netchanges** 関数は、ソース テーブルの変更された各行につき 1 つの変更を返します。 指定した期間に複数の変更が行に対して記録されていた場合は、列の値には行の最終的な内容が反映されます。 ターゲット環境の更新に必要な操作を正しく特定するには、その期間に行に対して行われた最初の操作と最後の操作の両方を TVF で考慮する必要があります。 行フィルター オプション 'all' を指定した場合、 **net changes** のクエリで返される操作は、挿入、削除、または更新 (新しい値) になります。 このオプションでは、更新マスクは常に null として返されます。これは、集計マスクの計算に関連するコストのためです。 行に対するすべての変更が反映された集計マスクが必要な場合は、'all with mask' オプションを使用します。 下流の処理で挿入と更新を区別する必要がない場合は、"all with merge" オプションを使用します。 この場合、操作の値に指定される値は 2 つのみです。削除を表す 1 と、挿入または更新の操作を表す 5 です。 このオプションを使用すると、挿入と更新のどちらの操作を派生させるかを特定する追加処理が不要になるので、この区別が不要な場合にクエリのパフォーマンスが向上します。  
  
 クエリ関数から返される更新マスクは、変更データの行で変更されたすべての列を特定できるように簡潔に表現したものです。 通常、この情報が必要とされるのは、キャプチャ対象列の小さなサブセットを使用する場合のみです。 アプリケーションでより直接的に使用できる形式の情報をこのマスクから抽出するための関数も用意されています。 [sys.fn_cdc_get_column_ordinal](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md) 関数は、特定のキャプチャ インスタンスの指定した列の位置を表す序数を返します。一方、 [sys.fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md) 関数は、関数呼び出しで指定した序数に基づいて、指定したマスクのビットのパリティを返します。 この 2 つの関数により、更新マスクから情報を効率的に抽出し、変更データの要求と共に返すことができます。 これらの関数の使用例については、"All With Mask を使用した差分変更の列挙" テンプレートを参照してください。  
  
##  <a name="Scenarios"></a> クエリ関数のシナリオ  
 以降のセクションでは、クエリ関数の cdc.fn_cdc_get_all_changes_<capture_instance> および cdc.fn_cdc_get_net_changes_<capture_instance> を使用して変更データ キャプチャ データのクエリを実行するための一般的なシナリオについて説明します。  
  
### <a name="querying-for-all-changes-within-the-capture-instance-validity-interval"></a>キャプチャ インスタンスの有効期間内のすべての変更のクエリ  
 変更データに対する最も単純な要求は、キャプチャ インスタンスの有効期間内の現在の変更データをすべて返す要求です。 このクエリを実行するには、まず、有効期間の LSN の下限と上限を求めます。 次に、それらの値を使用して、クエリ関数 cdc.fn_cdc_get_all_changes_<capture_instance> または cdc.fn_cdc_get_net_changes_<capture_instance> に渡すパラメーター @from_lsn および @to_lsn を特定します。 下限を取得するには [sys.fn_cdc_get_min_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md) 関数を使用し、上限を取得するには [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) 関数を使用します。 クエリ関数 cdc.fn_cdc_get_all_changes_<capture_instance> を使用して現在のすべての有効な変更のクエリを実行するためのサンプル コードについては、"有効な範囲のすべての変更の列挙" テンプレートを参照してください。 cdc.fn_cdc_get_net_changes_<capture_instance> 関数を使用した類似の例については、"有効な範囲の差分変更の列挙" テンプレートを参照してください。  
  
### <a name="querying-for-all-new-changes-since-the-last-set-of-changes"></a>前回の変更セット以降に発生したすべての新しい変更のクエリ  
 一般的なアプリケーションの場合、変更データのクエリは継続的なプロセスであり、前回の要求以降に発生したすべての変更の要求が定期的に行われます。 そのようなクエリでは、 [sys.fn_cdc_increment_lsn](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md) 関数を使用して、前回のクエリの上限から現在のクエリの下限を求めることができます。 この方法では、クエリ範囲が常に両端の値を含む閉区間として扱われるため、行の重複が起こらないことが保証されます。 次に、 [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) 関数を使用して、新しい要求期間の上限を取得します。 クエリ期間を体系的に移動させて前回の要求以降に発生したすべての変更を取得するためのサンプル コードについては、"前回の要求以降に発生したすべての変更の列挙" テンプレートを参照してください。  
  
### <a name="querying-for-all-new-changes-up-until-now"></a>現在までのすべての新しい変更のクエリ  
 クエリ関数から返される変更に対しては、前回の要求から現在の日時までの間に発生した変更のみを含める制約がよく適用されます。 この場合はまず、前回の要求で使用された @from_lsn 値に sys.fn_cdc_increment_lsn 関数を適用して下限を求めます。 期間の上限は特定の時点として表されるため、クエリ関数で使用するには先に LSN 値に変換する必要があります。 datetime 値を対応する LSN 値に変換するには、まず、指定した上限までの間にコミットされたすべての変更が既にキャプチャ プロセスによって処理されていることを確認する必要があります。 この確認は、該当するすべての変更が変更テーブルに反映されているようにするために必要です。 これを確認するには、wait ループを構成して、任意のデータベース変更テーブルに記録されたコミット LSN の現在の最大値が目的の要求期間の終了時間を超えているかどうかを定期的に確認する方法があります。  
  
 関連するすべてのログ エントリが既にキャプチャ プロセスによって処理されていることを遅延ループで確認したら、 [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) 関数を使用して、LSN 値として表された新しい上限を求めます。 指定した時刻までの間にコミットされたエントリがすべて取得されるようにするには、sys.fn_cdc_map_time_to_lsn 関数を呼び出してオプション 'largest less than or equal' を使用します。  
  
> [!NOTE]  
>  変更が発生していない期間には、cdc.lsn_time_mapping テーブルにダミー エントリが追加されて、特定のコミット時間までの変更が既にキャプチャ プロセスによって処理されていることが示されます。 これは、処理する新しい変更がない場合にキャプチャ プロセスの処理が遅れているように見えるのを防ぐためです。  
  
 "現在までのすべての変更の列挙" テンプレートは、上の方法を使用して変更データのクエリを実行する方法を示しています。  
  
### <a name="adding-a-commit-time-to-an-all-changes-result-set"></a>すべての変更結果セットへのコミット時間の追加  
 データベース変更テーブルの各エントリに対応するトランザクションのコミット時間は、 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)テーブルから取得できます。 すべての変更の要求で返された __$start_lsn 値を cdc.lsn_time_mapping テーブルのエントリの start_lsn 値と結合することにより、変更データと共に tran_end_time を返して、ソースにおけるトランザクションのコミット時間を使用して変更にタイム スタンプを付けることができます。 "すべての変更結果セットへのコミット時間の添付" テンプレートは、この結合の実行方法を示しています。  
  
### <a name="joining-change-data-with-other-data-from-the-same-transaction"></a>同じトランザクションの他のデータと変更データとの結合  
 変更データを、トランザクションがソースでコミットされたときに収集されたその他の情報と結合すると便利な場合があります。 cdc.lsn_time_mapping テーブルの tran_begin_lsn 列には、そのような結合を実行するために必要な情報が含まれています。 ソースの更新が発生したら、システム動的ビュー [sys.dm_tran_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md) の database_transaction_begin_lsn の値を、変更データと結合するその他の情報と共に保存する必要があります。 その後、fn_convertnumericlsntobinary 関数を使用して、database_transaction_begin_lsn の値と tran_begin_lsn の値を比較します。 この関数を作成するためのコードは、"fn_convertnumericlsntobinary 関数の作成" テンプレートに含まれています。 "特定の tran_begin_lsn を持つすべての変更の取得" テンプレートは、この結合の実行方法を示しています。  
  
### <a name="querying-using-datetime-wrapper-functions"></a>datetime ラッパー関数を使用したクエリ  
 変更データのクエリの一般的なアプリケーション シナリオの 1 つに、datetime 値で範囲指定されたスライディング ウィンドウを使用して変更データを定期的に要求するというものがあります。 この種のコンシューマーのために、ストアド プロシージャ [sys.sp_cdc_generate_wrapper_function](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md) が用意されています。このストアド プロシージャは、変更データ キャプチャ クエリ関数のカスタム ラッパー関数を作成するためのスクリプトを生成します。 これらのカスタム ラッパーを使用すると、クエリ範囲を datetime のペアとして表すことができます。  
  
 このストアド プロシージャでは、呼び出しオプションを使用することにより、呼び出し元がアクセスできるすべてのキャプチャ インスタンスに対してラッパーを生成することも、指定したキャプチャ インスタンスに対してのみ生成することもできます。 そのほか、キャプチャ間隔の上限が開いているか閉じているかを指定したり、使用可能なキャプチャ対象列のうちのどれを結果セットに含めるかを指定したり、結果セットに含める列のうちのどれに更新フラグを関連付けるかを指定したりすることもできます。 このプロシージャが返す結果セットには 2 つの列があります。1 つは、生成される関数の名前 (キャプチャ インスタンス名から派生する名前)、もう 1 つは、ラッパー ストアド プロシージャの作成ステートメントです。 すべての変更クエリをラップする関数は常に生成されます。 キャプチャ インスタンスの作成時に @supports_net_changes パラメーターが設定されていた場合は、差分変更追跡の関数をラップする関数も生成されます。  
  
 スクリプト生成ストアド プロシージャを呼び出してラッパー ストアド プロシージャの作成ステートメントを生成し、その結果の作成スクリプトを実行して関数を作成するのは、アプリケーション デザイナーの仕事です。 キャプチャ インスタンスの作成時に自動的には行われません。  
  
 datetime ラッパーはユーザーが所有します。呼び出し元の既定のスキーマには作成されません。 生成される関数はほとんどのユーザーがそのまま使用できますが、 関数を作成する前に、生成されたスクリプトをさらにカスタマイズすることもできます。  
  
 すべての変更クエリをラップする関数の名前は、fn_all_changes_ の後にキャプチャ インスタンスの名前を付けた名前になります。 差分変更追跡のラッパーに使用されるプレフィックスは fn_net_changes です。 どちらの関数も、関連する変更データ キャプチャ TVF と同じように 3 つの引数を受け取ります。 ただし、ラッパーのクエリ範囲は、2 つの LSN 値ではなく 2 つの datetime 値で範囲指定されます。 @row_filter_option パラメーターはどちらの場合も同じです。  
  
 生成されるラッパー関数は、変更データ キャプチャ タイムラインを体系的に進めるための規則をサポートしているため、前の期間の @end_time パラメーターは、次の期間の @start_time パラメーターとして使用されるものと見なされます。 またラッパー関数は、datetime 値を LSN 値にマップし、この規則に従った場合にデータの欠落や重複が発生しないようにします。  
  
 ラッパーは、指定のクエリ期間で閉じた上限をサポートするように生成することも、開いた上限をサポートするように生成することもできます。 つまり、抽出期間の上限とコミット時間が等しいエントリを、その期間に含めるかどうかを呼び出し元が指定できます。 既定では、上限が含まれます。  
  
 生成されるクエリ TVF では、@from_lsn 値または @to_lsn 値に NULL 値を渡すと失敗しますが、datetime ラッパー関数では、NULL を使用すると現在のすべての変更を取得できます。 つまり、datetime ラッパーにクエリ期間の下限として NULL を渡すと、クエリ TVF に適用される基になる SELECT ステートメントでキャプチャ インスタンスの有効期間の下限が使用されます。 同様に、クエリ期間の上限として NULL を渡すと、クエリ TVF に適用される SELECT ステートメントでキャプチャ インスタンスの有効期間の上限が使用されます。  
  
 ラッパー関数から返される結果セットには、要求したすべての列と、それに続いて、行に関連付けられている操作を示す 1 つまたは 2 つの文字として記録される操作列が含まれます。 更新フラグを要求した場合は、操作コードの後に、@update_flag_list パラメーターで指定した順にビット列として表示されます。 生成される datetime ラッパーをカスタマイズするための呼び出しオプションについては、「[sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)」を参照してください。  
  
 "更新フラグを含むラッパー TVF のインスタンス化" テンプレートは、生成されるラッパー関数をカスタマイズして、差分変更のクエリから返される結果セットに指定した列の更新フラグを追加する方法を示しています。 "スキーマの CDC ラッパー TVF のインスタンス化" テンプレートは、特定のデータベース スキーマのソース テーブルに対して作成されたすべてのキャプチャ インスタンスのクエリ TVF の datetime ラッパーをインスタンス化する方法を示しています。  
  
 datetime ラッパーを使用して変更データのクエリを実行する例については、"更新フラグを含むラッパーを使用した差分変更の取得" テンプレートを参照してください。 このテンプレートは、更新フラグを返すように構成されたラッパー関数を使用して差分変更のクエリを実行する方法を示しています。 基になるクエリ関数で更新時に NULL でない更新マスクを返すには、行フィルター オプション "all with mask" を使用する必要があります。 datetime の期間の下限と上限の両方に対して NULL 値を渡して、基になる LSN に基づくクエリの実行時にキャプチャ インスタンスの有効期間の下限と上限が使用されるようにします。 このクエリでは、キャプチャ インスタンスの有効期間内に発生したソース行の各変更ごとに 1 行のデータが返されます。  
  
### <a name="using-the-datetime-wrapper-functions-to-transition-between-capture-instances"></a>datetime ラッパー関数を使用したキャプチャ インスタンスの切り替え  
 変更データ キャプチャでは、追跡するソース テーブル 1 つに対してキャプチャ インスタンスを 2 つまで使用できます。 この機能は主に、ソース テーブルに対するデータ定義言語 (DDL) の変更によって追跡可能な列が増えた場合に、キャプチャ インスタンスを切り替えることができるようにするために使用されます。 新しいキャプチャ インスタンスに切り替える際に、基になるクエリ関数の名前の変更から上のアプリケーション レベルを保護するには、基になる呼び出しをラッパー関数でラップして、 ラッパー関数の名前が元の名前と同じになるようにする方法があります。 インスタンスの切り替えが行われるときに、古いラッパー関数を削除して、新しいクエリ関数を参照する同じ名前の新しいラッパー関数を作成できます。 生成されるスクリプトを事前に変更して同じ名前のラッパー関数が作成されるようにすることで、上のアプリケーション層に影響を与えずに新しいキャプチャ インスタンスに切り替えることができます。  
  
## <a name="see-also"></a>参照  
 [データ変更の追跡 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [変更データ キャプチャの有効化と無効化 &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)   
 [変更データ キャプチャの管理と監視 &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
