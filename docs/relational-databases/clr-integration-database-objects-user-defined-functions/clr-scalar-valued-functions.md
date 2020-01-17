---
title: CLR スカラー値関数 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- SVF
- scalar-valued functions
ms.assetid: 20dcf802-c27d-4722-9cd3-206b1e77bee0
author: rothja
ms.author: jroth
ms.openlocfilehash: ac063fa59d22308cb90206816555eea8474acca6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68009772"
---
# <a name="clr-scalar-valued-functions"></a>CLR スカラー値関数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  スカラー値関数 (SVF) は、文字列値、整数値、ビット値などの単一値を返します。任意の .NET Framework プログラミング言語を使用し、マネージド コードでユーザー定義スカラー値関数を作成できます。 これらの関数からは、[!INCLUDE[tsql](../../includes/tsql-md.md)] コードや他のマネージド コードにアクセスできます。 CLR 統合とマネージ コードの使い分けの利点については、[!INCLUDE[tsql](../../includes/tsql-md.md)]を参照してください[CLR 統合の概要](../../relational-databases/clr-integration/clr-integration-overview.md)します。  
  
## <a name="requirements-for-clr-scalar-valued-functions"></a>CLR スカラー値関数の要件  
 .NET Framework SVF は、.NET Framework アセンブリのクラスのメソッドとして実装されます。 入力パラメーターと SVF から返される型は任意のスカラー データ型でサポートされていることができる[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、除く**varchar**、 **char**、 **rowversion**、 **テキスト**、 **ntext**、**イメージ**、**タイムスタンプ**、**テーブル**、または**カーソル**. SVF では、実装メソッドの戻り値のデータ型が上記のいずれかの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型になるようにする必要があります。 型変換の詳細については、次を参照してください。 [CLR パラメーター データのマッピング](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)します。  
  
 .NET Framework 言語で .NET Framework SVF を実装するときに、 **SqlFunction**関数に関する情報を追加するカスタム属性を指定することができます。 **SqlFunction**属性はかどうか、その関数が、浮動小数点演算と関数にアクセスまたは確定的である場合にデータを変更するかどうかを示します。  
  
 ユーザー定義スカラー値関数は、決定的関数になる場合と非決定的関数になる場合があります。 特定の入力パラメーターのセットを渡して決定的関数を呼び出すと、常に同じ結果が返されます。 一方、特定の入力パラメーターのセットを渡して非決定的関数を呼び出すと、異なる結果が返されることがあります。  
  
> [!NOTE]  
>  入力値とデータベースの状態が同じでも、関数が必ずしも常に同じ出力値を生成しない場合は、その関数を決定的関数としてマークしないでください。 完全に決定的ではない関数を決定的関数としてマークした場合、インデックス付きビューと計算列が破損する可能性があります。 設定して決定的関数としてのマークを付ける、 **IsDeterministic**プロパティを true にします。  
  
### <a name="table-valued-parameters"></a>テーブル値パラメーター  
 テーブル値パラメーター (TVP) とは、プロシージャや関数に渡されるユーザー定義のテーブル型です。TVP を使用すると、複数行のデータを効率的にサーバーに渡すことができます。 TVP の機能はパラメーター配列に似ていますが、より柔軟性が高く、[!INCLUDE[tsql](../../includes/tsql-md.md)] との統合も緊密です。 テーブル値パラメーターを使用するとパフォーマンスが向上する可能性もあります。 また、サーバーへのラウンド トリップを減らすのにも役立ちます。 スカラー パラメーターのリストを使用するなどしてサーバーに複数の要求を送信する代わりに、データを TVP としてサーバーに送信できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のプロセスで実行されているマネージド ストアド プロシージャやマネージド関数にユーザー定義のテーブル型をテーブル値パラメーターとして渡したり、戻り値として受け取ったりすることはできません。 Tvp の詳細については、次を参照してください。[テーブル値パラメーターの&#40;データベース エンジン&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)します。  
  
## <a name="example-of-a-clr-scalar-valued-function"></a>CLR スカラー値関数の例  
 データにアクセスして整数値を返す簡単な SVF を次に示します。  
  
```csharp  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
  
public class T  
{  
    [SqlFunction(DataAccess = DataAccessKind.Read)]  
    public static int ReturnOrderCount()  
    {  
        using (SqlConnection conn   
            = new SqlConnection("context connection=true"))  
        {  
            conn.Open();  
            SqlCommand cmd = new SqlCommand(  
                "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
            return (int)cmd.ExecuteScalar();  
        }  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Public Class T  
    <SqlFunction(DataAccess:=DataAccessKind.Read)> _  
    Public Shared Function ReturnOrderCount() As Integer  
        Using conn As New SqlConnection("context connection=true")  
            conn.Open()  
            Dim cmd As New SqlCommand("SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
            Return CType(cmd.ExecuteScalar(), Integer)  
        End Using  
    End Function  
End Class  
```  
  
 コード参照の最初の行**Microsoft.SqlServer.Server**属性へのアクセスと**System.Data.SqlClient** ADO.NET 名前空間にアクセスします。 (この名前空間を含む**SqlClient**、.NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。  
  
 関数を次に、受信、 **SqlFunction**は、カスタム属性、 **Microsoft.SqlServer.Server**名前空間。 このカスタム属性は、UDF (ユーザー定義関数) がサーバーのデータを読み取るときにインプロセス プロバイダーを使用するかどうかを示します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、UDF によるデータの更新、挿入、または削除を許可していません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、インプロセス プロバイダーを使用しない UDF の実行を最適化できます。 これは、設定によって示されます**DataAccessKind**に**DataAccessKind.None**します。 その次の行で、対象のメソッドは public static (Visual Basic .NET では shared) になっています。  
  
 **SqlContext**クラスは、 **Microsoft.SqlServer.Server**名前空間にアクセスできるよう、 **SqlCommand**への接続を使用してオブジェクト、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]既に設定されているインスタンス。 ここで使用できませんが、現在のトランザクション コンテキストを利用も、 **System.Transactions**アプリケーション プログラミング インターフェイス (API)。  
  
 関数本体でコードの行のほとんどは、型を使用するクライアント アプリケーションを作成した開発者にとって身近になります、 **System.Data.SqlClient**名前空間。  
  
 [C#]  
  
```  
using(SqlConnection conn = new SqlConnection("context connection=true"))   
{  
   conn.Open();  
   SqlCommand cmd = new SqlCommand(  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
   return (int) cmd.ExecuteScalar();  
}    
```  
  
 [Visual Basic]  
  
```  
Using conn As New SqlConnection("context connection=true")  
   conn.Open()  
   Dim cmd As New SqlCommand( _  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
   Return CType(cmd.ExecuteScalar(), Integer)  
End Using  
```  
  
 初期化することにより、適切なコマンド テキストが指定されて、 **SqlCommand**オブジェクト。 前の例では、テーブル内の行の数をカウントする**SalesOrderHeader**します。 次に、 **ExecuteScalar**のメソッド、 **cmd**オブジェクトが呼び出されます。 型の値が返されます**int**クエリに基づいています。 最後に、注文数が呼び出し側に返されます。  
  
 このコードを FirstUdf.cs というファイルに保存すると、次のようにアセンブリとしてコンパイルできます。  
  
 [C#]  
  
```  
csc.exe /t:library /out:FirstUdf.dll FirstUdf.cs   
```  
  
 [Visual Basic]  
  
```  
vbc.exe /t:library /out:FirstUdf.dll FirstUdf.vb  
```  
  
> [!NOTE]  
>  `/t:library`は、実行可能ファイルではなくライブラリを生成することを示しています。 実行可能ファイルは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には登録できません。  
  
> [!NOTE]  
>  Visual C のデータベース オブジェクトをコンパイルした **/clr: 純粋な**で実行するためサポートされていません[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 このようなデータベース オブジェクトには、スカラー値関数などがあります。  
  
 アセンブリと UDF を登録する [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリと呼び出しの例を次に示します。  
  
```  
CREATE ASSEMBLY FirstUdf FROM 'FirstUdf.dll';  
GO  
  
CREATE FUNCTION CountSalesOrderHeader() RETURNS INT   
AS EXTERNAL NAME FirstUdf.T.ReturnOrderCount;   
GO  
  
SELECT dbo.CountSalesOrderHeader();  
GO  
  
```  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] で公開する関数名は、対象の public static メソッドの名前と一致している必要はありません。  
  
## <a name="see-also"></a>参照  
 [CLR パラメーター データのマッピング](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)   
 [CLR 統合のカスタム属性の概要](https://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)   
 [ユーザー定義関数](../../relational-databases/user-defined-functions/user-defined-functions.md)   
 [CLR データベース オブジェクトからのデータ アクセス](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
