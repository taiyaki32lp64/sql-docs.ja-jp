---
title: SQLdiag ユーティリティ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server], SQLdiag
- stopping diagnostic collection
- storing diagnostic information
- performance [SQL Server], diagnostic collection
- diagnostic records [SQL Server]
- scripts [SQL Server], diagnostic collection
- logs [SQL Server], diagnostic collection
- starting diagnostic collection
- clustered instance of SQL Server
- monitoring performance [SQL Server], diagnostic collection
- security [SQL Server], diagnostic collection
- SQLDIAG service
- space [SQL Server], diagnostic collection
- SQLdiag utility
- disk space [SQL Server], diagnostic collection
- configuration files [SQL Server]
- automatic diagnostic collection
- clusters [SQL Server], diagnostic collection
ms.assetid: 45ba1307-33d1-431e-872c-a6e4556f5ff2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7eadacbf0e3137cf22c9a870783da41a046c86fb
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251368"
---
# <a name="sqldiag-utility"></a>SQLdiag ユーティリティ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SQLdiag** ユーティリティは、コンソール アプリケーションまたはサービスとして実行できる汎用的な診断収集ユーティリティです。 **SQLdiag** を使用すると、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] やその他の種類のサーバーからログ ファイルやデータ ファイルを収集したり、サーバーを一定期間にわたって監視したり、サーバーに関する特定の問題をトラブルシューティングしたりすることができます。 **SQLdiag** は、 [!INCLUDE[msCoName](../includes/msconame-md.md)] カスタマー サポート サービスによる診断情報収集の高速化と簡素化も目的としています。  
  
> [!NOTE]  
>  ユーティリティは変更できますが、そのコマンド ライン引数や動作に依存するアプリケーションやスクリプトは今後のリリースで正常に機能しない場合があります。  
  
 **SQLdiag** が収集できる診断情報の種類は次のとおりです。  
  
-   Windows パフォーマンス ログ  
  
-   Windows イベント ログ  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] トレース  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のブロッキング情報  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の構成情報  
  
 構成ファイル SQLDiag.xml を編集することで、 **SQLdiag** が収集する情報の種類を指定することができます。これについては、次のセクションで説明します。  
  
## <a name="syntax"></a>構文  
  
```  
  
sqldiag   
     { [/?] }  
     |  
     { [/I configuration_file]  
       [/O output_folder_path]  
       [/P support_folder_path]  
       [/N output_folder_management_option]  
       [/M machine1 [ machine2 machineN]| @machinelistfile]  
       [/C file_compression_type]  
       [/B [+]start_time]  
       [/E [+]stop_time]  
       [/A SQLdiag_application_name]  
       [/T { tcp [ ,port ] | np | lpc } ]  
       [/Q] [/G] [/R] [/U] [/L] [/X] }  
     |  
     { [START | STOP | STOP_ABORT] }  
     |  
     { [START | STOP | STOP_ABORT] /A SQLdiag_application_name }  
```  
  
## <a name="arguments"></a>引数  
 **/?**  
 使用方法についての情報を表示します。  
  
 **/I** _configuration_file_  
 **SQLdiag** が使用する構成ファイルを設定します。 既定では、 **/I** は SQLDiag.Xml に設定されます。  
  
 **/O** _output_folder_path_  
 **SQLdiag** 出力を、指定されたフォルダーにリダイレクトします。 **/O** オプションが指定されない場合、 **SQLdiag** 出力は、 **SQLdiag** スタートアップ フォルダーの下にある SQLDIAG という名前のサブフォルダーに書き込まれます。 SQLDIAG フォルダーが存在しない場合、 **SQLdiag** によって作成されます。  
  
