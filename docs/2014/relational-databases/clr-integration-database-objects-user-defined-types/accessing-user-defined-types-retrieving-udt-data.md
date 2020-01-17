---
title: UDT データの取得 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SqlDataReader object
- ADO.NET [CLR integration]
- binding UDTs [CLR integration]
- UDTs [CLR integration], ADO.NET
- assemblies [CLR integration], user-defined types
- query parameters [CLR integration]
- user-defined types [CLR integration], ADO.NET
- bytes [CLR integration]
ms.assetid: 6a98ac8c-0e69-4c03-83a4-2062cb782049
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 085b1783214e7f629f1cb91084303edacd151c25
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874643"
---
# <a name="retrieving-udt-data"></a>UDT データの取得
  クライアント側で UDT (ユーザー定義型) を作成するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに UDT として登録されたアセンブリをクライアント アプリケーションで使用できるようにしておく必要があります。 この UDT アセンブリは、アプリケーションと同じディレクトリまたは GAC (グローバル アセンブリ キャッシュ) に配置できます。 また、プロジェクト内で、このアセンブリへの参照を設定することもできます。  
  
## <a name="requirements-for-using-udts-in-adonet"></a>ADO.NET で UDT を使用するための要件  
 クライアント側で UDT を作成するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に読み込まれたアセンブリとクライアント側に存在するアセンブリとの間に互換性がなくてはなりません。 `Native` シリアル化形式で定義した UDT の場合は、アセンブリの構造に互換性が必要です。 `UserDefined` 形式で定義したアセンブリの場合は、そのアセンブリをクライアント側で使用できる必要があります。  
  
 テーブルの UDT 列からデータをそのまま取得するために、クライアントに UDT アセンブリをコピーする必要はありません。  
  
> [!NOTE]  
>  **SqlClient**の UDT のバージョンが一致しないまたはその他の問題が発生した場合、UDT の読み込みに失敗します。 この場合、通常のトラブルシューティング メカニズムを使用して、呼び出し元のアプリケーションで UDT を含むアセンブリが検出されない原因を特定します。 詳細については、.NET Framework のドキュメントのトピック「マネージド デバッグ アシスタントによるエラーの診断」を参照してください。  
  
## <a name="accessing-udts-with-a-sqldatareader"></a>SqlDataReader による UDT へのアクセス  
 クライアント コードから `System.Data.SqlClient.SqlDataReader` を使用して、UDT 列を含む結果セットを取得することができます。この結果セットは、オブジェクトのインスタンスとして公開されます。  
  
### <a name="example"></a>例  
 この例では、`Main` メソッドを使用して、新しい `SqlDataReader` オブジェクトを作成する方法を示します。 このコード例では、次の操作が行われます。  
  
1.  Main メソッドでは、新しい `SqlDataReader` オブジェクトが作成され、Points テーブルから値が取得されます。このテーブルには、Point という名前の UDT 列があります。  
  
2.  Point UDT では、整数型として定義されている X 座標と Y 座標が公開されます。  
  
3.  UDT では、`Distance` メソッドと `GetDistanceFromXY` メソッドが定義されています。  
  
4.  このサンプル コードでは、UDT の機能を例示するために主キーと UDT 列の値を取得します。  
  
5.  サンプル コードでは、`Point.Distance` メソッドと `Point.GetDistanceFromXY` メソッドを呼び出します。  
  
6.  結果はコンソール ウィンドウに表示されます。  
  
> [!NOTE]  
>  アプリケーションでは、事前に UDT アセンブリへの参照が設定されている必要があります。  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
  
Module ReadPoints  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Retrieve the value of the UDT  
                Dim pnt As Point = CType(rdr(1), Point)  
  
             ' You can also use GetSqlValue and GetValue  
             ' Dim pnt As Point = CType(rdr.GetSqlValue(1), Point)  
             ' Dim pnt As Point = CType(rdr.GetValue(1), Point)  
  
                ' Print values  
                Console.WriteLine( _  
                 "ID={0} Point={1} X={2} Y={3} DistanceFromXY={4} Distance={5}", _  
                  id, pnt, pnt.X, pnt.Y, pnt.DistanceFromXY(1, 9), pnt.Distance())  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
         & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
  
