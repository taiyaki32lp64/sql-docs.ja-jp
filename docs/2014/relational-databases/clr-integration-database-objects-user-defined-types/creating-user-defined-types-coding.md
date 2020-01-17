---
title: ユーザー定義型のコーディング |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- validation [CLR integration]
- UDTs [CLR integration], coding
- UserDefined serialization format [CLR integration]
- Point UDT
- Parse method
- null values [CLR integration]
- ToString method
- ValidatePoint method
- attributes [CLR integration]
- coding user-defined types [CLR integration]
- Read method
- Write method
- nullability [CLR integration]
- user-defined types [CLR integration], coding
- Currency UDT
- validating UDT values
- exposing UDT properties [CLR integration]
ms.assetid: 1e5b43b3-4971-45ee-a591-3f535e2ac722
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7427de92691a2d5c0a92aac55ac16f47dd2ef6b1
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75232240"
---
# <a name="coding-user-defined-types"></a>ユーザー定義型のコーディング
  ユーザー定義型 (UDT) の定義をコーディングする際は、形式やシリアル化のオプションを選択するだけでなく、UDT をクラスと構造体のどちらで実装するかによって、さまざまな機能を実装する必要があります。  
  
 このセクションの例では、`Point` UDT を `struct` (Visual Basic では `Structure`) として実装する方法について説明します。 
  `Point` UDT は、プロパティ プロシージャとして実装される X 座標と Y 座標から構成されます。  
  
 UDT の定義に必要な名前空間を次に示します。  
  
```vb  
Imports System  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
```  
  
```csharp  
using System;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
```  
  
 
  `Microsoft.SqlServer.Server` 名前空間には、UDT のさまざまな属性に必要なオブジェクトが含まれています。また、`System.Data.SqlTypes` 名前空間には、アセンブリに使用できる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ネイティブ データ型を表すクラスが含まれています。 それ以外にもアセンブリが正しく機能するために必要な名前空間が存在する場合があります。 
  `Point` UDT は、文字列用の `System.Text` 名前空間も使用します。  
  
> [!NOTE]  
>  
  `/clr:pure` を指定してコンパイルした Visual C++ のデータベース オブジェクト (UDT など) は実行できません。  
  
## <a name="specifying-attributes"></a>属性の指定  
 UDT のストレージ表現を構築し、クライアントに UDT を値として転送するためにシリアル化を使用する方法は、属性で決まります。  
  
 
  `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` は必須です。 
  `Serializable` 属性は省略できます。 また、`Microsoft.SqlServer.Server.SqlFacetAttribute` を指定して、UDT の戻り値の型に関する情報を提供することもできます。 詳細については、「[CLR ルーチンのカスタム属性](../clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)」を参照してください。  
  
### <a name="point-udt-attributes"></a>Point UDT の属性  
 
  `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` の `Point` UDT のストレージ形式は `Native` に設定します。 
  `IsByteOrdered` は `true` に設定します。これにより、SQL Server の比較結果がマネージド コードの比較結果と等しくなります。 さらに、この UDT に `System.Data.SqlTypes.INullable` インターフェイスを実装し、NULL に対応できるようにします。  
  
 次のコードに `Point` UDT の属性を示します。  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True)> _  
  Public Structure Point  
    Implements INullable  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true)]  