> [!NOTE]  
>  出力フォルダーの場所は、 **/P**で指定できるサポート フォルダーの場所に応じて決まります。 まったく別の場所に出力フォルダーを設定するには、 **/O**に完全なディレクトリ パスを指定します。  
  
 **/P** _support_folder_path_  
 サポート フォルダーのパスを設定します。 既定では、 **/P** は **SQLdiag** 実行可能ファイルが存在するフォルダーに設定されます。 サポート フォルダーには、XML 構成ファイル、Transact-SQL スクリプト、診断情報の収集中にユーティリティが使用するその他のファイルなどの **SQLdiag** サポート ファイルが格納されています。 このオプションを使用して、別のサポート ファイルのパスを指定すると、 **SQLdiag** は指定されたフォルダーに必要なサポート ファイルが存在しない場合、それらのファイルを指定されたフォルダーへ自動的にコピーします。  
  
> [!NOTE]  
>  現在のフォルダーをサポート ファイルのパスとして設定するには、コマンド ラインの **%cd%** を次のように指定します。  
>   
>  **SQLDIAG /P %cd%**  
  
 **/N** _output_folder_management_option_  
 起動時に **SQLdiag** が出力フォルダーを上書きまたは名前を変更するかどうかを設定します。 使用できるオプションは次のとおりです。  
  
 1 = 出力フォルダーを上書きします (既定)。  
  
 2 = **SQLdiag** が起動したときに、SQLDIAG_00001、SQLDIAG_00002 のように、出力フォルダー名を変更します。 現在の出力フォルダーの名前が変更された後に、 **SQLdiag** によって、既定の出力フォルダー SQLDIAG に出力が書き込まれます。  
  
