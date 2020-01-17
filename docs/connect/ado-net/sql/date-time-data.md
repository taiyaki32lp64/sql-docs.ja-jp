---
title: 日付型と時刻型のデータ
description: SQL Server 2008 で導入された新しい日付と時刻のデータ型の使用方法について説明します。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 38626c6c726b9f45bd2d37d5deda480880556856
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452252"
---
# <a name="date-and-time-data"></a>日付型と時刻型のデータ

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 2008 では、日付と時刻の情報を処理するための新しいデータ型が導入されています。 新しいデータ型には、日付と時刻の個別の型と、範囲、有効桁数、およびタイムゾーンを認識する拡張データ型が含まれます。 SQL Server 用 Microsoft SqlClient Data Provider (<xref:Microsoft.Data.SqlClient>) は、SQL Server 2008 データベースエンジンのすべての新機能を完全にサポートしています。 SqlClient でこれらの新機能を使用するには、.NET Framework 3.5 SP1 (またはそれ以降) または .NET Core 1.0 (またはそれ以降) をインストールする必要があります。  
  
SQL Server 2008 より前のバージョンの SQL Server では、`datetime` と `smalldatetime` の日付と時刻の値を操作するためのデータ型は2つだけでした。 いずれのデータ型も日付値と時刻値の両方を保持するため、日付と時刻のどちらか一方の値のみを使用する場合にはかえって面倒になります。 また、これらのデータ型でサポートされるのは、英国のグレゴリオ暦が1753で導入された後に発生する日付のみです。 もう1つの制限事項は、これらの古いデータ型がタイムゾーンに対応していないことです。これにより、複数のタイムゾーンからのデータを操作するのが困難になります。  
  