public struct Point : INullable  
{  
```  
  
## <a name="implementing-nullability"></a>NULL 値の許容属性の実装  
 アセンブリの属性を正しく指定することに加えて、UDT で NULL 値の許容属性をサポートする必要があります。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に読み込まれる UDT は NULL 値に対応していますが、UDT に NULL 値を認識させるには、UDT に `System.Data.SqlTypes.INullable` インターフェイスを実装する必要があります。  
  
 CLR コード内から値が NULL かどうかを判断するのに必要な `IsNull` というプロパティを作成する必要があります。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では UDT が NULL インスタンスであることを検出すると、通常の NULL 値処理メソッドを使用して UDT を保存します。 そのため、サーバーが NULL の UDT の不要なシリアル化やシリアル化解除に時間を費やしたり、NULL の UDT を格納して領域を無駄にすることはありません。 この NULL に関するチェックは CLR から UDT が渡されるたびに実行されます。つまり、[!INCLUDE[tsql](../../includes/tsql-md.md)] の IS NULL コンストラクトを使用して NULL UDT のチェックを実行すると、必ず成功することを意味します。 また、`IsNull` プロパティは、インスタンスが NULL かどうかをテストするためにサーバーでも使用されます。 UDT が NULL であることを判断できれば、サーバーはネイティブの NULL 処理を使用できます。  
  
 
  `get()` の `IsNull` メソッドは決して特殊なケースではありません。 
  `Point` の `@p` 変数が `Null` の場合、`@p.IsNull` は既定で、"1" ではなく "NULL" と評価されます。 これは、`SqlMethod(OnNullCall)` メソッドの `IsNull get()` 属性が既定で False であるためです。 オブジェクトが `Null` であるため、プロパティを要求したときには、オブジェクトがシリアル化解除されることもメソッドが呼び出されることもなく、既定値の "NULL" が返されます。  
  
### <a name="example"></a>例  
 次の例では、プライベート変数の `is_Null` に、UDT のインスタンスが NULL かどうかに関する状態が格納されます。 コードを作成する際は、`is_Null` の値を適切な状態に保つように注意する必要があります。 また、UDT の NULL 値のインスタンスを返す `Null` という静的プロパティを UDT に含める必要があります。 これにより、データベース内の UDT のインスタンスが実際に NULL の場合に、UDT から NULL 値を返すことができます。  
  
```vb  
Private is_Null As Boolean  
  
Public ReadOnly Property IsNull() As Boolean _  
   Implements INullable.IsNull  
    Get  
        Return (is_Null)  
    End Get  
End Property  
  
Public Shared ReadOnly Property Null() As Point  
    Get  
        Dim pt As New Point  
        pt.is_Null = True  
        Return (pt)  
    End Get  
End Property  
```  
  
```csharp  
private bool is_Null;  
  
public bool IsNull  
{  
    get  
    {  
        return (is_Null);  
    }  
}  
  
public static Point Null  
{  
    get  
    {  
        Point pt = new Point();  
        pt.is_Null = true;  
        return pt;  
    }  
}  
```  
  
### <a name="is-null-vs-isnull"></a>IS NULL と IsNull  
 Points(id int, location Point) というスキーマ (`Point` は CLR UDT) を含むテーブルと次のクエリを考えてみます。  
  
```  
--Query 1  
SELECT ID  
FROM Points  
WHERE NOT (location IS NULL) -- Or, WHERE location IS NOT NULL;  
```  
  
```  
--Query 2:  
SELECT ID  
FROM Points  
WHERE location.IsNull = 0;  
```  
  
 これらのクエリは、location が `Null` ではない Points の ID を返します。 クエリ 1 では、通常の Null 処理が使用されるため、UDT のシリアル化解除は必要ありません。 一方、クエリ 2 では、`Null` プロパティの値を取得するために、`IsNull` でないオブジェクトをすべてシリアル化解除し、CLR を呼び出す必要があります。 
  `IS NULL` を使用する方が明らかにパフォーマンスがよく、UDT の `IsNull` プロパティを [!INCLUDE[tsql](../../includes/tsql-md.md)] コードから読み取らなければならない理由はまったくありません。  
  
 では、何のために `IsNull` プロパティを使用するのでしょうか。 1 つ目の理由は、値が `Null` かどうかを CLR コード内から判断するために必要だということです。 2 つ目の理由は、インスタンスが `Null` かどうかをテストするための手段として、サーバーがこのプロパティを使用するためです。 インスタンスが `Null` であることを判断できれば、サーバーはネイティブの NULL 処理を使用してこのインスタンスを処理できます。  
  
## <a name="implementing-the-parse-method"></a>Parse メソッドの実装  
 
  `Parse` メソッドと `ToString` メソッドを使用すると、UDT を文字列形式に変換したり、文字列形式から別の形式に変換できます。 
  `Parse` メソッドでは、文字列を UDT に変換できます。 このメソッドは `static` (Visual Basic では `Shared`) メソッドとして宣言され、`System.Data.SqlTypes.SqlString` 型のパラメーターを受け取る必要があります。  
  
 次のコードでは、`Parse` UDT の `Point` メソッドを実装します。このメソッドでは、X 座標と Y 座標を分離します。 
  `Parse` メソッドには `System.Data.SqlTypes.SqlString` 型の引数が 1 つあり、X と Y の値はコンマ区切りの文字列として提供されることを想定します。 
  `Microsoft.SqlServer.Server.SqlMethodAttribute.OnNullCall` 属性を `false` に設定すると、Point の NULL インスタンスから `Parse` メソッドが呼び出されなくなります。  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
    return pt;  
}  
```  
  
## <a name="implementing-the-tostring-method"></a>ToString メソッドの実装  
 