> [!NOTE]  
>  **SQLdiag** は起動時に、現在の出力フォルダーに出力を追加しません。 既定の出力フォルダーを上書きするか (オプション 1)、または既定のフォルダー名を変更して (オプション 2)、SQLDIAG という名前の新しい既定の出力フォルダーに出力を書き込むかのどちらかです。  
  
 **/M** _machine1_ [ *machine2* *machineN*] | *\@machinelistfile*  
 構成ファイルで指定されたコンピューターをオーバーライドします。 既定では、構成ファイルは SQLDiag.Xml です。または **/I** パラメーターで設定されます。 複数のコンピューターを指定する場合、それぞれのコンピューター名をスペースで区切ります。  
  
 *\@machinelistfile* を使用すると、構成ファイルに保存するコンピューター一覧のファイル名が指定されます。  
  
 **/C** _file_compression_type_  
 **SQLdiag** 出力フォルダー ファイルで使用されるファイル圧縮の種類を設定します。 使用できるオプションは次のとおりです。  
  
 0 = なし (既定)。  
  
 1 = NTFS 圧縮を使用します。  
  
 **/B** [ **+** ]*start_time*  
 診断データの収集を開始する日時は、  
  
 YYYYMMDD_HH:MM:SS の形式で指定します。  
  
 時間は 24 時間形式で指定します。 たとえば、午後 2:00 は は、 **14:00:00**と指定する必要があります。  
  
 現在の日時に対する相対時間を指定するには、日付を使用せず、HH:MM:SS の形式を使用して時間数を示し、 **+** を先頭に付加します。 たとえば、 **/B +02:00:00**と指定すると、 **SQLdiag** は情報収集を開始するまで 2 時間待機します。  
  
 **+** と指定した *start_time*との間には空白を挿入しないでください。  
  
 過去の時間を開始時間に指定すると、 **SQLdiag** は開始日を未来の開始日時に強制的に変更します。 たとえば、 **/B 01:00:00** を指定していて、現在の時間が 08:00:00 の場合、 **SQLdiag** はこの開始日を翌日の開始日に強制的に変更します。  
  
 **SQLdiag** は、ユーティリティが実行されているコンピューター上のローカル時間を使用することに注意してください。  
  
 **/E** [ **+** ]*stop_time*  
 診断データの収集を停止する日時は、  
  
 YYYYMMDD_HH:MM:SS の形式で指定します。  
  
 時間は 24 時間形式で指定します。 たとえば、午後 2:00 は は、 **14:00:00**と指定する必要があります。  
  
 現在の日時に対する相対時間を指定するには、日付を使用せず、HH:MM:SS の形式を使用して時間数を示し、 **+** を先頭に付加します。 たとえば、 **/B +02:00:00 /E +03:00:00**を使用して開始時間と終了時間を指定すると、情報の収集を開始する前に **SQLdiag** は 2 時間待機し、それから情報の収集を 3 時間行い、停止して終了します。 **/B** が指定されない場合、 **SQLdiag** はすぐに診断情報の収集を開始し、 **/E**で指定された日時に終了します。  
  
 **+** と指定した *start_time* または *end_time*との間には空白を挿入しないでください。  
  
 **SQLdiag** は、ユーティリティが実行されているコンピューター上のローカル時間を使用することに注意してください。  
  
 **/A**  _SQLdiag_application_name_  
 **SQLdiag** ユーティリティの複数のインスタンスの実行を、同一の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスに対して有効にします。  
  
 各 *SQLdiag_application_name* は、異なるインスタンスの **SQLdiag**を特定します。 *SQLdiag_application_name* インスタンスの名前と [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスの名前には関連性はありません。  
  
 *SQLdiag_application_name* を使用すると、 **SQLdiag** サービスの特定のインスタンスを開始または停止できます。  
  
 例:  
  
 **SQLDIAG START /A**  _SQLdiag_application_name_  
  
 **/R** オプションと共に使用し、 **SQLdiag** の特定のインスタンスをサービスとして登録することもできます。 例:  
  
 **SQLDIAG /R /A** _SQLdiag_application_name_  
  
> [!NOTE]  
>  **SQLdiag** は *SQLdiag_application_name*に指定されたインスタンス名に、自動的にプレフィックスの DIAG$ を付けます。 これにより、 **SQLdiag** をサービスとして登録する場合に、わかりやすいサービス名になります。  
  
 /T { tcp [ ,*port* ] | np | lpc }  
 指定されたプロトコルを使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスに接続します。  
  
 tcp [,*port*]  
 伝送制御プロトコル/インターネット プロトコル (TCP/IP)。 必要に応じて接続のポート番号を指定することができます。  
  
 np  
 名前付きパイプ。 既定で、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の既定のインスタンスは、名前付きインスタンスの名前付きパイプ `\\.\pipe\sql\query` および `\\.\pipe\MSSQL$<instancename>\sql\query` でリッスンします。 代替パイプの名前を使用して、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスに接続することはできません。  
  
 lpc  
 ローカル プロシージャ コールです。 クライアントが、同じコンピューター上で [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスに接続している場合は、この共有メモリ プロトコルを使用できます。  
  
 **/Q**  
 **SQLdiag** を非表示モードで実行します。 **/Q** を使用すると、パスワード プロンプトなど、すべてのプロンプトが表示されなくなります。  
  
 **/G**  
 **SQLdiag** を汎用モードで実行します。 **/G** が指定されていると、 **SQLdiag** はスタートアップ時に、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の接続チェックやユーザーが **sysadmin** 固定サーバー ロールのメンバーであることの確認を行いません。 その代わり、 **SQLdiag** は、要求された各診断情報を収集するための適切な権限をユーザーが持っているかどうかの判断を Windows にゆだねます。  
  
 **/G** が指定されていない場合、 **SQLdiag** は、ユーザーが Windows の **Administrators** グループのメンバーかどうかを判断するためのチェックを行い、ユーザーが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Administrators **グループのメンバーではない場合は** の診断情報を収集しません。  
  
 **/R**  
 **SQLdiag** をサービスとして登録します。 **SQLdiag** をサービスとして登録する場合に指定されるコマンド ライン引数は、後でサービスを実行するときのために維持されます。  
  
 **SQLdiag** がサービスとして登録されると、既定のサービス名は SQLDIAG となります。 既定のサービス名は **/A** 引数を使用して変更できます。  
  
 サービスを開始するには、次のとおり **START** コマンド ライン引数を使用します。  
  
 **SQLDIAG START**  
  
 **net start** コマンドを次のように使用してサービスを開始することもできます。  
  
 **net  start SQLDIAG**  
  
 **/U**  
 **SQLdiag** のサービスとしての登録を解除します。  
  
 **/A** 引数を使用して、名前付きの **SQLdiag** インスタンスの登録を解除することもできます。  
  
 **/L**  
 **/B** 引数または **/E** 引数それぞれに、開始時刻または終了時刻も指定されている場合に、 **SQLdiag** を連続モードで実行します。 **SQLdiag** は、定期的なシャットダウンによって診断情報の収集が停止した場合、自動的に再起動されます。 たとえば、 **/E** 引数または **/X** 引数で使用されます。  
  
> [!NOTE]  
>  **SQLdiag** は、 **/B** および **/E** コマンド ライン引数を使用して、開始時刻または終了時刻が指定されていない場合には、 **/L** 引数を無視します。  
  
 **/L** を使用しても、暗黙にサービス モードになることはありません。 **SQLdiag** をサービスとして実行するときに **/L** を使用する場合は、サービスの登録時にコマンド ラインで指定します。  
  
 **/X**  
 **SQLdiag** をスナップショット モードで実行します。 **SQLdiag** は、構成したすべての診断情報のスナップショットを作成してから、自動的にシャットダウンします。  
  
 **START** | **STOP** | **STOP_ABORT**  
 **SQLdiag** サービスを開始または停止します。 **STOP_ABORT** は、現在実行されている診断収集が終了していなくても、できるだけ早く強制的にサービスをシャットダウンします。  
  
 このサービス コントロール引数は、コマンド ラインで使用される最初の引数であることが必要です。 例:  
  
 **SQLDIAG START**  
  
 **START** 、 **STOP**、または **STOP_ABORT**と共に使用し、 **SQLdiag**サービスの特定のインスタンスを制御できるのは、 **SQLdiag** の名前付きインスタンスを指定した **/A** 引数のみです。 例:  
  
 **SQLDIAG START /A** _SQLdiag_application_name_  
  
## <a name="security-requirements"></a>セキュリティ要件  
 **SQLdiag** を汎用モード ( **/G** コマンド ライン引数を指定) 以外のモードで実行する場合は、 **SQLdiag** を実行するユーザーは、Windows **Administrators** グループのメンバー、および [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] **sysadmin** 固定サーバー ロールのメンバーであることが必要です。 既定では、 **SQLdiag** は Windows 認証を使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に接続しますが、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証もサポートされます。  
  
## <a name="performance-considerations"></a>パフォーマンスに関する考慮事項  
 **SQLdiag** を実行した場合のパフォーマンスへの影響は、収集用に構成した診断データの種類によって異なります。 たとえば、 **のトレース情報を収集するように** SQLdiag [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] を構成した場合、トレースを選択したイベント クラスの数に従ってサーバー パフォーマンスも影響を受けます。  
  
 **SQLdiag** の実行によるパフォーマンスへの影響は、構成した診断データを個別に収集する場合のコストの合計とほぼ同じになります。 たとえば、 **SQLdiag** でトレースを収集すると、 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]で収集した場合と同じパフォーマンス コストが生じます。 **SQLdiag** を使用した場合のパフォーマンスへの影響は無視しても問題ありません。  
  
## <a name="required-disk-space"></a>必要なディスク領域  
 **SQLdiag** ではさまざまな種類の診断情報を収集することができるため、 **SQLdiag** の実行に必要な空きディスク領域は、状況に応じて異なります。 収集される診断情報の量は、サーバーが処理している作業負荷の特性および量によって異なり、数 MB から数 GB までの範囲となる可能性があります。  
  
## <a name="configuration-files"></a>構成ファイル  
 スタートアップ時に、 **SQLdiag** は構成ファイルおよび指定されたコマンド ライン引数を読み取ります。 **SQLdiag** が収集する診断情報の種類は、構成ファイルに指定します。 既定では、 **SQLdiag** は **SQLdiag** ユーティリティ スタートアップ フォルダーにある SQLDiag.Xml 構成ファイルを使用します。この構成ファイルはツールが起動されるたびに抽出されます。 構成ファイルでは、XML スキーマである SQLDiag_schema.xsd が使用されます。このスキーマ ファイルは、 **SQLdiag** を実行するたびに、実行可能ファイルからユーティリティ スタートアップ ディレクトリへ抽出されます。  
  
### <a name="editing-the-configuration-files"></a>構成ファイルの編集  
 SQLDiag.Xml のコピーや編集によって、 **SQLdiag** が収集する診断データの種類を変更することができます。 構成ファイルを編集する場合は必ず、 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]など、XML スキーマに対して構成ファイルを検証できる XML エディターを使用します。 SQLDiag.Xml は直接編集しないでください。 代わりに、SQLDiag.Xml のコピーを作成し、同じフォルダーで新しいファイル名に変更します。 次にその新規のファイルを編集し、 **/I** 引数を使用して **SQLdiag**に渡します。  
  
