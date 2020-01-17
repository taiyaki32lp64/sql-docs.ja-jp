---
title: プロジェクトの設定 (変換) (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5d4936638fc9e283caafffc2f2a7cfdbed396920
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028764"
---
# <a name="project-settings-conversion-sybasetosql"></a>プロジェクトの設定 (変換) (SybaseToSQL)
[変換] ページ、**プロジェクト設定** ダイアログ ボックスには、SSMA を Sybase Adaptive Server Enterprise (ASE) の構文に変換する方法をカスタマイズする設定が含まれています。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure の構文。  
  
変換のウィンドウが表示されます、**プロジェクト設定**と**プロジェクト設定の既定の** ダイアログ ボックス。  
  
-   すべての SSMA プロジェクトの設定を指定するかどうか、**ツール**メニューの [**プロジェクト設定の既定の**、] をクリックして**全般**クリックし、左側のウィンドウの下部にあります。**変換**します。  
  
-   現在のプロジェクトの設定を指定する、**ツール**メニューの [**プロジェクトの設定**、] をクリックして**全般**左側のウィンドウの下部にあるをクリックして**変換**します。  
  
## <a name="miscellaneous-options"></a>その他のオプション  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure と ASE は、別のエラー コードを使用します。  
  
この設定を使用して、SSMA をへの参照を見つけたときに、出力またはエラー一覧ウィンドウに表示するメッセージ (警告またはエラー) の種類を指定する **@@ERROR**  ASE コード。  
  
-   選択した場合**変換し、の警告マーク**SSMA は、ステートメントに変換し、警告のコメントでマークします。  
  
-   選択した場合**エラー マーク**SSMA は変換をスキップし、エラーのコメント ステートメントをマークします。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** 変換し、の警告マーク  
  
**フル モード:** エラーをマークします。  
  
**LIKE 演算子の変換**  
Sybase ASE 動作と一致するオペランドのように変換するかどうかを指定します。 Sybase が like パターンに末尾の空白をトリムすることがポイントです。 回避策では、最大有効桁数を持つ固定長データ型に右の式のキャストを作成します。  
  
-   選択**単純変換**修正なしの式を変換します。  
  
-   ASE の動作の選択を使用する**固定長にキャストします。**  
  
[モード] ボックス変換モードを選択すると、SSMA には、次の設定が適用されます。  
  
**既定/オプティミスティック モード**:単純な変換  
  
**フル モード**:固定長にキャストします。  
  
**変換するか、空の文字列を数値型のキャスト**  
データ型の引数として数値型に変換またはキャスト式の中で、空または空白の文字列を処理する方法を指定します。 この設定は次のオプションです。  
  
-   選択**単純変換**修正なしの式を変換します。  
  
-   場合**空の文字列として 0 数値**が選択されている場合は、大文字と小文字の ltrim(rtrim({s})) で置き換えられる文字列パラメーター {0} s} 後ときに""、0 他 {0} s} 終了式  
  
[モード] ボックス変換モードを選択すると、SSMA には、次の設定が適用されます。  
  
**既定/オプティミスティック モード**:単純な変換  
  
**フル モード**:0 個の数値として空の文字列  
  
**NULL の連結**  
この設定では、文字列の連結で NULL に変換する方法を指定します。 この特定の設定は、次のオプションを設定できます。  
  
-   **ISNULL 関数をラップします。** このオプションが設定されている場合は、すべて非定数の連結では、' string_expression' が ISNULL(string_expression) でラップされ、Null は空の文字列に置き換えられます。  
  
-   **現在の構文を保持します。**  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** 現在の構文を保持します。  
  
**フル モード:** ISNULL 関数をラップします。  
  
**空の文字列の変換**  
この設定では、空の文字列に変換する方法を指定します。 この特定の設定は、次のオプションを設定できます。  
  
-   **領域を持つすべての文字列式を置き換えます**  
  
-   **空の文字列定数を領域に置き換えます**  
  
-   使用する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure の動作で、**現在の構文を保持**します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** 現在の構文を保持します。  
  
**フル モード:** 領域を持つすべての文字列式を置き換えます  
  