  `ToString` メソッドでは、`Point` UDT が文字列値に変換されます。 この場合は、`Point` 型の NULL インスタンスには文字列 "NULL" が返されます。 
  `ToString` メソッドでは、`Parse` を使用して `System.Text.StringBuilder` メソッドと逆の操作を行い、X 座標と Y 座標の値から構成されるコンマ区切りの `System.String` を返します。 **Invokeifreceiverisnull**の既定値は false であるため、の`Point` null インスタンスのチェックは必要ありません。  
  
```vb  
Private _x As Int32  
Private _y As Int32  
  
Public Overrides Function ToString() As String  
    If Me.IsNull Then  
        Return "NULL"  
    Else  
        Dim builder As StringBuilder = New StringBuilder  
        builder.Append(_x)  
        builder.Append(",")  
        builder.Append(_y)  
        Return builder.ToString  
    End If  
End Function  
```  
  
```csharp  
private Int32 _x;  
private Int32 _y;  
  
public override string ToString()  
{  
    if (this.IsNull)  
        return "NULL";  
    else  
    {  
        StringBuilder builder = new StringBuilder();  
        builder.Append(_x);  
        builder.Append(",");  
        builder.Append(_y);  
        return builder.ToString();  
    }  
}  
```  
  
## <a name="exposing-udt-properties"></a>UDT プロパティの公開  
 
  `Point` UDT は、`System.Int32` 型のパブリックの読み書きプロパティとして実装される X 座標と Y 座標を公開します。  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _x = Value  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _y = Value  
    End Set  
End Property  
```  
  
```csharp  
public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    set   
    {  
        _x = value;  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        _y = value;  
    }  
}  
```  
  
## <a name="validating-udt-values"></a>UDT 値の検証  
 UDT データの使用時は、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]により、バイナリ値が自動的に UDT 値に変換されます。 この変換処理では、値がその UDT のシリアル化形式に適しているかどうかがチェックされ、値を正しくシリアル化解除できるようにします。 これにより、値はバイナリ形式に再変換できるようになります。 また、バイト順の UDT の場合は、結果のバイナリ値が必ず元のバイナリ値と一致するようになります。 これにより、無効な値がデータベース内に存在する危険性が回避されます。 それでも、このレベルのチェックでは不十分である場合もあります。 UDT 値を一定の範囲内に制限する必要があるときは、さらに検証が必要になります。 たとえば、日付を実装する UDT の日の値は、特定の有効範囲内の正の数である必要があります。  
  
 
  `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute.ValidationMethodName` の `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` プロパティを使用すると、データを UDT に割り当てる場合および UDT に変換する場合にサーバーで実行される検証メソッドを指定できます。 また `ValidationMethodName` は、bcp ユーティリティ、BULK INSERT、DBCC CHECKDB、DBCC CHECKFILEGROUP、DBCC CHECKTABLE、分散クエリ、表形式のデータ ストリーム (TDS) リモート プロシージャ コール (RPC) などの操作の実行中にも呼び出されます。 
  `ValidationMethodName` の既定値は NULL です。これは、検証メソッドが指定されていないことを示します。  
  
### <a name="example"></a>例  
 次のコードでは、`Point` の `ValidationMethodName` を指定する `ValidatePoint` クラスを宣言します。  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True, _  
  ValidationMethodName:="ValidatePoint")> _  
  Public Structure Point  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true,   
  ValidationMethodName = "ValidatePoint")]  
public struct Point : INullable  
{  
```  
  
 検証メソッドを指定する場合は、次のコードに示すようなシグネチャが必要です。  
  