#### <a name="editing-the-configuration-file-when-sqldiag-runs-as-a-service"></a>SQLdiag をサービスとして実行する場合の構成ファイルの編集  
 **SQLdiag** をサービスとして既に実行していて、構成ファイルを編集する必要がある場合は、 **/U** コマンド ライン引数を指定して SQLDIAG サービスの登録を解除します。次に、 **/R** コマンド ライン引数を使用してサービスを再登録します。 サービスの登録を解除、再登録すると、Windows レジストリにキャッシュされた古い構成情報が削除されます。  
  
## <a name="output-folder"></a>出力フォルダー  
 出力フォルダーが **/O** 引数で指定されない場合、 **SQLdiag** は、 **SQLdiag** スタートアップ フォルダーの下に SQLDIAG という名前のサブフォルダーを作成します。 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] など、大容量のトレースを伴う診断情報の収集を行う場合は、出力フォルダーが、要求される診断出力を格納するのに十分な空き領域を持つローカル ドライブにあることを確認してください。  
  
 **SQLdiag** を再起動すると、出力フォルダーの内容が上書きされます。 上書きしない場合は、コマンド ラインで **/N 2** を指定します。  
  
## <a name="data-collection-process"></a>データ収集プロセス  
 **SQLdiag** を起動すると、SQLDiag.Xml で指定された診断情報を収集するための初期化チェックが実行されます。 このプロセスには数分かかる場合があります。 コンソール アプリケーションとして実行した場合に **SQLdiag** が診断データの収集を開始すると、メッセージが表示されます。このメッセージは、 **SQLdiag** による収集が開始され、Ctrl キーを押しながら C キーを押すと停止できることを通知するものです。 **SQLdiag** がサービスとして実行されると、同様のメッセージが Windows イベント ログに書き込まれます。  
  
 **SQLdiag** を使用して、再現可能な問題を診断する場合、このメッセージを受け取ってから、問題をサーバー上で再現する必要があります。  
  
 **SQLdiag** は、多数の診断データを並行して収集します。 情報が Windows パフォーマンス ログおよびイベント ログから収集される場合を除いて、すべての診断情報は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] **sqlcmd** ユーティリティや Windows コマンド プロセッサなどのツールに接続することで収集されます。 **SQLdiag** は、1 台のコンピューターにつき 1 つのワーカー スレッドを使用して、これらのツールによる診断データの収集を監視します。通常、複数のツールが終了するのを同時に待機します。 収集プロセスの間、 **SQLdiag** は出力を各診断から出力フォルダーへルーティングします。  
  
