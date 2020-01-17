---
title: プロジェクトの設定 (変換) (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 538c93cf-c5bb-43d5-b758-186d9fb00c19
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: e6918dac33ce0e69116f713cb8906b2774d00575
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68084547"
---
# <a name="project-settings-conversion-db2tosql"></a>プロジェクトの設定 (変換) (DB2ToSQL)
[変換] ページ、**プロジェクト設定** ダイアログ ボックスには、SSMA が DB2 構文に変換する方法をカスタマイズする設定が含まれています。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構文。  
  
変換のウィンドウが表示されます、**プロジェクト設定**と**プロジェクト設定の既定の** ダイアログ ボックス。  
  
-   上のすべての SSMA プロジェクトの設定を指定する、**ツール**ボタンをクリックし**プロジェクト設定の既定の**、設定は表示または変更に必要な移行プロジェクトの種類を選択します **。移行のターゲット バージョン**ボックスの一覧からクリック**全般**クリックし、左側のウィンドウの下部にある**変換**します。  
  
-   現在のプロジェクトの設定を指定する、**ツール**ボタンをクリックし**プロジェクトの設定**、順にクリックします**全般**左側のウィンドウの下部にあるをクリックして**変換**します。  
  
## <a name="conversion-messages"></a>メッセージの変換  
  
### <a name="generate-messages-about-issues-applied"></a>問題の適用に関するメッセージを生成します。  
SSMA に変換中に情報メッセージを生成し、され、出力ウィンドウに表示され、変換後のコードに追加するかどうかを指定します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** いいえ  
  
**フル モード:** いいえ  
  
## <a name="miscellaneous-options"></a>その他のオプション  
  
### <a name="cast-rownum-expressions-as-integers"></a>整数としてキャスト ROWNUM 式  
SSMA ROWNUM 式が変換されるときに、TOP 句の後に、式に式を変換します。 次の例では、DB2 の DELETE ステートメントで ROWNUM を示しています。  
  
`DELETE FROM Table1`  
  
`WHERE ROWNUM < expression and Field1 >= 2`  
  
次の例は、その結果[!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
`DELETE TOP (expression-1)`  
  
`FROM Table1`  
  
`WHERE Field1>=2`  
  
上部では、TOP 句の式が整数に評価が必要です。 整数が負の場合、ステートメントにエラーが発生します。  
  
-   選択した場合**はい**SSMA を整数として式をキャストします。  
  
-   選択した場合**いいえ**SSMA では、整数以外のすべての式は変換後のコードでエラーとしてマークします。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/フル モード:** いいえ  
  
**オプティミスティック モード:** はい  
  
### <a name="default-schema-mapping"></a>既定のスキーマ マッピング  
この設定は、SQL Server スキーマへの DB2 スキーマのマップ方法を指定します。 2 つのオプションは、この設定で使用できます。  
  
1.  **データベースにスキーマ:** このモードの DB2 スキーマ 'sch1' は、既定では SQL Server データベース 'sch1' の 'dbo' SQL Server スキーマにマップされます。  
  
2.  **スキーマをスキーマ:** DB2 このモードで 'sch1' のスキーマを既定では、接続ダイアログで提供される既定の SQL Server データベース内の 'sch1' SQL Server スキーマにマップされます。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** データベースにスキーマ  
  
### <a name="conversion-ways-of-merge-statement"></a>MERGE ステートメントの変換方法  
  
-   選択した場合**を使用して INSERT、UPDATE、DELETE ステートメント**SSMA は、INSERT、UPDATE に合併ステートメントを変換、および削除ステートメント。  
  
-   選択した場合**MERGE を使用してステートメント**、SSMA では変換で MERGE ステートメントの合併ステートメント[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
> [!WARNING]  
> このプロジェクトの設定オプションでのみ使用可能な[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008 では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 です。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** MERGE ステートメントを使用  
  
### <a name="convert-calls-to-subprograms-that-use-default-arguments"></a>既定の引数を使用して、サブプログラムへの呼び出しに変換します。  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 関数は、関数呼び出しでパラメーターの省略をサポートしていません。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]関数およびプロシージャは既定のパラメーター値として式はサポートされません。  
  
-   選択した場合**はい**関数呼び出しのパラメーターを省略しては、SSMA は、キーワードを挿入**既定**関数と呼び出しの正しい位置にします。 次に、警告の呼び出しを設定します。  
  
-   選択した場合**いいえ**SSMA では、関数の呼び出しをエラーとしてマークします。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** [はい]  
  
### <a name="convert-count-function-to-countbig"></a>COUNT 関数を COUNT_BIG に変換します。  
かどうか、COUNT 関数が返す値の 2,147, 483,647 を超える可能性がありますです 2<sup>31</sup>-1、COUNT_BIG 関数に変換する必要があります。  
  
-   選択した場合**はい**SSMA では、数のすべての使用は COUNT_BIG に変換します。  
  
-   選択した場合**いいえ**関数の数として残ります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 関数が 2 よりも大きい値を返す場合はエラーを返します<sup>31</sup>-1。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/フル モード:** [はい]  
  
**オプティミスティック モード:** いいえ  
  
### <a name="convert-forall-statement-to-while-statement"></a>WHILE FORALL ステートメントに変換ステートメント  
SSMA が PL/SQL コレクションの要素で FORALL ループを処理する方法を定義します。  
  
-   選択した場合**はい**、SSMA コレクションの要素が 1 つずつ取得が WHILE ループを作成します。  
  
-   選択した場合**いいえ**SSMA は、ノード () メソッドを使用してコレクションから行セットを生成し、1 つのテーブルとして使用します。 これにより、方が効率的ですが、出力コードに読みにくくなります。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** いいえ  
  
**フル モード:** はい  
  
### <a name="convert-foreign-keys-with-set-null-referential-action-on-column-that-is-not-null"></a>ある列の参照操作を NULL に設定された外部キーの変換は NOT NULL します。  
DB2 を NULL に設定アクションを実行できませんでした可能性があります参照先の列で null 値が許可されていないため、外部キー制約を作成します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] このような外部キーの構成は許可されません。  
  
-   選択した場合**はい**SSMA DB2 のように参照動作が生成されますが、制約を読み込む前に手動で変更する必要があります、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 たとえば、SET NULL ではなく、NO ACTION を選択できます。  
  
-   選択した場合**いいえ**制約をエラーとしてマークされます。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** いいえ  
  
### <a name="convert-function-calls-to-procedure-calls"></a>プロシージャ呼び出しを関数呼び出しに変換します。  
一部の DB2 関数が自律的なトランザクションとして定義されますまたはで無効になるステートメントを含む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 このような場合は、SSMA は、手順と、プロシージャのラッパーである関数を作成します。 変換後の関数は、実装のプロシージャを呼び出します。  
  
SSMA は、ラッパー関数の呼び出しをプロシージャの呼び出しに変換できます。 これによりより読みやすいコードを作成し、パフォーマンスを向上させることができます。 ただし、コンテキストが常に許可していません。たとえば、プロシージャ呼び出しで選択リスト内の関数呼び出しを置き換えることはできません。 SSMA では、一般的なケースをカバーする、いくつかのオプションがあります。  
  
-   選択した場合**常に**SSMA はプロシージャ呼び出しをラッパー関数の呼び出しを変換しようとしています。 現在のコンテキストがこの変換を許可していない場合、エラー メッセージが生成されます。 これにより、生成されたコードに関数呼び出しが残されますありません。  
  
-   選択した場合**可能であれば**関数に出力パラメーターがある場合にのみ、SSMA でプロシージャの呼び出しに移動が使用されます。 移動が不可能な場合は、パラメーターの出力属性が削除されます。 それ以外の場合は、SSMA は、関数呼び出しを残します。  
  
-   選択した場合**Never**SSMA は関数呼び出しとしてすべての関数呼び出しのままにします。 場合がありますこのオプションを選択できない可能性があります許容可能なパフォーマンス上の理由が原因です。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** 可能な場合  
  
### <a name="convert-lock-table-statements"></a>LOCK ステートメントを変換します。  
SSMA は、テーブル ヒントに多くのロック TABLE ステートメントを変換できます。 SSMA 副区分、パーティションが含まれているすべてのテーブルのロック ステートメントに変換できません@dblink、および NOWAIT 句、および変換エラー メッセージには、このようなステートメントとしてマークされます。  
  
-   選択した場合**はい**SSMA では、サポートされているテーブルのロック ステートメントはテーブル ヒントに変換します。  
  
-   選択した場合**いいえ**、SSMA 変換エラー メッセージを使用したすべてのテーブルのロック ステートメントとしてマークされます。  
  
次の表は、SSMA が DB2 のロック モードに変換する方法を示しています。  
  
|||  
|-|-|  
|DB2 のロック モード|SQL Server のテーブル ヒント|  
|行の共有|ROWLOCK、HOLDLOCK|  
|排他行|ROWLOCK、XLOCK、HOLDLOCK|  
|共有の更新プログラムの行の共有を =|ROWLOCK、HOLDLOCK|  
|共有|TABLOCK、HOLDLOCK|  
|排他的な共有行|TABLOCK、XLOCK、HOLDLOCK|  
|排他的|HOLDLOCK、TABLOCKX|  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** はい  
  
### <a name="convert-open-for-statements-for-ref-cursor-out-parameters"></a>REF CURSOR 出力パラメーターのオープン FOR ステートメントを変換します。  
Db2、サブプログラムの REF CURSOR 型のパラメーターを設定する結果を返すオープン FOR ステートメントを使用できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、ストアド プロシージャが直接の SELECT ステートメントの結果を返します。  
  
SSMA は、SELECT ステートメントに多くのオープン FOR ステートメントに変換できます。  
  
-   選択した場合**はい**SSMA は、クライアントに結果セットを返す SELECT ステートメントにオープン FOR ステートメントを変換します。  
  
-   選択した場合**いいえ**SSMA で変換後のコードと出力ウィンドウにエラー メッセージが生成されます。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** はい  
  
### <a name="convert-record-as-a-list-of-separates-variables"></a>分離の変数の一覧としてレコードに変換します。  
SSMA は、分離の変数に、特定の構造を持つ XML 変数に、DB2 のレコードを変換できます。  
  
-   選択した場合**はい**SSMA は、可能であれば分離変数の一覧に、レコードを変換します。  
  
-   選択した場合**いいえ**SSMA は、特定の構造を持つ XML 変数に、レコードを変換します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** [はい]  
  
### <a name="convert-substr-function-calls-to-substring-function-calls"></a>SUBSTRING 関数の呼び出しに SUBSTR 関数呼び出しに変換します。  
SSMA は DB2 SUBSTR 関数の呼び出しに変換できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**部分文字列**関数呼び出しのパラメーターの数によって異なります。 SSMA は SUBSTR 関数の呼び出しを変換できない、またはパラメーターの数がサポートされていません、SSMA で SUBSTR 関数の呼び出しがカスタムの SSMA 関数呼び出しに変換されます。  
  
-   選択した場合**はい**、SSMA に 3 つのパラメーターを使用する SUBSTR 関数呼び出しに変換されます[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **substring**します。 SUBSTR 他の関数は、カスタム SSMA 関数の呼び出しに変換されます。  
  
-   選択した場合**いいえ**SSMA を使用して、SUBSTR 関数の呼び出しをカスタム SSMA 関数呼び出しに変換されます。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** はい  
  
**フル モード:** いいえ  
  
### <a name="convert-subtypes"></a>サブタイプを変換します。  
SSMA は、2 つの方法で PL/SQL サブタイプに変換できます。  
  
-   選択した場合**はい**、SSMA は作成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ユーザー定義サブタイプからを入力し、このサブタイプの各変数の使用します。  
  
-   選択した場合**いいえ**SSMA は基になる型のサブタイプのすべてのソース宣言を置き換えるし、通常どおりの結果を変換します。 この場合、その他の種類は作成されませんで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** いいえ  
  
### <a name="convert-synonyms"></a>シノニムを変換します。  
次の DB2 オブジェクトのシノニムに移行できる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   テーブルとオブジェクト テーブル  
  
-   ビューとオブジェクトのビュー  
  
-   ストアド プロシージャおよび関数  
  
-   具体化されたビュー  
  
オブジェクトへの直接参照は、次の DB2 オブジェクトのシノニムを置き換えることができます。  
  
-   シーケンス  
  
-   パッケージ  
  
-   Java クラス スキーマ オブジェクト  
  
-   ユーザー定義オブジェクトの種類  
  
その他のシノニムを移行することはできません。 SSMA は、シノニムと、シノニムを使用するすべての参照のエラー メッセージを生成します。  
  
-   選択した場合**はい**、SSMA は作成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]シノニムと、前のリストに従って直接オブジェクト参照。  
  
-   選択した場合**いいえ**SSMA は、ここに表示されているすべてのシノニムを直接オブジェクト参照が作成されます。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** はい  
  
### <a name="convert-tochardate-format"></a>(日付、形式) の TO_CHAR を変換します。  
SSMA は、DB2 TO_CHAR(date, format) を sysdb データベースからのプロシージャに変換することができます。  
  
-   選択した場合**を使用して TO_CHAR_DATE 関数**、SSMA TO_CHAR_DATE 関数を使用して英語の言語の変換のために、TO_CHAR (日付、形式) を変換します。  
  
-   選択した場合**を使用して TO_CHAR_DATE_LS 関数 (NLS ケア)** 、SSMA TO_CHAR_DATE_LS 関数を使用してセッションの言語の変換のために、TO_CHAR (日付、形式) を変換します  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** TO_CHAR_DATE 関数を使用してください。  
  
**フル モード:** TO_CHAR_DATE_LS 関数 (NLS 注意が必要) を使用してください。  
  
### <a name="convert-transaction-processing-statements"></a>トランザクション処理ステートメントを変換します。  
SSMA は、DB2 トランザクション処理のステートメントに変換できます。  
  
-   選択した場合**はい**、SSMA 変換への DB2 トランザクション処理ステートメント[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ステートメント。  
  
-   選択した場合**いいえ**SSMA がステートメントとして変換エラーの処理、トランザクションをマークします。  
  
> [!NOTE]  
> DB2 では、トランザクションが暗黙的に開きます。 この動作をエミュレートする[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、する必要があります BEGIN TRANSACTION ステートメントを手動で追加のトランザクションを開始する場所。 または、セッションの先頭に SET IMPLICIT_TRANSACTIONS ON コマンドを実行することができます。 SSMA は自律的なトランザクションでのサブルーチンを変換するときに、SET IMPLICIT_TRANSACTIONS ON を自動的に追加します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** [はい]  
  
### <a name="emulate-db2-null-behavior-in-order-by-clauses"></a>ORDER BY 句での DB2 null の動作をエミュレートします。  
NULL 値が異なる方法で順序付けられた[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]および DB2:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、NULL 値は、順序付きリストで、最小値。 昇順、リストでは、NULL 値を先頭に表示されます。  
  
-   Db2 は、NULL 値は、順序付きリストで最高の値です。 既定では、NULL 値は、昇順で順序リストの最後に表示されます。  
  
-   DB2 は、最初の NULL と null 値の最後の句を持つ DB2 による null 値の順序を変更できます。  
  
SSMA は、NULL 値をチェックして、DB2 の ORDER BY の動作をエミュレートできます。 これは、最初が整列他の値によって指定された順序とし、注文の NULL 値で。  
  
-   選択した場合**はい**SSMA が DB2 の ORDER BY の動作をエミュレートするように、DB2 ステートメントに変換されます。  
  
-   選択した場合**いいえ**SSMA は DB2 のルールを無視して、最初の NULL と null 値の最後の句を見つけたときにエラー メッセージが生成されます。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** いいえ  
  
**フル モード:** [はい]  
  
### <a name="emulate-row-count-exceptions-in-select"></a>SELECT で行カウントの例外をエミュレートします。  
INTO 句を伴う SELECT ステートメントは、行を返さない、DB2 NO_DATA_FOUND 例外が発生します。 ステートメントには、2 つ以上の行が返されます、TOO_MANY_ROWS 例外が発生します。 変換後のステートメントで[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]行の数が 1 つの異なる場合、例外は発生しません。  
  
-   選択した場合**はい**SSMA は、各 SELECT ステートメントの後 sysdb プロシージャ db_error_exact_one_row_check への呼び出しを追加します。 この手順は、NO_DATA_FOUND と TOO_MANY_ROWS の例外をエミュレートします。 これは、既定値と、できるだけ近くに DB2 動作を再現することができます。 常に選択する必要があります**はい**ソース コードをこれらのエラーを処理する例外ハンドラーがある場合。 ユーザー定義関数の内部で SELECT ステートメントが発生した場合、このモジュールは、ストアド プロシージャを実行するためのストアド プロシージャに変換されますと、例外の発生と互換性がない[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]関数のコンテキスト。  
  
-   選択した場合**いいえ**例外は生成されません。 SSMA は、ユーザー定義関数を変換し、内の関数のままにするときに便利なをすることができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** [はい]  
  
### <a name="generate-error-for-dbmssqlparse"></a>DBMS_SQL のエラーを生成します。解析  
  
-   選択した場合**エラー**、SSMA DBMS_SQL 変換でエラーを生成します。解析します。  
  
-   選択した場合**警告**、SSMA DBMS_SQL 変換で警告を生成します。解析します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** Error  
  
### <a name="generate-rowid-column"></a>ROWID の列を生成します。  
SSMA が内のテーブルを作成するときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ROWID 列を作成できます。 データが移行されると、各行は、newid() 関数によって生成される新しい UNIQUEIDENTIFIER 値を取得します。  
  
-   選択した場合**はい**、ROWID 列のすべてのテーブルの作成と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]値を挿入するように Guid を生成します。 常に選択**はい**SSMA Tester を使用しようとしている場合。  
  
-   選択した場合**いいえ**ROWID 列はテーブルに追加されません。  
  
-   **トリガーを使用してテーブルの列を ROWID 追加**トリガーを含んでいるテーブル ROWID を追加します。  
  
> [!WARNING]  
> SQL Server 2005、SQL Server 2008 および SQL Server 2012 および 2014 の場合、既定の設定は**トリガーを使用してテーブルの列を追加 ROWID**します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** トリガーを使用してテーブルの列を ROWID 追加します。  
  
**フル モード:** [はい]  
  
### <a name="generate-unique-index-on-rowid-column"></a>ROWID の列に一意のインデックスを生成します。  
SSMA に ROWID が生成された列に一意のインデックス列が生成されるかどうかを指定します。 一意のインデックスが生成されるオプションが [はい] に設定されている場合、"NO"に設定されている場合、一意のインデックスは、ROWID 列は生成されません。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** [はい]  
  
### <a name="local-modules-conversion"></a>ローカル モジュールの変換  
入れ子になった DB2 サブプログラム (スタンドアロンのストアド プロシージャまたは関数で宣言) 変換の種類を定義します。  
  
-   選択した場合**インライン**、入れ子になったサブプログラム呼び出しは、本体で置き換えられます。  
  
-   選択した場合**ストアド プロシージャ**、入れ子になったサブプログラムは、SQL Server のストアド プロシージャに変換およびその呼び出しは次のプロシージャ呼び出しに置き換えられます。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** インライン  
  
### <a name="use-isnull-in-string-concatenation"></a>文字列の連結で ISNULL を使用します。  
DB2 と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]文字列の連結で NULL 値を含める場合は、異なる結果を返します。 DB2 では、NULL 値、空の文字セットのように扱われます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NULL を返します。  
  
-   選択した場合**はい**、SSMA は、DB2 の連結文字 (|) を置き換え、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連結記号 (+)。 SSMA では、NULL 値の連結の両側の式も確認します。  
  
-   選択した場合**いいえ**SSMA は、連結文字が置き換えられますが、NULL 値をチェックしません。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
### <a name="use-isnull-in-replace-function-calls"></a>置換関数の呼び出しで ISNULL を使用します。  
ISNULL のステートメントは、DB2 の動作をエミュレートする置換関数の呼び出しで使用されます。 次のオプションは、この設定。  
  
-   YES  
  
-   NO  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** いいえ  
  
**フル モード:** はい  
  
### <a name="use-isnull-in-concat-function-calls"></a>CONCAT 関数呼び出しで ISNULL を使用します。  
ISNULL のステートメントは、DB2 の動作をエミュレートする CONCAT 関数呼び出しに使用されます。 次のオプションは、この設定。  
  
-   YES  
  
-   NO  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** いいえ  
  
**フル モード:** はい  
  
### <a name="use-native-convert-function-when-possible"></a>可能であれば、ネイティブの convert 関数を使用して、  
  
-   選択した場合**はい**、SSMA 関数に変換します (日付、形式) TO_CHAR ネイティブ変換可能な場合。  
  
-   選択した場合**いいえ**、SSMA TO_CHAR_DATE または TO_CHAR_DATE_LS (これは、"変換 TO_CHAR(date, format)"オプションによって定義されます) に、TO_CHAR (日付、形式) を変換します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック モード:** はい  
  
**フル モード:** いいえ  
  
### <a name="use-selectfor-xml-when-converting-selectinto-for-record-variable"></a>選択を使用してください.FOR XML 変換するときに次のように選択してください.Record 変数の INTO  
Record 変数を選択すると設定 XML 結果を生成するかどうかを指定します。  
  
-   選択した場合**はい**、SELECT ステートメントは、XML を返します。  
  
-   選択した場合**いいえ**、SELECT ステートメントは結果セットを返します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** いいえ  
  
## <a name="returning-clause-conversion"></a>句の変換を返す  
  
### <a name="convert-returning-clause-in-delete-statement-to-output"></a>DELETE ステートメント内での RETURNING 句を出力に変換します。  
DB2 は、すぐに削除された値を取得する方法として、RETURNING 句を提供します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OUTPUT 句と共に、その機能を提供します。  
  
-   選択した場合**はい**OUTPUT 句には、SSMA を DELETE ステートメント内の RETURNING 句に変換されます。 テーブルのトリガーの値を変更できるため、返される値が異なる可能性があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DB2 の場合よりもします。  
  
-   選択した場合**いいえ**、SSMA 返された値を取得する DELETE ステートメントの前に、SELECT ステートメントが生成されます。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** はい  
  
### <a name="convert-returning-clause-in-insert-statement-to-output"></a>INSERT ステートメントの RETURNING 句を出力に変換します。  
DB2 は、すぐに、挿入された値を取得する方法として、RETURNING 句を提供します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OUTPUT 句と共に、その機能を提供します。  
  
-   選択した場合**はい**SSMA は、INSERT ステートメントで RETURNING 句を出力に変換されます。 テーブルのトリガーの値を変更できるため、返される値が異なる可能性があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DB2 の場合よりもします。  
  
-   選択した場合**いいえ**SSMA では、DB2 の機能をエミュレートして挿入と参照テーブルから値を選択します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** [はい]  
  
### <a name="convert-returning-clause-in-update-statement-to-output"></a>RETURNING 句で UPDATE ステートメントを出力に変換します。  
DB2 は、すぐに更新された値を取得する方法として、RETURNING 句を提供します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OUTPUT 句と共に、その機能を提供します。  
  
-   選択した場合**はい**OUTPUT 句には、SSMA を RETURNING 句で UPDATE ステートメントに変換されます。 テーブルのトリガーの値を変更できるため、返される値が異なる可能性があります[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DB2 の場合よりもします。  
  
-   選択した場合**いいえ**SSMA は返される値を取得する UPDATE ステートメントの後に SELECT ステートメントを生成します。  
  
変換モードを選択すると、**モード**SSMA ボックスには、次の設定が適用されます。  
  
**既定/オプティミスティック/フル モード:** [はい]  
  
## <a name="sequence-conversion"></a>シーケンスの変換  
  
### <a name="convert-sequence-generator"></a>シーケンス ジェネレーターを変換します。  
Db2 では、シーケンスを使用して一意の識別子を生成することができます。  
  
SSMA は、次のシーケンスを変換できます。  
  
-   SQL Server シーケンス ジェネレーターの (このオプションは使用可能な場合のみ SQL Server 2012 および SQL Server 2014 への変換) を使用します。  
  
-   SSMA シーケンス ジェネレーターを使用します。  
  
-   列の id を使用します。  
  
SQL Server 2012 または SQL Server 2014 に変換する際の既定のオプションでは、SQL Server シーケンス ジェネレーターを使用します。 ただし、SQL Server 2012 および SQL Server 2014 がサポートしていません (などを DB2 シーケンス currval メソッドの) 現在のシーケンス値を取得します。 ガイダンスについては、移行する DB2 シーケンス currval メソッドでの SSMA チーム ブログ サイトを参照してください。  
  
SSMA では、SSMA シーケンス エミュレーター DB2 シーケンスに変換することもできます。 これは、SQL Server 2012 より前変換する場合の既定のオプション  
  
最後に、SQL Server の id 値をテーブル内の列に割り当てられたシーケンスを変換することもできます。 DB2 で identity 列に、シーケンスの間のマッピングを指定する必要があります**テーブル** タブ  
  
### <a name="convert-currval-outside-triggers"></a>トリガーの外部の CURRVAL を変換します。  
変換のシーケンス ジェネレーターに設定されているときにのみ表示される**列 id を使用して**します。 DB2 のシーケンスはテーブルとは別のオブジェクトであるため、シーケンスを使用して多数のテーブルを生成し、新しいシーケンス値の挿入トリガーを使用します。 SSMA は、これらのステートメントをコメントまたはコメント アウト エラーが発生するときにエラーとしてマークを付けます。  
  
-   選択した場合**はい**SSMA は、変換後のトリガーの外部の警告 CURRVAL をシーケンス処理するすべての参照としてマークされます。  
  
-   選択した場合**いいえ**SSMA は、変換後のトリガーの外部エラー CURRVAL をシーケンス処理するすべての参照としてマークされます。  
  
## <a name="see-also"></a>関連項目  
[ユーザー インターフェイス リファレンス&#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