**バイナリ文字列変換の変換とキャスト**  
バイナリ値の数値への変換は、さまざまなプラットフォームで異なる値を返すことができます。 たとえば、x86 のプロセッサでは、変換 (整数、0x00000100) は、ASE に 65536 とで 256 を返します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 ASE には、バイト順序に応じて異なる値が返されます。  
  
この SSMA 変換の変換を制御する設定と値のバイナリが含まれる CASE 式を使用します。  
  
-   選択**単純変換**警告や修正なしの式を変換します。 ASE のサーバーにバイナリ値の変更を必要としないバイト順があることがわかっている場合は、この設定を使用します。  
  
-   選択**変換し、修正**SSMA 変換しで使用する式を修正して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 定数リテラルのバイト順が逆になります。 その他のすべてのバイナリ値 (バイナリ変数や列) は、エラーとマークされます。 ASE のサーバーにバイナリ値に変更を必要とするバイト順があることがわかっている場合は、この値を使用します。  
  
-   選択**変換し、の警告マーク**SSMA 変換、式を訂正してすべてのマークを付けるが、警告のコメントを含む式を変換します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定のモード:** 変換し、の警告マーク  
  
**オプティミスティック モード:** 単純な変換  
  
**フル モード:** 変換し、修正  
  
**動的 SQL**  
SSMA は、ASE のコードでの動的 SQL を見つけたときに出力またはエラー一覧 ウィンドウで表示するメッセージ (警告またはエラー) の種類を指定するのにには、この設定を使用します。  
  
-   選択した場合**変換し、の警告マーク**SSMA は動的 SQL に変換され、警告のコメント ステートメントをマークします。  
  
-   選択した場合**エラー マーク**SSMA は変換をスキップし、エラーのコメント ステートメントをマークします。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** 変換し、の警告マーク  
  
**フル モード:** エラーをマークします。  
  