```vb  
Private Function ValidationFunction() As Boolean  
    If (validation logic here) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidationFunction()  
{  
    if (validation logic here)  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
 検証メソッドには任意のスコープを設定でき、値が有効な場合は `true` を返し、それ以外の場合は `false` を返す必要があります。 このメソッドから `false` が返されるか例外がスローされると、その値は無効な値と見なされ、エラーが発生します。  
  
 次のコード例では、0 以上の値のみが X 座標および Y 座標として許可されます。  
  
```vb  
Private Function ValidatePoint() As Boolean  
    If (_x >= 0) And (_y >= 0) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidatePoint()  
{  
    if ((_x >= 0) && (_y >= 0))  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
### <a name="validation-method-limitations"></a>検証メソッドの制限事項  
 サーバーから検証メソッドが呼び出されるのは、サーバーで変換が実行されるときです。個別のプロパティを設定したり [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT ステートメントを使用してデータを挿入するときには呼び出されません。  
  
 すべての状況で検証メソッドを実行する場合は、 `Parse`プロパティ setter およびメソッドから明示的に検証メソッドを呼び出す必要があります。 この呼び出しは必須ではなく、場合によっては不適切な呼び出しになることもあります。  
  
### <a name="parse-validation-example"></a>Parse による検証の例  
 クラスで`ValidatePoint`メソッドが呼び出されるようにするには、 `Parse`メソッドと、X 座標と Y 座標の値を設定するプロパティプロシージャからメソッドを呼び出す必要があります。 `Point` 次のコードフラグメントは、 `ValidatePoint` `Parse`関数から検証メソッドを呼び出す方法を示しています。  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
  
    ' Call ValidatePoint to enforce validation  
    ' for string conversions.  
    If Not pt.ValidatePoint() Then  
        Throw New ArgumentException("Invalid XY coordinate values.")  
    End If  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
  
    // Call ValidatePoint to enforce validation  
    // for string conversions.  
    if (!pt.ValidatePoint())   
        throw new ArgumentException("Invalid XY coordinate values.");  
    return pt;  
}  
```  
  
### <a name="property-validation-example"></a>Property による検証の例  
 次のコードフラグメントは、X 座標と`ValidatePoint` Y 座標を設定するプロパティプロシージャから検証メソッドを呼び出す方法を示しています。  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _x  
        _x = Value  
        If Not ValidatePoint() Then  
            _x = temp  
            Throw New ArgumentException("Invalid X coordinate value.")  
        End If  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _y  
        _y = Value  
        If Not ValidatePoint() Then  
            _y = temp  
            Throw New ArgumentException("Invalid Y coordinate value.")  
        End If  
    End Set  
End Property  
```  
  
```csharp  
    public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    // Call ValidatePoint to ensure valid range of Point values.  
    set   
    {  
        Int32 temp = _x;  
        _x = value;  
        if (!ValidatePoint())  
        {  
            _x = temp;  
            throw new ArgumentException("Invalid X coordinate value.");  
        }  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        Int32 temp = _y;  
        _y = value;  
        if (!ValidatePoint())  
        {  
            _y = temp;  
            throw new ArgumentException("Invalid Y coordinate value.");  
        }  
    }  
}  
```  
  
## <a name="coding-udt-methods"></a>UDT メソッドのコーディング  
 UDT メソッドをコーディングする際は、使用するアルゴリズムが時間の経過と共に変化する可能性があるかどうかを考慮します。 変化する可能性がある場合は、UDT で使用するメソッド用に独立したクラスを作成することを検討します。 アルゴリズムが変化したら、新しいコードになったクラスを再コンパイルし、UDT に影響を与えることなくそのアセンブリを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に読み込むことができます。 多くの場合、UDT は [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY ステートメントを使用して再読み込みできますが、既存のデータとの間に問題が発生する可能性があります。 たとえば、AdventureWorks サンプル`Currency`データベースに含まれ**** ている UDT は、 **convertcurrency**関数を使用して、別のクラスに実装されている通貨値を変換します。 変換アルゴリズムが今後どう変化するかは予測できず、新しい機能が必要になる可能性もあります。 **Convertcurrency**関数を`Currency` UDT 実装から分離することで、将来の変更を計画するときの柔軟性が向上します。  
  
### <a name="example"></a>例  
 この`Point`クラスには、 **distance、** **DistanceFrom** 、 **DistanceFromXY**の3つの単純なメソッドが含まれています。 各メソッドから返されるのは、`double` から 0 までの距離、指定した地点から `Point` までの距離、および指定した X 座標と Y 座標から `Point` までの距離を示す `Point` 型の値です。 **Distance**と**DistanceFrom**はそれぞれ**DistanceFromXY**を呼び出し、メソッドごとに異なる引数を使用する方法を示します。  
  
```vb  
' Distance from 0 to Point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function Distance() As Double  
    Return DistanceFromXY(0, 0)  
End Function  
  
' Distance from Point to the specified point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFrom(ByVal pFrom As Point) As Double  
    Return DistanceFromXY(pFrom.X, pFrom.Y)  
End Function  
  
' Distance from Point to the specified x and y values.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFromXY(ByVal ix As Int32, ByVal iy As Int32) _  
    As Double  
    Return Math.Sqrt(Math.Pow(ix - _x, 2.0) + Math.Pow(iy - _y, 2.0))  
End Function  
```  
  
```csharp  
// Distance from 0 to Point.  
[SqlMethod(OnNullCall = false)]  
public Double Distance()  
{  
    return DistanceFromXY(0, 0);  
}  
  
// Distance from Point to the specified point.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFrom(Point pFrom)  
{  
    return DistanceFromXY(pFrom.X, pFrom.Y);  
}  
  
// Distance from Point to the specified x and y values.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFromXY(Int32 iX, Int32 iY)  
{  
    return Math.Sqrt(Math.Pow(iX - _x, 2.0) + Math.Pow(iY - _y, 2.0));  
}  
```  
  
### <a name="using-sqlmethod-attributes"></a>SqlMethod 属性の使用  
 
  `Microsoft.SqlServer.Server.SqlMethodAttribute` クラスにはカスタム属性が用意されています。このカスタム属性を使用して、決定性を示したり、NULL で呼び出したときの動作を指定したり、メソッドがミューテーターかどうかを指定するためにメソッド定義にマークを付けることができます。 これらのプロパティは既定値に設定されるので、既定値以外の値を設定する場合のみカスタム属性を使用します。  
  
> [!NOTE]  
>  
  `SqlMethodAttribute` クラスは `SqlFunctionAttribute` クラスを継承するので、`SqlMethodAttribute` は `FillRowMethodName` フィールドと `TableDefinition` フィールドを `SqlFunctionAttribute` から継承します。 これは、一見テーブル値メソッドを記述できることを示していますが、この場合には該当しません。 メソッドはコンパイルされ、アセンブリが配置されますが`IEnumerable` 、実行時に戻り値の型に関するエラーが発生します。アセンブリ '\<\<\<assembly> ' のクラス ' class> ' の "method、property、または field ' name> ' には、無効な戻り値の型があります。"  
  
 次の表では、UDT メソッドで使用できる `Microsoft.SqlServer.Server.SqlMethodAttribute` の関連プロパティについて説明し、それらの既定値を示します。  
  
 DataAccess  
 関数から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカル インスタンスに格納されているユーザー データにアクセスする必要があるかどうかを示します。 既定値は `DataAccessKind`.`None` です。  
  
 IsDeterministic  
 入力値とデータベースの状態が同じであれば、関数から同じ値が出力されるかどうかを示します。 既定値は `false` です。  
  
 IsMutator  
 メソッドにより UDT インスタンスの状態が変化するかどうかを示します。 既定値は `false` です。  
  
 IsPrecise  
 浮動小数点演算など、厳密な結果が算出されない計算が関数に含まれているかどうかを示します。 既定値は `false` です。  
  
 OnNullCall  
 入力引数に NULL 参照が指定されたときにメソッドが呼び出されるかどうかを示します。 既定値は `true` です。  
  
### <a name="example"></a>例  
 
  `Microsoft.SqlServer.Server.SqlMethodAttribute.IsMutator` プロパティを使用すると、UDT インスタンスの状態の変化を許可するようにメソッドをマークできます。 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] では、1 つの UPDATE ステートメントの SET 句に 2 つの UDT プロパティを設定できません。 ただし、2 つのメンバーを変更するミューテーターとしてメソッドをマークすることはできます。  
  
> [!NOTE]  
>  ミューテーター メソッドはクエリ内では使用できません。 代入ステートメントかデータ変更ステートメントでのみ、これらのメソッドを呼び出すことができます。 ミューテーターとしてマークされたメソッドが戻り値を返さない `void` (Visual Basic では `Sub`) の場合、CREATE TYPE はエラーで失敗します。  
  
 次のステートメントでは、`Triangles` メソッドを含む `Rotate` UDT が存在するものとします。 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] 更新ステートメントでは、`Rotate` メソッドを呼び出します。  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 
  `Rotate` メソッドは、`SqlMethod` が `IsMutator` に設定された `true` 属性で修飾されています。これにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はこのメソッドをミューテーター メソッドとしてマークできます。 また、このコードでは `OnNullCall` を `false` に設定しています。これは、いずれかの入力パラメーターが NULL 参照の場合に、メソッドから NULL 参照 (Visual Basic では `Nothing`) が返されることをサーバーに示しています。  
  
