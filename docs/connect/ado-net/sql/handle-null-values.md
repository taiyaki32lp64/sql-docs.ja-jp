---
title: null 値の処理
description: SQL Server と .NET で GUID と uniqueidentifier の値を操作する方法について説明します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: f18b288f-b265-4bbe-957f-c6833c0645ef
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 6ae2bc8d816dd2bc32572447483dacd76dd967f0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452188"
---
# <a name="handling-null-values"></a>null 値の処理

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

列の値が不明または見つからない場合は、リレーショナルデータベース内の null 値が使用されます。 Null は、空の文字列 (文字データ型または datetime データ型の場合) でも、ゼロ値 (数値データ型の場合) でもありません。 ANSI SQL-92 仕様では、すべての null が一貫して処理されるように、すべてのデータ型で null を同じにする必要があることが示されています。 <xref:System.Data.SqlTypes> 名前空間は、<xref:System.Data.SqlTypes.INullable> インターフェイスを実装することによって null セマンティクスを提供します。 <xref:System.Data.SqlTypes> の各データ型には、独自の `IsNull` プロパティと、そのデータ型のインスタンスに割り当てることができる `Null` 値があります。  
  
> [!NOTE]
>  .NET Framework バージョン2.0 および .NET Core バージョン1.0 では、null 許容型のサポートが導入されました。これにより、プログラマは、基になる型のすべての値を表すように値型を拡張できます。 これらの CLR null 許容型は、<xref:System.Nullable> 構造体のインスタンスを表します。 この機能は、値型をボックス化およびボックス化解除して、オブジェクト型との互換性を強化する場合に特に便利です。 ANSI SQL null は `null` 参照 (または Visual Basic で `Nothing`) と同じようには動作しないため、CLR null 許容型はデータベースの null の格納を目的としていません。 データベース ANSI SQL null 値を操作する場合は、<xref:System.Nullable> ではなく <xref:System.Data.SqlTypes> null を使用します。 でC#の CLR null 許容型の使用の詳細については、「 C# null 許容[型](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/)」を参照してください。また、「 [null 許容型の使用](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/using-nullable-types/)」を参照してください。  
  
## <a name="nulls-and-three-valued-logic"></a>Null と3つの値のロジック  
列定義で null 値を許可すると、アプリケーションに3つの値のロジックが導入されます。 比較は、次の3つの条件のいずれかに評価される場合があります。  
  
- True  
  
- False  
  
- Unknown  
  
Null は不明と見なされるため、相互に比較した2つの null 値は等しいと見なされません。 算術演算子を使用する式では、オペランドのいずれかが null の場合、結果も null になります。  
  
## <a name="nulls-and-sqlboolean"></a>Null および SqlBoolean  
任意の <xref:System.Data.SqlTypes> を比較すると、<xref:System.Data.SqlTypes.SqlBoolean> が返されます。 各 `SqlType` の `IsNull` 関数は <xref:System.Data.SqlTypes.SqlBoolean> を返し、null 値をチェックするために使用できます。 次の実際の表は、null 値が存在する場合の AND、OR、および NOT 演算子の動作を示しています。 (T = true、F = false、U = unknown、または null)。  
  
![真理値表](../media/truthtable-bpuedev11.gif "|::ref1::|")  
  
