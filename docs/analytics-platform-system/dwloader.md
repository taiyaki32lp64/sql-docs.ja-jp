---
title: dwloader コマンドラインローダー
description: dwloader は、並列データウェアハウス (PDW) のコマンドラインツールで、テーブルの行を既存のテーブルに一括して読み込みます。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 8ea941e45f5125beed0820c5d5242b0f86073f76
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401176"
---
# <a name="dwloader-command-line-loader-for-parallel-data-warehouse"></a>Parallel Data Warehouse 用の dwloader コマンドラインローダー
**dwloader**は、並列データウェアハウス (PDW) のコマンドラインツールで、テーブルの行を既存のテーブルに一括して読み込みます。 行を読み込むときに、テーブルの末尾にすべての行を追加 (*追加モード*または*fastappend モード*) したり、新しい行を追加して既存の行を更新 (*upsert モード*) したり、読み込み前に既存のすべての行を削除してから、すべての行を空のテーブルに挿入したり (*再読み込みモード*) できます。  
  
**データを読み込むためのプロセス**  
  
1.  ソース データを準備します。  
  
    独自の ETL プロセスを使用して、読み込むソースデータを作成します。 コピー元のデータは、変換先テーブルのスキーマに一致するように書式設定されている必要があります。 ソースデータを1つまたは複数のテキストファイルに格納し、そのテキストファイルを読み込んでいるサーバー上の同じディレクトリにコピーします。 読み込みサーバーの詳細については、「[読み込みサーバーの取得と構成](acquire-and-configure-loading-server.md)」を参照してください。  
  
2.  読み込みオプションを準備します。  
  
    使用する読み込みオプションを決定します。 読み込みオプションを構成ファイルに格納します。 構成ファイルを、読み込んでいるサーバー上のローカルの場所にコピーします。 **Dwloader**の構成オプションについては、このトピックで説明します。  
  
3.  読み込みエラーのオプションを準備します。  
  
    **Dwloader**で読み込みに失敗した行をどのように処理するかを決定します。 読み込みを実行するために、 **dwloader**はまずデータをステージングテーブルに読み込み、次にデータをコピー先テーブルに転送します。 ローダーは、ステージングテーブルにデータを読み込むときに、読み込みに失敗した行の数を追跡します。 たとえば、正しく書式設定されていない行は読み込みに失敗します。 失敗した行は、拒否ファイルにコピーされます。 既定では、別の拒否のしきい値を指定しない限り、最初の拒否の後に負荷が中止されます。  
  
4.  **Dwloader**をインストールします。  
  
    まだインストールされていない場合は、読み込みサーバーに dwloader をインストールします。 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  **Dwloader**を実行します。  
  
    読み込み中のサーバーにサインインし、適切なコマンドラインオプションを使用して実行可能な**dwloader**を実行します。  
  
6.  結果を確認します。  
  
    失敗した行ファイル (-R で指定) を確認すると、読み込みに失敗した行があるかどうかを確認できます。 このファイルが空の場合、すべての行が正常に読み込まれます。 **dwloader**はトランザクションであるため、(拒否された行以外の) いずれかのステップが失敗した場合、すべてのステップが初期状態にロールバックされます。  
  
<!-- 
![Topic link icon](media/topic-link.gif "Topic_Link")[Syntax Conventions](syntax-conventions-sql-server-pdw.md)  
-->  


## <a name="syntax"></a>構文  
  
```  
dwloader.exe { -h }  
  
dwloader.exe   
    {  
        { -U login_name  -P password  }  
        | -W  
    }  
    [ -f parameter_file ]  
    [ -S target_appliance ]  
    { -T target_database_name . [ schema ] . table_name }   
    { -i source_data_location } [ <source_data_options> ]  
    { -R load_failure_file_name } [ <load_failure_options> ]  
    [ <loading_options> ]  
}  
  
<source_data_options> ::=  
{  
    [ -fh number_header_rows ]  
    [ < variable_length_column_options > | < fixed_width_column_options > ]  
    [ -D { mdy | myd | ymd | ydm | dmy | dym | custom_date_format } ]  
    [ -dt datetime_format_file ]  
}  
  
<variable_length_column_options> ::=  
{  
    [ -e character_encoding ]  
    -r row_delimiter   
    [ -s string_delimiter ]  
    -t field_delimiter   
}  
  
<fixed_width_column_options> ::=  
{  
    -w fixed_width_config_file   
    [ -e character_encoding ]   
    -r row_delimiter   
}  
  
<load_failure_options> ::=  
{  
    [ -rt { value | percentage } ]  
    [ -rv reject_value ]  
    [ -rs reject_sample_value ]  
}  
  
<loading_options> ::=  
{  
    [ -d staging_database_name ]  
    [ -M { append | fastappend | upsert -K merge_column [ ,...n ] | reload } ]  
    [ -b batchsize ]   
    [ -c ]  
    [ -E ]  
    [ -m ]  
    [ -N ]  
    [ -se ]
    [ -l ]   
}  
```  
  