```vb  
<SqlMethod(IsMutator:=True, OnNullCall:=False)> _  
Public Sub Rotate(ByVal anglex as Double, _  
  ByVal angley as Double, ByVal anglez As Double)   
   RotateX(anglex)  
   RotateY(angley)  
   RotateZ(anglez)  
End Sub  
```  
  
```csharp  
[SqlMethod(IsMutator = true, OnNullCall = false)]  
public void Rotate(double anglex, double angley, double anglez)   
{  
   RotateX(anglex);  
   RotateY(angley);  
   RotateZ(anglez);  
}  
```  
  
## <a name="implementing-a-udt-with-a-user-defined-format"></a>ユーザー定義形式による UDT の実装  
 ユーザー定義形式を使用して UDT を実装する際は、`Read` メソッドと `Write` メソッドを実装する必要があります。これらのメソッドは、UDT データのシリアル化とシリアル化解除を処理する Microsoft.SqlServer.Server.IBinarySerialize インターフェイスを実装します。 また、`MaxByteSize` の `Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute` プロパティも指定する必要があります。  
  
### <a name="the-currency-udt"></a>Currency UDT  
 
  `Currency` 以降、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UDT は、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] と共にインストールできる CLR サンプルに同梱されています。  
  
 
  `Currency` UDT では、特定のカルチャの通貨システムでの金額の処理がサポートされます。 定義するフィールドは 2 つあります。`string` 型の `CultureInfo` フィールドでは、通貨の発行カルチャ (en-us など) を指定します。`decimal` 型の `CurrencyValue` フィールドでは金額を指定します。  
  
 
  `Currency` UDT がサーバーでの比較に使用されることはありませんが、この UDT には、1 つのメソッド `System.IComparable` を公開する `System.IComparable.CompareTo` インターフェイスが実装されます。 このインターフェイスは、クライアント側でカルチャ内の通貨値を正しく比較したり並べ替えたりする場合に使用されます。  
  
 CLR で実行されているコードでは、カルチャが通貨値とは別に比較されます。 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] コードでは、次の操作により比較結果が決まります。  
  