## <a name="stopping-data-collection"></a>データ収集の停止  
 **SQLdiag** が診断データの収集を開始した後は、これを停止するか、指定した時間に停止するように構成しない限り、データ収集は継続されます。 **SQLdiag** が指定された時間に停止するように構成するには、停止時間の指定ができる **/E** 引数を使用するか、 **SQLdiag** をスナップショット モードで実行する **/X** 引数を使用します。  
  
 **SQLdiag** が停止すると、開始されていたすべての診断情報が停止されます。 たとえば、 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] トレースの収集を停止すると、実行中の [!INCLUDE[tsql](../includes/tsql-md.md)] スクリプトが停止され、データ収集中に発生したすべてのサブ プロセスも停止されます。 診断データの収集が完了した後で、 **SQLdiag** が終了します。  
  
> [!NOTE]  
>  **SQLdiag** サービスの一時停止はサポートされていません。 **SQLdiag** サービスの一時停止を試行した場合は、一時停止したときに実行されている診断収集が完了してからサービスが停止されます。 停止した **SQLdiag** を再開すると、アプリケーションが再起動され、出力フォルダーが上書きされます。 この出力フォルダーを上書きしない場合は、コマンド ラインで **/N 2** を指定します。  
  
 **コンソール アプリケーションとしての実行時に SQLdiag を停止するには**  
  
 **SQLdiag** をコンソール アプリケーションとして実行している場合、これを停止するには、 **SQLdiag** が実行されているコンソール ウィンドウで Ctrl キーを押しながら C キーを押します。 Ctrl キーを押しながら C キーを押した後、コンソール ウィンドウにメッセージが表示され、 **SQLDiag** データ収集が終了したこと、およびプロセスがシャットダウンされるまで待機する必要があることが通知されます。プロセスのシャットダウンには数分かかる場合があります。  
  
 2 度続けて、Ctrl キーを押しながら C キーを押すと、すべての子診断プロセスが停止し、アプリケーションが直ちに終了します。  
  
 **サービスとしての実行時に SQLdiag を停止するには**  
  
 **SQLdiag** をサービスとして実行する場合、 **SQLdiag** スタートアップ フォルダーの **SQLDiag STOP** を実行してサービスを停止します。  
  
 同一のコンピューター上で **SQLdiag** のインスタンスを複数実行している場合、サービスを停止するときに、 **SQLdiag** インスタンス名をコマンド ラインに渡すこともできます。 たとえば、Instance1 という名前の **SQLdiag** インスタンスを停止するには、次の構文を使用します。  
  
