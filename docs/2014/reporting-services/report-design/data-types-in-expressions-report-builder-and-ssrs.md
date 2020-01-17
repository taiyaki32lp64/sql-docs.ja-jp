---
title: 式で使用されるデータ型 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 94fdf921-270c-4c12-87b3-46b1cc98fae5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 86aa646865ecfe3da6ed1ad4bacb75907ab39472
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891865"
---
# <a name="data-types-in-expressions-report-builder-and-ssrs"></a>式で使用されるデータ型 (レポート ビルダーおよび SSRS)
  データを効率よく格納し、処理できるように、さまざまなデータの種類を表すデータ型が用意されています。 代表的なデータ型としては、テキスト (文字列) 型、数値型 (小数点以下桁数を含む)、数値型 (小数点以下桁数を含まない)、日付/時刻型、イメージ型などがあります。 レポート内の値は、レポート定義言語 (RDL) データ型である必要があります。 値は、レポートに表示する場合に目的に応じて書式設定できます。 たとえば、通貨を表すフィールドの場合、データを浮動小数点数としてレポート定義に格納しておき、実際には、指定した書式設定プロパティに従ってさまざまな形式で表示することができます。  
  
 表示形式の詳細については、「 [レポート アイテムの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-report-items-report-builder-and-ssrs.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-definition-language-rdl-data-types-and-common-language-runtime-clr-data-types"></a>レポート定義言語 (RDL) データ型と共通言語ランタイム (CLR) データ型  
 RDL ファイルで指定した値は、RDL データ型である必要があります。 レポートをコンパイルして処理すると、RDL データ型は CLR データ型に変換されます。 次の表は、既定として指定された変換を示しています。  
  
|RDL 型|CLR 型|  
|--------------|---------------|  
|String|既定値:String<br /><br /> Chart、GUID、Timespan|  
|ブール値|既定値:ブール値|  
|整数型|既定値:Int64<br /><br /> Int16、Int32、Uint16、Uint64、Byte、Sbyte|  
|DateTime|既定値:DateTime<br /><br /> DateTimeOffset|  
|Float|既定値:Double<br /><br /> Single、Decimal|  
|Binary|既定値:Byte[]|  
|Variant|Byte[] 以外の上記すべて|  
|VariantArray|Variant の配列|  
|Serializable|Serializable に指定されている、または ISerializable を実装する Variant または型|  
  
## <a name="understanding-data-types-and-writing-expressions"></a>データ型と式の作成について  
 グループ式、フィルター式、集計計算など、値を比較したり結合したりする式を作成する際は、データ型について十分に理解しておく必要があります。 比較と計算は、同じデータ型のアイテム間でしか行えません。 データ型が異なる場合は、式を使用して、レポート アイテムのデータ型を明示的に変換する必要があります。  
  
 データ型の変換が必要になるケースとしては、次のような場合が考えられます。  
  
-   レポート パラメーターの値を別のデータ型のデータセット フィールドと比較する。  
  
-   データ型が異なる複数の値を比較するフィルター式を作成する。  
  
-   データ型が異なる複数のフィールドを結合する並べ替え式を作成する。  
  
-   データ型が異なる複数のフィールドを結合するグループ式を作成する。  
  
-   データ ソースから取得した値を別のデータ型に変換する。  
  
## <a name="determining-the-data-type-of-report-data"></a>レポート データのデータ型を調べる  
 レポート アイテムのデータ型を調べるには、そのアイテムのデータ型を返す式を作成します。 たとえば、 `MyField`というフィールドのデータ型を確認するには、テーブルのセルに `=Fields!MyField.Value.GetType().ToString()`という式を追加します。 式の結果には、`MyField` に使用されている CLR データ型 (`System.String` や `System.DateTime` など) が表示されます。  
  
## <a name="converting-dataset-fields-to-a-different-data-type"></a>データセット フィールドを異なるデータ型に変換する  
 レポートで使用するデータセット フィールドを事前に変換することもできます。 既存のデータセット フィールドを変換するには、次のような方法があります。  
  
-   データセット クエリを修正して、変換済みのデータを使った新しいクエリ フィールドを追加する。 リレーショナル データ ソースや多次元データ ソースの場合は、データ ソース リソースを使用して変換を行います。  
  
-   既存のレポート データセット フィールドに基づく計算フィールドを作成する。それには、結果セット列のすべてのデータを異なるデータ型の新しい列に変換する式を作成します。 たとえば、Year フィールドを整数値から文字列値に変換するには、 `=CStr(Fields!Year.Value)`という式を作成します。 詳細については、「[レポート データ ペインでのフィールドの追加、編集、更新 &#40;レポート ビルダーおよび SSRS&#41;](../report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)」を参照してください。  
  
-   使用しているデータ処理拡張機能に、書式設定済みのデータを取得するためのメタデータが含まれているかどうかを確認する。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] MDX クエリには、キューブの処理時に書式設定されたキューブ値を保持する FORMATTED_VALUE という拡張プロパティがあります。 詳細については、「[Analysis Services データベースに対する拡張フィールド プロパティ &#40;SSRS&#41;](../report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md)」を参照してください。  
  
## <a name="understanding-parameter-data-types"></a>パラメーターのデータ型について  
 レポート パラメーターは 5 つのデータ型のいずれかである必要があります。つまり、Boolean、DateTime、Integer、Float、または Text (String とも呼ばれます) です。 データセット クエリにクエリ パラメーターが含まれている場合は、レポート パラメーターが自動的に作成されて、対応するクエリ パラメーターに関連付けられます。 レポート パラメーターの既定のデータ型は String です。 レポート パラメーターの既定のデータ型を変更するには、 **[レポート パラメーターのプロパティ]** ダイアログ ボックスの **[全般]** ページで、 **[データ型]** ボックスの一覧から該当する値を選択します。  
  
> [!NOTE]  
>  DateTime データ型のレポート パラメーターは、ミリ秒をサポートしていません。 ミリ秒を含む値に基づいてパラメーターを作成することはできますが、ミリ秒が指定された Date 値または Time 値を値ドロップダウン リストから選択することはできません。  
  
## <a name="writing-expressions-that-convert-data-types-or-extract-parts-of-data"></a>データ型を変換する式やデータの一部を抽出する式を作成する  
 テキストとデータセット フィールドを連結演算子 (&) で結合する場合、通常は共通言語ランタイム (CLR) の既定の書式を使用できます。 データセット フィールドまたはパラメーターを特定のデータ型へと明示的に変換する場合は、CLR のメソッドを使用するか、Visual Basic のランタイム ライブラリ関数を使ってデータを変換する必要があります。  
  
 データ型の変換例を次の表に示します。  
  
|変換の種類|例|  
|------------------------|-------------|  
|DateTime から String|`=CStr(Fields!Date.Value)`|  
|String から DateTime|`=DateTime.Parse(Fields!DateTimeinStringFormat.Value)`|  
|String から DateTimeOffset|`=DateTimeOffset.Parse(Fields!DateTimeOffsetinStringFormat.Value)`|  
|年を抽出|`=Year(Fields!TimeinStringFormat.Value)`<br /><br /> `-- or --`<br /><br /> `=Year(Fields!TimeinDateTimeFormat.Value)`|  
|Boolean から Integer|`=CInt(Parameters!BooleanField.Value)`<br /><br /> True は -1、False は 0 になります。|  
|Boolean から Integer|`=System.Convert.ToInt32(Fields!BooleanFormat.Value)`<br /><br /> True は 1、False は 0 になります。|  
|DateTimeOffset 値から DateTime 部分のみを抽出|`=Fields!MyDatetimeOffset.Value.DateTime`|  
|DateTimeOffset 値から Offset 部分のみを抽出|`=Fields!MyDatetimeOffset.Value.Offset`|  
  
 Format 関数を使用して、値の表示形式を制御することもできます。 詳細については、「 [関数 (Visual Basic)](https://go.microsoft.com/fwlink/?linkid=111483)」を参照してください。  
  
## <a name="advanced-examples"></a>高度な例  
 データ ソースへの接続に使用するデータ プロバイダーが、すべてのデータ型の変換をサポートしているとは限りません。このような場合、サポートされていないデータ ソースの種類に対する既定のデータ型は String になります。 次の例では、データ型が文字列として返される場合の対処方法について説明します。  
  
### <a name="concatenating-a-string-and-a-clr-datetimeoffset-data-type"></a>String 型と CLR DateTimeOffset 型の連結  
 CLR には、ほとんどのデータ型について既定の変換方法が用意されているため、& 演算子を使用することで、データ型が異なる値を 1 つの文字列に連結できます。 たとえば、"The date and time are: " というテキストと、StartDate という <xref:System.DateTime> 型のデータセット フィールドを連結するには、 `="The date and time are: " & Fields!StartDate.Value`」を参照してください。  
  
 データ型によっては、ToString 関数が必要になる場合があります。 たとえば、先ほどと同じ例を、CLR データ型の <xref:System.DateTimeOffset>(日付、時刻、および、UTC タイム ゾーンを基準とするタイム ゾーン オフセットで構成される) を使って記述する場合は、 `="The time is: " & Fields!StartDate.Value.ToString()`」を参照してください。  
  
### <a name="converting-a-string-data-type-to-a-clr-datetime-data-type"></a>String 型から CLR の DateTime 型への変換  
 データ ソースで定義されているすべてのデータ型をデータ処理拡張機能がサポートしていない場合、サポート対象外のデータはテキストとして処理される可能性があります。 たとえば、`datetimeoffset(7)` データ型の値は String データ型として処理されます。 "July 1, 2008, at 6:05:07.9999999 A.M." に対応する文字列値は、オーストラリアのパースでは 次のようになります。  
  
 `2008-07-01 06:05:07.9999999 +08:00`  
  
 この例では、日付 (July 1, 2008) に続けて、小数点以下 7 桁の時刻値 (6:05:07.9999999 A.M.) と UTC タイム ゾーン オフセット (+8 時間、0 分) が続きます。 以下の例では、この値が `MyDateTime.Value` という `String` 型のフィールドに格納されています。  
  
 次のいずれかの方法を使用することで、このデータを 1 つまたは複数の CLR 値に変換できます。  
  
-   テキスト ボックスに、文字列の一部分を抽出する式を入力します。 以下に例を示します。  
  
    -   UTC タイム ゾーン オフセットの時間部分だけを抽出し、分に変換するには、次の式を使用します。 `=CInt(Fields!MyDateTime.Value.Substring(Fields!MyDateTime.Value.Length-5,2)) * 60`  
  
         結果は `480`です。  
  
    -   文字列を日時の値に変換するには、次の式を使用します。 `=DateTime.Parse(Fields!MyDateTime.Value)`  
  
         `MyDateTime.Value` の文字列に UTC オフセットが含まれている場合、まず、 `DateTime.Parse` 関数によって UTC オフセットの調整が行われます (ここでは、午前 7 時から [`+08:00`] を差し引いて、前日の午後 11 時という UTC 時刻が 求められます)。 次に、 `DateTime.Parse` 関数は、レポート サーバーのローカル UTC オフセットを適用し、必要に応じて夏時間のために再度時刻調整を行います。 たとえば、ワシントン州レドモンドの場合、夏時間調整後のローカル時刻オフセットは `[-07:00]`(午後 11 時の 7 時間前) になります。 結果は次`DateTime`の値になります。`2007-07-06 04:07:07 PM` (2007 年 7 月 6 日午後 4 時 07 分)。  
  
 文字列をデータ型に変換する`DateTime`方法の詳細については、「[日付と時刻文字列の解析](https://go.microsoft.com/fwlink/?LinkId=89703)」、「[特定のカルチャの日付と時刻の書式設定](https://go.microsoft.com/fwlink/?LinkId=89704)」、および「 [DateTime、DateTimeOffset、および TimeZoneInfo on の選択](https://go.microsoft.com/fwlink/?linkid=110652)」を参照してください。旧.  
  
-   レポート データセットに、文字列の一部分を抽出する式を使った新しい計算フィールドを追加します。 詳細については、「[レポート データ ペインでのフィールドの追加、編集、更新 &#40;レポート ビルダーおよび SSRS&#41;](../report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)」を参照してください。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数を使って日付と時刻の値を別々に抽出し、別個の列を作成するように、レポートのデータセット クエリを修正します。 次の例では、`DatePart` 関数を使用して、年の列と UTC タイム ゾーン (分単位) の列を追加しています。  
  
     `SELECT`  
  
     `MyDateTime,`  
  
     `DATEPART(year, MyDateTime) AS Year,`  
  
     `DATEPART(tz, MyDateTime) AS OffsetinMinutes`  
  
     `FROM MyDates`  
  
     結果セットには、3 つの列が格納されます。 1 列目には日付と時刻が、2 列目には年が、3 列目には分単位の UTC オフセットが格納されます。 次の行はサンプル データを示しています。  
  
     `2008-07-01 06:05:07             2008                   480`  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの型の詳細については、[SQL Server オンライン ブック](https://go.microsoft.com/fwlink/?linkid=120955) の「[データ型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)」および「[日付と時刻のデータ型および関数 &#40;Transact-SQL&#41;](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] のデータ型の詳細については、 [SQL Server オンライン ブック](https://docs.microsoft.com/analysis-services/multidimensional-models/olap-physical/data-types-in-analysis-services) の「 [SQL Server Books Onlの「e](https://go.microsoft.com/fwlink/?linkid=120955)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [レポート アイテムの書式設定 &#40;レポート ビルダーおよび SSRS&#41;](formatting-report-items-report-builder-and-ssrs.md)  
  
  
