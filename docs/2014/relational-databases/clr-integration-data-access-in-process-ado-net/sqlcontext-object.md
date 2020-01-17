---
title: SqlContext オブジェクト |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- Windows identity [CLR integration]
- SqlContext object
- context [CLR integration]
ms.assetid: 67437853-8a55-44d9-9337-90689ebba730
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 223111874ca34ba4df4968c550e6cc47edf2b390
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62920044"
---
# <a name="sqlcontext-object"></a>SqlContext オブジェクト
  プロシージャや関数の呼び出し時、CLR (共通言語ランタイム) ユーザー定義型のメソッドの呼び出し時、または任意の [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 言語で定義されたトリガーの起動時には、サーバーのマネージド コードを呼び出します。 このコードの実行はユーザー接続の一環として要求されるので、サーバーで実行しているコードから呼び出し元のコンテキストにアクセスできる必要があります。 また、特定のデータ アクセス操作には、コードが呼び出し元のコンテキストで実行されている場合にしか有効にならないものもあります。 たとえば、トリガー操作で使用される inserted 擬似テーブルや deleted 擬似テーブルにアクセスするには、コードが呼び出し元のコンテキストで実行されている必要があります。  
  
 呼び出し側のコンテキストは、`SqlContext` オブジェクト内で抽象化されています。 `SqlTriggerContext` メソッドおよびプロパティの詳細については、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK の `Microsoft.SqlServer.Server.SqlTriggerContext` クラスのリファレンス ドキュメントを参照してください。  
  
 `SqlContext` は、次のコンポーネントへのアクセスを提供します。  
  
-   `SqlPipe`:`SqlPipe`オブジェクトは、クライアントに流れる結果が通過「パイプ」を表します。 詳細については、`SqlPipe`オブジェクトを参照してください[SqlPipe オブジェクト](sqlpipe-object.md)します。  
  
-   `SqlTriggerContext`:`SqlTriggerContext` CLR トリガー内からオブジェクトが取得のみできます。 このオブジェクトでは、トリガーを起動した操作や、更新された列のマップについての情報を提供します。 詳細については、`SqlTriggerContext`オブジェクトを参照してください[SqlTriggerContext オブジェクト](sqltriggercontext-object.md)します。  
  
-   `IsAvailable`:`IsAvailable`プロパティはコンテキスト可用性を確認するために使用します。  
  
-   `WindowsIdentity`:`WindowsIdentity`プロパティを使用して、呼び出し元の Windows id を取得します。  
  
## <a name="determining-context-availability"></a>コンテキスト可用性の判断  
 `SqlContext` クラスをクエリすると、現在実行しているコードがインプロセスで実行されているかどうかを判定できます。 これを行うには、`IsAvailable` オブジェクトの `SqlContext` プロパティを確認します。 `IsAvailable` プロパティは読み取り専用で、呼び出し元のコードが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内で実行されており、他の `True` メンバーにアクセスできる場合は、`SqlContext` を返します。 `IsAvailable` プロパティから `False` が返された場合、他のすべての `SqlContext` メンバーから `InvalidOperationException` がスローされます (ただし、この例外が使用されている場合に限ります)。 `IsAvailable` プロパティから `False` が返された場合、接続文字列で "context connection=true" が指定されている接続オブジェクトを開く操作は失敗します。  
  
## <a name="retrieving-windows-identity"></a>Windows ID の取得  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内で実行されている CLR コードは、常に、プロセス アカウントのコンテキストで呼び出されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス ID ではなく、呼び出し元ユーザーの ID を使用して特定の操作を行う必要がある場合は、`WindowsIdentity` オブジェクトの `SqlContext` メソッドにより権限借用トークンを取得する必要があります。 `WindowsIdentity` プロパティは、呼び出し元ユーザーの [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ID を表す `WindowsIdentity` インスタンスを返します。クライアントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用して認証されている場合は、NULL を返します。 `EXTERNAL_ACCESS` 権限または `UNSAFE` 権限のあるアセンブリのみが、このプロパティにアクセスできます。  
  
 `WindowsIdentity` オブジェクトの取得後、呼び出し元は、クライアント アカウントの権限を借用して、操作を実行できます。  
  
 ストアド プロシージャまたは関数の実行を開始したユーザーが Windows 認証を使用してサーバーに接続している場合、`SqlContext.WindowsIdentity` が呼び出し元ユーザーの ID を取得する唯一の手段となります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証が使用されている場合、このプロパティは NULL になり、コードでは呼び出し元ユーザーの権限を借用することはできません。  
  
### <a name="example"></a>例  
 次の例では、呼び出し元であるクライアントの Windows ID を取得し、クライアントの権限を借用する方法を示します。  
  
 C#  
  
```  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void WindowsIDTestProc()  
{  
    WindowsIdentity clientId = null;  
    WindowsImpersonationContext impersonatedUser = null;  
  
    // Get the client ID.  
    clientId = SqlContext.WindowsIdentity;  
  
    // This outer try block is used to thwart exception filter   
    // attacks which would prevent the inner finally   
    // block from executing and resetting the impersonation.  
    try  
    {  
        try  
        {  
            impersonatedUser = clientId.Impersonate();  
            if (impersonatedUser != null)  
            {  
                // Perform some action using impersonation.  
            }  
        }  
        finally  
        {  
            // Undo impersonation.  
            if (impersonatedUser != null)  
                impersonatedUser.Undo();  
        }  
    }  
    catch  
    {  
        throw;  
    }  
}  
```  
  
 Visual Basic  
  
```  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  WindowsIDTestProcVB ()  
    Dim clientId As WindowsIdentity  
    Dim impersonatedUser As WindowsImpersonationContext  
  
    ' Get the client ID.  
    clientId = SqlContext.WindowsIdentity  
  
    ' This outer try block is used to thwart exception filter   
    ' attacks which would prevent the inner finally   
    ' block from executing and resetting the impersonation.  
  
    Try  
        Try  
  
            impersonatedUser = clientId.Impersonate()  
  
            If impersonatedUser IsNot Nothing Then  
                ' Perform some action using impersonation.  
            End If  
  
        Finally  
            ' Undo impersonation.  
            If impersonatedUser IsNot Nothing Then  
                impersonatedUser.Undo()  
            End If  
        End Try  
  
    Catch e As Exception  
  
        Throw e  
  
    End Try  
End Sub  
```  
  
## <a name="see-also"></a>参照  
 [SqlPipe オブジェクト](sqlpipe-object.md)   
 [SqlTriggerContext オブジェクト](sqltriggercontext-object.md)   
 [CLR トリガー](../../database-engine/dev-guide/clr-triggers.md)   
 [ADO.NET に対する SQL Server インプロセス固有の拡張機能](sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
