---
title: bcp ユーティリティ | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server]
- exporting data
- row exporting [SQL Server]
- copying data [SQL Server], bcp utility
- command prompt utilities [SQL Server], bcp
- tables [SQL Server], importing data
- column importing [SQL Server]
- bcp utility [SQL Server], command options
- file exporting [SQL Server]
- bulk copy [SQL Server]
- bcp utility [SQL Server], about bcp utility
- tables [SQL Server], exporting data
- row importing [SQL Server]
- importing data, bcp utility
- file importing [SQL Server]
- column exporting [SQL Server]
ms.assetid: c0af54f5-ca4a-4995-a3a4-0ce39c30ec38
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 01/14/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 0f9081562a0cb0f8ddba663f04305c7bd2b387fe
ms.sourcegitcommit: d65cef35cdf992297496095d3ad76e3c18c9794a
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72989574"
---
# <a name="bcp-utility"></a>bcp ユーティリティ

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

> Linux で bcp を使用する方法については、「 [linux での sqlcmd と bcp のインストール](../linux/sql-server-linux-setup-tools.md)」を参照してください。
>
> Bcp を Azure SQL Data Warehouse と共に使用する方法の詳細については、「bcp を使用し[たデータの読み込み](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp)」を参照してください。

**b**ulk **c**opy **p**rogram ユーティリティ (**bcp**) では、[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスと、ユーザー指定の形式のデータ ファイルとの間でデータの一括コピーを行います。 **bcp** ユーティリティを使うと、多数の新規行を [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] テーブルにインポートしたり、データをテーブルからデータ ファイルにエクスポートしたりできます。 このユーティリティでは **の知識は必要ありません。ただし、** queryout [!INCLUDE[tsql](../includes/tsql-md.md)]オプションと同時に使う場合はその知識が必要になります。 データをテーブルにインポートするには、そのテーブル用に作成されたフォーマット ファイルを使用するか、テーブルの構造およびテーブルの列に有効なデータの型を理解しておく必要があります。  

![トピック リンク アイコン](../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") **bcp** 構文で使用される構文表記規則については、「[Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)」をご覧ください。  

> [!NOTE]
> **bcp** を使ってデータをバックアップする場合、フォーマット ファイルを作成してデータ形式を記録します。 **bcp** データ ファイルには、スキーマ情報やフォーマット情報が **含まれない** ので、テーブルまたはビューが削除され、フォーマット ファイルがない場合は、データをインポートできないことがあります。

## <a name="download-the-latest-version-of-bcp-utility"></a>最新バージョンの bcp ユーティリティをダウンロードする

**[![ダウンロード](../ssdt/media/download.png) Microsoft Command Line Utilities 15.0 for SQL Server (x64) をダウンロードする](https://go.microsoft.com/fwlink/?linkid=2043518)**
<br>**[![ダウンロード](../ssdt/media/download.png) Microsoft Command Line Utilities 15.0 for SQL Server (x86) をダウンロードする](https://go.microsoft.com/fwlink/?linkid=2043622)**

コマンドラインツールは一般公開 (GA) ですが、[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]のインストーラーパッケージと共にリリースされています。

### <a name="version-information"></a>バージョン情報

リリース番号: 15.0 <br>
ビルド番号: 15.0.1000.34<br>
リリース日: 2018 年 10 月 18 日

新しいバージョンの SQLCMD では Azure AD 認証がサポートされています。これには、SQL Database、SQL Data Warehouse、Always Encrypted の機能に対する Multi-Factor Authentication (MFA) のサポートが含まれます。
新しい BCP では、SQL Database と SQL Data Warehouse に対する Multi-Factor Authentication (MFA) のサポートなど、Azure AD 認証がサポートされています。

### <a name="system-requirements"></a>システム要件

Windows 10、Windows 7、Windows 8、Windows 8.1、Windows Server 2008、Windows Server 2008 R2、Windows Server 2008 R2 SP1、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016

このコンポーネントには、SQL Server 用に[Windows インストーラー 4.5](https://www.microsoft.com/download/details.aspx?id=8483)と[Microsoft ODBC Driver 17.3 の](https://www.microsoft.com/download/details.aspx?id=56567)両方が必要です。

BCP のバージョンを確認するには `bcp /v` コマンドを実行し、15.0.1000.34 以上が使用されていることを確認します。

<table><th>構文</th><tr><td><pre>
bcp [<a href="#db_name">database_name.</a>] <a href="#schema">schema</a>.{<a href="#tbl_name">table_name</a> | <a href="#vw_name">view_name</a> | <a href="#query">"query"</a>}
    {<a href="#in">in</a> <a href="#data_file">data_file</a> | <a href="#out">out</a> <a href="#data_file">data_file</a> | <a href="#qry_out">queryout</a> <a href="#data_file">data_file</a> | <a href="#format">format</a> <a href="#format">nul</a>}
<a>                                                                                                         </a>
    [<a href="#a">-a packet_size</a>]
    [<a href="#b">-b batch_size</a>]
    [<a href="#c">-c</a>]
    [<a href="#C">-C { ACP | OEM | RAW | code_page } </a>]
    [<a href="#d">-d database_name</a>]
    [<a href="#e">-e err_file</a>]
    [<a href="#E">-E</a>]
    [<a href="#f">-f format_file</a>]
    [<a href="#F">-F first_row</a>]
    [<a href="#G">-G Azure Active Directory Authentication</a>]
    [<a href="#h">-h"hint [,...n]"</a>]
    [<a href="#i">-i input_file</a>]
    [<a href="#k">-k</a>]
    [<a href="#K">-K application_intent</a>]
    [<a href="#l">-l login_timeout</a>]
    [<a href="#L">-L last_row</a>]
    [<a href="#m">-m max_errors</a>]
    [<a href="#n">-n</a>]
    [<a href="#N">-N</a>]
    [<a href="#o">-o output_file</a>]
    [<a href="#P">-P password</a>]
    [<a href="#q">-q</a>]
    [<a href="#r">-r row_term</a>]
    [<a href="#R">-R</a>]
    [<a href="#S">-S [server_name[\instance_name]</a>]
    [<a href="#t">-t field_term</a>]
    [<a href="#T">-T</a>]
    [<a href="#U">-U login_id</a>]
    [<a href="#v">-v</a>]
    [<a href="#V">-V (80 | 90 | 100 | 110 | 120 | 130 ) </a>]
    [<a href="#w">-w</a>]
    [<a href="#x">-x</a>]
</pre></td></tr></table>

## <a name="arguments"></a>引数

 _**data\_file**_ <a name="data_file"></a>  
 データ ファイルの完全パスを指定します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]にデータを一括インポートする場合は、データ ファイルには指定したテーブルまたはビューにコピーするデータが含まれます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]からデータを一括エクスポートする場合は、データ ファイルにはテーブルまたはビューからコピーしたデータが含まれます。 パスは、1 文字から 255 文字までです。 データ ファイルに含めることができる行の数は最大 2^63 - 1 です。  
  
 _**database\_name**_ <a name="db_name"></a>  
 指定したテーブルまたはビューを含むデータベースの名前を指定します。 指定しない場合は、ユーザーの既定データベースになります。  
  
 **d-** で明示的にデータベース名を指定することもできます。  
  
 **in** *data_file* | **out** *data_file* | **の知識は必要ありません。ただし、** *data_file* | **format nul**  
 次に示すように、一括コピーの方向を指定します。  
  
-   **in**<a name="in"></a> はファイルからデータベース テーブルまたはビューへのコピーを行います。  
  
-   **out**<a name="out"></a> はデータベース テーブルまたはビューからファイルへのコピーを行います。 既存のファイルを指定すると、ファイルは上書きされます。 **bcp** ユーティリティは、データを抽出するときに、空文字列を NULL 文字列で、NULL 文字列を空文字列で表すことに注意してください。  
  
-   **queryout**<a name="qry_out"></a> はクエリからのコピーを行います。データをクエリから一括コピーする場合にのみ指定する必要があります。  
  
-   **format**<a name="format"></a> は、指定されたオプション ( **-n**、 **-c**、 **-w**、 **-N**) と、テーブルやビューの区切り記号に基づいてフォーマット ファイルを作成します。 データを一括コピーするとき、 **bcp** コマンドはフォーマット ファイルを参照することができるため、フォーマット情報を対話的に再入力する必要がなくなります。 **format** オプションには **-f** オプションが必要です。XML フォーマット ファイルを作成する場合には、 **-x** オプションも必要です。 詳細については、「[フォーマット ファイルの作成 &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md)」をご覧ください。 値として **nul** を指定する必要があります (**format nul**)。  
  
 _**owner**_ <a name="schema"></a>  
 テーブルまたはビューの所有者の名前を指定します。 操作を実行するユーザーが指定のテーブルまたはビューを所有している場合、*owner* は省略可能です。 *owner* が指定されず、操作を実行するユーザーが指定のテーブルまたはビューを所有していない場合は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] からエラー メッセージが返され、操作は取り消されます。  
  
**"** _**query**_ **"** <a name="query"></a> は、結果セットを返す [!INCLUDE[tsql](../includes/tsql-md.md)] クエリです。 クエリから複数の結果セットが返される場合、最初の結果セットのみがデータ ファイルにコピーされ、それ以降の結果セットは無視されます。 クエリは二重引用符で、クエリに埋め込まれたものは単一引用符で囲みます。 クエリからデータを一括コピーする場合には、**queryout** も指定する必要があります。  
  
 ストアド プロシージャ内で参照されるテーブルのすべてが bcp ステートメントの実行前に存在する場合に限り、クエリはストアド プロシージャを参照できます。 たとえば、ストアド プロシージャにより一時テーブルが生成される場合、この一時テーブルは実行時にだけ利用でき、ステートメントの実行時には利用できないため、 **bcp** ステートメントは失敗します。 このような場合、ストアド プロシージャの結果をテーブルに挿入し、 **bcp** を使用してテーブルからデータ ファイルにデータをコピーすることを検討してください。  
  
 _**table\_name**_ <a name="tbl_name"></a>  
 データを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にインポートする (**in**) 場合はインポート先のテーブルの名前、データを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] からエクスポートする (**out**) 場合はエクスポート元のテーブルの名前です。  
  
 _**view\_name**_ <a name="vw_name"></a>   
 データを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にコピーする (**in**) 場合はコピー先のビューの名前、データを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] からコピーする (**out**) 場合はコピー元のビューの名前です。 すべての列が同じテーブルを参照しているビューのみが、コピー先のビューとして使用できます。 ビューにデータをコピーするときの制限の詳細については、「[挿入 &#40;Transact-SQL&#41;](../t-sql/statements/insert-transact-sql.md)」をご覧ください。  
  
 **-a** _**packet\_size**_ <a name="a"></a>  
 サーバーとの間で送信されるネットワーク パケットごとのバイト数を指定します。 サーバー構成オプションは、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (または **sp_configure** システム ストアド プロシージャ) を使用して設定できます。 ただし、このオプションを使用すると、サーバー構成オプションを個別にオーバーライドできます。 *packet_size* の有効値は 4,096 バイトから 65,535 バイトです。既定値は 4,096 です。  
  
 パケット サイズを大きくすると、一括コピーのパフォーマンスを向上させることができます。 より大きなサイズのパケットを要求しても、許可されない場合、既定値が使用されます。 **bcp** ユーティリティが生成するパフォーマンス統計には、使用したパケット サイズが示されます。  
  
 **-b** _**batch\_size**_ <a name="b"></a>  
 一括インポートするデータの行数を指定します。 コミットされる前に、各バッチはすべてのバッチをインポートする個別のトランザクションとしてインポートおよび記録されます。 既定では、データ ファイルのすべての行が 1 つのバッチとしてインポートされます。 複数のバッチに行を分散するには、データ ファイルの行数よりも少ない *batch_size* を指定します。 バッチのトランザクションが失敗すると、現在のバッチの挿入のみがロールバックされます。 コミットされたトランザクションによって既にインポートされているバッチは、それ以降の失敗による影響を受けません。  
  
 このオプションは、 **-h "** ROWS_PER_BATCH **=** _bb_ **"** オプションと組み合わせて使用しないでください。  
 
 **-c**<a name="c"></a>  
 文字データ型を使用して操作を実行します。 このオプションを使用すると、フィールドごとにプロンプトが表示されません。 **char** をプレフィックスなしのストレージ型として、また **\t** (タブ) をフィールド区切り文字、 **\r\n** (改行文字) を行ターミネータとして使用します。 **-c** は **-w** と互換性がありません。  
  
 詳細については、「[文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)」をご覧ください。  
  
 **-C** { **ACP** | **OEM** | **RAW** | *code_page* }<a name="C"></a>   
 データ ファイル内のデータのコード ページを指定します。 *code_page* は、データに **char**、 **varchar**、 **text** 列 (文字値が 127 より大きいか、32 未満) が含まれている場合にのみ当てはまります。  
  
> [!NOTE]
> フォーマット ファイルの各列に対して照合順序名を指定することをお勧めします (65001 オプションを照合順序/コード ページ仕様よりも優先する場合を除く)。
  
|コード ページ値|[説明]|  
|---------------------|-----------------|  
|ACP|[!INCLUDE[vcpransi](../includes/vcpransi-md.md)]/Microsoft Windows (ISO 1252)。|  
|OEM|クライアントが使用する既定のコード ページです。 **-C** が指定されていない場合に使用される既定のコード ページです。|  
|RAW|コード ページの変換は行われません。 したがって、これは最も速いオプションです。|  
|*code_page*|850 などの特定のコード ページ番号を指定します。<br /><br /> バージョン 13 ([!INCLUDE[ssSQL15](../includes/sssql15-md.md)]) より前のバージョンでは、コード ページ 65001 (UTF-8 エンコード) はサポートされません。 バージョン 13 以降では、UTF-8 エンコードを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の前のバージョンにインポートできます。|  
  
 **-d** _**database\_name**_ <a name="d"></a>   
 接続先のデータベースを指定します。 既定では、bcp.exe はユーザーの既定のデータベースに接続します。 \* *-D database_name と3つの部分で構成される名前 (database_name の最初のパラメーターとして渡される) が指定されている場合、データベース名を2回指定することはできないため、エラーが発生します。 *database_name* がハイフン (-) またはスラッシュ (/) で始まる場合は、 **-d** とデータベース名の間に空白を入れないでください。  
  
 **-e** _**err\_file**_ <a name="e"></a>  
 **bcp** ユーティリティがファイルからデータベースに転送できなかったすべての行を格納するエラー ファイルの完全パスを指定します。 **bcp** コマンドからのエラー メッセージは、ユーザーのワークステーションに送られます。 このオプションを指定しないと、エラー ファイルは作成されません。  
  
 *err_file* がハイフン (-) またはスラッシュ (/) で始まる場合は、 **-e** と *err_file* 値の間に空白を入れないでください。  
  
 **-E**<a name="E"></a>   
 インポートしたデータ ファイルの ID 値 (複数可) を ID 列に使用することを指定します。 **-E** を指定しない場合、インポートされるデータ ファイルのこの列の ID 値は無視され、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] はテーブルの作成時に指定されたシードと増分の値に基づいて一意の値を自動的に割り当てます。  
  
 データ ファイルにテーブルまたはビュー内の ID 列の値が含まれない場合は、フォーマット ファイルを使用して、データのインポート時にテーブルまたはビュー内の ID 列を無視するように指定します。[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、一意な値が自動的にこの列に割り当てられます。 詳細については、「[DBCC CHECKIDENT &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)」をご覧ください。  
  
 **-E** オプションには、特別な権限が必要です。 詳細については、後の「[解説](#remarks)」を参照してください。  
   
 **-f** _**format\_file**_ <a name="f"></a>  
 フォーマット ファイルの完全パスを指定します。 このオプションの意味は、オプションが使用されている環境によって次のように異なります。  
  
-   **-f** を **format** オプションと共に使用した場合、指定されたテーブルまたはビューに対して、指定された *format_file* が作成されます。 XML フォーマット ファイルを作成するには、 **-x** オプションも指定します。 詳細については、「[フォーマット ファイルの作成 &#40;SQL Server&#41;](../relational-databases/import-export/create-a-format-file-sql-server.md)」をご覧ください。  
  
-   **in** または **out** オプションと共に使用する場合、 **-f** を使うには既存のフォーマット ファイルが必要です。  
  
    > [!NOTE]
    > **in** または **out** オプションを使う場合、フォーマット ファイルは省略可能です。 **-f** オプションを省略すると、 **-n**、 **-c**、 **-w**、または **-N** を指定しなかった場合に、コマンドによってフォーマット情報が要求され、それに対する応答がフォーマット ファイルに保存されます (既定のファイル名は Bcp.fmt)。
  
 *format_file* がハイフン (-) またはスラッシュ (/) で始まる場合は、 **-f** と *format_file* 値の間に空白を入れないでください。  
  
**-F** _**first\_row**_ <a name="F"></a>  
 テーブルからエクスポートする最初の行、またはデータ ファイルからインポートする最初の行の番号を指定します。 このパラメーターには、0 より大きく (> 0)、行の合計数以下 (< または =) となる値が必要です。 このパラメーターがない場合、既定ではファイルの最初の行となります。  
  
 *first_row* には、2^63-1 以下の正の整数を指定できます。 **-F** *first_row* is 1-based.  

**-G**<a name="G"></a>  
 このスイッチは、Azure SQL Database または Azure SQL Data Warehouse に接続し、Azure Active Directory 認証を使用してユーザーを認証するように指定する場合に、クライアントによって使用されます。 -G スイッチに[はバージョン 14.0.3008.27](https://go.microsoft.com/fwlink/?LinkID=825643)以降が必要です。 バージョンを判断するには、bcp -v を実行します。 詳細については、「 [SQL Database または SQL Data Warehouse での認証に Azure Active Directory 認証を使用する](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication)」を参照してください。 

> [!IMPORTANT]
> **-G** オプションは、Azure SQL Database と Azure Data Warehouse にのみ適用されます。
> AAD 統合認証および対話型認証は、現在、Linux または macOS ではサポートされていません。

> [!TIP]
>  お使いのバージョンの bcp に Azure Active Directory Authentication (AAD) 型の**bcp**がサポートされているかどうかを確認するには (bcp\<space >\<ダッシュ >\<ダッシュ >)、使用可能な引数の一覧に-G が表示されていることを確認します。

- **Azure Active Directory のユーザー名とパスワード:** 

    Azure Active Directory のユーザー名とパスワードを使用には、 **-G** オプションを指定します。ユーザー名とパスワードは、 **-U** オプションと **-P** オプションを指定する方法でも使用できます。 

    次の例では、ユーザーとパスワードが AAD 資格情報である Azure AD のユーザー名とパスワードを使用してデータをエクスポートします。 この例では、Azure server `bcptest` からデータベース `testdb` のテーブル `aadserver.database.windows.net` をエクスポートし、データをファイル `c:\last\data1.dat` に格納します。
    ``` 
    bcp bcptest out "c:\last\data1.dat" -c -t -S aadserver.database.windows.net -d testdb -G -U alice@aadtest.onmicrosoft.com -P xxxxx
    ``` 

    次の例では Azure AD ユーザー名とパスワードを使用してデータをインポートします。ユーザーとパスワードは AAD 資格情報です。 この例では、Azure AD のユーザー/パスワードを使用して、Azure サーバー `aadserver.database.windows.net` のデータベース `testdb` のテーブル `bcptest` に、ファイル `c:\last\data1.dat` からデータをインポートします。
    ```
    bcp bcptest in "c:\last\data1.dat" -c -t -S aadserver.database.windows.net -d testdb -G -U alice@aadtest.onmicrosoft.com -P xxxxx
    ```

- **Azure Active Directory 統合**

    Azure Active Directory 統合認証の場合、ユーザー名とパスワードなしで **-G** オプションを指定します。 この構成は、現在の Windows ユーザーアカウント (bcp コマンドが実行されているアカウント) が Azure AD とフェデレーションされていることを前提としています。 

    次の例では、Azure AD 統合アカウントを使用してデータをエクスポートします。 この例では、Azure server `aadserver.database.windows.net` から統合 Azure AD を使用してデータベース `testdb` からテーブル `bcptest` をエクスポートし、そのデータをファイル `c:\last\data2.dat`に格納します。

    ```
    bcp bcptest out "c:\last\data2.dat" -S aadserver.database.windows.net -d testdb -G -c -t
    ```

    次の例では、Azure AD 統合認証を使用してデータをインポートします。この例では、Azure AD 統合認証を使用して、Azure サーバー `aadserver.database.windows.net` のデータベース `testdb` のテーブル `bcptest` にファイル `c:\last\data2.txt` からデータをインポートします。

    ```
    bcp bcptest in "c:\last\data2.dat" -S aadserver.database.windows.net -d testdb -G -c -t
    ```

- **Azure Active Directory 対話型**  

   Azure AD Azure SQL Database および SQL Data Warehouse の対話型認証を使用すると、多要素認証をサポートする対話的な方法を使用できます。 詳細については、「 [Active Directory Interactive Authentication](../ssdt/azure-active-directory.md#active-directory-interactive-authentication)」を参照してください。 

   Azure AD interactive には、 **bcp** [バージョン 15.0.1000.34](#download-the-latest-version-of-bcp-utility)以降、および[ODBC バージョン 17.2](https://www.microsoft.com/download/details.aspx?id=56567)以降が必要です。  

   対話型認証を有効にするには、パスワードを指定せずに、-G オプションにユーザー名 (-U) のみを指定します。   

   次の例では Azure AD 対話型モードを使用してデータをエクスポートします。ユーザー名は AAD アカウントを表します。 これは、前のセクションで使用したのと同じ例です。 *Azure Active Directory ユーザー名とパスワード*です。  

   対話モードでは、パスワードを手動で入力するか、multi-factor authentication が有効になっているアカウントに対して、構成された MFA 認証方法を完了する必要があります。 

   ``` 
   bcp bcptest out "c:\last\data1.dat" -c -t -S aadserver.database.windows.net -d testdb -G -U alice@aadtest.onmicrosoft.com 
   ``` 

   Azure AD ユーザーが Windows アカウントを使用するドメインフェデレーションドメインである場合、コマンドラインで必要とされるユーザー名には、ドメインアカウントが含まれます (例: joe@contoso.com 下記参照)。   

   ```
   bcp bcptest out "c:\last\data1.dat" -c -t -S aadserver.database.windows.net -d testdb -G -U joe@contoso.com 
   ```

   ゲストユーザーが特定の Azure AD に存在し、bcp コマンドを実行するためのデータベースアクセス許可を持つ SQL DB に存在するグループの一部である場合は、ゲストユーザーのエイリアス ( *keith0@adventureworks.com* など) が使用されます。
  
**-h** _**"load hints**_ [ ,... *n*] **"** <a name="h"></a> データをテーブルまたはビューに一括インポートするときに使用するヒントを指定します。  
  
* **ORDER**( **_column_[ASC | DESC] [** , **..._n_])**  
データ ファイルのデータの並べ替え順序です。 インポートするデータをテーブル上のクラスター化インデックスに従って並べ替えると、一括インポートのパフォーマンスが向上します。 データ ファイルが異なる順序で並べ替えられている場合、つまり、クラスター化インデックス キーの順序以外で並べ替えられている場合、またはテーブルにクラスター化インデックスが存在しない場合、ORDER 句は無視されます。 指定する列の名前は、インポート先のテーブル内で有効な列の名前であることが必要です。 既定では、 **bcp** はデータ ファイルの並べ替えが行われていないことを前提としています。 最適な一括インポートのため、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、インポートするデータが並べ替えられているかどうかも検証されます。  
  
* **ROWS_PER_BATCH** **=** _**bb**_  
各バッチあたりのデータ行数 ( *bb*) です。 **-b** を指定しない場合に使うと、データ ファイル全体が 1 つのトランザクションとしてサーバーに送られます。 サーバーでは、*bb* の値に応じて一括読み込みの負荷が最適化されます。 ROWS_PER_BATCH の既定値はありません。  
  
* **KILOBYTES_PER_BATCH** **=** _**cc**_  
バッチごとのデータの概算キロバイト数 (KB) です ( *cc*)。 KILOBYTES_PER_BATCH の既定値はありません。  
  
* **TABLOCK**  
一括読み込み操作中に一括更新のテーブルレベルのロックが適用されます。これを指定しない場合、行レベルのロックが適用されます。 一括コピー操作時だけロックすることにより、テーブル ロックの競合が少なくなるので、このヒントはパフォーマンスを大幅に向上させます。 テーブルにインデックスがなく、 **TABLOCK** を指定した場合は、複数のクライアントで同時に 1 つのテーブルを読み込むことができます。 既定では、ロック動作はテーブル オプション **table lock on bulkload**によって決定されます。  
  
  > [!NOTE]
  > 対象テーブルがクラスター化列ストア インデックスの場合、複数の同時実行クライアントで読み込むための TABLOCK ヒントは不要です。インデックス内で同時実行スレッドそれぞれに個別の行グループが割り当てられ、データが読み込まれるためです。 詳細については、列ストア インデックスの概念に関するトピックを参照してください。
  
  **CHECK_CONSTRAINTS**  
  一括インポート操作中、対象テーブルまたはビューに対するすべての制約を検証します。 CHECK_CONSTRAINTS ヒントを指定しない場合、CHECK 制約および FOREIGN KEY 制約は無視され、操作の後でテーブルの制約は信頼されていないものとしてマークされます。  
  
  > [!NOTE]
  > UNIQUE、PRIMARY KEY、および NOT NULL 制約は常に適用されます。
  
  テーブル全体の制約は、任意の時点で必ず検証してください。 一括インポート操作の前にテーブルが空でなかった場合、制約を再検証するコストは、増分データに CHECK 制約を適用するコストを超える場合があります。 したがって、通常は、増分一括インポート時の制約チェックを有効にすることをお勧めします。  
  
  入力データに制約違反の行が含まれている場合などは、制約を無効 (既定の動作) にできます。 CHECK 制約を無効にした場合、データをインポートした後で、 [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを使用して無効なデータを削除できます。  
  
  > [!NOTE]
  > **bcp** によってデータ検証とデータ チェックが実行されるようになったため、無効なデータを含むデータ ファイルに対して実行した場合、このスクリプトは失敗する可能性があります。
  
  > [!NOTE]
  > **-m** *max_errors* スイッチは、制約チェックには適用されません。
  
* **FIRE_TRIGGERS**  
**in** 引数と共に指定されている場合、一括コピーの操作時に、コピー先のテーブル上で定義されている挿入トリガーを実行します。 FIRE_TRIGGERS が指定されていない場合は、挿入トリガーは実行されません。 FIRE_TRIGGERS は、 **out**引数、 **queryout**引数、および **format** 引数では無視されます。  
  
**-i** _**input\_file**_ <a name="i"></a>  
応答ファイルの名前を指定します。応答ファイルには、対話モード ( **-n**、 **-c**、 **-w**、または **-N** が指定されていないモード) で一括コピーを実行する場合の、各データ フィールドに関するコマンド プロンプトの質問への応答が含まれます。  
  
*input_file* がハイフン (-) またはスラッシュ (/) で始まる場合は、 **-i** と *input_file* 値の間に空白を入れないでください。  
  
**-k**<a name="k"></a>  
一括コピー操作時、空の列には、挿入される列の既定値ではなく、NULL 値が保持されます。 詳細については、「[一括インポート中の NULL の保持または既定値の使用 &#40;SQL Server&#41;](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)」をご覧ください。  
  
**-K** _**application\_intent**_ <a name="K"></a>   
アプリケーションがサーバーに接続するときのワークロードのタイプを宣言します。 指定できる値は、 **ReadOnly**だけです。 **-K** を指定しない場合、bcp ユーティリティでは Always On 可用性グループのセカンダリ レプリカへの接続がサポートされません。 詳細については、「[アクティブなセカンダリ: 読み取り可能なセカンダリ レプリカ &#40;Always On 可用性グループ&#41;](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)」を参照してください。  
  
**-l** _**login\_timeout**_ <a name="l"></a>  
ログインのタイムアウトを指定します。 -l オプションでは、サーバーへの接続の試行時に、SQL Server へのログインがタイムアウトするまでの秒数を指定します。 既定のログインタイムアウトは15秒です。 ログイン タイムアウトは、0 から 65,534 の数値にする必要があります。 指定した値が数値以外の場合、または範囲外の場合、bcp はエラー メッセージを生成します。 値が0の場合は、タイムアウトが無制限であることを示します。
  
**-L** _**last\_row**_ <a name="L"></a>  
テーブルからエクスポートする最後の行、またはデータ ファイルからインポートする最後の行の番号を指定します。 このパラメーターには、0 より大きく (> 0)、最後の行の番号以下 (< または =) となる値が必要です。 このパラメーターがない場合、既定ではファイルの最後の行となります。  
  
*last_row* には、2^63-1 以下の正の整数を指定できます。  
  
**-m** _**max\_errors**_ <a name="m"></a>  
**bcp** 操作が取り消される前に発生可能な構文エラーの最大数を指定します。 構文エラーは、対象となるデータ型へのデータの変換エラーを意味しています。 *max_errors* の合計では、制約違反など、サーバーでのみ検出できるエラーはすべて対象外となります。  
  
 **bcp** ユーティリティでコピーできない行は無視され、1 つのエラーとしてカウントされます。 このオプションが指定されない場合の既定値は 10 になります。  
  
> [!NOTE]
> **-m** オプションは、 **money** データ型または **bigint** データ型の変換にも適用されません。
  
**-n**<a name="n"></a>  
データのネイティブ (データベース) データ型を使用して一括コピー操作を実行します。 このオプションを使用すると、フィールドごとにプロンプトが表示されません。ネイティブ値が使用されます。  
  
詳細については、「[ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)」をご覧ください。  
  
**-N**<a name="N"></a>  
文字以外のデータについてはデータベースのネイティブなデータ型を使用し、文字データについては Unicode 文字を使用して、一括コピー操作を実行します。 **-w** オプションの代わりにこのオプションを使用すると、高いパフォーマンスが得られます。このオプションは、データ ファイルを使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスから別のインスタンスにデータを転送する場合に使用します。 フィールドごとにプロンプトは表示されません。 ANSI 拡張文字を含むデータを転送し、ネイティブ モードのパフォーマンスを利用する場合は、このオプションを使用します。  
  
 詳細については、「[Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)」をご覧ください。  
  
 データをエクスポートした後で、 **-N** を付けて bcp.exe を実行して同じテーブル スキーマにそのデータをインポートした場合、Unicode 以外の固定長の文字の列 (**char(10)** など) があると、切り捨ての警告が表示されることがあります。  
  
 この警告は、無視してもかまいません。 この警告を解決するには、 **-N** ではなく **-n**を使用する方法があります。  
  
 **-o** _**output\_file**_ <a name="o"></a>  
 コマンド プロンプトからリダイレクトされた出力を受け取るファイル名を指定します。  
  
 *output_file* がハイフン (-) またはスラッシュ (/) で始まる場合は、 **-o** と *output_file* 値の間に空白を入れないでください。  
  
 **-P** _**password**_ <a name="P"></a>  
 ログイン ID のパスワードを指定します。 このオプションを指定しない場合、 **bcp** コマンドによってパスワードが要求されます。 また、このオプションをコマンド プロンプトの最後にパスワードなしで使用すると、 **bcp** では既定のパスワード (NULL) が使用されます。  
  
> [!IMPORTANT]
> [!INCLUDE[ssNoteStrongPass](../includes/ssnotestrongpass-md.md)]
  
 パスワードをマスクする場合は、 **-P** オプションを **-U** オプションと共に指定しないでください。 **bcp** を **-U** オプションおよび他のスイッチと共に指定した後 ( **-P**は指定しない)、Enter キーを押すと、このコマンドによってパスワードが要求されます。 この方法を使用すると、入力時にパスワードが確実にマスクされます。  
  
 *password* がハイフン (-) またはスラッシュ (/) で始まる場合は、 **-P** と *password* 値の間に空白を入れないでください。  
  
 **-q**<a name="q"></a>  
 **bcp** ユーティリティと [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のインスタンス間の接続で、SET QUOTED_IDENTIFIERS ON ステートメントを実行します。 名前に空白や単一引用符が含まれるデータベース、所有者、テーブル、またはビューを指定する場合に、このオプションを使用します。 3 つの要素から成るテーブル名またはビュー名全体を、二重引用符 (" ") で囲みます。  
  
 空白や単一引用符を含むデータベース名を指定するには、 **-q** オプションを使用する必要があります。  
  
 **-q** は、 **-d**に渡される値には適用されません。  
  
 詳細については、後の「 [解説](#remarks)」を参照してください。  
  
 **-r** _**row\_term**_ <a name="r"></a>  
 行ターミネータを指定します。 既定値は **\n** (改行文字) です。 既定の行ターミネータをオーバーライドする場合、このパラメーターを使用します。 詳細については、「 [フィールド ターミネータと行ターミネータの指定 &#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)」を参照してください。  
  
 bcp.exe コマンドでは、行ターミネータを 16 進数表記で指定すると、値が 0x00 で切り捨てられます。 たとえば、0x410041 を指定した場合、使用されるのは 0x41 になります。  
  
 *row_term* がハイフン (-) またはスラッシュ (/) で始まる場合は、 **-r** と *row_term* 値の間に空白を入れないでください。  
  
 **-R**<a name="R"></a>  
 通貨、日付、時刻のデータを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に一括コピーする場合に、クライアント コンピューターのロケール設定に定義された地域別設定が使用されます。 既定の設定では、地域別設定は無視されます。  
  
 **-S** _**server\_name**_ [\\ _**instance\_name**_ ]<a name="S"></a> 接続先となる [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスを指定します。 サーバーを指定しない場合、 **bcp** ユーティリティは、ローカル コンピューター上の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の既定のインスタンスに接続されます。 ネットワーク上のリモート コンピューターまたはローカルの名前付きインスタンスから **bcp** コマンドを実行するときは、このオプションが必要です。 サーバー上にある [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の既定のインスタンスに接続するには、 *server_name*のみを指定します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の名前付きインスタンスに接続するには、_server\_name_ **\\** _instance\_name_ を指定します。  
  
 **-t** _**フィールド\_用語**_ <a name="t"></a>  
 フィールド ターミネータを指定します。 既定値は **\t** (タブ文字) です。 既定のフィールド ターミネータをオーバーライドする場合、このパラメーターを使用します。 詳細については、「[フィールド ターミネータと行ターミネータの指定 &#40;SQL Server&#41;](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)」をご覧ください。  
  
 bcp.exe コマンドでは、フィールド ターミネータを 16 進数表記で指定すると、値が 0x00 で切り捨てられます。 たとえば、0x410041 を指定した場合、使用されるのは 0x41 になります。  
  
 *field_term* がハイフン (-) またはスラッシュ (/) で始まる場合は、 **-t** と *field_term* 値の間に空白を入れないでください。  
  
 **-T**<a name="T"></a>  
 **bcp** ユーティリティが統合セキュリティを使用した信頼関係接続を使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に接続することを指定します。 ネットワーク ユーザーのセキュリティ資格情報である *login_id*および *password* は必要ありません。 **-T** を指定しない場合、正常にログインするには **-U** と **-P** を指定する必要があります。
 
> [!IMPORTANT]
> **bcp** ユーティリティが、統合セキュリティを使用したセキュリティ接続で [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に接続している場合は、 **user name** と *password* の組み合わせではなく、 *-T* オプション (セキュリティ接続) を使用します。 **bcp** ユーティリティが SQL Database または SQL Data Warehouse に接続している場合、Windows 認証または Azure Active Directory 認証の使用はサポートされません。 **-U** および **-P** オプションを使用します。 
  
 **-U** _**login\_id**_ <a name="U"></a>  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]への接続に使用されるログイン ID を指定します。  
  
> [!IMPORTANT]
> **bcp** ユーティリティが、統合セキュリティを使用したセキュリティ接続で [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に接続している場合は、 **user name** と *password* の組み合わせではなく、 *-T* オプション (セキュリティ接続) を使用します。 **bcp** ユーティリティが SQL Database または SQL Data Warehouse に接続している場合、Windows 認証または Azure Active Directory 認証の使用はサポートされません。 **-U** および **-P** オプションを使用します。
  
 **-v**<a name="v"></a>  
 **bcp** ユーティリティのバージョン番号と著作権に関する情報を報告します。  
  
 **-V** (**80** | **90** | **100** | **110** | **120** | **130)<a name="V"></a>  
 以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のデータ型を使用して一括コピー操作を実行します。 このオプションを使用すると、フィールドごとにプロンプトが表示されません。既定値が使用されます。  
  
 **80** = [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]  
  
 **90** = [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] および [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[ssSQL15](../includes/sssql15-md.md)]  
  
 たとえば、 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]でサポートされておらず、それ以降のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]で導入された型のデータを生成する場合は、-V80 オプションを使用します。  
  
 詳細については、「 [以前のバージョンの SQL Server からのネイティブ形式データおよび文字形式データのインポート](../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)」をご覧ください。  
  
 **-w**<a name="w"></a>  
 Unicode 文字を使用して一括コピー操作を実行します。 このオプションを使用すると、フィールドごとにプロンプトが表示されません。ストレージ型 **nchar** 、プレフィックスなし、フィールド区切り文字 **\t** (タブ)、および行ターミネータ **\n** (改行文字) が使用されます。 **-w** は **-c** と互換性がありません。  
  
 詳細については、「 [Unicode 文字形式を使用したデータのインポートまたはエクスポート &#40;SQL Server&#41;](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)」をご覧ください。  
  
 **-x**<a name="x"></a>  
 **format** および **-f** *format_file* オプションと共に使用し、既定の XML ではないフォーマット ファイルの代わりに XML ベースのフォーマット ファイルを生成します。 **-x** はデータのインポート時とエクスポート時には機能しません。 **format** および **-f** *format_file*の両方を指定せずに使用すると、エラーが生成されます。  

## 解説<a name="remarks"></a>

 **bcp** 13.0 クライアントは、 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] のツールをインストールしたときにインストールされます。 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] と以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の両方のツールがインストールされている場合、PATH 環境変数の値の順番によっては、 **bcp** 13.0 クライアントではなく、以前の **bcp** クライアントを使用している可能性があります。 この環境変数によって Windows で実行可能ファイルを探すときに使用されるディレクトリのセットが定義されます。 使用しているバージョンを確認するには、Windows のコマンド プロンプトで **bcp /v** コマンドを実行します。 コマンド パスを PATH 環境変数で設定する方法の詳細については、Windows のヘルプを参照してください。  
 
bcp ユーティリティは、[Microsoft SQL Server 2016 Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676) とは別にダウンロードすることもできます。  `ENU\x64\MsSqlCmdLnUtils.msi` または `ENU\x86\MsSqlCmdLnUtils.msi`を選択してください。

  
 XML フォーマット ファイルは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ツールが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client と共にインストールされている場合のみサポートされます。  
  
 **bcp** ユーティリティのある場所や、実行する方法、コマンド プロンプト ユーティリティの構文規則については、「[コマンド プロンプト ユーティリティ リファレンス &#40;データベース エンジン&#41;](../tools/command-prompt-utility-reference-database-engine.md)」をご覧ください。  
  
 データを一括インポートまたはエクスポート用に準備する方法については、「[一括エクスポートまたは一括インポートのデータの準備 &#40;SQL Server&#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)」をご覧ください。  
  
 一括インポートによって実行される行挿入操作がトランザクション ログに記録される条件について詳しくは、「 [一括インポートで最小ログ記録を行うための前提条件](../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)」をご覧ください。  

## <a name="native-data-file-support"></a>ネイティブ データ ファイルのサポート

 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]の **bcp** ユーティリティでは、 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]、 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]、 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]、および [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]と互換性のあるネイティブ データ ファイルがサポートされています。  

## <a name="computed-columns-and-timestamp-columns"></a>計算列とタイムスタンプ列

 計算列または **timestamp** 列にインポートされるデータ ファイル内の値は無視され、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] によって自動的に値が割り当てられます。 データ ファイルにテーブル内の計算列または **timestamp** 列の値が含まれない場合は、フォーマット ファイルを使用して、データのインポート時にテーブル内の計算列または **timestamp** 列を無視するように指定します。この列の値は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] によって自動的に割り当てられます。  
  
 計算列と **timestamp** 列は、通常どおり、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] からデータ ファイルに一括コピーされます。  

## <a name="specifying-identifiers-that-contain-spaces-or-quotation-marks"></a>空白や引用符を含む識別子の指定

 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 識別子には、空白や引用符などを埋め込むことができます。 これらの識別子は次のように扱う必要があります。  
  
-   コマンド プロンプトで空白や引用符を含む識別子またはファイル名を指定する場合、識別子を二重引用符 (" ") で囲みます。  
  
     たとえば、次の `bcp out` コマンドでは、 `Currency Types.dat`という名前のデータ ファイルが作成されます。  
  
    ```  
    bcp AdventureWorks2012.Sales.Currency out "Currency Types.dat" -T -c  
    ```  
  
-   空白や引用符を含むデータベース名を指定するには、 **-q** オプションを使用する必要があります。  
  
-   空白文字や引用符を含んでいる所有者、テーブル、またはビューの名前については、次のうちのいずれかを行うことができます。  
  
    -   **-q** オプションを指定します。  
  
    -   所有者名、テーブル名、またはビュー名を、引用符内でかっこ ([ ]) を使用して囲みます。  

## <a name="data-validation"></a>データの検証

 **bcp** によってデータ検証とデータ チェックが実行されるようになったため、無効なデータを含むデータ ファイルに対して実行した場合、このスクリプトは失敗する可能性があります。 たとえば、 **bcp** では次の検証が行われます。  
  
-   float データ型または real データ型のネイティブ表記が有効かどうか。  
  
-   Unicode データが偶数バイト長かどうか。  
  
 以前のリリースでは、クライアントが無効なデータにアクセスを試みるまでは失敗が発生することはありませんでしたが、以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] で一括インポート可能であった無効な形式のデータが、新しいバージョンでは読み込みに失敗する場合があります。 今回のリリースでは検証機能が追加されたため、一括読み込み後のクエリで発生する問題を最小限に抑えられます。  

## <a name="bulk-exporting-or-importing-sqlxml-documents"></a>SQLXML ドキュメントの一括エクスポートまたは一括インポート

 SQLXML データを一括エクスポートまたは一括インポートする場合、フォーマット ファイルのデータ型には次のいずれかを使用します。  
  
|データ型|結果|  
|---------------|------------|  
|SQLCHAR または SQLVARYCHAR|データは、クライアント コード ページまたは照合順序で暗黙的に指定されるコード ページで送られます。 結果は、フォーマット ファイルを指定せずに **-c** スイッチを指定した場合と同じです。|  
|SQLNCHAR または SQLNVARCHAR|データは Unicode として送られます。 結果は、フォーマット ファイルを指定せずに **-w** スイッチを指定した場合と同じです。|  
|SQLBINARY または SQLVARYBIN|データは変換なしで送られます。|  

## <a name="permissions"></a>アクセス許可

 **bcp out** 操作には、ソース テーブルでの SELECT 権限が必要です。  
  
 **bcp in** 操作には、対象となるテーブルでの SELECT/INSERT 権限が最低限必要となります。 また、次のうちのいずれかに該当する場合は、ALTER TABLE 権限が必要です。  
  
-   制約が存在するため、CHECK_CONSTRAINTS ヒントを指定しません。  
  
    > [!NOTE]
    > 制約の無効化は既定の動作です。 制約を明示的に有効にするには、CHECK_CONSTRAINTS ヒントと共に **-h** オプションを使用します。
  
-   トリガーが存在するため、FIRE_TRIGGER ヒントを指定しません。  
  
    > [!NOTE]
    > 既定では、トリガーは起動しません。 トリガーを明示的に起動するには、FIRE_TRIGGERS ヒントと共に **-h** オプションを使用します。
  
-   **-E** オプションを使用して、データ ファイルから ID 値をインポートします。  
  
> [!NOTE]
> [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]からは、対象テーブルでの ALTER TABLE 権限が必要となりました。 この新しい要件により、対象テーブルでの ALTER TABLE 権限がユーザー アカウントに与えられていないと、トリガーおよび制約チェックを実行しない **bcp** スクリプトは失敗する可能性があります。

## <a name="character-mode--c-and-native-mode--n-best-practices"></a>キャラクター モード (-c) およびネイティブ モード (-n) のベスト プラクティス

 このセクションでは、キャラクター モード (-c) およびネイティブ モード (-n) の推奨事項について説明します。  
  
-   (管理者/ユーザー) 可能であれば、ネイティブ形式 (-n) を使用して、区切り記号の問題を回避します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]を使用してエクスポートおよびインポートを行うには、ネイティブ形式を使用します。 データを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 以外のデータベースにインポートする場合は、データを[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] からエクスポートするときに -c または -w オプションを使用します。  
  
-   (管理者) BCP OUT を使用するときに、データを検証します。 たとえば、BCP OUT、BCP IN、その後 BCP OUT を使用する場合、データが正しくエクスポートされ、ターミネータ値がデータ値の一部として使用されていないことを確認します。 ターミネータ値とデータ値の競合を回避するために、-t および -r オプションを使用して、既定のターミネータ値をランダムな 16 進数値でオーバーライドすることを検討してください。  
  
-   (ユーザー) 実際の文字列値と競合する可能性を最小限に抑えるために、長くて一意のターミネータ (バイトまたはキャラクターの任意のシーケンス) を使用します。 これには、-t および -r オプションを使用します。  

## <a name="examples"></a>使用例

ここでは、次の例について説明します。

A. **bcp** ユーティリティ バージョンの特定

B. データ ファイルへのテーブル行のコピー (セキュリティ接続を使用)

C. データ ファイルへのテーブル行のコピー (混合モード認証を使用)

D. ファイルからテーブルへのデータのコピー

E. データ ファイルへの特定の列のコピー

F. データ ファイルへの特定の行のコピー

G. クエリからデータ ファイルへのデータのコピー

H. フォーマット ファイルの作成

I. フォーマット ファイルを使用した **bcp**での一括インポート

J. コード ページの指定

### <a name="example-test-conditions"></a>**テスト条件の例**

以下の例では、SQL Server (2016 以降) および Azure SQL Database 用の `WideWorldImporters` サンプル データベースを利用しています。  `WideWorldImporters` は [https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) からダウンロードできます。  サンプル データベースを復元する構文については、「 [RESTORE (Transact-SQL)](../t-sql/statements/restore-statements-transact-sql.md) 」を参照してください。  特記していない場合、この例では、Windows 認証を使用していること、および **bcp** コマンドを実行しているサーバー インスタンスへのセキュリティ接続があることを前提としています。  多くの例では、 `D:\BCP` というディレクトリを使用します。

以下のスクリプトでは、`WideWorldImporters.Warehouse.StockItemTransactions` テーブルの空のコピーを作成し、主キー制約を追加します。  SQL Server Management Studio (SSMS) で、次の T-SQL スクリプトを実行します。

```sql  
USE WideWorldImporters;  
GO  

SET NOCOUNT ON;

IF NOT EXISTS (SELECT * FROM sys.tables WHERE name = 'Warehouse.StockItemTransactions_bcp')     
BEGIN
    SELECT * INTO WideWorldImporters.Warehouse.StockItemTransactions_bcp
    FROM WideWorldImporters.Warehouse.StockItemTransactions  
    WHERE 1 = 2;  

    ALTER TABLE Warehouse.StockItemTransactions_bcp 
    ADD CONSTRAINT PK_Warehouse_StockItemTransactions_bcp PRIMARY KEY NONCLUSTERED 
    (StockItemTransactionID ASC);
END
```

> [!NOTE]
> 必要に応じて、 `StockItemTransactions_bcp` テーブルの全行を削除します。
>
> TRUNCATE TABLE WideWorldImporters.Warehouse.StockItemTransactions_bcp;

### <a name="a--identify-bcp-utility-version"></a>A.  **bcp** ユーティリティ バージョンの特定

コマンド プロンプトで、次のコマンドを入力します。

```
bcp -v
```
  
### <a name="b-copying-table-rows-into-a-data-file-with-a-trusted-connection"></a>B. データ ファイルへのテーブル行のコピー (セキュリティ接続を使用)

次の例は、`WideWorldImporters.Warehouse.StockItemTransactions` テーブルに対する **out** オプションを示しています。

- **基本** `StockItemTransactions_character.bcp` という名前のデータ ファイルを作成し、**文字**形式を使用してテーブルのデータをこのデータ ファイルにコピーします。

  コマンド プロンプトで、次のコマンドを入力します。

  ```
  bcp WideWorldImporters.Warehouse.StockItemTransactions out D:\BCP\StockItemTransactions_character.bcp -c -T
  ```

 - **拡張**  
`StockItemTransactions_native.bcp` という名前のデータ ファイルを作成し、 **ネイティブ** 形式を使用してテーブルのデータをこのデータ ファイルにコピーします。  この例では、構文エラーの最大数、エラー ファイル、出力ファイルも指定しています。

    コマンド プロンプトで、次のコマンドを入力します。
    ```
    bcp WideWorldImporters.Warehouse.StockItemTransactions OUT D:\BCP\StockItemTransactions_native.bcp -m 1 -n -e D:\BCP\Error_out.log -o D:\BCP\Output_out.log -S -T
    ```

`Error_out.log` と `Output_out.log`を確認します。  `Error_out.log` は、空白にする必要があります。  `StockItemTransactions_character.bcp` と `StockItemTransactions_native.bcp`のファイル サイズを比較します。 

### <a name="c-copying-table-rows-into-a-data-file-with-mixed-mode-authentication"></a>C. データ ファイルへのテーブル行のコピー (混合モード認証を使用)

次の例では、`WideWorldImporters.Warehouse.StockItemTransactions` テーブルに対して **out** オプションを実行します。  `StockItemTransactions_character.bcp` という名前のデータ ファイルを作成し、 **文字** 形式を使用してテーブルのデータをこのデータ ファイルにコピーします。  
  
 この例では、混合モード認証を使用していることを前提としているため、ログイン ID の指定に **-U** スイッチを使用する必要があります。 また、ローカル コンピューター上にある [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の既定のインスタンスに接続する以外の場合は、 **-S** スイッチを使用して、システム名と、オプションでインスタンス名を指定します。  

コマンド プロンプトに次のコマンドを入力します。 \(パスワードの入力が求められます。\)

```
bcp WideWorldImporters.Warehouse.StockItemTransactions out D:\BCP\StockItemTransactions_character.bcp -c -U<login_id> -S<server_name\instance_name>
```

### <a name="d-copying-data-from-a-file-to-a-table"></a>D. ファイルからテーブルへのデータのコピー

次の例は、上で作成したファイルを使用して、 **テーブルの** in `WideWorldImporters.Warehouse.StockItemTransactions_bcp` オプションを示しています。

- **基本** この例では、以前に作成した `StockItemTransactions_character.bcp` データ ファイルを使用します。

  コマンド プロンプトで、次のコマンドを入力します。

  ```
  bcp WideWorldImporters.Warehouse.StockItemTransactions_bcp IN D:\BCP\StockItemTransactions_character.bcp -c -T
  ```

- **拡張** この例では、以前に作成した `StockItemTransactions_native.bcp` データ ファイルを使用します。  この例では、ヒント **TABLOCK**を使用し、バッチ サイズ、構文エラーの最大数、エラー ファイル、出力ファイルも指定しています。
  
コマンド プロンプトで、次のコマンドを入力します。

```
bcp WideWorldImporters.Warehouse.StockItemTransactions_bcp IN D:\BCP\StockItemTransactions_native.bcp -b 5000 -h "TABLOCK" -m 1 -n -e D:\BCP\Error_in.log -o D:\BCP\Output_in.log -S -T
```

  `Error_in.log` と `Output_in.log`を確認します。

### <a name="e-copying-a-specific-column-into-a-data-file"></a>E. データ ファイルへの特定の列のコピー

特定の列をコピーする場合に、 **queryout** オプションを使用できます。  次の例では、 `StockItemTransactionID` テーブルの `Warehouse.StockItemTransactions` 列のみをデータ ファイルにコピーします。
  
コマンド プロンプトで、次のコマンドを入力します。

```
bcp "SELECT StockItemTransactionID FROM WideWorldImporters.Warehouse.StockItemTransactions WITH (NOLOCK)" queryout D:\BCP\StockItemTransactionID_c.bcp -c -T
```

### <a name="f-copying-a-specific-row-into-a-data-file"></a>F. データ ファイルへの特定の行のコピー

特定の行をコピーする場合に、 **queryout** オプションを使用できます。 次の例では、`Amy Trefl` という名前の個人の行のみを `WideWorldImporters.Application.People` テーブルからデータ ファイル `Amy_Trefl_c.bcp` へコピーします。  注: **-d** スイッチは、データベースの識別に使用されます。
  
コマンド プロンプトで、次のコマンドを入力します。

```
bcp "SELECT * from Application.People WHERE FullName = 'Amy Trefl'" queryout D:\BCP\Amy_Trefl_c.bcp -d WideWorldImporters -c -T
```

### <a name="g-copying-data-from-a-query-to-a-data-file"></a>G. クエリからデータ ファイルへのデータのコピー

Transact-SQL ステートメントからデータ ファイルに結果セットをコピーするには、 **queryout** オプションを使用します。  次の例では、フル ネームで並べ替えた名前を `WideWorldImporters.Application.People` テーブルから `People.txt` データ ファイルへコピーします。  注: **-t** スイッチは、コンマ区切りファイルを作成するために使用します。

コマンド プロンプトで、次のコマンドを入力します。

```
bcp "SELECT FullName, PreferredName FROM WideWorldImporters.Application.People ORDER BY FullName" queryout D:\BCP\People.txt -t, -c -T
```

### <a name="h-creating-format-files"></a>H. フォーマット ファイルの作成

次の例では、`WideWorldImporters` データベース内の `Warehouse.StockItemTransactions` テーブルに対して 3 種類のフォーマット ファイルを作成します。  作成した各ファイルの内容を確認します。

コマンド プロンプトで、次のコマンドを入力します。

```
REM non-XML character format
bcp WideWorldImporters.Warehouse.StockItemTransactions format nul -f D:\BCP\StockItemTransactions_c.fmt -c -T 

REM non-XML native format
bcp WideWorldImporters.Warehouse.StockItemTransactions format nul -f D:\BCP\StockItemTransactions_n.fmt -n -T

REM XML character format
bcp WideWorldImporters.Warehouse.StockItemTransactions format nul -f D:\BCP\StockItemTransactions_c.xml -x -c -T
```

> [!NOTE]
> **-x** スイッチを使用するには、 **bcp** 9.0 クライアントを使用している必要があります。 **bcp** 9.0 クライアントの使用方法の詳細については、「[解説](#remarks)」を参照してください。
  
 詳細については、「[XML 以外のフォーマット ファイル &#40;SQL Server&#41;](../relational-databases/import-export/non-xml-format-files-sql-server.md)」と「[XML フォーマット ファイル &#40;SQL Server&#41;](../relational-databases/import-export/xml-format-files-sql-server.md)」を参照してください。
  
### <a name="i-using-a-format-file-to-bulk-import-with-bcp"></a>I. フォーマット ファイルを使用した bcp での一括インポート

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のインスタンスにデータをインポートするときに、既に作成してあるフォーマット ファイルを使用するには、 **-f** スイッチを **in** オプションと共に使用します。  たとえば、次のコマンドは、作成済みのフォーマット ファイル ( `StockItemTransactions_character.bcp`) を使用して、データ ファイル ( `Warehouse.StockItemTransactions_bcp` ) の内容を `StockItemTransactions_c.xml`テーブルのコピーに一括コピーします。  注: **-L** スイッチは、最初の 100 レコードのみをインポートするために使用されます。

コマンド プロンプトで、次のコマンドを入力します。

```
bcp WideWorldImporters.Warehouse.StockItemTransactions_bcp in D:\BCP\StockItemTransactions_character.bcp -L 100 -f D:\BCP\StockItemTransactions_c.xml -T
```

> [!NOTE]  
>  フォーマット ファイルは、データ ファイルのフィールドとテーブル列の数、順序、データ型などが異なる場合に役立ちます。 詳細については、「 [データのインポートまたはエクスポート用のフォーマット ファイル &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)オプションと同時に使う場合はその知識が必要になります。  

### <a name="j-specifying-a-code-page"></a>J. コード ページの指定

次の部分的なコード例は、コード ページ 65001 を指定した bcp インポートを示しています。

```
bcp.exe MyTable in "D:\data.csv" -T -c -C 65001 -t , ...  
```

## <a name="additional-examples"></a>その他の例

|次のトピックでは、bcp の使用例を示します。 |
|---|
|一括インポートまたは一括エクスポートのデータ形式 (SQL Server)<br />&emsp;&#9679;&emsp;[ネイティブ形式を使用したデータのインポートまたはエクスポート (SQL Server)](../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[文字形式を使用したデータのインポートまたはエクスポート (SQL Server)](../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Unicode ネイティブ形式を使用したデータのインポートまたはエクスポート (SQL Server)](../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Unicode 文字形式を使用したデータのインポートまたはエクスポート (SQL Server)](../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)<br /><br />[フィールド ターミネータと行ターミネータの指定 (SQL Server)](../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)<br /><br />[一括インポート中の NULL の保持または既定値の使用 (SQL Server)](../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)<br /><br />[データの一括インポート時の ID 値の保持 (SQL Server)](../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)<br /><br />データのインポートまたはエクスポート用のフォーマット ファイル (SQL Server)<br />&emsp;&#9679;&emsp;[フォーマット ファイルの作成 (SQL Server)](../relational-databases/import-export/create-a-format-file-sql-server.md)<br />&emsp;&#9679;&emsp;[データの一括インポートでのフォーマット ファイルの使用 (SQL Server)](../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)<br />&emsp;&#9679;&emsp;[フォーマット ファイルを使用したテーブル列のスキップ (SQL Server)](../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)<br />&emsp;&#9679;&emsp;[フォーマット ファイルを使用したデータ フィールドのスキップ (SQL Server)](../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)<br />&emsp;&#9679;&emsp;[フォーマット ファイルを使用したテーブル列とデータ ファイル フィールドのマッピング (SQL Server)](../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)<br /><br />[XML ドキュメントの一括インポートと一括エクスポートの例 (SQL Server)](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)<br /><p>  </p>|

## <a name="see-also"></a>参照

 [一括エクスポートまたは一括インポートのデータの準備 &#40;SQL Server&#41;](../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../t-sql/functions/openrowset-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_tableoption &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)   
 [データのインポートまたはエクスポート用のフォーマット ファイル &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)

## <a name="feedback"></a>フィードバック

![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL クライアント ツール フォーラム](https://social.msdn.microsoft.com/Forums/home?forum=sqltools)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
