---
title: CREATE TABLE - SQL コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE [ODBC]
ms.assetid: be2143ba-fc16-42c9-84f7-8985cd924860
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f979ccb5a44ada8e86424e0f6134f39d28a021d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096599"
---
# <a name="create-table---sql-command"></a>CREATE TABLE - SQL コマンド
指定したフィールドを持つテーブルを作成します。  
  
 Visual FoxPro ODBC ドライバーでは、このコマンドのネイティブの Visual FoxPro 言語の構文をサポートしています。 ドライバー固有の情報を参照してください。**ドライバー解説**します。  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE TABLE | DBF TableName1 [NAME LongTableName] [FREE]  
   (FieldName1FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]   
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
   [, FieldName2 ...]  
      [, PRIMARY KEY eExpression2 TAG TagName2  
      |, UNIQUE eExpression3 TAG TagName3]  
      [, FOREIGN KEY eExpression4 TAG TagName4 [NODUP]  
            REFERENCES TableName3 [TAG TagName5]]  
      [, CHECK lExpression2 [ERROR cMessageText2]])  
| FROM ARRAY ArrayName  
```  
  
## <a name="arguments"></a>引数  
 テーブルを作成する&#124;DBF *TableName1*  
 作成するテーブルの名前を指定します。 テーブルと DBF のオプションは同じです。  
  
 名前*LongTableName*  
 テーブルの長い名前を指定します。 長いテーブル名がデータベースに格納されているために、データベースが開いたときにのみ、長いテーブル名を指定できます。  
  
 長い名前は、最大 128 文字を含めることができ、データベース内の短いファイル名の代わりに使用できます。  
  
 FREE  
 テーブルが開いているデータベースに追加されませんを指定します。 FREE は、データベースが開いていない場合に必要はありません。  
  
 *(FieldName1 FieldType* [( *nFieldWidth* [、 *nPrecision*])]  
 フィールド名、フィールドの型、フィールドの幅、およびフィールドの有効桁数 (小数点以下桁数の番号) をそれぞれ指定します。  
  
 *FieldType*フィールドのことを示す 1 つの文字は、[データ型](../../odbc/microsoft/visual-foxpro-field-data-types.md)します。 一部のフィールド データ型を指定することを必要と*nFieldWidth*または*nPrecision*またはその両方です。  
  
 *nFieldWidth*と*nPrecision* D、G は、L、M、P、T、Y を無視する型。 *nPrecision*場合の既定値 0 (数値) *nPrecision* B、F、または N 型に対して含まれていません。  
  
 NULL  
 フィールドの null 値を許可します。  
  
 NOT NULL  
 フィールドの値を null にできないようにします。  
  
 省略 NULL と NOT NULL、SET NULL の現在の設定は、フィールドで null 値を許容するかどうかを決定します。 ただし、NOT NULL NULL を省略し、主キーまたは一意の句を含める、NULL に設定の現在の設定は無視され、フィールドの既定値は NOT NULL します。  
  
 確認*lExpression1*  
 フィールドの検証規則を指定します。 *lExpression1*ユーザー定義関数であることができます。 空のレコードを追加すると、されるたびに検証規則がチェックされます。 検証規則では、追加されたレコードのフィールドが空白の値が許可されていませんがある場合は、エラーが生成されます。  
  
 ERROR *cMessageText1*  
 Visual FoxPro は、フィールド規則は、エラーを生成するときに表示されます。 エラー メッセージを指定します。 [参照] ウィンドウまたは編集ウィンドウ内でデータが変更されたときにのみ、メッセージが表示されます。  
  
 既定の*eExpression1*  
 フィールドの既定値を指定します。 データ型*eExpression1*フィールドのデータ型と同じである必要があります。  
  
 PRIMARY KEY  
 フィールドのプライマリ インデックスを作成します。 プライマリ インデックス タグでは、フィールドと同じ名前があります。  
  
 UNIQUE  
 フィールドの候補のインデックスを作成します。 候補のインデックス タグでは、フィールドと同じ名前があります。  
  
> [!NOTE]  
>  候補者 (CREATE TABLE または ALTER TABLE - SQL で独自のオプションを含めることによって作成された) インデックスは、INDEX コマンドに固有のオプションを使用して作成されたインデックスと同じではありません。 INDEX コマンドに固有のオプションを使用して作成されたインデックスにより、重複するインデックスのキー。候補となるインデックスでは、重複するインデックス キーは許可されません。 参照してください[インデックス](../../odbc/microsoft/index-command.md)固有のオプションの詳細についてはします。  
  
 プライマリまたは候補のインデックスを使用するフィールドには、null 値と重複するレコードが許可されていません。 ただし、null 値をサポートするフィールドのプライマリまたは候補のインデックスを作成する場合、Visual FoxPro はエラーを生成しません。 Visual FoxPro には、プライマリまたは候補のインデックスに使用されるフィールドに null または重複する値を入力しようとした場合に、エラーが発生します。  
  
 参照*TableName2*[タグ*TagName1*]  
 永続的な関係を確立する親テーブルを指定します。 タグを省略した場合*TagName1*、親テーブルのプライマリ インデックスのキーを使用して関係を確立します。 親テーブルがプライマリ インデックスを持たない場合、Visual FoxPro はエラーを生成します。  
  
 タグを含める*TagName1*親テーブルの既存のインデックス タグに基づく関係を確立します。 タグのインデックス名は、最大 10 個の文字を含めることができます。  
  
 親テーブルには、無料のテーブルをすることはできません。  
  
 NOCPTRANS  
 文字およびメモ フィールドの異なるコード ページに変換できないようにします。 テーブルは別のコード ページに変換する場合、NOCPTRANS が指定されているフィールドは翻訳されません。 NOCPTRANS は文字とメモ フィールドに対してのみ指定できます。  
  
 次の例では、2 つのフィールドの文字と 2 つのメモ フィールドを含む mytable という名前のテーブルを作成します。 2 番目の文字のフィールド、char2、および 2 番目のメモ フィールド memo2、変換を防ぐために NOCPTRANS が含まれます。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 主キー *eExpression2*タグ*TagName2*  
 プライマリのインデックスを作成するを指定します。 *eExpression2*テーブルのすべてのフィールドまたはフィールドの組み合わせを指定します。 タグ*TagName2*作成されるプライマリ インデックス タグの名前を指定します。 タグのインデックス名は、最大 10 個の文字を含めることができます。  
  
 テーブルが 1 つだけのプライマリ インデックスを持てないために、フィールドのプライマリ インデックスを既に作成している場合、この句を含めることはできません。 Visual FoxPro は、テーブルの作成に主キーの 1 つ以上の句を含める場合は、エラーを生成します。  
  
 一意*eExpression3*タグ*TagName3*  
 候補のインデックスを作成します。 *eExpression3*テーブルのすべてのフィールドまたはフィールドの組み合わせを指定します。 ただし、プライマリ キーのオプションのいずれかのプライマリ インデックスを作成した場合は、プライマリ インデックスで指定されたフィールドを含めることはできません。 タグ*TagName3*作成される候補インデックス タグのタグ名を指定します。 タグのインデックス名は、最大 10 個の文字を含めることができます。  
  
 テーブルには、複数の候補となるインデックスを持つことができます。  
  
 外部キー *eExpression4*タグ*TagName4*[NODUP]  
 外部 (プライマリ) のインデックスを作成し、親テーブルとのリレーションシップを確立します。 *eExpression4*外部インデックスのキー式を指定し、 *TagName4*作成される外部インデックス キーのタグの名前を指定します。 タグのインデックス名は、最大 10 個の文字を含めることができます。 候補の外部インデックスを作成する NODUP が含まれます。  
  
 複数の外部テーブル、インデックスを作成できますが、外部インデックス式は、テーブル内のさまざまなフィールドを指定する必要があります。  
  
 参照*TableName3*[タグ*TagName5*]  
 永続的な関係を確立する親テーブルを指定します。 タグを含める*TagName5*親テーブルのインデックス タグに基づく関係を確立します。 タグのインデックス名は、最大 10 個の文字を含めることができます。 タグを省略した場合、既定で*TagName5、* 親テーブルのプライマリ インデックスのキーを使用して関係を確立します。  
  
 CHECK *eExpression2*[ERROR *cMessageText2*]  
 テーブルの検証規則を指定します。 エラー *cMessageText2* Visual FoxPro は、テーブルの検証ルールが実行されたときに表示されます。 エラー メッセージを指定します。 データ [参照] ウィンドウで変更されたかウィンドウを編集する場合にのみ、メッセージが表示されます。  
  
 配列から*ArrayName*  
 既存の名前、型、有効桁数、およびテーブル内の各フィールドの小数点以下桁数で構成される配列の名前を指定します。 配列の内容を定義すること、 **AFIELDS**() 関数。  
  
## <a name="remarks"></a>コメント  
 新しいテーブルでは、利用可能な最小の作業領域でが開かれ、そのエイリアスを使用してアクセスできます。 排他的な設定の現在の設定に関係なく、新しいテーブルが排他的に開かれます。  
  
 データベースが開かれていると、無料の句を指定しないと、新しいテーブルがデータベースに追加されます。 データベースのテーブルと同じ名前で新しいテーブルを作成できません。  
  
 データベースが開いている場合は、CREATE TABLE - SQL には、データベースを排他的に使用が必要です。 排他的に使用するデータベースを開くには、するには、開くデータベースの排他を含めます。  
  
 新しいテーブルを作成するときに、データベースが開いていない場合は、名前、チェック、既定、外部キー、主キー、または参照の句を含むエラーを生成します。  
  
> [!NOTE]  
>  CREATE TABLE 構文は、特定のテーブルの作成オプションを区切るコンマを使用します。 また、列定義を含むかっこの中で、NULL、いない NULL、チェック、既定、主キー、および一意の句を配置しなければなりません。  
  
## <a name="driver-remarks"></a>ドライバーの解説  
 アプリケーションが ODBC SQL ステートメントを送信するときに Visual FoxPro ODBC ドライバーであるデータ ソースにテーブルを作成、次の表に示す構文を使用して Visual FoxProCREATE テーブル コマンドをコマンドに変換します。  
  
|ODBC 構文|Visual FoxPro 構文|  
|-----------------|--------------------------|  
|CREATE TABLE *base-table-name*<br /><br /> (*列識別子のデータ型*<br /><br /> [NULL 以外]<br /><br /> [、*列識別子のデータ型*<br /><br /> [NOT NULL]...)|テーブルを作成する*TableName1* [名前*LongTableName*]<br /><br /> (*FieldName1* *FieldType*<br /><br /> [(*nFieldWidth* [, *nPrecision*])]<br /><br /> [NULL 以外])|  
  
 ドライバーを使用してテーブルを作成するときに、ドライバーは、他のユーザーがテーブルにアクセスできるように作成後すぐに、テーブルを閉じます。 これは、Visual FoxPro は、テーブルを作成時にのみ開いたままにするとは異なります。 ただし、CREATE TABLE ステートメントを含む、データ ソースのストアド プロシージャが実行されたテーブルが開いたままです。  
  
 Visual FoxPro ODBC ドライバーがという名前のテーブルを作成し、データ ソースがデータベース (.dbc ファイル) の場合は、 *LongTableName*と同じ名前で、*ベース テーブル名*します。  
  
### <a name="using-data-definition-language-ddl"></a>データ定義言語 (DDL) を使用します。  
 DDL は、次の場所に含めることはできません。  
  
-   SQL ステートメントのバッチでトランザクションが必要です。  
  
-   アプリケーションが最初に呼び出す場合を除き、トランザクションを必要とするステートメントの後の手動コミット モードで**SQLTransact**します。  
  
 たとえば、一時テーブルを作成する場合は、トランザクションを必要とするステートメントを開始する前にテーブルを作成する必要があります。 バッチ トランザクションを必要とする SQL ステートメントに CREATE TABLE ステートメントを含めると、ドライバーはエラー メッセージを返します。  
  
## <a name="see-also"></a>関連項目  
 [ALTER TABLE - SQL コマンド](../../odbc/microsoft/alter-table-sql-command.md)   
 [サポートされるデータ型 (Visual FoxPro ODBC ドライバー)](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [INSERT - SQL コマンド](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT - SQL コマンド](../../odbc/microsoft/select-sql-command.md)