```  
SQLDIAG STOP /A Instance1  
```  
  
> [!NOTE]  
>  **/A** は、 **START**、 **STOP**、または **STOP_ABORT**と共に使用できる唯一のコマンド ライン引数です。 **SQLdiag** の名前付きインスタンスをサービスのコントロール動詞のいずれかと共に指定する必要がある場合、上記の構文例に示したように、コマンド ラインでコントロール動詞の後に **/A** を指定します。 コントロール動詞を使用するときは、コマンド ラインの最初の引数であることが必要です。  
  
 できるだけ早くサービスを停止するには、ユーティリティ スタートアップ フォルダーで **SQLDIAG STOP_ABORT** を実行します。 このコマンドは、現在実行されている診断収集の終了を待たずに、収集を中断します。  
  
> [!NOTE]  
>  **SQLdiag** サービスを停止するには、 **SQLDiag STOP** または **SQLDIAG STOP_ABORT** を使用します。 **SQLdiag** またはその他の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] サービスを停止する場合は、Windows サービス コンソールを使用しないでください。  
  
## <a name="automatically-starting-and-stopping-sqldiag"></a>SQLdiag の自動開始と停止  
 指定された時間に診断データ収集を自動的に開始および停止するには、 **/B**_start\_time_ 引数と **/E**_stop\_time_ 引数を使用します (24 時間形式を使用)。 たとえば、ほぼ 02:00:00 に定期的に発生する問題のトラブルシューティングを行う場合、01:00 に診断データの収集を自動的に開始して、03:00:00 に自動的に終了するように **SQLdiag** を構成することができます。 開始時間および終了時間を指定するには、 **/B** 引数と **/E** 引数を使用します。 24 時間表記を使用して、YYYYMMDD_HH:MM:SS 形式で開始日時と終了日時を正確に指定します。 開始時間や終了時間を相対的に指定するには、次の例のように、開始時間および終了時間の前に **+** を付け、日付部分 (YYYYMMDD_) を省略します。次の例では、 **SQLdiag** は情報の収集を開始する前に 1 時間待機し、それから情報の収集を 3 時間行い、停止して終了します。  
  