1.  
  `IsByteOrdered` 属性を true に設定します。これは、ディスク上に保存されたバイナリ表現を使用して比較を行うように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に指示します。  
  
2.  
  `Write` UDT に `Currency` メソッドを使用して、この UDT をディスクに保存する形式と、その情報に基づいて [!INCLUDE[tsql](../../includes/tsql-md.md)] 演算で UDT 値を比較し順序付ける方法を決定します。  
  
3.  次のバイナリ形式を使用して `Currency` UDT を保存します。  
  
    1.  0 バイト目から 19 バイト目までは UTF-16 エンコードされた文字列としてカルチャを保存します。右側の不足バイトには NULL 文字が埋め込まれます。  
  
    2.  20 バイト目以降を使用して、通貨の 10 進値を保存します。  
  
 NULL 文字を埋め込む目的は、カルチャと通貨値を完全に分離することです。これにより、[!INCLUDE[tsql](../../includes/tsql-md.md)] コードで UDT が比較されるとき、カルチャ バイトどうし、通貨バイト値どうしが比較されるようになります。  
  
 `Currency` UDT の完全なコードリストについては、 [SQL Server データベースエンジンのサンプル](https://msftengprodsamples.codeplex.com/)で CLR サンプルをインストールする方法に関する説明に従ってください。  
  
### <a name="currency-attributes"></a>Currency の属性  
 
  `Currency` UDT には、次の属性が定義されます。  
  
```vb  
<Serializable(), Microsoft.SqlServer.Server.SqlUserDefinedType( _  
    Microsoft.SqlServer.Server.Format.UserDefined, _  
    IsByteOrdered:=True, MaxByteSize:=32), _  
    CLSCompliant(False)> _  
Public Structure Currency  
Implements INullable, IComparable, _  
Microsoft.SqlServer.Server.IBinarySerialize  
```  
  
```csharp  
[Serializable]  
[SqlUserDefinedType(Format.UserDefined,   
    IsByteOrdered = true, MaxByteSize = 32)]  
    [CLSCompliant(false)]  
    public struct Currency : INullable, IComparable, IBinarySerialize  
    {  
```  
  
## <a name="creating-read-and-write-methods-with-ibinaryserialize"></a>IBinarySerialize を備えた Read メソッドと Write メソッドの作成  
 
  `UserDefined` シリアル化形式を選択した場合は、`IBinarySerialize` インターフェイスを実装し、独自の `Read` メソッドと `Write` メソッドを実装する必要があります。 次の `Currency` UDT のプロシージャでは、`System.IO.BinaryReader` と `System.IO.BinaryWriter` を使用して UDT に対する読み取りと書き込みを行います。  
  
```vb  
' IBinarySerialize methods  
' The binary layout is as follow:  
'    Bytes 0 - 19: Culture name, padded to the right with null  
'    characters, UTF-16 encoded  
'    Bytes 20+: Decimal value of money  
' If the culture name is empty, the currency is null.  
Public Sub Write(ByVal w As System.IO.BinaryWriter) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Write  
    If Me.IsNull Then  
        w.Write(nullMarker)  
        w.Write(System.Convert.ToDecimal(0))  
        Return  
    End If  
  
    If cultureName.Length > cultureNameMaxSize Then  
        Throw New ApplicationException(String.Format(CultureInfo.CurrentUICulture, _  
           "{0} is an invalid culture name for currency as it is too long.", cultureNameMaxSize))  
    End If  
  
    Dim paddedName As String = cultureName.PadRight(cultureNameMaxSize, CChar(vbNullChar))  
  
    For i As Integer = 0 To cultureNameMaxSize - 1  
        w.Write(paddedName(i))  
    Next i  
  
    ' Normalize decimal value to two places  
    currencyVal = Decimal.Floor(currencyVal * 100) / 100  
    w.Write(currencyVal)  
End Sub  
  
Public Sub Read(ByVal r As System.IO.BinaryReader) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Read  
    Dim name As Char() = r.ReadChars(cultureNameMaxSize)  
    Dim stringEnd As Integer = Array.IndexOf(name, CChar(vbNullChar))  
  
    If stringEnd = 0 Then  
        cultureName = Nothing  
        Return  
    End If  
  
    cultureName = New String(name, 0, stringEnd)  
    currencyVal = r.ReadDecimal()  
End Sub  
  
```  
  
```csharp  
// IBinarySerialize methods  
// The binary layout is as follow:  
//    Bytes 0 - 19:Culture name, padded to the right   
//    with null characters, UTF-16 encoded  
//    Bytes 20+:Decimal value of money  
// If the culture name is empty, the currency is null.  
public void Write(System.IO.BinaryWriter w)  
{  
    if (this.IsNull)  
    {  
        w.Write(nullMarker);  
        w.Write((decimal)0);  
        return;  
    }  
  
    if (cultureName.Length > cultureNameMaxSize)  
    {  
        throw new ApplicationException(string.Format(  
            CultureInfo.InvariantCulture,   
            "{0} is an invalid culture name for currency as it is too long.",   
            cultureNameMaxSize));  
    }  
  
    String paddedName = cultureName.PadRight(cultureNameMaxSize, '\0');  
    for (int i = 0; i < cultureNameMaxSize; i++)  
    {  
        w.Write(paddedName[i]);  
    }  
  
    // Normalize decimal value to two places  
    currencyValue = Decimal.Floor(currencyValue * 100) / 100;  
    w.Write(currencyValue);  
}  
public void Read(System.IO.BinaryReader r)  
{  
    char[] name = r.ReadChars(cultureNameMaxSize);  
    int stringEnd = Array.IndexOf(name, '\0');  
  
    if (stringEnd == 0)  
    {  
        cultureName = null;  
        return;  
    }  
  
    cultureName = new String(name, 0, stringEnd);  
    currencyValue = r.ReadDecimal();  
}  
```  
  
 `Currency` UDT の完全なコードリストについては、「 [SQL Server データベースエンジンサンプル](https://msftengprodsamples.codeplex.com/)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ユーザー定義型の作成](creating-user-defined-types.md)  
  