namespace Microsoft.Samples.SqlServer  
{  
class ReadPoints  
{  
static void Main()  
{  
  string connectionString = GetConnectionString();  
  using (SqlConnection cnn = new SqlConnection(connectionString))  
  {  
    cnn.Open();  
    SqlCommand cmd = new SqlCommand(  
       "SELECT ID, Pnt FROM dbo.Points", cnn);  
    SqlDataReader rdr = cmd.ExecuteReader();  
  
    while (rdr.Read())  
    {  
      // Retrieve the value of the Primary Key column  
      int id = rdr.GetInt32(0);  
  
        // Retrieve the value of the UDT  
        Point pnt = (Point)rdr[1];  
  
        // You can also use GetSqlValue and GetValue  
        // Point pnt = (Point)rdr.GetSqlValue(1);  
        // Point pnt = (Point)rdr.GetValue(1);  
  
        Console.WriteLine(  
        "ID={0} Point={1} X={2} Y={3} DistanceFromXY={4} Distance={5}",   
        id, pnt, pnt.X, pnt.Y, pnt.DistanceFromXY(1, 9), pnt.Distance());  
    }  
  rdr.Close();  
  Console.WriteLine("done");  
  }  
  static private string GetConnectionString()  
  {  
    // To avoid storing the connection string in your code,   
    // you can retrieve it from a configuration file.  
    return "Data Source=(local);Initial Catalog=AdventureWorks;"  
        + "Integrated Security=SSPI";  
  }  
}  
```  
  
## <a name="binding-udts-as-bytes"></a>バイト型としての UDT のバインド  
 場合によっては、UDT 列からそのままデータを取得する必要が生じることもあります。 たとえば、型がローカルに存在しない場合や、UDT のインスタンスを作成したくない場合などです。 使用してバイト配列に生バイトを読み取ることができます、 **GetBytes**のメソッド、`SqlDataReader`します。 このメソッドでは、バイトのストリームを、指定した列オフセットから、指定したバッファー オフセットから始まる配列のバッファーに読み取ることができます。 いずれかを使用することも、 **GetSqlBytes**または**GetSqlBinary**メソッドと 1 つの操作の内容のすべての読み取り。 どちらの場合も、UDT オブジェクトのインスタンスが作成されることはないので、クライアントのアセンブリで UDT への参照を設定する必要はありません。  
  
### <a name="example"></a>例  
 この例は、取得する方法を示します、**ポイント**を使用してバイト配列に未処理のバイトとしてのデータを`SqlDataReader`します。 このコードでは、`System.Text.StringBuilder` を使用して、生のバイト列をコンソール ウィンドウに表示する文字列形式に変換します。  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.Text  
  
Module GetRawBytes  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Retrieve the raw bytes into a byte array  
                Dim buffer(31) As Byte  
                Dim byteCount As Integer = _  
                 CInt(rdr.GetBytes(1, 0, buffer, 0, 31))  
  
                ' Format and print bytes   
                Dim str As New StringBuilder  
                str.AppendFormat("ID={0} Point=", id)  
  
                Dim i As Integer  
                For i = 0 To (byteCount - 1)  
                    str.AppendFormat("{0:x}", buffer(i))  
                Next  
                Console.WriteLine(str.ToString)  
  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Text;  
  
class GetRawBytes  
{  
    static void Main()  
    {  
        string connectionString = GetConnectionString();  
        using (SqlConnection cnn = new SqlConnection(connectionString))  
        {  
            cnn.Open();  
            SqlCommand cmd = new SqlCommand("SELECT ID, Pnt FROM dbo.Points", cnn);  
            SqlDataReader rdr = cmd.ExecuteReader();  
  
            while (rdr.Read())  
            {  
                // Retrieve the value of the Primary Key column  
                int id = rdr.GetInt32(0);  
  
                // Retrieve the raw bytes into a byte array  
                byte[] buffer = new byte[32];  
                long byteCount = rdr.GetBytes(1, 0, buffer, 0, 32);  
  
                // Format and print bytes   
                StringBuilder str = new StringBuilder();  
                str.AppendFormat("ID={0} Point=", id);  
  
                for (int i = 0; i < byteCount; i++)  
                    str.AppendFormat("{0:x}", buffer[i]);  
                Console.WriteLine(str.ToString());  
            }  
            rdr.Close();  
            Console.WriteLine("done");  
        }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
### <a name="example-using-getsqlbytes"></a>GetSqlBytes メソッドの使用例  
 この例では、取得、**ポイント**を使用して、1 つの操作で未処理のバイトとしてのデータ、 **GetSqlBytes**メソッド。 このコードでは、`StringBuilder` を使用して、生のバイト列をコンソール ウィンドウに表示する文字列形式に変換します。  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports System.Text  
  
Module GetRawBytes  
    Sub Main()  
        Dim connectionString As String = GetConnectionString()  
        Using cnn As New SqlConnection(connectionString)  
            cnn.Open()  
            Dim cmd As New SqlCommand( _  
             "SELECT ID, Pnt FROM dbo.Points", cnn)  
            Dim rdr As SqlDataReader  
            rdr = cmd.ExecuteReader  
  
            While rdr.Read()  
                ' Retrieve the value of the Primary Key column  
                Dim id As Int32 = rdr.GetInt32(0)  
  
                ' Use SqlBytes to retrieve raw bytes  
                Dim sb As SqlBytes = rdr.GetSqlBytes(1)  
                Dim byteCount As Long = sb.Length  
  
                ' Format and print bytes   
                Dim str As New StringBuilder  
                str.AppendFormat("ID={0} Point=", id)  
  
                Dim i As Integer  
                For i = 0 To (byteCount - 1)  
                    str.AppendFormat("{0:x}", sb(i))  
                Next  
                Console.WriteLine(str.ToString)  
  
            End While  
            rdr.Close()  
            Console.WriteLine("done")  
        End Using  
    End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data.Sql;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Text;  
  
class GetRawBytes  
{  
    static void Main()  
    {  
         string connectionString = GetConnectionString();  
        using (SqlConnection cnn = new SqlConnection(connectionString))  
        {  
            cnn.Open();  
            SqlCommand cmd = new SqlCommand(  
                "SELECT ID, Pnt FROM dbo.Points", cnn);  
            SqlDataReader rdr = cmd.ExecuteReader();  
  
            while (rdr.Read())  
            {  
                // Retrieve the value of the Primary Key column  
                int id = rdr.GetInt32(0);  
  
                // Use SqlBytes to retrieve raw bytes  
                SqlBytes sb = rdr.GetSqlBytes(1);  
                long byteCount = sb.Length;  
  
                // Format and print bytes   
                StringBuilder str = new StringBuilder();  
                str.AppendFormat("ID={0} Point=", id);  
  
                for (int i = 0; i < byteCount; i++)  
                    str.AppendFormat("{0:x}", sb[i]);  
                Console.WriteLine(str.ToString());  
            }  
            rdr.Close();  
            Console.WriteLine("done");  
        }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
## <a name="working-with-udt-parameters"></a>UDT パラメーターを使用した作業  
 ADO.NET コードでは、UDT は入力パラメーターと出力パラメーターのどちらとしても使用することができます。  
  
## <a name="using-udts-in-query-parameters"></a>クエリ パラメーターでの UDT の使用  
 UDT は、`SqlParameter` オブジェクトの `System.Data.SqlClient.SqlCommand` を設定する際にパラメーター値として使用できます。 `SqlDbType.Udt` オブジェクトの `SqlParameter` 列挙値は、`Add` コレクションに対して `Parameters` メソッドを呼び出す際、パラメーターが UDT であることを示すために使用します。 `UdtTypeName`のプロパティを`SqlCommand`オブジェクトはデータベースを使用して、UDT の完全修飾名を指定するために使用、 *database.schema_name.object_name*構文。 必須ではありませんが、完全修飾名を使用すると、コードを明確にすることができます。  
  
> [!NOTE]  
>  クライアント プロジェクトが、UDT アセンブリのローカル コピーを使用できることが前提です。  
  
### <a name="example"></a>例  
 この例のコードでは、`SqlCommand` オブジェクトと `SqlParameter` オブジェクトを使用して、テーブルの UDT 列にデータを挿入します。 このコードでは、`SqlDbType.Udt` 列挙値を使用してデータ型を指定し、`UdtTypeName` オブジェクトの `SqlParameter` プロパティを使用してデータベースの UDT の完全修飾名を指定します。  
  
```vb  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports system.Data  
Imports System.Data.Sql  
Imports System.Data.SqlClient  
  
Module Module1  
  