### <a name="understanding-the-ansi_nulls-option"></a>ANSI_NULLS オプションについて  
<xref:System.Data.SqlTypes> は、SQL Server で ANSI_NULLS オプションが on に設定されている場合と同じセマンティクスを提供します。 すべての算術演算子 (+、-、*、/、%)、ビット演算子 (~、&、&#124;)、およびほとんどの関数では、プロパティ `IsNull` を除き、オペランドまたは引数が NULL であった場合に NULL を返します。  
  
ANSI SQL-92 標準では、WHERE 句で *columnName* = NULL とすることは認められていません。 SQL Server では、ANSI_NULLS オプションは、データベースの既定の null 値許容と null 値に対する比較の評価を制御します。 ANSI_NULLS が有効になっている場合 (既定)、null 値をテストするときに IS NULL 演算子を式で使用する必要があります。 たとえば、ANSI_NULLS を ON にした場合、次の比較では、必ず UNKNOWN が返されます。  
  
```console
colname > NULL  
```  
  
Null 値を含む変数との比較でも不明な結果が返されます。  
  
```console
colname > @MyVariable  
```  
  
IS NULL 述語または IS NOT NULL 述語は、NULL 値があるかどうかを調べるのに使用します。 ただし、これを使用すると WHERE 句は複雑になります。 たとえば、AdventureWorks Customer テーブルの TerritoryID 列では、null 値を使用できます。 SELECT ステートメントで特定の値の他に NULL 値の有無も調べるには、IS NULL 述語を使用する必要があります。  
  
```sql
SELECT CustomerID, AccountNumber, TerritoryID  
FROM AdventureWorks.Sales.Customer  
WHERE TerritoryID IN (1, 2, 3)  
   OR TerritoryID IS NULL  
```  
  
SQL Server で ANSI_NULLS を off に設定した場合は、等値演算子を使用して null と比較する式を作成できます。 ただし、別の接続がその接続に対して null オプションを設定するのを防ぐことはできません。 Null 値をテストするために IS NULL を使用すると、接続の ANSI_NULLS 設定に関係なく、常に動作します。  
  
`DataSet` では、ANSI_NULLS の設定はサポートされていません。 <xref:System.Data.SqlTypes> で null 値を処理する場合、常に ANSI SQL-92 標準に従います。  
  
## <a name="assigning-null-values"></a>Null 値の割り当て  
Null 値は特殊な値であり、ストレージと割り当てのセマンティクスは、型システムとストレージシステムによって異なります。 `Dataset` は、さまざまな種類およびストレージシステムで使用できるように設計されています。  
  
このセクションでは、さまざまな型システムで <xref:System.Data.DataRow> 内の <xref:System.Data.DataColumn> に null 値を割り当てるための null セマンティクスについて説明します。  
  
`DBNull.Value`  
この割り当ては、任意の型の `DataColumn` に対して有効です。 型に `INullable` が実装されている場合、`DBNull.Value` は適切に型指定された適切な Null 値に強制変換されます。  
  
`SqlType.Null`  
すべての <xref:System.Data.SqlTypes> データ型は `INullable` を実装します。 厳密に型指定された null 値を、暗黙的なキャスト演算子を使用して列のデータ型に変換できる場合は、割り当てが行われます。 それ以外の場合は、無効なキャスト例外がスローされます。  
  
`null`  
' Null ' が指定された `DataColumn` データ型に対して有効な値である場合、`INullable` の型 (`SqlType.Null`) に関連付けられている適切な `DbNull.Value` または `Null` に強制されます。  
  
`derivedUdt.Null`  
UDT 列の場合、null は常に、`DataColumn` に関連付けられた型に基づいて格納されます。 `INullable` を実装していない `DataColumn` に関連付けられた UDT が、そのサブクラスで実行される場合を考えてみます。 この場合、派生クラスに関連付けられた厳密に型指定された null 値が割り当てられると、null ストレージは常に DataColumn のデータ型と一致するため、型指定されていない `DbNull.Value` として格納されます。  
  
> [!NOTE]
>  `Nullable<T>` または <xref:System.Nullable> 構造は、現在、`DataSet` ではサポートされていません。  
  
### <a name="multiple-column-row-assignment"></a>複数列 (行) の割り当て  
行にマップされる <xref:System.Data.DataRow.ItemArray%2A> を受け入れる `DataTable.Add`、`DataTable.LoadDataRow`、またはその他の Api では、' null ' を DataColumn の既定値にマップします。 配列内のオブジェクトに `DbNull.Value` または厳密に型指定された対応するオブジェクトが含まれている場合は、前述の規則と同じ規則が適用されます。  
  
また、`DataRow.["columnName"]` の null 割り当てのインスタンスには、次の規則が適用されます。  
  
- 既定の *default* 値は `DbNull.Value` です。ただし、それが厳密に型指定された適切な NULL 値となる、厳密に型指定された NULL 列は例外です。  
  
- XML ファイルへのシリアル化中に Null 値が書き出されることはありません ("xsi: nil" のように)。  
  
- Null 以外のすべての値 (既定値を含む) は、XML へのシリアル化中に常に書き込まれます。 これは、null 値 (xsi: nil) が明示的で、既定値が暗黙的である (XML に存在しない場合、検証パーサーが関連 XSD スキーマから取得できる) XSD/XML セマンティクスとは異なります。 `DataTable` の場合、これとは逆になります。 null 値は暗黙的で、既定値は explicit です。  
  
- XML 入力から読み取られた行の欠損列値にはすべて NULL が割り当てられます。 <xref:System.Data.DataTable.NewRow%2A> または同様の方法を使用して作成された行には、DataColumn の既定値が割り当てられます。  
  
- <xref:System.Data.DataRow.IsNull%2A> メソッドは、`DbNull.Value` と `INullable.Null` の両方に対して `true` を返します。  
  
## <a name="assigning-null-values"></a>Null 値の割り当て  
すべての <xref:System.Data.SqlTypes> インスタンスの既定値は null です。  
  
<xref:System.Data.SqlTypes>の null は型固有であり、1つの値 (`DbNull` など) で表すことはできません。 `IsNull` プロパティを使用して、null かどうかを確認します。  
  
次のコード例に示すように、Null 値を <xref:System.Data.DataColumn> に割り当てることができます。 Null 値は、例外をトリガーすることなく `SqlTypes` 変数に直接割り当てることができます。  
  
### <a name="example"></a>例  
次のコード例では、<xref:System.Data.SqlTypes.SqlInt32> と <xref:System.Data.SqlTypes.SqlString> として定義された2つの列を持つ <xref:System.Data.DataTable> を作成します。 このコードでは、既知の値の行を1つ追加し、null 値の行を1行追加した後、<xref:System.Data.DataTable> を反復処理して変数に値を割り当て、コンソールウィンドウに出力を表示します。  
  
[!code-csharp[DataWorks SqlInt32_IsNull#1](~/../sqlclient/doc/samples/SqlInt32_IsNull.cs#1)]
  
この例では、次の結果が表示されます。  
  
```console
isColumnNull=False, ID=123, Description=Side Mirror  
isColumnNull=True, ID=Null, Description=Null  
```  
  
## <a name="comparing-null-values-with-sqltypes-and-clr-types"></a>SqlTypes と CLR 型との null 値の比較  
Null 値を比較する場合は、CLR 型の場合と比較して、`Equals` メソッドが <xref:System.Data.SqlTypes> で null 値を評価する方法の違いを理解しておくことが重要です。 すべての <xref:System.Data.SqlTypes> `Equals` メソッドは、null 値の評価にデータベースセマンティクスを使用します。いずれかまたは両方の値が null の場合、比較によって null が生成されます。 一方、2つの <xref:System.Data.SqlTypes> で CLR `Equals` メソッドを使用すると、両方が null の場合に true が生成されます。 これは、CLR `String.Equals` メソッドなどのインスタンスメソッドを使用する場合と、静的/共有メソッドを使用する場合の違い (`SqlString.Equals`) を反映しています。  
  
次の例では、各に null 値のペアが渡され、次に空の文字列のペアが渡された場合の、`SqlString.Equals` メソッドと `String.Equals` メソッドの結果の違いを示します。  
  
[!code-csharp[DataWorks SqlString_Equals#1](~/../sqlclient/doc/samples/SqlString_Equals.cs#1)]
  
このコードを実行すると、次の出力が生成されます。  
  
```console
SqlString.Equals shared/static method:  
  Two nulls=Null  
  
String.Equals instance method:  
  Two nulls=True  
  
SqlString.Equals shared/static method:  
  Two empty strings=True  
  
String.Equals instance method:  
  Two empty strings=True   
```  
  
## <a name="next-steps"></a>次の手順
- [SQL Server のデータ型と ADO.NET](sql-server-data-types.md)