## <a name="arguments"></a>引数  
**-h**  
ローダーの使用に関する簡単なヘルプ情報を表示します。 他のコマンドラインパラメーターが指定されていない場合にのみ、ヘルプが表示されます。  
  
**-U** *login_name*  
負荷を実行するための適切なアクセス許可を持つ有効な SQL Server 認証ログイン。  
  
**-P** *パスワード*  
SQL Server 認証*login_name*のパスワード。  
  
**-W**  
Windows 認証を使用します。 ( *Login_name*または*パスワード*は必要ありません)。 

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *parameter_file_name*  
コマンドラインパラメーターの代わりにパラメーターファイル*parameter_file_name*を使用します。 *parameter_file_name*には、 *user_name*と*パスワード*を除く任意のコマンドラインパラメーターを含めることができます。 パラメーターがコマンドラインとパラメーターファイルに指定されている場合、コマンドラインはファイルパラメーターをオーバーライドします。  
  
パラメーターファイルには、プレフィックスの**-** ない1つのパラメーターが行ごとに含まれています。  
  
例:  
  
`rt=percentage`  
  
`rv=25`  
  
**-S** *target_appliance*  
読み込まれたデータを受信する SQL Server PDW アプライアンスを指定します。  
  
*Infiniband 接続の*場合、 *target_appliance*は <アプライアンス名>-SQLCTL01 として指定されます。 この名前付き接続を構成するには、「 [Configure InfiniBand Network Adapters](configure-infiniband-network-adapters.md)」を参照してください。  
  
イーサネット接続の場合、 *target_appliance*は制御ノードクラスターの IP アドレスです。  
  
省略した場合、dwloader のインストール時に指定した値が既定値に設定されます。 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**-T** *target_database_name。*[*スキーマ*]。*table_name*  
コピー先テーブルの3部構成の名前。  
  
**-I** *source_data_location*  
読み込む1つ以上のソースファイルの場所。 各ソースファイルは、テキストファイルであるか、gzip で圧縮されたテキストファイルである必要があります。 各 gzip ファイルに圧縮できるソースファイルは1つだけです。  
  
ソースファイルをフォーマットするには:  
  
-   ソースファイルは、読み込みオプションに従ってフォーマットする必要があります。  
  
-   ソースファイル内の各行には、1つのテーブル行のデータが含まれています。 ソースデータは、変換先テーブルのスキーマと一致している必要があります。 列の順序とデータ型も一致する必要があります。 行内の各フィールドは、変換先テーブルの列を表します。  
  
-   既定では、フィールドは可変長で区切り記号で区切られます。 区切り記号の種類を指定するには、<variable_length_column_options> のコマンドラインオプションを使用します。 固定長フィールドを指定するには、<fixed_width_column_options> のコマンドラインオプションを使用します。  
  
ソースデータの場所を指定するには:  
  
-   ソースデータの場所には、ネットワークパスまたは読み込み元のサーバー上のディレクトリへのローカルパスを指定できます。  
  
-   ディレクトリ内のすべてのファイルを指定するには、ディレクトリパスを入力し、その後に * ワイルドカード文字を入力します。  ローダーは、ソースデータの場所にあるサブディレクトリからファイルを読み込みません。 ディレクトリが gzip ファイルに存在する場合のローダーエラー。  
  
-   ディレクトリ内の一部のファイルを指定するには、文字と * ワイルドカードの組み合わせを使用します。  
  
1つのコマンドで複数のファイルを読み込むには、次のようにします。  
  
-   すべてのファイルが同じディレクトリに存在する必要があります。  
  
-   ファイルは、すべてのテキストファイル、すべての gzip ファイル、またはテキストファイルと gzip ファイルの組み合わせである必要があります。  
  
-   ファイルにヘッダー情報を含めることはできません。  
  
-   すべてのファイルは、同じ文字エンコードの種類を使用する必要があります。 -E オプションを参照してください。  
  
-   すべてのファイルを同じテーブルに読み込む必要があります。  
  
-   すべてのファイルは1つのファイルと同じように連結されて読み込まれ、拒否された行は1つの拒否ファイルに送られます。  
  
例:  
  
-   -i \\、load、毎日\\* gz  
  
-   -i \\\ load\ \ (毎日\\) * .txt  
  
-   -i \\\loadserver\loads\daily\monday. *  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\\ 1 日に1回\\*  
  
**-R** *load_failure_file_name*  
読み込みエラーが発生した場合、 **dwloader**は、読み込みに失敗した行とエラーの説明を*load_failure_file_name*という名前のファイルに格納します。 このファイルが既に存在する場合は、dwloader によって既存のファイルが上書きされます。 *load_failure_file_name*は、最初のエラーが発生したときに作成されます。 すべての行が正常に読み込まれた場合、 *load_failure_file_name*は作成されません。  
  