SQL Server のデータ型の詳細なドキュメントについては SQL Server オンラインブックを参照してください。 日付と時刻のデータのエントリレベルのトピックについては[、「日付と時刻のデータの使用](https://go.microsoft.com/fwlink/?LinkID=98361)」を参照してください。
  
## <a name="datetime-data-types-introduced-in-sql-server-2008"></a>SQL Server 2008 で導入された日付/時刻データ型  
 次の表では、新しい日付と時刻のデータ型について説明します。  
  
|SQL Server データ型|[説明]|  
|--------------------------|-----------------|  
|`date`|`date` データ型は、01 年 1 月 1 日から 9999 年 12 月 31 日の範囲を 1 日の精度で表すことができます。 既定値は1900年1月1日です。 ストレージ サイズは 3 バイトです。|  
|`time`|`time` データ型は、24 時間形式で時刻値のみを格納します。 `time` データ型の範囲は 00:00: 00.0000000 ~ 23:59: 59.9999999 で、精度は100ナノ秒です。 既定値は 00:00: 00.0000000 (午前0時) です。 `time` データ型はユーザー定義による 1 秒未満の時間の有効桁数をサポートし、記憶領域のサイズは、指定された有効桁数に応じて 3 バイトから 6 バイトまでになります。|  
|`datetime2`|`datetime2` データ型は、`date` データ型と `time` データ型の範囲と有効桁数を1つのデータ型に結合します。<br /><br /> 既定値とリテラル文字列の形式は、`date` データ型および `time` データ型で定義されている形式と同じです。|  
|`datetimeoffset`|`datetimeoffset` データ型は、`datetime2` のすべての機能に加えて、タイム ゾーン オフセットを持ちます。 タイム ゾーン オフセットは、[+&#124;-] HH:MM として表されます。 HH は、タイム ゾーン オフセットの時間数を表す 00 から 14 までの 2 桁の数字です。 MM は、タイム ゾーン オフセットの付加的な分数を表す 00 から 59 までの 2 桁の数字です。 時刻形式の精度は 100 ナノ秒までサポートされています。 必須の + または-記号は、現地時刻を取得するために、タイムゾーンオフセットが UTC (協定世界時またはグリニッジ標準時) から加算されるか減算されるかを示します。|  
  
> [!NOTE]
>  `Type System Version` キーワードの詳細については、「<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>」を参照してください。  
  
## <a name="date-format-and-date-order"></a>日付の形式と日付の順序  
日付と時刻の値を解析 SQL Server 方法は、型システムのバージョンとサーバーのバージョンだけでなく、サーバーの既定の言語と形式の設定にも依存します。 ある言語の日付形式に対して機能する日付文字列は、別の言語および日付形式の設定を使用する接続によってクエリが実行される場合には認識されない可能性があります。  
  
Transact-sql SET LANGUAGE ステートメントでは、日付部分の順序を決定する DATEFORMAT が暗黙的に設定されます。 接続に対して SET DATEFORMAT Transact-sql ステートメントを使用すると、MDY、DMY、YMD、YDM、MYD、DYM の順序で日付部分を並べ替えることにより、日付の値を明確にすることができます。  
  
接続に対して DATEFORMAT を指定しなかった場合、SQL Server は接続に関連付けられている既定の言語を使用します。 たとえば、日付文字列 ' 01/02/03 ' は、言語設定が米国 English であるサーバーでは MDY (1 月2日、2003) として解釈され、言語設定がイギリス英語のサーバーでは DMY (2 月 2003 1 日) として解釈されます。 年は SQL Server の終了年のルールを使用して決定されます。このルールは、世紀の値を割り当てる期間の終了日を定義します。 詳細については、SQL Server オンライン ブックの「[two digit year cutoff オプション](https://go.microsoft.com/fwlink/?LinkId=120473)」を参照してください。  
  
> [!NOTE]
>  YDM 日付形式は、文字列形式から `date`、`time`、`datetime2`、または `datetimeoffset` への変換ではサポートされていません。  
  
SQL Server で日付と時刻のデータがどのように解釈されるかの詳細については、SQL Server 2008 オンライン ブックの「[日時データの使用](https://go.microsoft.com/fwlink/?LinkID=98361)」を参照してください。  
  
## <a name="datetime-data-types-and-parameters"></a>日付/時刻データ型とパラメーター  
新しい日付と時刻のデータ型をサポートするために、次の列挙が <xref:System.Data.SqlDbType> に追加されました。  
  
- `SqlDbType.Date`  
  
- `SqlDbType.Time`  
  
- `SqlDbType.DateTime2`  
  
- `SqlDbType.DateTimeOffSet`  

<xref:Microsoft.Data.SqlClient.SqlParameter> のデータ型は、前の <xref:System.Data.SqlDbType> 列挙型のいずれかの値を使って指定できます。 

> [!NOTE]
> `SqlParameter` の `DbType` プロパティを `SqlDbType.Date` に設定することはできません。

`SqlParameter` オブジェクトの <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> プロパティを特定の <xref:System.Data.DbType> に設定することで、汎用的に <xref:Microsoft.Data.SqlClient.SqlParameter> の型を指定することもできます。 `datetime2` 型と `datetimeoffset` 型をサポートするため、<xref:System.Data.DbType> には、次の列挙値が追加されています。  
  
- DateTime2  
  
- DbType. DateTimeOffset  
  
これらの新しい列挙型は、`Date`、`Time`、および `DateTime` 列挙を補完します。  
  
パラメーターオブジェクトの Microsoft SqlClient Data Provider 型は、パラメーターオブジェクトの値の .NET 型、または parameter オブジェクトの `DbType` から推論されます。 新しい日付と時刻のデータ型をサポートするために新しい <xref:System.Data.SqlTypes> データ型は導入されていません。 次の表では、SQL Server 2008 の日付と時刻のデータ型と CLR データ型の間のマッピングについて説明します。  
  
|SQL Server データ型|.NET の種類|SqlDbType|System.string. DbType|  
|--------------------------|-------------------------|---------------------------|------------------------|  
|date|System.DateTime|date|date|  
|time|System.TimeSpan|Time|Time|  
|datetime2|System.DateTime|datetime2|datetime2|  
|datetimeoffset|System.DateTimeOffset|DateTimeOffset|DateTimeOffset|  
|DATETIME|System.DateTime|DateTime|DateTime|  
|smalldatetime|System.DateTime|DateTime|DateTime|  
  
### <a name="sqlparameter-properties"></a>SqlParameter のプロパティ  
 次の表では、日付と時刻のデータ型に関連する `SqlParameter` のプロパティについて説明します。  
  
|プロパティ|[説明]|  
|--------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.IsNullable%2A>|値が null 値を許容するかどうかを取得または設定します。 サーバーに null パラメーター値を送信する場合は、`null` (Visual Basic で `Nothing`) ではなく、<xref:System.DBNull> を指定する必要があります。 データベースの null の詳細については、「 [null 値の処理](handle-null-values.md)」を参照してください。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Precision%2A>|値を表すために使用される最大桁数を取得または設定します。 日付と時刻のデータ型では、この設定は無視されます。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Scale%2A>|小数点以下の桁数を取得または設定します。これは `Time`、`DateTime2`、`DateTimeOffset` の時刻部分の値の処理で使用されます。 既定値は0です。これは、実際のスケールが値から推論され、サーバーに送信されることを意味します。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|日付と時刻のデータ型では無視されます。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|パラメーター値を取得または設定します。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|パラメーター値を取得または設定します。|  
  
> [!NOTE]
>  時刻値が0未満または24時間以上の場合、<xref:System.ArgumentException> がスローされます。  
  
### <a name="creating-parameters"></a>パラメーターの作成  
コンストラクターを使用するか、<xref:Microsoft.Data.SqlClient.SqlCommand> に追加することによって、<xref:Microsoft.Data.SqlClient.SqlParameter> オブジェクトを作成できます。<xref:Microsoft.Data.SqlClient.SqlCommand.Parameters%2A> <xref:Microsoft.Data.SqlClient.SqlParameterCollection> の `Add` メソッドを呼び出すことによって収集されます。 `Add` メソッドは、コンストラクター引数または既存のパラメーターオブジェクトのいずれかを入力として受け取ります。  
  
このトピックの次のセクションでは、日付と時刻のパラメーターを指定する方法の例について説明します。
  
### <a name="date-example"></a>日付の例  
次のコードフラグメントは、`date` パラメーターを指定する方法を示しています。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Date";  
parameter.SqlDbType = SqlDbType.Date;  
parameter.Value = "2007/12/1";  
```  
  
### <a name="time-example"></a>時間の例  
次のコードフラグメントは、`time` パラメーターを指定する方法を示しています。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@time";  
parameter.SqlDbType = SqlDbType.Time;  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
### <a name="datetime2-example"></a>Datetime2 の例  
次のコードフラグメントは、日付部分と時刻部分の両方を含む `datetime2` パラメーターを指定する方法を示しています。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Datetime2";  
parameter.SqlDbType = SqlDbType.DateTime2;  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
### <a name="datetimeoffset-example"></a>DateTimeOffSet の例  
次のコードフラグメントは、日付、時刻、およびタイムゾーンオフセットが0の `DateTimeOffSet` パラメーターを指定する方法を示しています。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@DateTimeOffSet";  
parameter.SqlDbType = SqlDbType.DateTimeOffSet;  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
### <a name="addwithvalue"></a>Addwithvalue メソッド  
次のコードフラグメントに示すように、<xref:Microsoft.Data.SqlClient.SqlCommand> の `AddWithValue` メソッドを使用してパラメーターを指定することもできます。 ただし、`AddWithValue` メソッドでは、パラメーターの <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> または <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> を指定することはできません。  
  
```csharp  
command.Parameters.AddWithValue(   
    "@date", DateTimeOffset.Parse("16660902"));  
```  
  
`@date` パラメーターは、サーバー上の `date`、`datetime`、または `datetime2` データ型にマッピングできます。 新しい `datetime` データ型を使用する場合は、パラメーターの <xref:System.Data.SqlDbType> プロパティをインスタンスのデータ型に明示的に設定する必要があります。 <xref:System.Data.SqlDbType.Variant> を使用するか、暗黙的にパラメーター値を指定すると、`datetime` データ型および `smalldatetime` データ型との下位互換性の問題が発生する可能性があります。  
  
次の表は、CLR 型から推論される `SqlDbTypes` を示しています。  
  
|CLR 型|推定される SqlDbType|  
|--------------|------------------------|  
|DateTime|SqlDbType|  
|TimeSpan|SqlDbType|  
|DateTimeOffset|SqlDbType|  
  
## <a name="retrieving-date-and-time-data"></a>日付と時刻のデータの取得  
SQL Server 2008 の date 値と time 値を取得するためのメソッドを次の表に示します。  
  
|SqlClient のメソッド|[説明]|  
|----------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTime%2A>|指定された列の値を <xref:System.DateTime> 構造体として取得します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|指定された列の値を <xref:System.DateTimeOffset> 構造体として取得します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>|フィールドの基になるプロバイダー固有の型である型を返します。 新しい日付型と時刻型の `GetFieldType` と同じ型を返します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>|指定した列の値を取得します。 新しい日付型と時刻型の `GetValue` と同じ型を返します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>|指定した配列内の値を取得します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|列の値を <xref:System.Data.SqlTypes.SqlString> として取得します。 データを `SqlString` として表現できない場合、<xref:System.InvalidCastException> が発生します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>|列データを既定の `SqlDbType` として取得します。 新しい日付型と時刻型の `GetValue` と同じ型を返します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>|指定した配列内の値を取得します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A>|Type System Version が SQL Server 2005 に設定されている場合、列の値を文字列として取得します。 データを文字列として表現できない場合、<xref:System.InvalidCastException> が発生します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetTimeSpan%2A>|指定された列の値を <xref:System.TimeSpan> 構造体として取得します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>|基になる CLR 型として、指定された列の値を取得します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>|配列内の列の値を取得します。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>|結果セットのメタデータを記述する <xref:System.Data.DataTable> を返します。|  
  
> [!NOTE]
>  新しい日付と時刻の `SqlDbTypes` は、SQL Server でインプロセスで実行されているコードではサポートされていません。 これらの型のいずれかがサーバーに渡されると、例外が発生します。  
  
## <a name="specifying-date-and-time-values-as-literals"></a>日付と時刻の値をリテラルとして指定する  
日付と時刻のデータ型を指定するには、さまざまなリテラル文字列形式を使用します。これは、実行時に評価 SQL Server、内部の日付/時刻構造に変換されます。 SQL Server は、単一引用符 (') で囲まれた日付と時刻のデータを認識します。 次の例では、いくつかの形式について説明します。  
  
- `'October 15, 2006'` などのアルファベットの日付形式。  
  
- 数値の日付形式 (`'10/15/2006'` など)。  
  
- ISO 標準の日付形式を使用している場合、2006年10月15日として解釈される、`'20061015'` などの区切られていない文字列形式。  
  
> [!NOTE]
>  すべてのリテラル文字列の形式と、日付と時刻のデータ型のその他の機能については、SQL Server オンラインブックを参照してください。  
  
時刻値が0未満または24時間以上の場合、<xref:System.ArgumentException> がスローされます。  
  
## <a name="resources-in-sql-server-2008-books-online"></a>SQL Server 2008 オンラインブックのリソース  
SQL Server 2008 での日付と時刻の値の操作の詳細については、SQL Server 2008 オンラインブックの次の情報を参照してください。  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[日付と時刻のデータ型および関数 (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98360)|Transact-SQL の日付と時刻のデータ型と関数の概要を説明します。|  
|[日時データの使用](https://go.microsoft.com/fwlink/?LinkId=98361)|日付と時刻のデータ型と関数に関する情報とそれらの使用例を提供します。|  
|[データ型 (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98362)|SQL Server 2008 のシステムデータ型について説明します。|  
  
## <a name="next-steps"></a>次の手順
- [SQL Server のデータ型と ADO.NET](sql-server-data-types.md)
