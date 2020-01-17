---
title: ALTER TABLE - SQL コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- alter table [ODBC]
ms.assetid: 3a01a291-f4d9-43bc-a725-5a95546ff364
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8c78d3f20e5a03fc80029549318c9c53662e4121
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901377"
---
# <a name="alter-table---sql-command"></a>ALTER TABLE - SQL コマンド
プログラムによってテーブルの構造を変更します。  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER TABLE TableName1  
   ADD | ALTER [COLUMN] FieldName1  
      FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]  
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
 - Or -  
ALTER TABLE TableName1  
   ALTER [COLUMN] FieldName2  
      [NULL | NOT NULL]  
      [SET DEFAULT eExpression2]  
      [SET CHECK lExpression2 [ERROR cMessageText2]]  
      [DROP DEFAULT]  
      [DROP CHECK]  
 - Or -  
ALTER TABLE TableName1  
   [DROP [COLUMN] FieldName3]  
   [SET CHECK lExpression3 [ERROR cMessageText3]]  
   [DROP CHECK]  
   [ADD PRIMARY KEY eExpression3 TAG TagName2]  
   [DROP PRIMARY KEY]  
   [ADD UNIQUE eExpression4 [TAG TagName3]]  
   [DROP UNIQUE TAG TagName4]  
   [ADD FOREIGN KEY [eExpression5] TAG TagName4  
      REFERENCES TableName2 [TAG TagName5]]  
   [DROP FOREIGN KEY TAG TagName6 [SAVE]]  
   [RENAME COLUMN FieldName4 TO FieldName5]  
   [NOVALIDATE]  