**-fh** *number_header_rows*  
*Source_data_file_name*の開始時に無視する行 (行) の数。 既定値は 0 です。  
  
<variable_length_column_options>  
文字区切りの可変長列を含む*source_data_file_name*のオプション。 既定では、 *source_data_file_name*には可変長列に ASCII 文字が含まれています。  
  
ASCII ファイルの場合、区切り記号を連続して配置することで Null が表現されます。 たとえば、パイプで区切られたファイル ("|") では、"| |" によって NULL が示されます。 コンマ区切りのファイルでは、",," によって NULL が示されます。 また、 **-E** (--emptystringasnull) オプションを指定する必要があります。 -E の詳細については、以下を参照してください。  
  
**-e** *character_encoding*  
データファイルから読み込むデータの文字エンコーディングの種類を指定します。 オプションは ASCII (既定)、UTF8、UTF16、または UTF16BE です。この場合、UTF16 はリトルエンディアン、UTF16BE はビッグエンディアンです。 これらのオプションでは大文字と小文字が区別されます。  
  
**-t** *field_delimiter*  
行の各フィールド (列) の区切り記号。 フィールド区切り記号は、これらの ASCII エスケープ文字または ASCII 16 進値の1つ以上です。  
  
|名前|Escape Character|16進文字|  
|--------|--------------------|-----------------|  
|Tab|\t|0x09|  
|復帰 (CR)|\r|0x0d|  
|ラインフィード (LF)|\n|0x0a|  
|CRLF|\r\n|0x0d0x0a|  
|コンマ|','|0x2c|  
|二重引用符|\\"|0x22|  
|単一引用符|\\'|0x27|  
  
パイプ文字をコマンドラインで指定するには、二重引用符 "|" で囲みます。 これは、コマンドラインパーサーによって誤って解釈されることを回避します。 その他の文字は単一引用符で囲みます。  
  
例:  
  
-t "|"  
  
-t ' '  
  
-t 0x0a  
  
-t \t  
  
-t ' ~ | ~ '  
  
**-r** *row_delimiter*  
ソースデータファイルの各行の区切り記号。 行区切り記号は、1つまたは複数の ASCII 値です。  
  
キャリッジリターン (CR)、改行 (LF)、またはタブ文字を区切り記号として指定するには、エスケープ文字 (\r、\n、\t) または16進値 (0x、0d、09) を使用できます。 その他の特殊文字を区切り記号として指定するには、16進値を使用します。  
  
CR + LF の例:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR の例:  
  
-r \r  
  
-r 0x0d  
  
LF の例:  
  
-r \n  
  
-r 0x0a  
  
Unix には LF が必要です。 Windows には CR が必要です。  
  
**-s** *string_delimiter*  
テキスト区切りの入力ファイルの文字列データ型フィールドの区切り記号。 文字列の区切り記号は、1つまたは複数の ASCII 値です。  これは、文字 (たとえば、-s *) として、または16進数値として指定できます (例:-s 0x22 (二重引用符の場合))。  
  
例:  
  
2$s  
  
-s 0x22  
  
< fixed_width_column_options>  
固定長列を含むソースデータファイルのオプションです。 既定では、 *source_data_file_name*には可変長列に ASCII 文字が含まれています。  
  
-E が UTF8 の場合、固定幅列はサポートされません。  
  
**-w** *fixed_width_config_file*  
各列の文字数を指定する構成ファイルのパスと名前。 すべてのフィールドを指定する必要があります。  
  
このファイルは、読み込み中のサーバー上に存在する必要があります。 パスには、UNC、相対パス、または絶対パスを指定できます。 *Fixed_width_config_file*の各行には、1つの列の名前とその列の文字数が含まれています。 次のように、列ごとに1つの行があり、ファイル内の順序は、コピー先のテーブルの順序と一致している必要があります。  
  
*column_name*=*num_chars*  
  
*column_name*=*num_chars*  
  
固定幅構成ファイルの例:  
  
SalesCode = 3  
  
SalesID = 10  
  
*Source_data_file_name*の行の例:  
  
230Shirts0056  
  
320To、S1356  
  
前の例では、最初に読み込まれた行に SalesCode = ' 230 ' と Salescode = ' Shirts0056 ' が設定されています。 2番目に読み込まれた行には、SalesCode = ' 320 ' と SaleID = ' Towels1356 ' が含まれます。  
  
固定幅モードでの先頭および末尾のスペースまたはデータ型の変換を処理する方法については、「 [dwloader のデータ型変換規則](dwloader-data-type-conversion-rules.md)」を参照してください。  
  
