---
title: 式の例 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 03/08/2017
ms.openlocfilehash: 77aca108aa3acae73dfb3fa226aa0530b6a9b8b5
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661283"
---
# <a name="expression-examples-report-builder-and-ssrs"></a>式の例 (レポート ビルダーおよび SSRS)

レポートでは、内容と外観を制御するために式をよく使用します。 式はで[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]記述され、組み込み関数のカスタムコード、レポート変数、グループ変数、およびユーザー定義変数を使用できます。 式は等号 (=) で始まります。 式エディターと使用できる参照の種類の詳細については、「[レポートでの式の使用 &#40;レポート ビルダーおよび SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)」および「[式の追加 &#40;レポート ビルダーおよび SSRS&#41;](add-an-expression-report-builder-and-ssrs.md)」を参照してください。  

> [!IMPORTANT]  
>  RDL サンドボックスが有効になっている場合は、レポートのパブリッシュ時に式のテキストで使用できる型およびメンバーが特定の型およびメンバーに制限されます。 詳細については、「 [RDL サンドボックスの有効化と無効化](../enable-and-disable-rdl-sandboxing.md)」を参照してください。  

このトピックでは、レポート内で一般的なタスクに使用できる式の例を示します。  

-   [Visual Basic の関数](#VisualBasicFunctions) [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] の日付関数、文字列関数、変換関数、および条件関数の例。  

-   [レポートの関数](#ReportFunctions) 集計および組み込みのレポート関数の例。  

-   [レポート データの表示方法](#AppearanceofReportData) レポートの外観を変更する例。  

-   [プロパティ](#Properties) 形式または表示を制御するために、レポート アイテムのプロパティを設定する例。  

-   [パラメーター](#Parameters) 式の中でパラメーターを使用する例。  

-   [カスタム コード](#CustomCode) 埋め込まれたカスタム コードの例。  

特定用途ごとの式の例については、次のトピックを参照してください。  

-   [グループ式の例 &#40;レポート ビルダーおよび SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  

-   [フィルター式の例 &#40;レポート ビルダーおよび SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)  

-   [一般的に使用されるフィルター &#40;レポート ビルダーおよび SSRS&#41;](commonly-used-filters-report-builder-and-ssrs.md)  

-   [レポート変数コレクションとグループ変数コレクションの参照 &#40;レポート ビルダーおよび SSRS&#41;](built-in-collections-report-and-group-variables-references-report-builder.md)  

単純型と複合型の式、式を使用できる場所、式に使用できる参照の種類など、レポート式の詳細については、「 [式 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)」を参照してください。 式が集計の計算のために評価されるコンテキストの詳細については、「[合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  

多数の関数および演算子がこのトピックでも式の例に使用されていますが、これらを使用して式を作成する方法をレポート作成のコンテキストで学習するには、「[チュートリアル:式の概要](../tutorial-introducing-expressions.md)」を参照してください。  

式エディターには、組み込み関数を階層形式で表示できるビューが用意されています。 特定の関数を選択すると、[値] ペインにコード例が表示されます。 詳細については、[レポートビルダー &#40;&#41;](../expression-dialog-box-report-builder.md)[[式] ダイアログボックス](../expression-dialog-box.md)または [式] ダイアログボックスを参照してください。  

## <a name="functions"></a>関数  

レポート内の多くの式には、関数が含まれています。 これらの関数を使用して、データの書式を設定し、ロジックを適用し、レポートのメタデータにアクセスできます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] ランタイム ライブラリの関数や、<xref:System.Convert> 名前空間および <xref:System.Math> 名前空間の関数を使用する式を記述できます。 また、他のアセンブリまたはカスタム コードの関数への参照も追加できます。 また、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]などの <xref:System.Text.RegularExpressions>」を参照してください。  

###  <a name="VisualBasicFunctions"></a> Visual Basic の関数  
[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] の関数を使用して、テキスト ボックスに表示されるデータや、レポートのパラメーター、プロパティ、または他の領域に使用されるデータを操作できます。 ここでは、このような関数のうち、いくつかの例を紹介します。 各関数の詳細については、MSDN の「 [Visual Basic ランタイム ライブラリのメンバー](https://go.microsoft.com/fwlink/?LinkId=198941) 」を参照してください。  

[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] には、日付固有の書式など、さまざまなカスタム書式が用意されています。 詳細については、MSDN の「 [型の書式設定](https://go.microsoft.com/fwlink/?LinkId=112024) 」を参照してください。  

#### <a name="math-functions"></a>算術関数  

-   `Round` 関数は、数値を最も近い整数に丸める場合に役立ちます。 次の式は、1.3 を 1 に丸めます。  

```  
= Round(1.3)  
```  

Excel の `MRound` 関数のように、指定の倍数値に値を丸める式を記述することもできます。 整数値を作成する係数で値を乗算し、その数値を丸め、同じ係数で除算します。 たとえば、1.3 を最も近い 0.2 の倍数 (1.4) に丸めるには、次の式を使用します。  

```  
= Round(1.3*5)/5  
```  

####  <a name="DateFunctions"></a> 日付関数  

-   `Today` 関数は現在の日付を返します。 この式は、レポートに日付を表示するテキスト ボックス、または現在の日付に基づいてデータをフィルター処理するパラメーターに使用できます。  

```  
=Today()  
```  

-   `DateAdd` 関数は、1 つのパラメーターに基づいて日付の範囲を指定する場合に役立ちます。 次の式では、 *StartDate*という名前のパラメーターで指定した日付の 6 か月後の日付が返されます。  

```  
=DateAdd(DateInterval.Month, 6, Parameters!StartDate.Value)  
```  

-   `Year` 関数は、特定の日付の年を表示します。 この関数を使用して、日付をグループ化したり、一連の日付のラベルとして年を表示したりできます。 次の式では、指定した販売注文日グループの年が返されます。 また、`Month` 関数および他の関数を使用して、日付を操作することもできます。 詳細については、次を参照してください。、[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]ドキュメント。  

```  
=Year(Fields!OrderDate.Value)  
```  

-   式の中で関数を組み合わせることで、形式をカスタマイズすることができます。 次の式は、"月-日-年" の日付の形式を "月-週番号" に変更します。 たとえば、"12/23/2009" は "December Week 3" になります。  

```  
=Format(Fields!MyDate.Value, "MMMM") & " Week " &   
(Int(DateDiff("d", DateSerial(Year(Fields!MyDate.Value),   
Month(Fields!MyDate.Value),1), Fields!FullDateAlternateKey.Value)/7)+1).ToString  
```  

この式をデータセット内の計算フィールドとしてグラフで使用すると、各月の週ごとに値を集計できます。  

-   次の式は、SellStartDate の値を MMM-YY の書式で設定します。 SellStartDate フィールドは、datetime データ型です。  

```  
=FORMAT(Fields!SellStartDate.Value, "MMM-yy")  
```  

-   次の式は、SellStartDate の値を dd/MM/yyyy の書式で設定します。 SellStartDate フィールドは、datetime データ型です。  

```  
=FORMAT(Fields!SellStartDate.Value, "dd/MM/yyyy")  
```  

-   `CDate` 関数は、値を日付に変換します。 `Now` 関数は、使用中のシステムに応じて、現在の日付と時刻を含む日付値を返します。 `DateDiff` は、2 つの日付値の間にある期間を数値で示す Long 値を返します。  

次の例では、今年の最初の日が表示されます。  

```  
=DateAdd(DateInterval.Year,DateDiff(DateInterval.Year,CDate("01/01/1900"),Now()),CDate("01/01/1900"))  
```  

-   次の例では、現在の月に基づいて、前の月の最初の日が表示されます。  

```  
=DateAdd(DateInterval.Month,DateDiff(DateInterval.Month,CDate("01/01/1900"),Now())-1,CDate("01/01/1900"))  
```  

-   次の式は、SellStartDate と LastReceiptDate の間にある年数を生成します。 これらのフィールドは、DataSet1 と DataSet2 の異なる 2 つのデータセットに含まれます。 集計関数である [First 関数 &#40;レポート ビルダーおよび SSRS&#41;](report-builder-functions-first-function.md) は、DataSet1 にある SellStartDate の最初の値と、DataSet2 にある LastReceiptDate の最初の値を返します。  

```  
=DATEDIFF("yyyy", First(Fields!SellStartDate.Value, "DataSet1"), First(Fields!LastReceiptDate.Value, "DataSet2"))  
```  

-   `DatePart` 関数は、特定の日付値の指定されたコンポーネントを含む整数値を返します。次の式は、DataSet1 にある SellStartDate の最初の値の年を返します。 レポートに複数のデータセットがあるため、データセット スコープが指定されます。  

```  
=Datepart("yyyy", First(Fields!SellStartDate.Value, "DataSet1"))  

```  

-   `DateSerial` 関数は、時間情報が午前 0 時に設定されている、指定の年月日を表す日付値を返します。 次の例では、現在の月に基づいて、前の月の最終日が表示されます。  

```  
=DateSerial(Year(Now()), Month(Now()), "1").AddDays(-1)  
```  

-   次の式では、ユーザーによって選択された日付のパラメーター値に基づくさまざまな日付が表示されます。  

|例の説明|例|  
|-------------------------|-------------|  
|[昨日]|`=DateSerial(Year(Parameters!TodaysDate.Value),Month(Parameters!TodaysDate.Value),Day(Parameters!TodaysDate.Value)-1)`|  
|2 日前|`=DateSerial(Year(Parameters!TodaysDate.Value),Month(Parameters!TodaysDate.Value),Day(Parameters!TodaysDate.Value)-2)`|  
|1 か月前|`=DateSerial(Year(Parameters!TodaysDate.Value),Month(Parameters!TodaysDate.Value)-1,Day(Parameters!TodaysDate.Value))`|  
|2 か月前|`=DateSerial(Year(Parameters!TodaysDate.Value),Month(Parameters!TodaysDate.Value)-2,Day(Parameters!TodaysDate.Value))`|  
|1 年前|`=DateSerial(Year(Parameters!TodaysDate.Value)-1,Month(Parameters!TodaysDate.Value),Day(Parameters!TodaysDate.Value))`|  
|2 年前|`=DateSerial(Year(Parameters!TodaysDate.Value)-2,Month(Parameters!TodaysDate.Value),Day(Parameters!TodaysDate.Value))`|  

####  <a name="StringFunctions"></a> 文字列関数  

-   連結演算子および [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] の定数を使用して、複数のフィールドを組み合わせます。 次の式では、2 つのフィールドが、同じテキスト ボックス内の別々の行に返されます。  

```  
=Fields!FirstName.Value & vbCrLf & Fields!LastName.Value   
```  

-   `Format` 関数を使用して、文字列内の日付と数値の書式を設定します。 次の式では、 *StartDate* パラメーターおよび *EndDate* パラメーターの値が長い日付形式で表示されます。  

```  
=Format(Parameters!StartDate.Value, "D") & " through " &  Format(Parameters!EndDate.Value, "D")    
```  

テキストボックスに日付または数字のみが含まれている場合は、テキストボックス内の`Format`関数の代わりに書式を適用するために、テキストボックスの [書式] プロパティを使用する必要があります。  

-   `Right`、`Len`、 `InStr` の各関数は、サブストリングを返す場合に役立ちます。たとえば、 *DOMAIN*\\*username* の文字列からユーザー名だけを返します。 次の式では、\\User *というパラメーターで取得できる文字列のうち、円記号 (* ) より右側の部分のみが返されます。  

```  
=Right(Parameters!User.Value, Len(Parameters!User.Value) - InStr(Parameters!User.Value, "\"))  
```  

次の式では、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] <xref:System.String> System.String [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] クラスのメンバーを使用しています。返される値は、上記の式と同じです。  

```  
=Parameters!User.Value.Substring(Parameters!User.Value.IndexOf("\")+1, Parameters!User.Value.Length-Parameters!User.Value.IndexOf("\")-1)  
```  

-   複数の値を持つパラメーターから選択した値を表示します。 次の例では`Join` 、関数を使用して、 *myselection*パラメーターの選択した値を1つの文字列に連結します。この文字列は、レポートアイテムのテキストボックスの値を表す式として設定できます。  

```  
= Join(Parameters!MySelection.Value)  
```  

次の例では、前の例と同じ処理を行うだけでなく、選択した値のリストの前にテキスト文字列を表示します。  

```  
="Report for " & JOIN(Parameters!MySelection.Value, " & ")  

```  

-   の`Regex` 関数は、<xref:System.Text.RegularExpressions>電話番号の書式設定など、既存の文字列の書式を変更する場合に便利です。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 次の式では`Replace` 、関数を使用して、フィールド内の10桁の電話番号の形式を "*nnn*-*nnn*-*nnnn*" から "(*nnn*) *nnn* -に変更します。*nnnn*":  

```  
=System.Text.RegularExpressions.Regex.Replace(Fields!Phone.Value, "(\d{3})[ -.]*(\d{3})[ -.]*(\d{4})", "($1) $2-$3")  
```  

> [!NOTE]  
>  Fields!Phone.Value に余分なスペースがないことと、データ型が <xref:System.String>」を参照してください。  

#### <a name="lookup"></a>Lookup  

-   キー フィールドを指定することで、`Lookup` 関数を使用し、1 対 1 のリレーションシップ (キーと値のペアなど) の値をデータセットから取得することができます。 次の式では、入力された製品識別子に一致する製品名をデータセット ("Product") から取得し、表示します。  

```  
=Lookup(Fields!PID.Value, Fields!ProductID.Value, Fields!ProductName.Value, "Product")  
```  

#### <a name="lookupset"></a>LookupSet  

-   キー フィールドを指定することで、`LookupSet` 関数を使用し、1 対多のリレーションシップの値のセットをデータセットから取得することができます。 たとえば、1 人の個人が複数の電話番号を持っていることがあります。 次の例では、PhoneList データセットに個人識別子が含まれ、各行に電話番号が格納されているものとしています。 `LookupSet` は、値の配列を返します。 次の例では、返された値を 1 つの文字列として結合し、ContactID で指定される個人の電話番号の一覧を表示します。  

```  
=Join(LookupSet(Fields!ContactID.Value, Fields!PersonID.Value, Fields!PhoneNumber.Value, "PhoneList"),",")  
```  

####  <a name="ConversionFunctions"></a> 変換関数  
[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] の関数を使用して、フィールドのデータ型を別のデータ型に変換することができます。 変換関数を使用すると、フィールドの既定のデータ型を、計算やテキストの連結に必要なデータ型に変換できます。  

-   次の式では、フィルター式の [値] フィールドの [!INCLUDE[tsql](../../includes/tsql-md.md)] money データ型と比較するために、定数 500 を Decimal 型に変換します。  

```  
=CDec(500)  
```  

-   次の式では、複数の値を持つパラメーター *MySelection*で選択された値の数が表示されます。  

```  
=CStr(Parameters!MySelection.Count)  
```  

####  <a name="DecisionFunctions"></a> 決定関数  

-   `Iif` 関数では、式が True かどうかによって、2 つの値のいずれかが返されます。 次の式では、`Iif` 関数を使用して、`LineTotal` の値が 100 を超える場合にブール値 `True` が返されます。 それ以外の場合は、`False` が返されます。  

```  
=IIF(Fields!LineTotal.Value > 100, True, False)  
```  

-   複数の `IIF` 関数 ("入れ子になった IIF" とも呼ばれます) を使用すると、`PctComplete` の値に応じて 3 つの値のいずれかを返すことができます。 次の式をテキスト ボックスの塗りつぶしの色に使用すると、テキスト ボックスの値に応じて背景色を変更できます。  

```  
=IIF(Fields!PctComplete.Value >= 10, "Green", IIF(Fields!PctComplete.Value >= 1, "Blue", "Red"))  
```  

背景は、値が 10 以上の場合は緑色、1 ～ 9 の場合は青色、1 未満の場合は赤色になります。  

-   同じ機能を実現するには、`Switch` 関数を使用するという方法もあります。 `Switch` 関数は、検証する条件が 3 つ以上ある場合に役立ちます。 `Switch` 関数は、True に評価される一連の式のうちの最初の式に関連付けられた値を返します。  

```  
=Switch(Fields!PctComplete.Value >= 10, "Green", Fields!PctComplete.Value >= 1, "Blue", Fields!PctComplete.Value = 1, "Yellow", Fields!PctComplete.Value <= 0, "Red",)  
```  

背景は、値が 10 以上の場合は緑色、1 ～ 9 の場合は青色、1 の場合は黄色、0 以下の場合は赤色になります。  

-   `ImportantDate` フィールドの値を検証し、経過日数が 1 週間を超えている場合は "Red"、それ以外の場合は "Blue" を返します。 この式を使用して、レポート アイテムに含まれるテキスト ボックスの Color プロパティを制御できます。  

```  
=IIF(DateDiff("d",Fields!ImportantDate.Value, Now())>7,"Red","Blue")  
```  

-   `PhoneNumber` フィールドの値を検証し、値が `null` ([!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] では `Nothing`) の場合は "No Value" を返し、それ以外の場合は電話番号の値を返します。 この式を使用して、レポート アイテムに含まれるテキスト ボックスの値を制御できます。  

```  
=IIF(Fields!PhoneNumber.Value Is Nothing,"No Value",Fields!PhoneNumber.Value)  
```  

-   `Department` フィールドの値を検証し、サブレポート名または `null` ([!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] では `Nothing`) を返します。 この式は、条件付きドリルスルー サブレポートで使用できます。  

```  
=IIF(Fields!Department.Value = "Development", "EmployeeReport", Nothing)  
```  

-   フィールド値が NULL かどうかを検証します。 この式を使用すると、画像レポート アイテムの `Hidden` プロパティを制御できます。 次の例では、LargePhoto というフィールドの値が NULL でない場合にのみ、このフィールドで指定された画像が表示されます。  

```  
=IIF(IsNothing(Fields!LargePhoto.Value),True,False)  
```  

-   `MonthName` 関数は、指定した月に対応する月名を含む文字列値を返します。 次の例では、フィールドに 0 という値が格納されている場合に、Month フィールドで NA と表示されます。  

```  
IIF(Fields!Month.Value=0,"NA",MonthName(IIF(Fields!Month.Value=0,1,Fields!Month.Value)))  

```  

###  <a name="ReportFunctions"></a> レポートの関数  
レポートには、これ以外にも、レポート内のデータを操作するレポート関数への参照を追加することができます。 ここでは、このような関数のうち 2 つの例を紹介します。 レポートの関数と例の詳細については、「[集計関数リファレンス &#40;レポート ビルダーおよび SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)」を参照してください。  

#####  <a name="Sum"></a> Sum  

-   `Sum` 関数を使用すると、グループまたはデータ領域内の値を合計できます。 この関数は、グループのヘッダーまたはフッターで役立ちます。 次の式では、Order グループまたは Order データ領域内のデータの合計が表示されます。  

```  
=Sum(Fields!LineTotal.Value, "Order")  
```  

-   `Sum` 関数は、条件付き集計計算にも使用できます。 たとえば、データセットに State という名前のフィールドが存在し、Not Started、Started、Finished という値を設定できる場合、次の式をグループ ヘッダーで使用すると、値 Finished の合計のみが計算されます。  

```  
=Sum(IIF(Fields!State.Value = "Finished", 1, 0))  
```  

#####  <a name="RowNumber"></a> RowNumber  

-   `RowNumber` 関数をデータ領域内のテキスト ボックスで使用すると、式が表示されるテキスト ボックスの各インスタンスの行数が表示されます。 この関数は、テーブル内の行数を数える場合に役立ちます。 また、行数に基づいた改ページの指定など、より複雑なタスクにも役立ちます。 詳細については、このトピックの「 [改ページ](#PageBreaks) 」を参照してください。  

`RowNumber` に指定したスコープによって、どの時点で番号の再設定を開始するかが制御されます。 この関数に `Nothing` キーワードを指定することで、最も外側のデータ領域内の最初の行からカウントが開始されます。 入れ子になったデータ領域内でカウントを開始するには、データ領域の名前を使用します。 グループ内でカウントを開始するには、グループの名前を使用します。  

```  
=RowNumber(Nothing)  
```  

##  <a name="AppearanceofReportData"></a> レポート データの表示方法  
式を使用して、レポートにデータを表示する方法を操作できます。 たとえば、2 つのフィールドの値を 1 つのテキスト ボックスに表示したり、レポートに関する情報を表示したり、レポートに改ページを挿入する方法に影響を与えたりすることができます。  

###  <a name="PageHeadersandFooters"></a> ページ ヘッダーとページ フッター  
レポートをデザインする場合、必要に応じてレポート名とページ番号をレポート フッターに表示できます。 この操作を行うには、以下の式を使用できます。  

-   次の式では、レポート名、およびレポートが実行された時刻が返されます。 この式は、レポート フッターまたはレポート本文のテキスト ボックスで使用できます。 時間の書式は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の短い日付用の書式設定の文字列を使用して設定されます。  

```  
=Globals.ReportName & ", dated " & Format(Globals.ExecutionTime, "d")  
```  

-   次の式では、レポートのページ番号および全ページ数が返されます。この式は、レポートのフッター内のテキスト ボックスで使用できます。  

```  
=Globals.PageNumber & " of " & Globals.TotalPages  
```  

以下の例では、ディレクトリの一覧の内容と同様に、ページ ヘッダーにページの最初と最後の値を表示する方法について説明します。 この例では、 `LastName`という名前のテキスト ボックスを含むデータ領域を想定しています。  

-   次の式は、ページ ヘッダーの左側にあるテキスト ボックスで使用されます。この式では、そのページの `LastName` テキスト ボックスの最初の値が返されます。  

```  
=First(ReportItems("LastName").Value)  
```  

-   次の式は、ページ ヘッダーの右側にあるテキスト ボックスで使用されます。この式では、そのページの `LastName` テキスト ボックスの最後の値が返されます。  

```  
=Last(ReportItems("LastName").Value)  
```  

次の例では、合計ページ数の表示方法について説明します。 この例では、 `Cost`という名前のテキスト ボックスを含むデータ領域を想定しています。  

-   次の式は、ページ ヘッダーまたはページ フッターで使用されます。この式では、 `Cost` テキスト ボックスの値の合計がそのページに返されます。  

```  
=Sum(ReportItems("Cost").Value)  
```  

> [!NOTE]  
>  ページ ヘッダーまたはページ フッターでは、1 つの式につき 1 つのレポート アイテムしか参照できません。 また、ページ ヘッダーまたはページ フッターの式では、テキスト ボックスの名前を参照することはできますが、テキスト ボックス内の実際のデータ式は参照できません。  

###  <a name="PageBreaks"></a> 改ページ  
レポートによっては、グループやレポート アイテムに改ページを設定せずに、またはグループやレポート アイテムの改ページに追加する形で、指定した行数の最後に改ページを挿入したい場合があります。 この操作を行うには、必要なグループや詳細レコードを含むグループを作成し、そのグループに改ページを追加した後、指定された行数でグループ化を行うグループ式を追加します。  

-   次の式をグループ式で使用すると、25 行ごとに数値が割り当てられます。 グループに改ページが定義されている場合は、この式の結果として、25 行ごとに改ページが行われます。  

```  
=Ceiling(RowNumber(Nothing)/25)  
```  

ユーザーが 1 ページあたりの行数の値を設定できるようにするには、 `RowsPerPage` という名前のパラメーターを作成し、次の式で示すように、そのパラメーターに基づいてグループ式を作成します。  

```  
=Ceiling(RowNumber(Nothing)/Parameters!RowsPerPage.Value)  
```  

グループに改ページを設定する方法の詳細については、「[改ページの追加 &#40;レポート ビルダーおよび SSRS&#41;](add-a-page-break-report-builder-and-ssrs.md)」を参照してください。  

##  <a name="Properties"></a> プロパティ  
式は、テキスト ボックスにデータを表示するためだけに使用するものではありません。 レポート アイテムにプロパティを適用する方法を変更する場合にも使用できます。 レポート アイテムのスタイル情報を変更したり、情報の表示を変更することができます。  

###  <a name="Formatting"></a> 書式設定  

-   テキスト ボックスの Color プロパティで次の式を使用すると、 `Profit` フィールドの値に応じてテキストの色が変更されます。  

```  
=Iif(Fields!Profit.Value < 0, "Red", "Black")  
```  

また、 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] のオブジェクト変数 `Me`を使用することもできます。 この変数は、テキスト ボックスの値を参照するもう 1 つの手段です。  

`=Iif(Me.Value < 0, "Red", "Black")`  

-   データ領域にあるレポート アイテムの BackgroundColor プロパティで次の式を使用すると、各行の背景色に薄緑色と白が交互に設定されます。  

```  
=Iif(RowNumber(Nothing) Mod 2, "PaleGreen", "White")  
```  

特定のスコープに対して式を使用する場合は、次のように、集計関数に対してデータセットを指定する必要があります。  

```  
=Iif(RowNumber("Employees") Mod 2, "PaleGreen", "White")  
```  

> [!NOTE]  
>  使用できる色は、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の KnownColor 列挙体の色です。  

### <a name="chart-colors"></a>グラフの色  
図形グラフの色を指定するには、色がデータ点にマップされる順序を制御するカスタム コードを使用できます。 これは複数のグラフで同じカテゴリ グループの色を統一するときに役立ちます。 詳細については、「[複数の図形グラフでの色の統一 &#40;レポート ビルダーおよび SSRS&#41;](charts-report-builder-and-ssrs.md)」を参照してください。  

###  <a name="Visibility"></a> 表示  
レポート アイテムの表示プロパティを使用して、レポート内のアイテムの表示/非表示を切り替えることができます。 テーブルなどのデータ領域では、最初に、式の値に基づいて詳細行を非表示にできます。  

-   グループ内の詳細行の初期表示に次の式を使用すると、 `PctQuota` フィールドで 90% を超えるすべての売上の詳細行が表示されます。  

```  
=Iif(Fields!PctQuota.Value>.9, False, True)  
```  

-   テーブルの Hidden プロパティに次の式を設定すると、テーブルの行数が 12 行を超えた場合にのみテーブルが表示されます。  

```  
=IIF(CountRows()>12,false,true)  
```  

-   次の式は、列の`Hidden`プロパティで設定した場合、データソースからデータが取得された後にレポートデータセットにフィールドが存在する場合にのみ、列を表示します。  

```  
=IIF(Fields!Column_1.IsMissing, true, false)  
```  

###  <a name="Hyperlinks"></a> URL  
レポート データを使用して URL をカスタマイズできます。また、テキスト ボックスに対するアクションとして URL を追加するかどうかを、条件付きで制御することもできます。  

-   次の式をテキスト ボックスに対するアクションとして使用すると、URL パラメーターとしてデータセット フィールド `EmployeeID` を指定する、カスタマイズされた URL が生成されます。  

```  
="http://adventure-works/MyInfo?ID=" & Fields!EmployeeID.Value  
```  

詳細については、「[URL へのハイパーリンクの追加 &#40;レポート ビルダーおよび SSRS&#41;](add-a-hyperlink-to-a-url-report-builder-and-ssrs.md)」を参照してください。  

-   次の式では、テキスト ボックス内に URL を追加するかどうかを、条件付きで制御します。 この式では、アクティブ URL をレポートに含めるかどうかをユーザーが決定できるように、 `IncludeURLs` という名前のパラメーターを使用しています。 この式は、テキスト ボックスに対するアクションとして設定されます。 パラメーターを False に設定してからレポートを表示すると、ハイパーリンクなしでレポートを Microsoft Excel にエクスポートできます。  

```  
=IIF(Parameters!IncludeURLs.Value,"http://adventure-works.com/productcatalog",Nothing)  
```  

##  <a name="ReportData"></a> レポート データ  
式を使用して、レポートで使用するデータを操作できます。 パラメーターおよび他のレポート情報を参照できます。 レポートのデータを取得するために使用されるクエリを変更することもできます。  

###  <a name="Parameters"></a> パラメーター  
パラメーターの式を使用して、パラメーターの既定値を変更できます。 たとえば、パラメーターを使用して、レポートの実行に使用されるユーザー ID に基づき、特定のユーザーに合わせてデータをフィルター処理することができます。  

-   パラメーターの既定値として次の式を使用すると、レポートを実行するユーザーのユーザー ID が収集されます。  

```  
=User!UserID  
```  

-   レポートのクエリ パラメーター、フィルター式、テキスト ボックスなどの領域でパラメーターを参照するには、`Parameters` グローバル コレクションを使用します。 この例では、パラメーターの名前が *Department*であることを想定しています。  

```  
=Parameters!Department.Value  
```  

-   パラメーターはレポート内に作成できますが、非表示に設定されます。 レポート サーバーでレポートが実行される際、パラメーターがツール バーに表示されないため、レポートを表示するユーザーは既定値を変更できません。 既定値に設定された非表示パラメーターは、カスタム定数として使用できます。 この値は、フィールド式など、あらゆる式で使用できます。 次の式では、 *ParameterField*という名前を持つパラメーターの既定値で指定されたフィールドを特定しています。  

```  
=Fields(Parameters!ParameterField.Value).Value  
```  

## <a name="CustomCode"></a> カスタム コード

レポート内では、カスタム コードを使用できます。 カスタム コードは、レポート内に埋め込むか、レポートで使用されるカスタム アセンブリに格納します。 カスタム コードの詳細については、「[レポート デザイナーでカスタム コードやアセンブリを式から参照する &#40;SSRS&#41;](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)」を参照してください。  

### <a name="using-group-variables-for-custom-aggregation"></a>グループ変数を使用したカスタム集計

特定のグループ スコープ内のローカルなグループ変数の値を初期化し、その変数を式の中で参照することができます。 カスタム コードでグループ変数を使用するシナリオとしては、カスタム集計の実装が挙げられます。 詳細については、「 [グループ変数を使ったカスタム集計 (Reporting Services 2008)](https://go.microsoft.com/fwlink/?LinkId=128714)」を参照してください。  

変数の詳細については、「 [レポート変数コレクションとグループ変数コレクションの参照 &#40;レポート ビルダーおよび SSRS&#41;](built-in-collections-report-and-group-variables-references-report-builder.md)」を参照してください。  

## <a name="suppressing-null-or-zero-values-at-run-time"></a>実行時の NULL 値または 0 の非表示

式内の一部の値は、レポート処理時に NULL または未定義と評価されることがあります。 その結果、実行時エラーが発生して、評価した式ではなく **#Error** がテキスト ボックスに表示される場合があります。 `IIF` 関数は特にこの動作の影響を受けます。これは、If-Then-Else ステートメントとは異なり、`IIF` ステートメントの各部分 (関数呼び出しを含む) が、`true` であるか `false` であるかを検証するルーチンに渡される前に評価されるためです。 `=IIF(Fields!Sales.Value is NOTHING, 0, Fields!Sales.Value)` ステートメントを実行すると、 **が NOTHING の場合は、表示されたレポートに** #Error `Fields!Sales.Value` と表示されます。  

この状況を回避するには、次のいずれかの方法を使用します。  

-   フィールド B の値が 0 または未定義の場合は、分子に 0、分母に 1 を設定します。それ以外の場合は、分子にフィールド A の値、分母にフィールド B の値を設定します。  

```  
=IIF(Field!B.Value=0, 0, Field!A.Value / IIF(Field!B.Value =0, 1, Field!B.Value))  
```  

-   カスタム コード関数を使用して、式の値を返します。 次の例では、現在の値と前の値の差がパーセンテージで返されます。 これを使用すると、任意の連続する 2 つの値の差を計算できます。また、最初の比較のエッジ ケース (前の値が存在しない場合) と、前の値または現在の値が `null` ([!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] では `Nothing`) であるケースを処理できます。  

```  
Public Function GetDeltaPercentage(ByVal PreviousValue, ByVal CurrentValue) As Object  
     If IsNothing(PreviousValue) OR IsNothing(CurrentValue) Then  
          Return Nothing  
     Else if PreviousValue = 0 OR CurrentValue = 0 Then  
          Return Nothing  
     Else
          Return (CurrentValue - PreviousValue) / CurrentValue  
     End If  
End Function  
```  

次の式に、"ColumnGroupByYear" コンテナーのテキスト ボックスからこのカスタム コードを呼び出す方法を示します (グループまたはデータ領域)。  

```  
=Code.GetDeltaPercentage(Previous(Sum(Fields!Sales.Value),"ColumnGroupByYear"), Sum(Fields!Sales.Value))  
```  

実行時例外の発生はこのようにして防ぐことができます。 テキスト ボックスの `Color` プロパティで `=IIF(Me.Value < 0, "red", "black")` のような式を使用し、その値が 0 より大きいか小さいかの条件に基づいて、テキストを表示できるようになりました。  

## <a name="see-also"></a>関連項目

- [フィルター式の例 &#40;レポート ビルダーおよび SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)
- [グループ式の例 &#40;レポート ビルダーおよび SSRS&#41;](expression-examples-report-builder-and-ssrs.md)
- [レポートでの式の使用 (レポート ビルダーおよび SSRS)](expression-uses-in-reports-report-builder-and-ssrs.md)
- [式 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)
- [一般的に使用されるフィルター &#40;レポート ビルダーおよび SSRS&#41;](commonly-used-filters-report-builder-and-ssrs.md)