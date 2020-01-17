---
title: Sqlcmd | を使用した接続Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd
ms.assetid: 61a2ec0d-1bcb-4231-bea0-cff866c21463
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a782db89033da42ebf17ed33565ec680fafa0d04
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005913"
---
# <a name="connecting-with-sqlcmd"></a>sqlcmd による接続
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[sqlcmd](https://go.microsoft.com/fwlink/?LinkID=154481) ユーティリティは、Linux および macOS の [!INCLUDE[msCoName](../../../includes/msconame_md.md)]ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で使用できます。
  
次のコマンドは、Windows 認証 (Kerberos) と[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]認証をそれぞれ使用する方法を示しています。
  
```  
sqlcmd -E -Sxxx.xxx.xxx.xxx  
sqlcmd -Sxxx.xxx.xxx.xxx -Uxxx -Pxxx  
```  
  
## <a name="available-options"></a>利用可能なオプション

現在のリリースでは、次のオプションを使用できます。  
  
- -? 使用`sqlcmd`法を表示します。  
  
- -a パケット サイズを要求します。  
  
- -b エラーがある場合にバッチ ジョブを終了します。  
  
- -c *batch_terminator*バッチターミネータを指定します。  
  
- -C サーバー証明書を信頼します。  

- -d *database_name*を開始`USE` `sqlcmd`するときに*database_name*ステートメントを実行します。  

- -D `sqlcmd` -S オプションに渡された値が、データ ソース名 (DSN) として解釈されるようにします。 詳細については、このトピックの最後の「`sqlcmd` および `bcp` の DSN サポート」を参照してください。  
  
- -e 入力スクリプトを標準出力デバイス (stdout) に書き込みます。

- 信頼関係接続の統合認証を使用します。Linux または macOS クライアントからの統合認証を使用する信頼関係接続の作成の詳細については、「[統合認証の使用](../../../connect/odbc/linux-mac/using-integrated-authentication.md)」を参照してください。

- -h *number_of_rows*  列ヘッダーの間に出力する行数を指定します。  
  
- -H ワークステーション名を指定します。  
  
- -i *input_file*[,*input_file*[,...]] SQL ステートメントまたはストアド プロシージャのバッチを含むファイルを指定します。  
  
- -[ `SET QUOTED_IDENTIFIER`接続] オプションを [オン] に設定します。  
  
- -k  制御文字を削除するか、置き換えます。  
  
- **-K**_アプリケーション\_の目的_  
アプリケーションがサーバーに接続するときのワークロードのタイプを宣言します。 現在サポートされている値は、 **ReadOnly**だけです。 **-K** を指定しない場合、`sqlcmd` では AlwaysOn 可用性グループのセカンダリ レプリカへの接続がサポートされません。 詳細については、[Linux と macOS の ODBC ドライバー - 高可用性とディザスター リカバリー](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)に関するページをご覧ください。  
  
> [!NOTE]  
> **-K** は、CTP for SUSE Linux ではサポートされていません。 ただし、**に渡される DSN ファイルで**ApplicationIntent=ReadOnly`sqlcmd` キーワードを指定できます。 詳細については、このトピックの最後の「`sqlcmd` および `bcp` の DSN サポート」を参照してください。  
  
- -l *timeout* サーバーへの接続の試行時に、`sqlcmd` のログインがタイムアウトするまでの秒数を指定します。

- -m *error_level* stdout に送信されるエラー メッセージを制御します。  
  
- **-M**_マルチサブ\_ネットフェールオーバー_  
[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 可用性グループまたは [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] フェールオーバー クラスター インスタンスの可用性グループ リスナーに接続する際には、必ず **-M** を指定してください。 **-M** を指定すると、フェールオーバーを迅速に検出して、(現在) アクティブなサーバーに接続できます。 **-M** を指定しない場合、 **-M** は無効になります。 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)] について詳しくは、「[Linux と macOS の ODBC ドライバーでの高可用性とディザスター リカバリーのサポート](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)」をご覧ください。  
  
> [!NOTE]  
> **-M** は、CTP for SUSE Linux ではサポートされていません。 ただし、`sqlcmd` に渡される DSN ファイルで **MultiSubnetFailover=Yes** キーワードを指定できます。 詳細については、このトピックの最後の「`sqlcmd` および `bcp` の DSN サポート」を参照してください。  
  
- -N 接続を暗号化します。  
  
- -o *output_file* `sqlcmd` からの出力を受信するファイルを指定します。  
  
- -p  すべての結果セットのパフォーマンス統計を出力します。  
  
- -P  ユーザー パスワードを指定します。  
  
- -q *commandline_query*は、の起動時`sqlcmd`にクエリを実行しますが、クエリの実行が完了しても終了しません。  

- -Q *commandline_query*は、の起動時`sqlcmd`にクエリを実行します。 クエリが終了すると `sqlcmd` は終了します。  

- -r エラー メッセージを stderr にリダイレクトします。

- -R ドライバーがクライアントの地域別設定を使用して、通貨および日時データを文字データへ変換します。 現時点では、en_US (英語 (米国)) 書式設定のみを使用します。
  
- -s *column_separator_char*列区切り文字を指定します。  