**-e** *character_encoding*  
データファイルから読み込むデータの文字エンコーディングの種類を指定します。 オプションは ASCII (既定)、UTF8、UTF16、または UTF16BE です。この場合、UTF16 はリトルエンディアン、UTF16BE はビッグエンディアンです。 これらのオプションでは大文字と小文字が区別されます。  
  
-E が UTF8 の場合、固定幅列はサポートされません。  
  
**-r** *row_delimiter*  
ソースデータファイルの各行の区切り記号。 行区切り記号は、1つまたは複数の ASCII 値です。  
  
キャリッジリターン (CR)、改行 (LF)、またはタブ文字を区切り記号として指定するには、エスケープ文字 (\r、\n、\t) または16進値 (0x、0d、09) を使用できます。 その他の特殊文字を区切り記号として指定するには、16進値を使用します。  
  
CR + LF の例:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
CR の例:  
  
-r \r  
  
-r 0x0d  
  
LF の例:  
  
-r \n  
  
-r 0x0a  
  
Unix には LF が必要です。 Windows には CR が必要です。  
  
**-D** { **ymd** | ydm | mdy | myd | dmy |dym |*custom_date_format* }  
入力ファイル内のすべての datetime フィールドの月 (m)、日 (d)、および年 (y) の順序を指定します。 既定の順序は ymd です。 同じソースファイルに対して複数の注文形式を指定するには、-dt オプションを使用します。  
  
ymd |dmy  
ydm と dmy では、同じ入力形式を使用できます。 どちらも、年を日付の先頭または末尾にすることができます。 たとえば、 **ydm**と**dmy**の両方の日付形式の場合、入力ファイルに2013-02-03 または02-03-2013 を含めることができます。  
  
ydm  
データ型が datetime および smalldatetime の列には、ydm として書式設定された入力のみを読み込むことができます。 Datetime2、date、または datetimeoffset データ型の列に ydm 値を読み込むことはできません。  
  
mdy  
mdy が<month> <space> <day> <comma>許可<year>します。  
  
1975年1月1日の mdy 入力データの例を次に示します。  
  
-   1975年1月1日  
  
-   75年1月01日  
  
-   Jan/1/75  
  
-   01011975  
  
myd  
2010年3月4日の入力ファイルの例 (2010: 03-2010-04、3/2010/4)  
  
dym  
2010年3月4日の入力ファイルの例: 04-2010-03、4/2010/3  
  
*custom_date_format*  
*custom_date_format*はカスタム日付形式 (例: MM/dd/yyyy) であり、旧バージョンとの互換性のためだけに含まれています。 dwloader では、カスタムの日付形式が適用されません。 代わりに、カスタム日付形式を指定すると、 **dwloader**は、ymd、ydm、mdy、myd、dym、または dmy の対応する設定に変換します。  
  
たとえば、-D MM/dd/yyyy を指定した場合、dwloader では、すべての日付入力が month first、day、year (mdy) で並べ替えられることを想定しています。 カスタム日付形式で指定されているように、2文字の月、2桁の日、および4桁の年は適用されません。 ここでは、日付形式が-D MM/dd/yyyy: 01/02/2013、02.2013、1/2/2013 の場合に、入力ファイルで日付を書式設定する方法の例をいくつか示します。  
  
より包括的な書式設定情報については、「 [dwloader のデータ型変換規則](dwloader-data-type-conversion-rules.md)」を参照してください。  
  
**-dt** *datetime_format_file*  
各 datetime 形式は、 *datetime_format_file*という名前のファイルで指定されます。 コマンドラインパラメーターとは異なり、スペースを含むファイルパラメーターを二重引用符で囲むことはできません。 データの読み込み時に datetime 形式を変更することはできません。 コピー先のテーブルのソースデータファイルとそれに対応する列の形式は同じである必要があります。  
  
各行には、変換先テーブルの列の名前とその datetime 形式が含まれています。  
  
例:  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d** *staging_database_name*  
ステージングテーブルを格納するデータベース名。 既定値は、-T オプションで指定されたデータベースです。これは、変換先テーブルのデータベースです。 ステージングデータベースの使用方法の詳細については、「[ステージングデータベースの作成](staging-database.md)」を参照してください。  
  
**-M** *load_mode_option*  
データを追加、upsert、または再読み込みするかどうかを指定します。 既定のモードは append です。  
  
append  
ローダーは、変換先テーブルの既存の行の末尾に行を挿入します。  
  
fastappend  
ローダーは、一時テーブルを使用せずに、コピー先テーブルの既存の行の末尾に行を直接挿入します。 fastappend には、マルチトランザクション (-m) オプションが必要です。 Fastappend を使用する場合、ステージングデータベースを指定することはできません。 Fastappend のロールバックはありません。これは、失敗または中止された負荷からの復旧を、独自の読み込みプロセスで処理する必要があることを意味します。  
  
upsert *****merge_column* [,...*n* ]    
ローダーは、SQL Server Merge ステートメントを使用して、既存の行を更新し、新しい行を挿入します。  
  