```  
  
## <a name="arguments"></a>引数  
 *TableName1*  
 その構造が変更されたテーブルの名前を指定します。  
  
 [列] の追加*FieldName1*  
 追加するフィールドの名前を指定します。  
  
 ALTER [COLUMN] *FieldName1*  
 変更する既存のフィールドの名前を指定します。  
  
 *FieldType* [( *nFieldWidth* [, *nPrecision*]])  
 新しいまたは変更されたフィールドのフィールドの型、フィールドの幅、およびフィールドの有効桁数 (小数点以下桁数の数) を指定します。  
  
 *FieldType*を示す、フィールドの 1 つの文字は、[データ型](../../odbc/microsoft/visual-foxpro-field-data-types.md)します。 一部のフィールド データ型を指定することを必要と*nFieldWidth*または*nPrecision*またはその両方です。  
  
 *nFieldWidth*と*nPrecision* D、G は、L、M、P、T、Y を無視する型。 既定では、 *nPrecision*場合は 0 (数値) は、 *nPrecision*は、B、F、または N 型に対しては含まれません。  
  
 NULL &#124; NOT NULL  
 許可または、フィールドに null 値を防止します。  
  
 省略 NULL と NOT NULL、SET NULL の現在の設定は、フィールドで null 値を許容するかどうかを決定します。 ただし、NOT NULL NULL を省略し、主キーまたは一意の句を含める、SET NULL の現在の設定は無視され、フィールドがない既定では NULL です。  
  
 確認*lExpression1*  
 フィールドの検証規則を指定します。 *lExpression1*論理式を評価する必要があり、ユーザー定義関数またはストアド プロシージャを指定できます。 空のレコードを追加すると、されるたびに検証規則がチェックされます。 検証規則が追加されたレコードのフィールドが空白の値を許可しない場合は、エラーが生成されます。  
  
 ERROR *cMessageText1*  
 フィールドの検証規則がエラーを生成するときにエラー メッセージが表示されますを指定します。  
  
 既定の*eExpression1*  
 フィールドの既定値を指定します。 データ型*eExpression1*フィールドのデータ型と同じである必要があります。  
  
 PRIMARY KEY  
 プライマリ インデックス タグを作成します。 インデックスのタグには、フィールドと同じ名前があります。  
  
 UNIQUE  
 フィールドと同じ名前の候補のインデックスのタグを作成します。  
  
> [!NOTE]  
>  候補者 (ALTER TABLE または CREATE TABLE で ANSI 互換性を保つのため、独自のオプションを含めることによって作成された) インデックスとインデックス コマンドを独自のオプションを使用して作成されたインデックスは異なります。 UNIQUE INDEX コマンドを使用して作成されたインデックスにより、重複するインデックスのキー。候補となるインデックスでは、重複するインデックス キーは許可されません。  
  
 プライマリまたは候補のインデックスに使用されるフィールドには、null 値と重複するレコードが許可されていません。  
  
 追加の列を使用して新しいフィールドを作成する場合は、null 値をサポートするフィールドのプライマリまたは候補のインデックスを作成する場合、Visual FoxPro はいないエラーが生成されます。 ただし、Visual FoxPro であっても、プライマリまたは候補のインデックスに使用されるフィールドに null または重複する値を入力しようとする場合、エラーが生成されます。  
  
 既存のフィールドと、プライマリを変更する、またはテーブル内のフィールドから成る候補インデックスの式、Visual FoxPro は null 値または重複するレコードが含まれるかどうかを表示するフィールドを確認します。 その場合は、Visual FoxPro エラーが発生し、テーブルは変更されません。  
  
 参照*TableName2*タグ*TagName1*  
 永続的な関係を確立する親テーブルを指定します。 タグ*TagName1*リレーションシップの基になる、親テーブルのインデックスのタグを指定します。 タグのインデックス名は、最大 10 個の文字を含めることができます。  
  
 NOCPTRANS  
 文字およびメモ フィールドの異なるコード ページに変換できないようにします。 テーブルは別のコード ページに変換する場合、NOCPTRANS が指定されているフィールドは翻訳されません。 NOCPTRANS は文字とメモ フィールドに対してのみ指定できます。  
  
 次の例では、2 つのフィールドの文字と 2 つのメモ フィールドを含む mytable という名前のテーブルを作成します。 2 番目の文字のフィールド、char2、および 2 番目のメモ フィールド memo2、変換を防ぐために NOCPTRANS が含まれます。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [COLUMN] *FieldName2*  
 変更する既存のフィールドの名前を指定します。  
  
 既定値に設定*eExpression2*  
 既存のフィールドの新しい既定値を指定します。 データ型*eExpression2*フィールドのデータ型と同じである必要があります。  
  
 セット チェック*lExpression2*  
 既存のフィールドに対して新しい検証規則を指定します。 *lExpression2*論理式を評価する必要があり、ユーザー定義関数またはストアド プロシージャがあります。  
  
 ERROR *cMessageText2*  
 フィールドの検証規則がエラーを生成するときにエラー メッセージが表示されますを指定します。 参照または編集ウィンドウ内でデータが変更されたときにのみ、メッセージが表示されます。  
  
 DROP DEFAULT  
 既存のフィールドの既定値を削除します。  
  
 チェックを削除します。  
 既存のフィールドの検証規則を削除します。  
  
 [列] ドロップ*FieldName3*  
 テーブルから削除するフィールドを指定します。 テーブルからフィールドを削除すると、フィールドの既定値の設定とフィールド検証ルールも削除されます。  
  
 インデックスのキーまたはトリガーの式では、フィールドを参照する場合、式のフィールドが削除されると無効になります。 この場合、フィールドが削除されますが、無効なインデックスのキーまたはトリガーの式は実行時にエラーを生成、エラーは生成されません。  
  
 セット チェック*lExpression3*  
 テーブルの検証規則を指定します。 *lExpression3*論理式を評価する必要があり、ユーザー定義関数またはストアド プロシージャがあります。  
  
 ERROR *cMessageText3*  
 テーブルの検証ルールがエラーを生成するときに、エラー メッセージが表示されますを指定します。 参照または編集ウィンドウ内でデータが変更されたときにのみ、メッセージが表示されます。  
  
 チェックを削除します。  
 テーブルの検証規則を削除します。  
  
 追加のプライマリ キー *eExpression3*タグ*TagName2*  
 プライマリ インデックスをテーブルに追加します。 *eExpression3*プライマリ インデックスのキー式を指定し、 *TagName2*プライマリ インデックス タグの名前を指定します。 タグのインデックス名は、最大 10 個の文字を含めることができます。 場合タグ*TagName2*を省略すると、 *eExpression3* 1 つのフィールドは、プライマリ インデックス タグの同じ名前で指定されたフィールドとに*eExpression3*。  
  
 プライマリ キーを削除します  
 プライマリ インデックスとそのインデックス タグを削除します。 テーブルが 1 つのプライマリ キーを持てないために、主キーの名前を指定する必要はありません。 プライマリ インデックスを削除すると、主キーに基づく永続的なリレーションシップも削除されます。  
  
 追加の UNIQUE *eExpression4*[タグ*TagName3*]  
 候補のインデックスをテーブルに追加します。 *eExpression4*候補インデックスのキー式を指定し、 *TagName3*候補インデックス タグの名前を指定します。 タグのインデックス名は、最大 10 個の文字を含めることができます。 タグを省略した場合*TagName3*場合*eExpression4* 1 つのフィールドは、候補のインデックスのタグがで指定されたフィールドとして同じ名前を持つ*eExpression4*します。  
  
 一意のタグをドロップ*TagName4*  
 候補のインデックスとそのインデックス タグを削除します。 テーブルには、複数の候補キーを持つことができますため、候補のインデックスのタグの名前を指定する必要があります。  
  
 外部キーの追加 [ *eExpression5*] タグ*TagName4*  
 テーブルには、外部 (プライマリ) のインデックスを追加します。 *eExpression5*外部インデックスのキー式を指定し、 *TagName4*外部インデックス タグの名前を指定します。 タグのインデックス名は、最大 10 個の文字を含めることができます。  
  
 参照*TableName2*[タグ*TagName5*]  
 永続的な関係を確立する親テーブルを指定します。 タグを含める*TagName5*親テーブルの既存のインデックス タグに基づく関係を確立します。 タグのインデックス名は、最大 10 個の文字を含めることができます。 タグを省略した場合*TagName5*、親テーブルのプライマリ インデックスのタグを使用して関係を確立します。  
  
 DROP 外部キー タグ*TagName6*[保存]  
 インデックスのタグは、外部キーを削除します*TagName6*します。 保存を省略した場合、インデックスのタグは、構造のインデックスから削除されます。 構造のインデックスからインデックス タグの削除を防ぐために保存が含まれます。  
  
 列の名前の変更*FieldName4*TO *FieldName5*  
 テーブルのフィールドの名前を変更することができます。 *FieldName4*名前を変更するフィールドの名前を指定します。 *FieldName5*フィールドの新しい名前を指定します。  
  
> [!CAUTION]  
>  インデックス式、フィールドとテーブルの検証規則、コマンド、および関数は、元のフィールド名を参照できますので、テーブルのフィールドの名前を変更する場合は注意してください。  
  
 NOVALIDATE  
 Visual FoxPro にテーブルの構造体への変更ができることを指定しますこれらの変更は、テーブル内のデータの整合性を侵害する可能性があります。 既定では、Visual FoxPro テーブル内のデータの整合性に違反する変更を行う、ALTER TABLE ができないようにします。 この既定の動作をオーバーライドする NOVALIDATE が含まれます。  
  
## <a name="remarks"></a>コメント  
 ALTER TABLE を使用してをデータベースに追加されていないテーブルの構造を変更できます。 ただし、Visual FoxPro は、既定、外部キー、主キー、参照、または無料のテーブルを変更するときに、句を設定する場合にエラーが発生します。  
  
 ALTER TABLE では、新しいテーブル ヘッダーを作成し、テーブル ヘッダーにレコードを追加して、テーブルを再構築可能性があります。 たとえば、フィールドの型または幅を変更すると、再構築するテーブルが発生可能性があります。  
  
 テーブルが再構築後は、種類または幅が変更されたすべてのフィールドのフィールド検証ルールが実行されます。 型またはテーブルの任意のフィールドの幅を変更する場合は、テーブルのルールが実行されます。  
  
 レコードのあるテーブルのフィールドやテーブルの検証規則を変更する場合、Visual FoxPro は、既存のデータに対する新しいフィールドやテーブルの検証規則をテストしに最初に見つかった位置のフィールドやテーブルの検証規則またはトリガーに違反の警告を発行します。  
  
 変更するテーブルは、データベースの ALTER TABLE - SQL には、データベースを排他的に使用が必要です。 排他的に使用するデータベースを開くには、するには、開くデータベースの排他を含めます。  
  
## <a name="see-also"></a>関連項目  
 [CREATE TABLE - SQL コマンド](../../odbc/microsoft/create-table-sql-command.md)   
 [INDEX コマンド](../../odbc/microsoft/index-command.md)