  Sub Main()  
    Dim ConnectionString As String = GetConnectionString()  
    Dim cnn As New SqlConnection(ConnectionString)  
    Using cnn  
      Dim cmd As SqlCommand = cnn.CreateCommand()  
      cmd.CommandText = "INSERT INTO dbo.Points (Pnt) VALUES (@Point)"  
      cmd.CommandType = CommandType.Text  
  
      Dim param As New SqlParameter("@Point", SqlDbType.Udt)      param.UdtTypeName = "TestPoint.dbo.Point"      param.Direction = ParameterDirection.Input      param.Value = New Point(5, 6)      cmd.Parameters.Add(param)  
  
      cnn.Open()  
      cmd.ExecuteNonQuery()  
      Console.WriteLine("done")  
    End Using  
  End Sub  
    Private Function GetConnectionString() As String  
        ' To avoid storing the connection string in your code,    
        ' you can retrieve it from a configuration file.  
        Return "Data Source=(local);Initial Catalog=AdventureWorks;" _  
           & "Integrated Security=SSPI;"  
    End Function  
End Module  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlClient;  
  
class Class1  
{  
static void Main()  
{  
  string ConnectionString = GetConnectionString();  
     using (SqlConnection cnn = new SqlConnection(ConnectionString))  
     {  
       SqlCommand cmd = cnn.CreateCommand();  
       cmd.CommandText =   
         "INSERT INTO dbo.Points (Pnt) VALUES (@Point)";  
       cmd.CommandType = CommandType.Text;  
  
       SqlParameter param = new SqlParameter("@Point", SqlDbType.Udt);       param.UdtTypeName = "TestPoint.dbo.Point";       param.Direction = ParameterDirection.Input;       param.Value = new Point(5, 6);       cmd.Parameters.Add(param);  
  
       cnn.Open();  
       cmd.ExecuteNonQuery();  
       Console.WriteLine("done");  
     }  
    static private string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,   
        // you can retrieve it from a configuration file.  
        return "Data Source=(local);Initial Catalog=AdventureWorks;"  
            + "Integrated Security=SSPI";  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [ADO.NET でのユーザー定義型へのアクセス](accessing-user-defined-types-in-ado-net.md)  
  
  