-K オプションは、マージの基準となる列を指定します。 これらの列は、一意の行を表すマージキーを形成します。 マージキーが変換先テーブルに存在する場合は、行が更新されます。 マージキーが変換先テーブルに存在しない場合は、行が追加されます。  
  
ハッシュ分散テーブルの場合、merge キーはディストリビューション列にする必要があります。  
  
レプリケートされたテーブルの場合、merge キーは1つ以上の列の組み合わせです。 これらの列は、アプリケーションのニーズに応じて指定されます。  
  
複数の列は、スペースを使用しないでコンマで区切る必要があります。または、コンマ区切りでスペースで区切り、単一引用符で囲む必要があります。  
  
ソーステーブルの2つの行が一致するマージキーの値を持つ場合、それぞれの行が同一である必要があります。  
  
直し  
ローダーは、ソースデータを挿入する前に、変換先テーブルを切り捨てます。  
  
**-b** *batchsize*  
Microsoft サポートで使用する場合にのみ推奨されます。 *batchsize*は、DMS が計算ノードの SQL Server インスタンスに対して実行する一括コピーの SQL Server バッチサイズです。  *Batchsize*を指定すると、SQL Server PDW によって、各負荷に対して動的に計算されるバッチ読み込みサイズが上書きされます。  
  
SQL Server 2012 PDW 以降では、コントロールノードは、既定で各負荷のバッチサイズを動的に計算します。 この自動計算は、メモリサイズ、ターゲットテーブル型、ターゲットテーブルスキーマ、読み込みの種類、ファイルサイズ、ユーザーのリソースクラスなど、いくつかのパラメーターに基づいています。  
  
たとえば、読み込みモードが FASTAPPEND で、テーブルにクラスター化列ストアインデックスがある場合、SQL Server PDW は既定では1048576のバッチサイズを使用しようとします。これにより、行グループが閉じられ、列ストアに直接読み込まれます。デルタストア。 メモリでバッチサイズ1048576が許可されていない場合、dwloader は小さい batchsize を選択します。  
  
読み込みの種類が FASTAPPEND の場合、 *batchsize*はテーブルへのデータの読み込みに適用されます。それ以外の場合は、データをステージングテーブルに読み込む場合に*batchsize*が適用されます。  
  
<reject_options>  
ローダーが許可する読み込みエラーの数を決定するためのオプションを指定します。 読み込みエラーがしきい値を超えると、ローダーは停止し、行はコミットされません。  
  
**-rt** { **value** | パーセント}  
**-Rv** *reject_value*オプションの-*reject_value*がリテラルの行数 (値) であるか、または失敗率 (%) であるかを指定します。 既定値は value です。  
  
割合オプションは、-rs オプションに従って間隔で実行されるリアルタイムの計算です。  
  
たとえば、ローダーが100行の読み込みを試行し、25回失敗し、75が成功した場合、エラー率は25% になります。  
  
**-rv** *reject_value*  
読み込みを停止するまでに許可する行の拒否の数または割合を指定します。 **-Rt**オプションは、 *reject_value*が行の数または行の割合を参照するかどうかを決定します。  
  
既定の*reject_value*は0です。  
  
-Rt 値と共に使用すると、ローダーは、拒否された行数が reject_value を超えたときに負荷を停止します。  
  
-Rt パーセントを使用する場合、ローダーは間隔 (-rs オプション) で割合を計算します。 したがって、失敗した行の割合は*reject_value*を超える可能性があります。  
  
**-rs** *reject_sample_size*  
`-rt percentage`オプションと共に使用して、増分パーセンテージチェックを指定します。 たとえば、reject_sample_size が1000の場合、ローダーは1000行の読み込みを試行した後に失敗した行の割合を計算します。 追加の1000行の読み込みを試行した後、失敗した行の割合を再計算します。  
  
**-c**  
Char、nchar、varchar、および nvarchar の各フィールドの左辺と右辺から空白文字を削除します。 空白文字のみを含む各フィールドを空の文字列に変換します。  
  
例:  
  
' ' は ' ' に切り捨てられます。  
  
' abc ' は ' abc ' に切り捨てられます  
  
-C を-E と共に使用すると、-E 操作が最初に実行されます。 空白文字のみを含むフィールドは、NULL ではなく、空の文字列に変換されます。  
  
**-E**  
空の文字列を NULL に変換します。 既定では、これらの変換は実行されません。  
  
**-m**  
読み込みの2番目のフェーズでは、マルチトランザクションモードを使用します。ステージングテーブルから分散テーブルにデータを読み込む場合。  
  
**-M**を使用すると、SQL Server PDW は並行して負荷を実行し、コミットします。 この動作は、既定の読み込みモードよりもはるかに高速ですが、トランザクションセーフではありません。  
  