```  
sqldiag /B +01:00:00 /E +03:00:00  
```  
  
 相対的な *start_time* が指定された場合、 **SQLdiag** は、現在の日時を基準とした相対的な時間に開始されます。 相対的な *end_time* が指定された場合、 **SQLdiag** は、指定された *start_time*を基準とした相対的な時間に終了します。 指定した開始日時または終了日時が過去の場合、 **SQLdiag** は開始日を未来の開始日時に強制的に変更します。  
  
 これは、選択する開始日および終了日に対して重大な影響があります。 次の例を参照してください。  
  
```  
sqldiag /B +01:00:00 /E 08:30:00  
```  
  
 現在の時間が 08:00 の場合、終了時間は、診断の収集が実際に開始される時間よりも過去の時間になってしまいます。 指定した時間が過去となった場合、 **SQLDiag** は自動的に開始日および終了日を次の日に調整するため、この例では、診断収集は今日の 09:00 (相対開始時間が **+** で指定されている) に開始され、翌朝の 08:30 まで収集が継続されます。  
  
### <a name="stopping-and-restarting-sqldiag-to-collect-daily-diagnostics"></a>診断を毎日収集するための SQLdiag の停止と再起動  
 **SQLdiag**を手動で開始および停止せずに、指定した診断のセットを毎日収集するには、 **/L** 引数を指定します。 **/L** 引数により、定期的なシャットダウンの後で自動的に再起動されるため、 **SQLdiag** は継続的に実行されます。 **/L** が指定されている場合で、 **/E** 引数で指定された終了時間に到達したために **SQLdiag** 引数が停止する、または **/X** 引数を使用してスナップショット モードで実行されているために停止する場合、 **SQLdiag** は終了せずに再起動されます。  
  
 次の例では、 **SQLdiag** は継続モードで実行され、診断データの収集が 03:00:00 から 05:00:00 まで行われた後、自動的に再起動されます。  
  
```  
sqldiag /B 03:00:00 /E 05:00:00 /L  
```  
  
 次の例では、 **SQLdiag** は継続モードで実行され、診断データ スナップショットが 03:00:00 に作成された後、自動的に再起動されます。  
  
```  
sqldiag /B 03:00:00 /X /L  
```  
  
