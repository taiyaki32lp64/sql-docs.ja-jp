---
title: osql ユーティリティ | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- statements [SQL Server], command prompt
- QUIT command
- Transact-SQL statements, command prompt
- EXIT command
- operating systems [SQL Server], commands
- osql utility [SQL Server]
- stored procedures [SQL Server], command prompt
- scripts [SQL Server], command prompt
- RESET command
- GO command
- command prompt utilities [SQL Server], osql
- CTRL+C command
ms.assetid: cf530d9e-0609-4528-8975-ab8e08e40b9a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: cfd8bc56a642442e1a5c5f673ca70bd86eb3ef6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105755"
---
# <a name="osql-utility"></a>osql ユーティリティ
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  **osql** ユーティリティを使用すると、 [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメント、システム プロシージャ、およびスクリプト ファイルを入力できます。 また、このユーティリティは ODBC を使用してサーバーと通信します。  
  
> [!IMPORTANT]  
>  この機能は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の将来のバージョンで削除される予定です。 新しい開発作業では、この機能を使用しないでください。また、現在この機能を使用しているアプリケーションの変更を計画してください。 代わりに **sqlcmd** を使用します。 詳細については、「 [sqlcmd Utility](../tools/sqlcmd-utility.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
osql  
[-?] |  
[-L] |  
[  
  {  
     {-Ulogin_id [-Ppassword]} | -E }  
     [-Sserver_name[\instance_name]] [-Hwksta_name] [-ddb_name]  
     [-ltime_out] [-ttime_out] [-hheaders]  
     [-scol_separator] [-wcolumn_width] [-apacket_size]  
     [-e] [-I] [-D data_source_name]  
     [-ccmd_end] [-q "query"] [-Q"query"]  
     [-n] [-merror_level] [-r {0 | 1}]  
     [-iinput_file] [-ooutput_file] [-p]  
     [-b] [-u] [-R] [-O]  
]  
```  
  
## <a name="arguments"></a>引数  
 **-?**  
 **osql** のスイッチに関する構文の概要を表示します。  
  
 **-L**  
 ローカルに構成されたサーバーと、ネットワーク上でブロードキャストしているサーバー名の一覧を表示します。  
  
> [!NOTE]  
>  ネットワーク上のブロードキャストの特性によっては、 **osql** は、一部のサーバーからタイムリーな応答を受信できない場合があります。 そのため、返されるサーバーのリストは、このオプションの実行ごとに異なる可能性があります。  
  
 **ｰU** _login_id_  
 ユーザーのログイン ID です。 ログイン ID では大文字と小文字は区別されます。  
  
 **-P** _password_  
 ユーザーが指定するパスワードです。 **-P** オプションを使用しない場合は、 **osql** ではパスワードの入力が要求されます。 **-P** オプションをコマンド プロンプトの最後にパスワードなしで使用すると、 **osql** ではデフォルトのパスワード (NULL) が使用されます。  
  
> [!IMPORTANT]  
>  空白のパスワードは使用しないでください。 強力なパスワードを使用してください。 詳細については、「 [Strong Passwords](../relational-databases/security/strong-passwords.md)」を参照してください。  
  
 パスワードでは大文字と小文字が区別されます。  
  
 OSQLPASSWORD 環境変数を使用して、現在のセッションの既定のパスワードを設定できます。 したがって、バッチ ファイルにパスワードを書き込む必要がありません。  
  
 **-P** オプションを使用してパスワードを指定しないと、 **osql** では最初に OSQLPASSWORD 変数が確認されます。 値が設定されていないと、 **osql** では既定のパスワード (NULL) が使用されます。 次の例では、コマンド プロンプトで OSQLPASSWORD 変数を設定してから **osql** ユーティリティにアクセスします。  
  
```  
C:\>SET OSQLPASSWORD=abracadabra  
C:\>osql   
```  
  
> [!IMPORTANT]  
>  パスワードをマスクする場合は、 **-P** オプションを **-U** オプションと共に指定しないでください。 **osql** を **-U** オプションおよび他のスイッチと共に指定した後 ( **-P**は指定しない)、Enter キーを押すと、 **osql** によってパスワードが要求されます。 この方法を使用すると、入力時にパスワードが確実にマスクされます。  
  
 **-E**  
 パスワードを要求せずに、セキュリティ接続を使用します。  
  
 **-S** _server\_name_[ **\\** _instance\_name_]  
 接続先となる [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスを指定します。 サーバー上の *の既定のインスタンスに接続するには、* server_name [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を指定します。 サーバー上の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の名前付きインスタンスに接続するには、_server\_name_ **\\** _instance\_name_ を指定します。 サーバーを指定しない場合、 **osql** は、ローカル コンピューター上にある [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の既定のインスタンスに接続します。 ネットワーク上のリモート コンピューターから **osql** を実行するときは、このオプションが必要です。  
  
 **-H** _wksta_name_  
 ワークステーション名を指定します。 ワークステーション名は **sysprocesses.hostname** に格納され、 **sp_who**により表示されます。 このオプションが指定されていない場合は、現在のコンピューター名であると見なされます。  
  
 **-d** _db_name_  
 *osql* の開始時に USE **db_name**ステートメントを発行します。  
  
 **-l** _time_out_  
 **osql** がログイン タイムアウトになる時間を秒単位で指定します。**osql** でのログインに関する既定のタイムアウトは 8 秒です。  
  
 **-t** _time_out_  
 コマンドの実行待ち時間を秒単位で指定します。*time_out* 値を指定しないと、コマンドはタイムアウトしません。  
  
 **-h** _headers_  
 列ヘッダーの間に出力する行数を指定します。 既定では、各クエリの結果に対して、ヘッダーは 1 つだけ表示されます。 ヘッダーを出力しない場合は、-1 を指定します。 -1 を使用する場合、パラメーターと設定値の間には空白を入れないでください ( **-h -1** ではなく **-h-1**)。  
  
 **-s** _col_separator_  
 列の区切り文字を指定します。既定値は空白文字です。 オペレーティング システムで特別な意味を持つ文字 (| ; & < > など) を使用するには、その文字を二重引用符 (") で囲みます。  
  
 **-w** _column_width_  
 出力用の画面幅を設定できます。 既定値は 80 文字です。 出力行が画面幅の最大値を超えると、複数の行に分けて出力されます。  
  
 **-a** _packet_size_  
 サイズの異なるパケットが要求できます。 *packet_size* の有効値は 512 ～ 65535 です。 既定値 **osql** はサーバーの既定値です。 パケット サイズを大きくすると、各 GO コマンドの間に多くの SQL ステートメントが含まれているサイズの大きいスクリプトを実行する場合に、パフォーマンスが向上します。 [!INCLUDE[msCoName](../includes/msconame-md.md)] のテストでは、一括コピーが最も速くなる設定値は 8,192 という結果が出ています。 大きなパケット サイズを要求することもできますが、要求が認められない場合は、サーバーでの既定値が **osql** での既定値になります。  
  
 **-e**  
 入力のエコーを返します。  
  
 **-I**  
 QUOTED_IDENTIFIER 接続オプションを有効にします。  
  
 **-D** _data_source_name_  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]用の ODBC ドライバーを使用して定義された ODBC データ ソースに接続します。 **osql** 接続では、データ ソースで指定されたオプションが使用されます。  
  
> [!NOTE]  
>  このオプションは、他のドライバー用に定義されたデータ ソースでは機能しません。  
  
 **-c** _cmd_end_  
 コマンド ターミネータを指定します。 既定では、GO だけが入力されている行があると、コマンドが終了したと見なされ、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に送られます。 コマンド ターミネータをリセットする場合、 [!INCLUDE[tsql](../includes/tsql-md.md)] の予約語やオペレーティング システムで特別な意味を持つ文字は、先頭に円記号が付いているかどうかに関係なく、使用しないでください。  
  
 **-q "** _query_ **"**  
 **osql** の起動時にクエリを実行しますが、クエリが完了しても **osql** を終了しません。 クエリ ステートメントには GO を含めないでください。 バッチ ファイルからクエリを実行する場合は、% 変数 (環境変数 %variable%) も使用できます。 例:  
  
```  
SET table=sys.objects  
osql -E -q "select name, object_id from %table%"  
```  
  
 クエリは二重引用符で、クエリに埋め込まれたものは単一引用符で囲みます。  
  
 **-Q"** _query_ **"**  
 クエリの実行後、直ちに **osql**を終了します。 クエリは二重引用符で、クエリに埋め込まれたものは単一引用符で囲みます。  
  
 **-n**  
 入力行から行番号とプロンプト記号 (>) を削除します。  
  
 **-m** _error_level_  
 エラー メッセージの表示をカスタマイズします。 指定した重大度レベル以上のエラーが発生すると、メッセージ番号、状況、エラー レベルが表示されます。 指定した重大度レベルより低いレベルのエラーの場合は、何も表示されません。 **-1** を指定すると、単なる情報メッセージであっても、すべてのヘッダーがメッセージと共に返されます。 **-1**を使用する場合、パラメーターと設定値の間には空白を入れないでください ( **-m -1**ではなく、 **-m-1**を使用)。  
  
 **-r** { **0**| **1**}  
 メッセージ出力を画面にリダイレクトします (**stderr**)。 パラメーターを指定しない場合や、 **0**を指定した場合は、重大度レベル 11 以上のエラー メッセージだけがリダイレクトされます。 **1**を指定した場合は、"print" を含むすべてのメッセージ出力がリダイレクトされます。  
  
 **-i** _input_file_  
 SQL ステートメントまたはストアド プロシージャのバッチを含むファイルを指定します。 **\<** -i **の代わりに、未満を示す比較演算子 (** ) を使用することもできます。  
  
 **-o** _output_file_  
 **osql**からの出力を受信するファイルを指定します。 **>** -o **の代わりに、より大きい (** ) 比較演算子を使用することもできます。  
  
 *input_file* が Unicode ではなく、 **-u** が指定されていない場合、 *output_file* は OEM 形式で格納されます。 *input_file* が Unicode であるか、 **-u** が指定されている場合、 *output_file* は Unicode 形式で格納されます。  
  
 **-p**  
 パフォーマンス統計を出力します。  
  
 **-b**  
 エラーが発生したときに、 **osql** を終了し、DOS ERRORLEVEL 値を返します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のエラー メッセージの重大度が 11 以上の場合は、DOS ERRORLEVEL 変数に返される値は 1 です。それ以外の場合は、値 0 が返されます。 [!INCLUDE[msCoName](../includes/msconame-md.md)] MS-DOS バッチ ファイルにより、DOS ERRORLEVEL の値をテストすることができ、エラーを適切に処理できます。  
  
 **-u**  
 *input_file* の形式に関係なく、 *output_file*を Unicode 形式で格納するように指定します。  
  
 **-R**  
 通貨、日付、および時刻データを文字データに変換するときに、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ODBC ドライバーでクライアントの設定を使用することを指定します。  
  
 **-O**  
 **isql** の先行バージョンの動作と一致するように、 **osql**の一部の機能を使用不能にします。 このオプションを指定すると、次の機能は使用できなくなります。  
  
-   EOF バッチ処理  
  
-   コンソール幅の自動スケーリング  
  
-   広範なメッセージ  
  
 また、このオプションは DOS ERRORLEVEL の既定値を -1 に設定します。  
  
> [!NOTE]  
>  **-n**、 **-O** および **-D** オプションは、 **osql**ではサポートされなくなりました。  
  
## <a name="remarks"></a>Remarks  
 **osql** ユーティリティは、ここに記載された、大文字と小文字では異なる機能を持つオプションを使用して、オペレーティング システムから直接起動されます。 起動されると、 **osql**は SQL ステートメントを受け取り、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に対話的に送ります。 結果はフォーマットされ、画面に表示されます (**stdout**)。 **osql**を終了するには、QUIT または EXIT を使用します。  
  
 ユーザー名を指定せずに **osql**を起動すると、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、 **osqluser=(** _user_ **)** や **osqlserver=(** _server_ **)** などの環境変数が確認され、それらの値が使用されます。 環境変数が設定されていない場合は、ワークステーションのユーザー名が使用されます。 サーバーを指定していない場合は、ワークステーション名が使用されます。  
  
 **-U** と **-P** のどちらのオプションも使用しない場合は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では接続時に [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows 認証モードが使用されます。 認証は、 [!INCLUDE[msCoName](../includes/msconame-md.md)] osql **を実行しているユーザーの**Windows アカウントに基づいて行われます。  
  
 **osql** ユーティリティでは ODBC API が使用されます。 またこのユーティリティでは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の ISO 接続オプションに対して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ODBC ドライバーの既定の設定が使用されます。 詳細については、「ANSI オプションの効果」を参照してください。  
  
> [!NOTE]  
>  **osql** ユーティリティでは CLR ユーザー定義データ型はサポートされていません。 これらのデータ型を処理するには、 **sqlcmd** ユーティリティを使用する必要があります。 詳細については、「 [sqlcmd Utility](../tools/sqlcmd-utility.md)」を参照してください。  
  
## <a name="osql-commands"></a>OSQL コマンド  
 [!INCLUDE[tsql](../includes/tsql-md.md)] osql **では、** ステートメントの他に次のコマンドも使用できます。  
  
|コマンド|[説明]|  
|-------------|-----------------|  
|GO|最後の GO の後に入力したすべてのステートメントを実行します。|  
|RESET|入力したステートメントをすべて消去します。|  
|QUIT または EXIT( )|**osql**を終了します。|  
|Ctrl + C|クエリを終了しますが、 **osql**は終了しません。|  
  
> [!NOTE]  
>  !! コマンド および ED コマンドは **osql**ではサポートされなくなりました。  
  
 コマンド ターミネータ GO (既定値)、RESET、EXIT、QUIT、および Ctrl + C は、行頭の **osql** プロンプトの直後に使用した場合にだけ認識されます。  
  
 GO は、バッチの終わりとキャッシュされた [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの実行を知らせます。 各入力行の終わりで Enter キーを押すと、 **osql** はその行のステートメントをキャッシュします。 GO を入力した後 Enter キーを押すと、現在キャッシュされているすべてのステートメントが一括して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に送られます。  
  
 現在の **osql** ユーティリティは、実行する各スクリプトの終わりに暗黙の GO があるものとして動作します。したがって、スクリプト内のすべてのステートメントが実行されます。  
  
 行頭にコマンド ターミネータを入力すると、コマンドが終了します。 コマンド ターミネータの後ろに整数を入力すると、コマンドの実行回数を指定できます。 たとえば、コマンドを 100 回実行するには、次のように入力します。  
  
```  
SELECT x = 1  
GO 100  
```  
  
 結果は、実行終了時に 1 回出力されます。 **osql** で 1 行に入力できる文字数は、最大で 1,000 文字です。 大きなステートメントは、複数の行に分けてください。  
  
 Windows のコマンド再呼び出し機能を使用すると、 **osql** ステートメントの再呼び出しと修正が可能になります。 RESET を入力すると、既存のクエリ バッファーをクリアできます。  
  
 ストアド プロシージャを実行するとき、 **osql** は同じバッチの各結果セットの間に空白行を 1 行ずつ出力します。 また、"0 件処理されました" というメッセージは、そのメッセージが実行したステートメントに該当する場合にだけ表示されます。  
  
## <a name="using-osql-interactively"></a>osql の対話的使用  
 **osql** を対話的に使用するには、コマンド プロンプトで **osql** コマンド (および任意のオプション) を入力します。  
  
 次のようなコマンドを入力すると、 **osql** によって実行されるクエリ (Stores.qry など) が含まれているファイルの内容を読み取ることができます。  
  
```  
osql -E -i stores.qry  
```  
  
 次のようなコマンドを入力すると、クエリ (Titles.qry など) が含まれているファイルを読み取り、結果を別のファイルに出力できます。  
  
```  
osql -E -i titles.qry -o titles.res  
```  
  
> [!IMPORTANT]  
>  可能であれば、 **-E**オプションを使用します (信頼関係接続)。  
  
 対話的に **osql** を使用している場合、 **:r**_file\_name_を使用して、オペレーティング システム ファイルをコマンド バッファーに読み取ることができます。 これにより、 *file_name* 内の SQL スクリプトが単一のバッチとして直接サーバーへ送信されます。  
  
> [!NOTE]  
>  **osql**を使用するとき、GO によって SQL スクリプト ファイルに構文エラーが発生する場合、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は GO をバッチ区切り記号として処理しています。  
  
## <a name="inserting-comments"></a>コメントの挿入  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] osql **で**に送られる Transact-SQL ステートメントには、コメントを挿入することができます。 2 種類のコメント スタイルがあります: `--` と `/*...*/` です。  
  
## <a name="using-exit-to-return-results-in-osql"></a>EXIT によって osql から返される結果  
 **osql**からの戻り値に、SELECT ステートメントの結果を使用できます。 数値の場合、結果行の最終行の最終列は、4 バイトの (長) 整数に変換されます。 MS-DOS は、下位バイトを親プロセスやオペレーティング システムのエラー レベルに渡します。 Windows では、4 バイトの整数全体を渡します。 構文は次のとおりです。  
  
```  
EXIT ( < query > )  
```  
  
 例:  
  
```  
EXIT(SELECT @@ROWCOUNT)  
```  
  
 バッチ ファイルの一部として、EXIT パラメーターを使用することもできます。 例:  
  
```  
osql -E -Q "EXIT(SELECT COUNT(*) FROM '%1')"  
```  
  
 **osql** ユーティリティでは、かっこ **()** 内のすべての情報が、入力されたとおりにサーバーに送信されます。 システム ストアド プロシージャが値セットを選択し、値を返す場合、選択した値だけが返されます。 かっこ内に何も指定せずに EXIT **()** ステートメントを指定すると、バッチ内のそのステートメントよりも前にあるものすべてを実行し、戻り値を返さずに終了します。  
  
 EXIT には、次の 4 つの形式があります。  
  
-   EXIT  
  
> [!NOTE]  
>  バッチを実行せずに直ちに終了し、値を返しません。  
  
-   EXIT **()**  
  
> [!NOTE]  
>  バッチを実行してから終了し、値を返しません。  
  
-   EXIT **(** _query_ **)**  
  
> [!NOTE]  
>  クエリを含むバッチを実行し、クエリの結果を返して終了します。  
  
-   状態 127 の RAISERROR ステートメント  
  
> [!NOTE]  
>  RAISERROR を **osql** スクリプトの中で使用し、状態 127 が発生すると、 **osql** は終了し、メッセージ ID がクライアントに返されます。 例:  
  
```  
RAISERROR(50001, 10, 127)  
```  
  
 このエラーが発生すると、 **osql** スクリプトが終了し、メッセージ ID 50001 がクライアントに返されます。  
  
 戻り値 -1 ～ -99 は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]によって予約済みです。 **osql** では次のような値を定義しています。  
  
-   -100  
  
     戻り値を選択する前に、エラーが発生した。  
  
-   -101  
  
     戻り値を選択するときに、行が見つからなかった。  
  
-   -102  
  
     戻り値を選択するときに、変換エラーが発生した。  
  
## <a name="displaying-money-and-smallmoney-data-types"></a>money (金額) と smallmoney (短精度金額) のデータ型の表示  
 **money** データ型と **smallmoney** データ型については、 **では内部的に小数点以下 4 桁の数値で格納されますが、** osql [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では小数点以下 2 桁の数値が表示されます。 次の例の結果を参照してください。  
  
```  
SELECT CAST(CAST(10.3496 AS money) AS decimal(6, 4))  
GO  
```  
  
 このステートメントの実行結果は `10.3496`で、小数点以下のすべての桁をそのままにして値を格納することを示しています。  
  
## <a name="see-also"></a>参照  
 [コメント &#40;MDX&#41;](../mdx/comment-mdx.md)   
 [-- &#40;コメント&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)   
 [CAST および CONVERT &#40;Transact-SQL&#41;](../t-sql/functions/cast-and-convert-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