**-M**を指定しない場合、SQL Server PDW は、各コンピューティングノード内のディストリビューション全体、および計算ノード間で同時に負荷を分散します。 この方法は、マルチトランザクションモードよりも低速ですが、トランザクションセーフです。  
  
**-m**は、 *append*、 *reload*、および*upsert*では省略可能です。  
  
fastappend には **、-m**が必要です。  
  
**-m は、** レプリケートされたテーブルでは使用できません。  
  
**-m**は、2番目の読み込みフェーズにのみ適用されます。 最初の読み込みフェーズには適用されません。ステージングテーブルにデータを読み込んでいます。  
  
マルチトランザクションモードのロールバックはありません。つまり、失敗した負荷または中止された負荷からの復旧は、独自の負荷プロセスによって処理される必要があります。  
  
データを失わずに復旧できるように、空のテーブルに読み込む場合にのみ **-m**を使用することをお勧めします。 読み込みエラーから復旧するには、変換先テーブルを削除し、読み込みの問題を解決して、変換先テーブルを再作成してから、再度読み込みます。  
  
**-N**  
ターゲットアプライアンスが、信頼された機関からの有効な SQL Server PDW 証明書を持っていることを確認します。 これを使用すると、攻撃者によってデータがハイジャックされないようにして、不正な場所に送信することができます。 証明書はアプライアンスに既にインストールされている必要があります。 証明書をインストールする唯一の方法として、アプライアンス管理者が Configuration Manager ツールを使用してインストールする方法があります。 アプライアンスに信頼された証明書がインストールされているかどうかわからない場合は、アプライアンス管理者に問い合わせてください。  
  
**-se**  
空のファイルの読み込みをスキップします。 これにより、空の gzip ファイルの圧縮解除もスキップします。

**-l**  
CU 7.4 更新プログラムで使用可能で、読み込むことができる行の最大長 (バイト単位) を指定します。 有効な値は、32768 ~ 33554432 の整数です。 クライアントとサーバーにより多くのメモリが割り当てられるため、必要な場合にのみを使用して大きな行 (32 KB より大きい) を読み込みます。
  
## <a name="return-code-values"></a>リターン コードの値  
0 (成功) またはその他の整数値 (失敗)  
  
コマンドウィンドウまたはバッチファイルで、を`errorlevel`使用してリターンコードを表示します。 例:  
  
```  
dwloader  
echo ReturnCode=%errorlevel%  
if not %errorlevel%==0 echo Fail  
if %errorlevel%==0 echo Success  
```  
  
PowerShell を使用する場合`$LastExitCode`は、を使用します。  
  
## <a name="permissions"></a>アクセス許可  
コピー先のテーブルには、読み込み権限と適用可能な権限 (INSERT、UPDATE、DELETE) が必要です。 ステージングデータベースに CREATE 権限 (一時テーブルを作成する場合) が必要です。 ステージングデータベースが使用されていない場合は、コピー先データベースに対して CREATE 権限が必要です。 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>全般的な解説  
Dwloader での読み込み時のデータ型変換の詳細については、「 [dwloader のデータ型変換規則](dwloader-data-type-conversion-rules.md)」を参照してください。  
  
パラメーターに1つ以上のスペースが含まれている場合は、パラメーターを二重引用符で囲みます。  
  
ローダーは、インストールされている場所から実行する必要があります。 Dwloader 実行可能ファイルはアプライアンスと共にプレインストールされ、C:\Program モジュール SQL Server Data Warehouse\DWLoader ディレクトリにあります。  
  
パラメーターファイルに指定されているパラメーター (-f オプション) は、コマンドラインパラメーターとして指定することによってオーバーライドできます。  
  
ローダーの複数のインスタンスを同時に実行できます。 ローダーインスタンスの最大数は事前に構成されており、変更することはできません。 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
読み込まれたデータは、ソースの場所よりもアプライアンス上の領域が必要になる場合があります。 データのサブセットを使用してテストインポートを実行し、ディスクの使用量を見積もることができます。  
  
**Dwloader**はトランザクションプロセスであり、エラーが発生した場合には正常にロールバックされますが、一括読み込みが正常に完了したらロールバックすることはできません。 アクティブな**dwloader**プロセスをキャンセルするには、CTRL + C キーを押します。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
同時に発生するすべての負荷の合計サイズは、データベースの LOG_SIZE よりも小さくする必要があります。同時読み込みの合計サイズは、LOG_SIZE の50% 未満にすることをお勧めします。 このサイズ制限を実現するために、大きな負荷を複数のバッチに分割できます。 LOG_SIZE の詳細については、「 [CREATE DATABASE](../t-sql/statements/create-database-parallel-data-warehouse.md) 」を参照してください。  
  
1つの load コマンドを使用して複数のファイルを読み込む場合、拒否されたすべての行が同じ拒否ファイルに書き込まれます。 拒否ファイルには、拒否された各行を含む入力ファイルは表示されません。  
  