- -S [*protocol*:] *server*[ **,** _port_]  
接続するの[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンスを指定します。または、-D が使用されている場合は、DSN を指定します。 Linux および macOS の ODBC ドライバーには、-S が必要です。 **Tcp**が唯一の有効なプロトコルであることに注意してください。  
  
- -t *query_timeout* コマンド (または SQL ステートメント) がタイムアウトになるまでの時間を秒数で指定します。  
  
- -u input_file の形式に関係なく、output_file を Unicode 形式で格納するように指定します。  
  
- -U *login_id*ユーザーログイン id を指定します。  
  
- -V *error_severity_level* ERRORLEVEL 変数を設定するために使用される重大度レベルを制御します。  
  
- -w *column_width*出力用の画面幅を指定します。  
  
- -W 列から後続の空白を削除します。  
  
- -x 変数の代入を無効にします。  
  
- -X コマンド、スタートアップ スクリプト、および環境変数を無効にします。  
  
- -y *variable_length_type_display_width*スクリプト変数`sqlcmd` `SQLCMDMAXFIXEDTYPEWIDTH`を設定します。
  
- -Y *fixed_length_type_display_width*スクリプト変数`sqlcmd` `SQLCMDMAXVARTYPEWIDTH`を設定します。


## <a name="available-commands"></a>使用可能なコマンド

現在のリリースでは、次のコマンドを使用できます。  
  
-   [:]!!  
  
-   :Connect  
  
-   :Error  
  
-   [:]EXIT  
  
-   GO [*count*]  
  
-   :Help  
  
-   :List  
  
-   :Listvar  
  
-   :On Error  
  
-   :Out  
  
-   :Perftrace  
  
-   [:]QUIT  
  
-   :r  
  
-   :RESET  
  
-   :setvar  
  
## <a name="unavailable-options"></a>利用できないオプション
現在のリリースでは、次のオプションは使用できません。  

- -A  専用管理者接続 (DAC) を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にログインします。 専用管理者接続 (DAC) を作成する方法については、「[プログラミング ガイドライン](../../../connect/odbc/linux-mac/programming-guidelines.md)」を参照してください。  
  
- -f *code_page* 入力と出力のコード ページを指定します。  
  
- -L  ローカルに構成されたサーバー コンピューターと、ネットワーク上でブロードキャストしているサーバー コンピューター名の一覧を表示します。  
  
- -v  `sqlcmd` スクリプトで使用できる `sqlcmd` スクリプト変数を作成します。  
  
次の代替方法を使用できます。パラメーターを1つのファイル内に配置して、別のファイルに追加することができます。 これにより、パラメーター ファイルを使用して値を置き換えることができます。 たとえば、次のコンテンツを使用して、`a.sql` というファイル (パラメーター ファイル) を作成します。
  
    :setvar ColumnName object_id  
    :setvar TableName sys.objects  
  
次に、置換のためのパラメーターを使用して、`b.sql` というファイルを作成します。  
  
    select $(ColumnName) from $(TableName)  

コマンドラインで、次の`a.sql`コマンド`b.sql` `c.sql`を使用してとを結合します。  
  
    cat a.sql > c.sql 
  
    cat b.sql >> c.sql  
  
を`sqlcmd`実行し`c.sql`て、入力ファイルとして使用します。  
  
    slqcmd -S<...> -P<..> -U<..> -I c.sql  

- -z*パスワード*を変更します。  
  
- -Z*パスワード*を変更して、終了します。  

## <a name="unavailable-commands"></a>利用できないコマンド

現在のリリースでは、次のコマンドは利用できません。  
  
-   :ED  
  
-   :ServerList  
  
-   :XML  
  
## <a name="dsn-support-in-sqlcmd-and-bcp"></a>sqlcmd および bcp の DSN サポート

-D を指定した場合は、**sqlcmd** または **bcp** `-S` オプション (または **sqlcmd**: 接続コマンド) でサーバー名ではなくデータ ソース名 (DSN) を指定できます。 -D を指定すると、 **sqlcmd**または**bcp**は、-S オプションで DSN に指定されているサーバーに接続します。  
  
システム dsn は、 `odbc.ini` (`/etc/odbc.ini`標準インストール時に) ODBC sysconfigdir ディレクトリのファイルに格納されます。 ユーザー dsn は、ユーザー `.odbc.ini`のホームディレクトリ (`~/.odbc.ini`) に格納されます。
  
Linux または macOS 上の DSN では、次のエントリがサポートされています。

-   **ApplicationIntent=ReadOnly**  

-   **データベース =** _データベース\_名_  
  
-   **Driver = Odbc driver 11 for SQL Server**または**Driver = odbc driver 13 for SQL Server**
  
-   **MultiSubnetFailover=Yes**  
  
-   **サーバー =** _サーバー\_名また\_は\_IPアドレス\__  
  
-   **Trusted_Connection=yes**|**no**  
  
DSN では DRIVER エントリのみが必要ですが、サーバーに接続するには、`sqlcmd` または `bcp` が SERVER エントリ内の値を必要とします。  

DSN と `sqlcmd` または `bcp` コマンド ラインの両方で同じオプションが指定されている場合は、コマンドライン オプションが、DSN で使用される値をオーバーライドします。 たとえば、DSN に DATABASE エントリがあり、`sqlcmd` コマンドラインに **-d** が含まれる場合、 **-d** に渡される値が使用されます。 DSN で **Trusted_Connection=yes** が指定されている場合は、Kerberos 認証が使用され、ユーザー名 ( **-U**) とパスワード ( **-P**) は無視されます (指定されている場合)。

エイリアス `alias isql="sqlcmd -D"` を定義して、`isql` を呼び出す既存のスクリプトを、`sqlcmd` を使用するように変更できます。  

## <a name="see-also"></a>参照  
[**bcp** による接続](../../../connect/odbc/linux-mac/connecting-with-bcp.md)  
 
