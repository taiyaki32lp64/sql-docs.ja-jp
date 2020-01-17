---
title: CLR 統合のカスタム属性の概要 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- custom attributes [CLR integration]
- attributes [CLR integration]
- common language runtime [SQL Server], attributes
- database objects [CLR integration], custom attributes
- building database objects [CLR integration], custom attributes
ms.assetid: ecf5c097-0972-48e2-a9c0-b695b7dd2820
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8df7881dd5f38935628cb6653d57763a8846e60f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62781107"
---
# <a name="overview-of-clr-integration-custom-attributes"></a>CLR 統合のカスタム属性の概要
  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] の CLR (共通言語ランタイム) では、属性という説明用のキーワードを使用できます。 これらの属性は、メソッドやクラスなどの多くの要素に関する追加情報を提供します。 属性はオブジェクトのメタデータと共にアセンブリに保存され、記述したコードを他の開発ツールに説明したり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部での実行時の動作に影響することを説明するために使用できます。  
  
 CLR ルーチンを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に登録すると、そのルーチンに関する一連のプロパティが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により抽出されます。 これらのプロパティによって、ルーチンにインデックスを作成できるかどうかなど、そのルーチンの機能が決まります。 たとえば、`DataAccess` プロパティを `DataAccessKind.Read` に設定すると、CLR 関数内から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザー テーブルのデータにアクセスできるようになります。 次の例を単純なケースを示しています、`DataAccess`ユーザー テーブルからのデータ アクセスを容易に設定されて**table1**します。  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
  
public partial class UserDefinedFunctions  
{  
    [SqlFunction(DataAccess = DataAccessKind.Read)]  
    public static string func1()  
    {  
        // Open a connection and create a command  
        SqlConnection conn = new SqlConnection("context connection = true");  
        conn.Open();  
        SqlCommand cmd = conn.CreateCommand();  
        cmd.CommandText = "SELECT str_val FROM table1 WHERE int_val = 10";  
        // where table1 is a user table  
        // Execute this command   
        SqlDataReader rd = cmd.ExecuteReader();  
        // Set string ret_val to str_val returned from the query  
        string ret_val = rd.GetValue(0).ToString();  
        rd.Close();  
        return ret_val;  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Public partial Class UserDefinedFunctions  
    <SqlFunction(DataAccess = DataAccessKind.Read)> _   
    Public Shared Function func1() As String  
        ' Open a connection and create a command  
        Dim conn As SqlConnection = New SqlConnection("context connection = true")   
        conn.Open()  
        Dim cmd As SqlCommand =  conn.CreateCommand()   
        cmd.CommandText = "SELECT str_val FROM table1 WHERE int_val = 10"  
        ' where table1 is a user table  
        ' Execute this command   
        Dim rd As SqlDataReader =  cmd.ExecuteReader()   
        ' Set string ret_val to str_val returned from the query  
        Dim ret_val As String =  rd.GetValue(0).ToString()   
        rd.Close()  
        Return ret_val  
    End Function  
End Class  
```  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ルーチンの場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、ルーチン定義から直接ルーチンのプロパティが抽出されます。 CLR ルーチンの場合は、これらのプロパティを抽出するときに、サーバーでルーチン本体が分析されません。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 言語で実装されているクラスとクラスのメンバーには、カスタム属性を使用できます。  
  
 CLR ルーチン、ユーザー定義型、およびユーザー定義集計に必要なカスタム属性は、`Microsoft.SqlServer.Server` 名前空間で定義します。  
  
## <a name="see-also"></a>参照  
 [CLR ルーチンのカスタム属性](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)  
  
  