空の文字列を区切り記号として使用することはできません。 空の文字列が行区切り記号として使用されている場合、読み込みは失敗します。 列区切り記号として使用する場合、読み込みでは区切り記号が無視され、既定の "|" が列区切り記号として使用されます。 文字列の区切り記号として使用すると、空の文字列は無視され、既定の動作が適用されます。  
  
## <a name="locking-behavior"></a>ロック動作  
**dwloader**のロック動作は、 *load_mode_option*によって異なります。  
  
-   **append** -append は推奨され、最も一般的なオプションです。 追加、ステージングテーブルにデータを読み込みます。 ロックについては、以下で詳しく説明します。  
  
-   **高速 append** -高速追加は、ExclusiveUpdate テーブルロックを取得する最終テーブルに直接読み込まれます。ステージングテーブルを使用しないモードは、このモードのみです。  
  
-   **再**読み込み-再読み込みを行うと、データがステージングテーブルに読み込まれ、ステージングテーブルと最終テーブルの両方に排他ロックが必要になります。 同時実行操作では、再読み込みは推奨されません。  
  
-   **upsert** upsert は、ステージングテーブルにデータを読み込み、ステージングテーブルから最終的なテーブルへのマージ操作を実行します。 Upsert では、最終的なテーブルに対して排他ロックは必要ありません。 Upsert を使用すると、パフォーマンスが異なる場合があります。 環境で動作をテストします。  
  
### <a name="locking-behavior"></a>ロック動作  
**追加モードのロック**  
  
追加は、(-m 引数を使用して) マルチトランザクションモードで実行できますが、トランザクションセーフではありません。 そのため、(-m 引数を使用せずに) トランザクション操作として append を使用する必要があります。 残念ながら、最終的な挿入選択操作では、トランザクションモードは現在、マルチトランザクションモードより6倍遅くなります。  
  
追加モードでは、2つのフェーズでデータが読み込まれます。 フェーズ1では、ソースファイルからステージングテーブルにデータを同時に読み込みます (断片化が発生する可能性があります)。 フェーズ2では、ステージングテーブルから最終テーブルにデータを読み込みます。 2番目のフェーズでは、 **INSERT INTO...WITH (TABLOCK) 操作を選択し**ます。 次の表は、最後のテーブルのロック動作と、append モードを使用した場合のログ記録の動作を示しています。  
  
|テーブルの種類|マルチトランザクション<br />モード (-m)|テーブルが空です|サポートされている同時実行|ログの記録|  
|--------------|-----------------------------------|------------------|-------------------------|-----------|  
|ヒープ|はい|はい|はい|最小限|  
|ヒープ|はい|いいえ|はい|最小限|  
|ヒープ|いいえ|はい|いいえ|最小限|  
|ヒープ|いいえ|いいえ|いいえ|最小限|  
|付い|はい|はい|いいえ|最小限|  
|付い|はい|いいえ|はい|完全|  
|付い|いいえ|はい|いいえ|最小限|  
|付い|いいえ|いいえ|はい|完全|  
  
上の表は、ヒープまたはクラスター化インデックス (CI) テーブルへの読み込みモードを使用した**dwloader**を示しています。これには、マルチトランザクションフラグが指定されているか使用されていないか、空のテーブルまたは空でないテーブルに読み込まれています。 このような負荷の組み合わせのロックとログの動作は、テーブルに表示されます。 たとえば、追加モードを持つ (2 番目の) フェーズを、マルチトランザクションモードでも空のテーブルにも、クラスター化インデックスに読み込む場合、PDW によってテーブルに排他ロックが作成され、ログ記録が最小限になります。 これは、顧客が (2 番目の) フェーズとクエリを空のテーブルに同時に読み込むことができないことを意味します。 ただし、空でないテーブルに同じ構成を使用して読み込む場合、PDW はテーブルに排他ロックを発行せず、同時実行が可能です。 残念ながら、完全なログ記録が行われ、プロセスが遅くなります。  
  
## <a name="examples"></a>例  
  
### <a name="a-simple-dwloader-example"></a>A. 単純な dwloader の例  
次の例では、必要なオプションだけを選択して**ローダー**を開始します。 その他のオプションは、グローバル構成ファイルである*loadparamfile*から取得されます。  
  
SQL Server 認証を使用する例。  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
```  
  
Windows 認証を使用した同じ例。  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -W -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -W -f /configfiles/loadparamfile.txt  
```  
  
ソースファイルとエラーファイルの引数を使用した例。  
  
```  
--Load over Ethernet  
dwloader.exe -U mylogin -P 123jkl -S 10.192.63.148  -i C:\SQLData\AWDimEmployees.csv -T AdventureWorksPDW2012.dbo.DimEmployees -R C:\SQLData\LoadErrors  
```  
  