**等しいかどうかチェックの変換**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/場合は、ANSI_NULLS の設定では、SQL Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/等値比較に null 値が含まれている場合、SQL Azure は UNKNOWN を返します。 ANSI_NULLS がオフの場合は、null 値を含む等値比較 true を返します比較対象の列と式、または 2 つの式の両方が null です。 同様に動作の比較 (ANSINULL OFF) の既定の Sybase ASE の等値による[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ANSI_NULLS OFF で SQL Azure です。  
  
-   選択した場合**単純変換**、SSMA は、ASE のコードを変換は[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/null 値の特別なチェックなしの SQL Azure の構文。 ANSI_NULLS はオフにする場合、この設定を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure またはケースごとに等値比較を変更するかどうか。  
  
-   選択した場合**検討 NULL 値**SSMA は、IS NULL と IS NOT NULL 句を使用して null 値のチェックを追加します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** 単純な変換  
  
**フル モード:** NULL 値を検討してください。  
  
**書式指定文字列**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure をサポートしていません、 *format_string* PRINT ステートメントおよび RAISERROR ステートメントの引数。 *Format_string*変数には、置き換え可能パラメーターを文字列に直接配置し、実行時にパラメーターがサポートされています。 代わりに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]文字列リテラル、または変数を使用して構築された文字列を使用して完全な文字列が必要です。 詳細については、次を参照してください。、"印刷 ( [!INCLUDE[tsql](../../includes/tsql-md.md)])」のトピック[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブックの「します。  
  
SSMA が検出した場合、 *format_string*引数、変数を使用してリテラル文字列を作成または新しい変数を作成してその変数を使用して文字列を作成します。  
  
-   印刷と RAISERROR の関数の文字列リテラルを使用する**新しい文字列を作成する**します。  
  
    このモードでのプレース ホルダーとローカル変数は、PRINT または RAISERROR ステートメントを使用しない場合、ステートメントは変更されません。 二重のパーセント記号 (%)印刷の文字列リテラルで 1 つのパーセント記号 % に変更されます。  
  
    PRINT または RAISERROR ステートメントのプレース ホルダーと 1 つを使用している場合、または次の例に示すような複数のローカル変数。  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA を次の構文に変換されます。  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    場合*format_string*など、変数を次のステートメントでは。  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA は、単純な文字列の変換を行うことはできませんし、新しい変数を作成する必要があります。  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        CAST (@arg1 AS varchar(max)))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        CAST (@arg2 AS varchar(max)))  
    PRINT @print_format_1  
    ```  
    使用している場合**新しい文字列を作成する**モードでは、SSMA を想定、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CONCAT_NULL_YIELDS_NULL オプションは OFF です。 そのため、SSMA では、null 引数をチェックしません。  
  
-   SSMA 印刷と RAISERROR の各ステートメントに対して新しい変数を作成し、文字列値をその変数を使用には、次のように選択します。**を作成する新しい変数**します。  
  
    このモードでのプレース ホルダーとローカル変数は、PRINT または RAISERROR ステートメントを使用しない場合 SSMA 文字を置き換えますすべて二重パーセント (%)準拠する 1 つのパーセント記号と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure の構文。  
  
    PRINT または RAISERROR ステートメントのプレース ホルダーと 1 つを使用している場合、または次の例に示すような複数のローカル変数。  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA を次の構文に変換されます。  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1 = 'Total: %1!%'  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))  
    PRINT @print_format_1  
    ```  
    場合*format_string*など、変数を次のステートメントでは。  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA 新しい変数を作成、次のように、各引数に null 値の確認します。  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@arg1 AS varchar(max)),''))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        ISNULL(CAST (@arg2 AS varchar(max)),''))  
    PRINT @print_format_1  
    ```  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** 新しい文字列を作成します。  
  
**フル モード:** 新しい変数を作成します。  
  
**Timestamp 列に明示的な値を挿入します。**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure では、timestamp 列に明示的な値を挿入することはできません。  
  
-   INSERT ステートメントから、timestamp 列を除外する次のように選択します。**除外列**します。  
  
-   INSERT ステートメントに timestamp 列があるたびに、エラー メッセージを印刷するには、選択**エラー マーク**します。 このモードでは、INSERT ステートメントは変換されませんし、エラーのコメントが付けられます。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** 列を除外します。  
  
**フル モード:** エラーをマークします。  
  
**プロシージャで定義されているストアの一時オブジェクト**  
この設定は、変換中にソースのメタデータでの手順で表示される一時オブジェクトの定義を格納する必要があるかどうかを指定します。  
  
-   選択**はい**メタデータを格納します。  
  
-   選択**いいえ**オブジェクトが格納されていない必要がある場合。  
  
**既定/オプティミスティック モード:** はい  
  
**フル モード:** いいえ  
  
**プロキシのテーブルの変換**  
ASE のプロキシのテーブルに変換されますを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/または SQL Azure のテーブルが変換されないと、コードがエラーのコメントで示されています。  
  
-   選択**変換**プロキシ テーブルを通常のテーブルに変換します。  
  
-   選択**エラー マーク**単に、プロキシ テーブル コメントによるコード エラーをマークします。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** エラーをマークします。  
  
**RAISERROR の基本メッセージ数**  
ASE のユーザー メッセージは、各データベースに格納されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザー メッセージが一元的に格納され、をとおして利用可能な**sys.messages**カタログ ビューです。 ASE ユーザー メッセージを 20000 から開始するさらに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エラー メッセージが 50001 から開始します。  
  
この設定は、ASE のユーザーのメッセージ番号に変換を追加する数を指定します、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ユーザー メッセージ。 場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ユーザー メッセージを持つ、 **sys.messages**カタログ ビューでは、大きい値にこの番号を変更する必要があります。 これは、変換後のメッセージ番号は、既存のメッセージ番号と競合しないようにします。  
  
次の点に注意してください。  
  
-   17000 19999 範囲内で ASE のメッセージは、sysmessages システム テーブルは変換されません。  
  
-   RAISERROR ステートメントで参照されているメッセージ数が定数である場合は、SSMA は新しいユーザーのメッセージ数を決定する定数を基本メッセージ番号を追加します。  
  
-   参照されているメッセージ数が変数または式の場合は、SSMA は中間のローカル変数を作成します。  
  
-   SSMA では、オプティミスティック モードで想定する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CONCAT_NULL_YIELDS_NULL オプションはオフであり、引数が null のチェックはありません。  
  
-   フル モードでは、SSMA は、null 引数をチェックします。  
  
-   RAISERROR と errordata のような*一覧*は変換されません。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** 30001  
  
**システム オブジェクト**  
SSMA は、ASE システム オブジェクトの使用を見つけたときに出力またはエラー一覧 ウィンドウで表示するメッセージ (警告またはエラー) の種類を指定するのにには、この設定を使用します。  
  
-   選択した場合**変換し、の警告マーク**SSMA はシステム オブジェクトへの参照を変換および警告のコメント ステートメントとしてマークされます。  
  
-   選択した場合**エラー マーク**SSMA はシステム オブジェクトへの参照を変換しないとエラー コメント付きのステートメントとしてマークされます。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** 変換し、の警告マーク  
  
**フル モード:** エラーをマークします。  
  
**未解決の識別子**  
SSMA は、識別子を解決できない場合に出力またはエラー一覧 ウィンドウで表示するメッセージ (警告またはエラー) の種類を指定するのにには、この設定を使用します。  
  
-   選択した場合**変換し、の警告マーク**、SSMA 未解決識別子への参照の変換を試みるし、警告のコメント ステートメントとしてマークされます。  
  
-   選択した場合**エラー マーク**、SSMA 未解決識別子への参照は変換されませんし、エラー コメント付きのステートメントとしてマークされます。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** 変換し、の警告マーク  
  
**フル モード:** エラーをマークします。  
  
## <a name="system-function-options"></a>システム関数のオプション  
**CHARINDEX 関数**  
ASE では、すべての入力式が NULL の場合にのみ、CHARINDEX は NULL を返します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または任意の入力式が NULL の場合、SQL Azure は NULL を返します。  
  
-   ASE の動作を使用するには、次のように選択します。**関数を置き換える**します。 CHARINDEX 関数に対するすべての呼び出しは、(で作成したスキーマ名 's2ss' のユーザー データベース)、Sybase ASE の動作をエミュレートするために渡されるパラメーターの型に基づく CHARINDEX_VARCHAR または CHARINDEX_NVARCHAR のいずれかのユーザー定義関数の呼び出しに置き換えられます。  
  
-   使用する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure の動作で、**現在の構文を保持**します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** 現在の構文を保持します。  
  
**フル モード:** Replace 関数  
  
**DATALENGTH 関数**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure と ASE は、値が 1 つのスペースの場合は、DATALENGTH 関数によって返される値が異なります。 この場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure は 0 を返し、ASE は 1 を返します。  
  
-   ASE の動作を使用するには、次のように選択します。**関数を置き換える**します。 DATALENGTH 関数に対するすべての呼び出しは、Sybase ASE の動作をエミュレートする CASE 式に置き換えられます。  
  
-   既定値を使用する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure の動作で、**現在の構文を保持**します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** 現在の構文を保持します。  
  
**フル モード:** Replace 関数  
  
**INDEX_COL 関数**  
ASE は、省略可能なサポート*user_id* ; INDEX_COL 関数の引数、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]、[SQL Azure は、この引数をサポートしていません。 使用する場合、 *user_id*引数では、この関数に変換できない[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure の構文。  
  
-   ASE の動作を使用するには、次のように選択します。**関数に変換**します。 コードが含まれている場合、 *user_id*引数、SSMA エラーが表示されます。  
  
-   その INDEX_COL が検出されるたびに、エラー メッセージを表示するには、選択**エラー マーク**します。 SSMA は、関数への参照は変換されませんし、エラー コメントを指定してステートメントをマークします。  
  
**既定/オプティミスティック/フル モード:** エラーをマークします。  
  
**INDEX_COLORDER 関数**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure の INDEX_COLORDER のシステム関数ではありません。  
  
-   ASE の動作を使用するには、次のように選択します。**関数に変換**します。 INDEX_COLORDER 関数に対するすべての呼び出しは、同じ名前 (スキーマ名 's2ss' のユーザー データベースで作成した)、Sybase ASE の動作をエミュレートする INDEX_COLORDER を持つユーザー定義関数の呼び出しに置き換えられます。  
  
-   その INDEX_COLORDER が検出されるたびに、エラー メッセージを印刷するには、選択**エラー マーク**します。 SSMA は、関数への参照は変換されませんし、エラー コメントを指定してステートメントをマークします。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** エラーをマークします。  
  
**LEFT および RIGHT 関数**  
左と右 Sybase 関数が負の値の長さのパラメーターの動作が異なる。  
  
-   ASE の動作を使用するには、次のように選択します。 **Replace 関数**します。 長さのパラメーターは、CASE 式を返す負の値を null に置き換えられます。  
  
-   SQL Server の動作を使用する**現在の構文を保持**  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** 現在の構文を保持します。  
  
**フル モード:** Replace 関数  
  
> [!NOTE]  
> 長さのパラメーターは、リテラル値と複雑な式ではありませんが場合、長さの値はプロジェクト設定に関係なく null に常に置き換えられます。  
  
**NEXT_IDENTITY 関数**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure の NEXT_IDENTITY のシステム関数ではありません。  
  
-   ASE の動作を使用するには、次のように選択します。**変換関数**します。 NEXT_IDENTITY 関数に対するすべての呼び出しは、式 (IDENT_CURRENT(parameter Value) + Sybase ASE 動作をエミュレートする IDENT_INCR(parameter Value) で置き換えられます。  
  
-   その NEXT_IDENTITY が検出されるたびに、エラー メッセージを印刷するには、選択**エラー マーク**します。 SSMA は、関数への参照は変換されませんし、エラー コメントを指定してステートメントをマークします。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** エラーをマークします。  
  
**PATINDEX 関数**  
Sybase ASE 動作と一致する PATINDEX 関数に変換するかどうかを指定します。 Sybase が検索パターンに末尾の空白をトリムすることがポイントです。 回避策では、固定長データが最大有効桁数と入力し、パターンを検索する rtrim 関数を適用する値の式のキャストを作成します。  
  
-   ASE の動作の選択を使用する**使用**します。  
  
-   既定値を使用する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure の動作で、**使用しないでください**します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** 使用しない  
  
**フル モード:** 新しく使用する機能  
  
**REPLICATE 関数**  
REPLICATE 関数では、文字列の指定した回数だけ繰り返されます。 0 回では、文字列を繰り返すことを指定する場合は、ASE に、結果が null です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure では、結果は空の文字列。  
  
-   ASE の動作を使用するには、次のように選択します。**関数を置き換える**します。 REPLICATE 関数に対するすべての呼び出しは、(で作成したスキーマ名 's2ss' のユーザー データベース)、Sybase ASE の動作をエミュレートするために渡されるパラメーターの型に基づく REPLICATE_VARCHAR または REPLICATE_NVARCHAR のいずれかのユーザー定義関数の呼び出しに置き換えられます。  
  
-   既定値を使用する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure の動作で、 **Replace 関数**します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード/フル モード:** Replace 関数  
  
**TRIM (LTRIM、RTRIM) 関数**  
この設定では、Sybase ASE 的に等しい構文関数 (LTRIM、RTRIM) Trim 関数への呼び出しを置換するか、現在の構文を保持するかどうかを指定します。 次のオプションは、この特定の設定。  
  
-   **Replace 関数**  
  
-   **現在の構文を保持します。**  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード/フル モード:** Replace 関数  
  
**SUBSTRING 関数**  
ASE では、関数で`SUBSTRING(expression, start, length)`式の文字の数より大きい開始値が指定されている場合、または長さが 0 に等しい場合は NULL を返します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure では、同等の式が空の文字列を返します。  
  
-   ASE の動作を使用するには、次のように選択します。**関数を置き換える**します。 SUBSTRING 関数に対するすべての呼び出しがエミュレートするために (ユーザー データベース、スキーマ名 's2ss' の下に作成した) に渡されるパラメーターの型に基づく SUBSTRING_VARCHAR または SUBSTRING_NVARCHAR SUBSTRING_VARBINARY のユーザー定義関数の呼び出しに置き換えられます、Sybase ASE の動作です。  
  
-   使用する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure の動作で、**現在の構文を保持**します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** 現在の構文を保持します。  
  
**フル モード:** Replace 関数  
  
## <a name="tables"></a>TABLES  
**主キーを追加します。**  
新しいプライマリ キーを作成、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Access のテーブルには、主キーまたは一意のインデックスがあるない場合、SQL Azure テーブル。  
  
-   **既定のモード**:False  
  
-   **オプティミスティック モード**:False  
  
-   **フル モード**:True  
  
> [!NOTE]  
> SQL Azure に接続しているときに既定では True。  
  
## <a name="see-also"></a>参照  
[ユーザー インターフェイス リファレンス&#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
