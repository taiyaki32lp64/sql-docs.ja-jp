---
title: SELECT - SQL コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- select [ODBC]
ms.assetid: 2149c3ca-3a71-446d-8d53-3d056e2f301a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85f281aefe79a09806c42e13cd771f976362d053
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943787"
---
# <a name="select---sql-command"></a>SELECT - SQL コマンド
1 つまたは複数のテーブルからデータを取得します。  
  
 Visual FoxPro ODBC ドライバーでは、このコマンドのネイティブの Visual FoxPro 言語の構文をサポートしています。 ドライバー固有の情報を参照してください。**ドライバー解説**します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT [ALL | DISTINCT]  
   [Alias.] Select_Item [AS Column_Name]  
   [, [Alias.] Select_Item [AS Column_Name] ...]   
FROM [DatabaseName!]Table [Local_Alias]  
   [, [DatabaseName!]Table [Local_Alias] ...]   
[WHERE JoinCondition [AND JoinCondition  
...]  
   [AND | OR FilterCondition [AND | OR FilterCondition ...]]]  
[GROUP BY GroupColumn [, GroupColumn ...]]  
[HAVING FilterCondition]  
[UNION [ALL] SELECTCommand]  
[ORDER BY Order_Item [ASC | DESC] [, Order_Item [ASC | DESC] ...]]  
```  
  
## <a name="arguments"></a>引数  
  
> [!NOTE]  
>  A*サブクエリ*、次の引数で参照される、SELECT、SELECT 内では、およびかっこで囲む必要があります。 同じレベルで最大 2 つのサブクエリを持つことができます (入れ子になっていない) WHERE 句でします。 (引数の該当セクションを参照してください)。サブクエリは、複数の結合条件を含めることができます。  
  
 [すべて&#124;DISTINCT]  [*エイリアス*]。*Select_Item* [AS *Column_Name*] [、[*エイリアス*]。*Select_Item* [AS *Column_Name*]...]  
 SELECT 句では、フィールド、定数、およびクエリの結果に表示される式を指定します。  
  
 、既定では、クエリ結果内のすべての行すべて表示します。  
  
 DISTINCT では、クエリの結果からすべての行の重複を除外します。  
  
> [!NOTE]  
>  SELECT 句、DISTINCT を 1 回だけを使用できます。  
  
 *エイリアス*します。 一致する項目の名前を修飾します。 各項目で指定した*Select_Item*クエリ結果の 1 つの列が生成されます。 2 つ以上の項目の同じ名前である場合は、テーブルの別名と列が重複することを防ぐために項目名の前にピリオドが含まれます。  
  
 *Select_Item*クエリの結果に含まれる項目を指定します。 項目には、次のいずれかを指定できます。  
  
-   FROM 句内のテーブルからのフィールドの名前。  
  
-   同じ定数値がクエリ結果のすべての行に表示されることを指定する定数。  
  
-   ユーザー定義関数の名前を指定できる式です。  
  
 **ユーザー定義関数での選択**  
  
 SELECT 句でユーザー定義関数を使用して明らかな利点がありますが、次の制限も考慮する必要があります。  
  
-   選択で実行される操作の速度は、このようなユーザー定義関数の実行速度によって制限される可能性があります。 ユーザー定義関数に関連する大量の操作は、API と C# またはアセンブリ言語で記述されたユーザー定義関数を使用してより実現可能性があります。  
  
-   選択から呼び出されるユーザー定義関数に値を渡す唯一信頼できる方法は、メソッドが呼び出されたときに、関数に渡される引数のリストです。  
  
-   FoxPro の特定のバージョンで正常に動作すると思われる禁止された操作を検出し、場合でもは引き続き以降のバージョンで動作する保証はありません。  
  
 これらの制限とは別のユーザー定義関数は、SELECT 句で許容されます。 ただし、SELECT を使用すると、パフォーマンスが低下することに注意してください。  
  
 次のフィールド関数は、select 項目には、フィールドまたはフィールドを含む式で使用できるようにします。  
  
-   AVG (*Select_Item*) の数値データの列の平均を計算します。  
  
-   カウント (*Select_Item*)-列の選択項目の数をカウントします。 COUNT(*) では、クエリの出力内の行の数をカウントします。  
  
-   MIN (*Select_Item*)-の最小値を決定*Select_Item*列にします。  
  
-   最大 (*Select_Item*)-の最大値を決定します。 *Select_Item*列にします。  
  
-   SUM (*Select_Item*) の数値データの列を合計します。  
  
 フィールドの関数を入れ子にすることはできません。  
  
 AS *Column_Name*  
 クエリの出力列の見出しを指定します。 これは、ときに便利です*Select_Item*式またはフィールドを含む関数とするが、列にわかりやすい名前を付与します。 *Column_Name*式を指定できますが、テーブルのフィールド名は許可されない文字 (スペースなど) を含めることはできません。  
  
 FROM [*DatabaseName*!]*Table* [*Local_Alias*]   [, [*DatabaseName*!]*Table* [*Local_Alias*] ...]  
 クエリで取得されたデータを含むテーブルを一覧表示します。 開いているテーブルがない場合は、Visual FoxPro が表示されます、**開く** ダイアログ ボックスのファイルの場所を指定できるようにします。 開かれた後、テーブルは、クエリが完了したら開いたのままです。  
  
 *DatabaseName*! データ ソースで指定されている以外のデータベースの名前を指定します。 データ ソースと、データベースが指定されていない場合は、テーブルを含むデータベースの名前を含める必要があります。 データベース名の後に、テーブル名の前に感嘆符 (!) 区切り記号が含まれます。  
  
 *Local_Alias*でという名前のテーブルの一時的な名前を指定します*テーブル*します。 ローカルのエイリアスを指定する場合は、SELECT ステートメントでテーブル名ではなくローカルのエイリアスを使用する必要があります。 ローカルのエイリアスでは、Visual FoxPro 環境は影響しません。  
  
 場所*JoinCondition* [AND *JoinCondition* ...]   [AND&#124;または*FilterCondition* [AND&#124;または*FilterCondition* ...]  
 Visual FoxPro、クエリの結果に特定のレコードだけを含めるように指示します。 複数のテーブルからデータを取得するために必要な場合。  
  
 *JoinCondition* FROM 句でテーブルをリンクするフィールドを指定します。 1 つ以上のテーブルをクエリに含める場合、最初より後すべてのテーブルの結合条件を指定する必要があります。  
  
> [!IMPORTANT]  
>  結合条件を作成するときに、次の情報を考慮してください。  
  
-   クエリに 2 つのテーブルを含めるし、結合条件を指定しない場合、フィルター条件が満たされる限り、最初のテーブル内のすべてのレコードが 2 番目のテーブルのすべてのレコードに結合されます。 このようなクエリでは、長い結果を生成できます。  
  
-   Visual FoxPro 空のフィールドに一致するために、空のフィールドを持つテーブルを結合する際に、注意を使用します。 たとえば、顧客に参加している場合です。ZIP と請求書。Zip 圧縮し、クエリの出力には顧客には、空の 100 の zip コードが含まれています。 請求書には、空の zip コードの 400 が含まれている場合は、空のフィールドによって作成された 40,000 の余分なレコードが含まれています。 使用して、**空 ()** クエリ出力から空のレコードを排除する関数。  
  
-   AND 演算子を使用して、複数の結合条件を接続する必要があります。 各結合条件では、次の形式があります。  
  
     *FieldName1 比較 FieldName2*  
  
     *FieldName1* 1 つのテーブルからのフィールドの名前を指定*FieldName2*別のテーブルからのフィールドの名前を指定および*比較*は、次の表で説明されている演算子の 1 つです。  
  
|演算子|条件式|  
|--------------|----------------|  
|=|等しい|  
|==|正確に等しい|  
|LIKE|ような SQL|  
|<>, !=, #|等しくない|  
|>|複数の|  
|>=|大きいか等しい|  
|<|次の値未満|  
|<=|以下|  
  
 使用すると、= 演算子、文字列、動作が異なる、設定の ANSI の設定に応じて。 ANSI の設定が OFF に設定されている場合、Visual FoxPro は、Xbase ユーザーが使い慣れている方法で文字列比較を扱います。 ANSI の設定が ON に設定されている場合、Visual FoxPro には、文字列比較のための ANSI 規格に従います。 参照してください[設定の ANSI](../../odbc/microsoft/set-ansi-command.md)と[設定の正確な](../../odbc/microsoft/set-exact-command.md)Visual FoxPro が文字列の比較を実行する方法の詳細についてはします。  
  
 *FilterCondition*クエリの結果に含まれるレコードが満たす必要のある条件を指定します。 AND で接続して、必要な数のフィルター クエリ内の条件を含めることができますか、OR 演算子。 NOT 演算子を使用して、論理式の値を反転するかを使用することができます**空 ()** 空のフィールドを確認します。 *FilterCondition*次の例で、フォームのいずれかを実行できます。  
  
 **例 1** *FieldName1 比較 FieldName2*  
  
 `customer.cust_id = orders.cust_id`  
  
 **例 2** *FieldName 比較式*  
  
 `payments.amount >= 1000`  
  
 **例 3** *FieldName 比較*すべて (*サブクエリ*)  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 フィルター条件には、すべてが含まれている場合、フィールドは、そのレコードがクエリ結果に含める前に、サブクエリによって生成されたすべての値の比較条件を満たす必要があります。  
  
 **例 4** *FieldName 比較*ANY &#124; SOME (*サブクエリ*)  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 フィルター条件は、いずれかまたはいくつか含まれている場合、フィールドは、サブクエリによって生成された値の少なくとも 1 つの比較条件を満たす必要があります。  
  
 次の例は、フィールドの値が値の指定した範囲内かどうかを確認します。  
  
 **例 5** *FieldName* [NOT] BETWEEN *Start_Range* AND *End_Range*  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 次の例は、少なくとも 1 つの行が、サブクエリの条件を満たすかどうかを確認します。 フィルター条件が True に評価された、フィルター条件には、EXISTS が含まれている場合 (します。T.) しない限り、空のセットにサブクエリが評価されます。  
  
 **例 6** [NOT] が存在する (*サブクエリ*)  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **例 7** *FieldName* [NOT] IN *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 フィルター条件に含まれる場合、そのレコードがクエリ結果に含める前に、フィールドが、値のいずれかを含める必要があります。  
  
 **例 8** *FieldName* [NOT] IN (*サブクエリ*)  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 ここで、フィールドでは、そのレコードがクエリ結果に含める前に、サブクエリによって返される値の 1 つ含める必要があります。  
  
 **例 9** *FieldName* [NOT] LIKE *cExpression*  
  
 `customer.country NOT LIKE "USA"`  
  
 このフィルター条件に一致する各フィールドを検索*cExpression*します。 パーセント記号 (%) を使用することができます。一部として、アンダー スコア (_) ワイルドカード文字と*cExpression*します。 アンダー スコアは、文字列内の 1 つの不明な文字を表します。  
  
 GROUP BY *GroupColumn* [、 *GroupColumn* ...]  
 1 つまたは複数の列の値に基づくクエリで行グループ。 *GroupColumn*次のいずれかを指定できます。  
  
-   通常のテーブルのフィールドの名前。  
  
-   SQL フィールド関数を含むフィールドです。  
  
-   結果のテーブル内の列の位置を示す数値式。 (左端の列数は 1 です)。  
  
 ある*FilterCondition*  
 クエリの結果に含まれるグループが満たす必要のあるフィルター条件を指定します。 HAVING は GROUP BY を使用する必要があり、AND で接続されている、必要な数のフィルター条件を含めることができますか、OR 演算子。 論理式の値を逆に使用することもできます。  
  
 *FilterCondition*サブクエリを含めることはできません。  
  
 HAVING 句、GROUP BY 句なしでは、WHERE 句のように動作します。 HAVING 句では、ローカルのエイリアスとフィールド関数を使用できます。 HAVING 句に関数フィールドにはが含まれていない場合は、パフォーマンスを向上させる、where 句を使用します。  
  
 [ALL] 共用体*SELECTCommand*]  
 もう 1 つの SELECT の最終的な結果を 1 つの SELECT の最終的な結果を結合します。 既定は、共用体は、結合された結果をチェックし、重複する行を除外します。 かっこを使用して、複数の UNION 句を結合します。  
  
 すべては共用体が結合された結果から重複する行を排除することを防ぎます。  
  
 UNION 句では、これらの規則に従います。  
  
-   共用体を使用して、サブクエリを結合することはできません。  
  
-   両方のコマンドを選択、クエリ出力に同じ数の列が必要です。  
  
-   1 つの SELECT のクエリ結果内の各列は、その他の選択に対応する列として、同じデータ型と幅が必要です。  
  
-   最後の選択 だけには、番号で出力列を参照する必要がある ORDER BY 句、ことができます。 ORDER BY 句が含まれている場合は、完全な結果に影響します。  
  
 外部結合をシミュレートするために、UNION 句を使用することもできます。  
  
 クエリで 2 つのテーブルを結合すると、出力に、結合フィールドに値が一致するレコードのみが含まれます。 親テーブル内のレコードには、子テーブルの対応するレコードがない場合、出力には、親テーブル内のレコードが含まれていません。 外部結合では、子テーブルで一致するレコードと一緒に出力では、親テーブルのすべてのレコードを含めることができます。 Visual FoxPro の外部結合を作成するには、次の例のように、入れ子になった SELECT コマンドを使用する必要があります。  
  
```  
SELECT customer.company, orders.order_id, orders.emp_id ;  
FROM customer, orders ;  
WHERE customer.cust_id = orders.cust_id ;  
UNION ;  
SELECT customer.company, 0, 0 ;  
FROM customer ;  
WHERE customer.cust_id NOT IN ;  
(SELECT orders.cust_id FROM orders)  
```  
  
> [!NOTE]  
>  各セミコロンの直前にあるスペースを含めることを確認します。 それ以外の場合、エラーが表示されます。  
  
 UNION 句は、両方のテーブルからレコードを選択します。 前に、コマンドのセクションがある一致する値。 関連付けられている請求書がない顧客企業は含まれません。 UNION 句の後にコマンドのセクションでは、一致するレコードを orders テーブルではありませんが、customer テーブルのレコードを選択します。  
  
 2 番目のコマンドは、セクションに関する次のことを確認してください。  
  
-   かっこの中で SELECT ステートメントは、最初に処理されます。 このステートメントでは、orders テーブルのすべての顧客番号の選択範囲を作成します。  
  
-   WHERE 句は、orders テーブルにない、customer テーブル内のすべての顧客番号を検索します。 コマンドの最初のセクションに、orders テーブルで、顧客番号のあるすべての会社が提供されているので、customer テーブル内のすべての企業はようになりましたクエリの結果に含まれます。  
  
-   2 番目の SELECT ステートメントを表すために 2 つのプレース ホルダーがある共用体に含まれるテーブルの構造は同じである必要があります、ため*orders.order_id*と*orders.emp_id*最初の選択からステートメント。  
  
    > [!NOTE]  
    >  プレース ホルダーは、それが表すフィールドと同じ型である必要があります。 プレース ホルダーをする必要があります、フィールドが日付型の場合は、{//}。 プレース ホルダーが空の文字列には、フィールドが文字のフィールドの場合は、("")。  
  
 ORDER BY *Order_Item* [ASC &#124; DESC] [、 *Order_Item* [ASC &#124; DESC]...]  
 1 つまたは複数の列のデータをに基づいて、クエリの結果を並べ替える。 各*Order_Item*クエリ結果内の列に対応する必要があり、次のいずれかを指定できます。  
  
-   (サブクエリ) ではなく、メインの SELECT 句で select 項目になっている FROM テーブル内のフィールド。  
  
-   結果のテーブル内の列の位置を示す数値式。 (左端の列の番号は 1 です)。  
  
 ASC は、注文アイテムまたはアイテムに基づいて、クエリの結果を昇順を指定します、ORDER BY の既定値です。  
  
 DESC には、クエリの結果を降順を指定します。  
  
 ORDER BY で注文を指定しない場合は、順序付けられていないクエリの結果が表示されます。  
  
## <a name="remarks"></a>コメント  
 選択は、Visual FoxPro、他の Visual FoxPro コマンドのように組み込まれた SQL コマンドです。 使用すると、クエリが発生する選択、Visual FoxPro は、クエリを解釈し、テーブルから、指定されたデータを取得します。 (Visual FoxPro コマンド) と同様、コマンド プロンプト ウィンドウまたは Visual FoxPro プログラム内から SELECT クエリを作成できます。  
  
> [!NOTE]  
>  選択は、フィルターの設定で指定された現在のフィルター条件を優先しません。  
  
## <a name="driver-remarks"></a>ドライバーの解説  
 アプリケーションでは、ODBC SQL ステートメント を選択をデータ ソースに送信するときに Visual FoxPro ODBC ドライバーは、コマンドには、ODBC エスケープ シーケンスが含まれていない場合、翻訳しないで Visual FoxPro 選択コマンドにコマンドを変換します。 ODBC エスケープ シーケンスで囲まれた項目は、Visual FoxPro 構文に変換されます。 ODBC を使用しての詳細については、エスケープ シーケンスは、「[時刻および日付関数](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md)し、 *Microsoft ODBC プログラマ リファレンス*、を参照してください[odbc エスケープ シーケンス](../../odbc/reference/develop-app/escape-sequences-in-odbc.md).  
  
## <a name="see-also"></a>関連項目  
 [CREATE TABLE - SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL](../../odbc/microsoft/insert-sql-command.md)   
 [セットの ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [正確な設定します。](../../odbc/microsoft/set-exact-command.md)