## <a name="running-sqldiag-as-a-service"></a>サービスとしての SQLdiag の実行  
 **SQLdiag** を使用して長期間にわたる診断データを収集するとき、その収集期間中に、 **SQLdiag** が実行されているコンピューターからログアウトしなければならない場合は、サービスとして実行する必要があります。  
  
 **サービスとしての実行する SQLdiag を登録するには**  
  
 **SQLdiag** を登録して、サービスとして実行するには、コマンド ラインで **/R** 引数を指定します。 これにより、 **SQLdiag** が登録され、サービスとして実行されます。 **SQLdiag** サービス名は SQLDIAG です。 **SQLDiag** をサービスとして登録するときにコマンド ラインに指定したその他の引数は維持され、サービスの開始時に再使用されます。  
  
 既定の SQLDIAG サービス名を変更するには、 **/A** コマンド ライン引数を使用して、別の名前を指定します。 **SQLdiag** は **/A** で指定されたどの **SQLdiag** インスタンスにも、自動的にプレフィックスの DIAG$ を付け、わかりやすいサービス名を作成します。  
  
 **SQLDIAG サービスの登録を解除するには**  
  
 サービスの登録を解除するには、 **/U** 引数を指定します。 サービスとしての **SQLdiag** の登録を解除すると、Windows サービスのレジストリ キーも削除されます。  
  
 **SQLDIAG サービスを開始または再起動するには**  
  
 SQLDIAG サービスを開始または再起動するには、コマンド ラインから **SQLDiag START** を実行します。  
  
 **/A** 引数を使用して、複数の **SQLdiag** インスタンスを実行する場合、サービスを開始するときに、コマンド ラインの **SQLdiag** インスタンス名を渡すこともできます。 たとえば、Instance1 という名前の **SQLdiag** インスタンスを開始するには、次の構文を使用します。  
  
```  
SQLDIAG START /A Instance1  
```  
  
 **net start** コマンドを使用して SQLDIAG サービスを開始することもできます。  
  
 **SQLdiag**を再起動すると、現在の出力フォルダーの内容が上書きされます。 上書きしない場合は、コマンド ラインで **/N 2** を指定して、ユーティリティが起動するときに、出力フォルダーの名前を変更します。  
  
 **SQLdiag** サービスの一時停止はサポートされていません。  
  
## <a name="running-multiple-instances-of-sqldiag"></a>複数の SQLdiag インスタンスの実行  
 同一コンピューター上で複数の **SQLdiag** インスタンスを実行するには、コマンド ラインで **/A**_SQLdiag\_application\_name_ を指定します。 これは、同一の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスから別の診断セットを同時に収集する場合に便利です。 たとえば、簡単なデータ収集を連続して実行するように、 **SQLdiag** の名前付きインスタンスを構成できます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]で特定の問題が発生した場合は、既定の **SQLdiag** インスタンスを実行し、その問題に対する診断データを収集したり、 [!INCLUDE[msCoName](../includes/msconame-md.md)] カスタマー サポート サービスが収集を要望している問題に対する一連の診断データを収集したりできます。  
  
## <a name="collecting-diagnostic-data-from-clustered-sql-server-instances"></a>クラスター化された SQL Server インスタンスからの診断データの収集  
 **SQLdiag** は、クラスター化された [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスからの診断データの収集をサポートしています。 クラスター化された [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスから診断データを収集するには、構成ファイル SQLDiag.Xml 内にある **\<Machine>** 要素の **name** 属性に **"."** が指定されていることを確認してください。コマンド ラインで **/G** 引数は指定しないでください。 既定では、構成ファイル内の **name** 属性に対して **"."** が指定されていて、 **/G** 引数はオフになっています。 通常、クラスター化された [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスから収集する場合、構成ファイルの編集やコマンド ライン引数の変更は必要ありません。  
  
 **"."** がコンピューター名として指定されている場合、 **SQLdiag** はこのコンピューターがクラスター上で実行されていることを検出し、同時に、クラスター上にインストールされているすべての仮想 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] から診断情報を取得します。 コンピューター上で実行されている 1 つの仮想 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のみから診断情報を収集する場合、SQLDiag.Xml 内の **\<Machine>** 要素の **name** 属性に対して仮想 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を指定します。  
  
> [!NOTE]  
>  クラスター化された [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] インスタンスから [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] トレース情報を収集するには、管理共有 (ADMIN$) をクラスター上で有効にする必要があります。  
  
## <a name="see-also"></a>参照  
 [コマンド プロンプト ユーティリティ リファレンス &#40;データベース エンジン&#41;](../tools/command-prompt-utility-reference-database-engine.md)  
  
  