### <a name="b-load-data-into-an-adventureworks-table"></a>B. AdventureWorks テーブルへのデータの読み込み  
次の例は、 **AdventureWorksPDW2012**にデータを読み込むバッチスクリプトの一部です。  完全なスクリプトを表示するには、 **AdventureWorksPDW2012**インストールパッケージに付属している aw_create の .bat ファイルを開きます。 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

次のスクリプトスニペットでは、dwloader を使用して、Dbo.dimaccount テーブルと DimCurrency テーブルにデータを読み込みます。 このスクリプトは、イーサネットアドレスを使用しています。 InfiniBand を使用していた場合、サーバーは`-SQLCTL01` *>appliance_name<* されます。  
  
```  
set server=10.193.63.134  
set user=<MyUser>  
set password=<MyPassword>  
  
set schema=AdventureWorksPDW2012.dbo  
set load="C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe"  
set mode=reload  
  
--Loads data into the AdventureWorksPDW2012.dbo.DimAccount table  
--Source data is stored in the file DimAccount.txt,   
--which is in the current directory.  
  
set t1=DimAccount  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%   
  
--Loads data from the DimCurrency.txt file into  
--AdventureWorksPDW2012.dbo.DimCurrency  
set t1=DimCurrency  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%  
```  
  
次に、Dbo.dimaccount テーブルの DDL を示します。  
  
```  
CREATE TABLE DimAccount(  
AccountKey int NOT NULL,  
ParentAccountKey int,  
AccountCodeAlternateKey int,  
ParentAccountCodeAlternateKey int,  
AccountDescription nvarchar(50),  
AccountType nvarchar(50),  
Operator nvarchar(50),  
CustomMembers nvarchar(300),  
ValueType nvarchar(50),  
CustomMemberOptions nvarchar(200))  
with (CLUSTERED INDEX(AccountKey),  
DISTRIBUTION = REPLICATE);  
```  
  
次に、テーブル Dbo.dimaccount に読み込むデータを含むデータファイル Dbo.dimaccount の例を示します。  
  
```  
--Sample of data in the DimAccount.txt load file.  
  
1||1||Balance Sheet||~||Currency|  
2|1|10|1|Assets|Assets|+||Currency|  
3|2|110|10|Current Assets|Assets|+||Currency|  
4|3|1110|110|Cash|Assets|+||Currency|  
5|3|1120|110|Receivables|Assets|+||Currency|  
6|5|1130|1120|Trade Receivables|Assets|+||Currency|  
7|5|1140|1120|Other Receivables|Assets|+||Currency|  
8|3|1150|110|Allowance for Bad Debt|Assets|+||Currency|  
9|3|1160|110|Inventory|Assets|+||Currency|  
10|9|1162|1160|Raw Materials|Assets|+||Currency|  
11|9|1164|1160|Work in Process|Assets|+||Currency|  
12|9|1166|1160|Finished Goods|Assets|+||Currency|  
13|3|1170|110|Deferred Taxes|Assets|+||Currency|  
```  
  
### <a name="c-load-data-from-the-command-line"></a>C. コマンドラインからのデータの読み込み  
例 B のスクリプトは、次の例に示すように、コマンドラインですべてのパラメーターを入力することで置き換えることができます。  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe -S <Control node IP> -E -M reload -e UTF16 -i .\DimAccount.txt -T AdventureWorksPDW2012.dbo.DimAccount -R DimAccount.bad -t "|" -r \r\n -U <login> -P <password>  
```  
  
コマンドラインパラメーターの説明:  
  
-   *SQL Server C:\Program Warehouse\100\dwloader.exe Parallel Data*は、インストールされている dwloader .exe です。  
  
-   *-S*の後に、コントロールノードの IP アドレスを指定します。  
  
-   *-E は、* 空の文字列を NULL として読み込むことを指定します。  
  
-   *-M reload*は、ソースデータを挿入する前に、変換先テーブルを切り捨てることを指定します。  
  
-   *-e UTF16*は、ソースファイルでリトルエンディアン文字エンコードの種類が使用されていることを示します。  
  
-   *-i .\DimAccount.txt*は、現在のディレクトリに存在する dbo.dimaccount という名前のファイルにデータがあることを指定します。  
  
-   *-T AdventureWorksPDW2012 dbo.dimaccount*は、データを受信するテーブルの3部構成の名前を指定します。  
  
-   *-R dbo.dimaccount*は、読み込みに失敗した行が dbo.dimaccount という名前のファイルに書き込まれることを指定します。  
  
-   *-t "|"* 入力ファイル Dbo.dimaccount のフィールドがパイプ文字で区切られていることを示します。  
  
-   *-r \R\n* dbo.dimaccount の各行は、キャリッジリターンと改行文字で終了します。  
  
-   *-U <login_name>-P <password> *は、読み込みを実行するアクセス許可を持つログインのログインとパスワードを指定します。  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
  
