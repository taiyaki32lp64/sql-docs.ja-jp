---
title: SqlContext オブジェクト |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 746ce8cec228b6fe9a9d36c4e0287ad7c2f3c517
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951674"
---
# <a name="sqlcontext-object"></a>SqlContext オブジェクト
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  プロシージャや関数の呼び出し時、CLR (共通言語ランタイム) ユーザー定義型のメソッドの呼び出し時、または任意の [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 言語で定義されたトリガーの起動時には、サーバーのマネージド コードを呼び出します。 このコードの実行はユーザー接続の一環として要求されるので、サーバーで実行しているコードから呼び出し元のコンテキストにアクセスできる必要があります。 また、特定のデータ アクセス操作には、コードが呼び出し元のコンテキストで実行されている場合にしか有効にならないものもあります。 たとえば、トリガー操作で使用される inserted 擬似テーブルや deleted 擬似テーブルにアクセスするには、コードが呼び出し元のコンテキストで実行されている必要があります。  
  
 呼び出し元のコンテキストが抽象化を**SqlContext**オブジェクト。 詳細については、 **SqlTriggerContext**メソッドとプロパティを参照してください、 **Microsoft.SqlServer.Server.SqlTriggerContext**クラスのリファレンス ドキュメントで、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK。  
  
 **SqlContext**次のコンポーネントへのアクセスを提供します。  
  
-   **SqlPipe**:**SqlPipe**オブジェクトは、クライアントに流れる結果が通過「パイプ」を表します。 詳細については、 **SqlPipe**オブジェクトを参照してください[SqlPipe オブジェクト](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)します。  
  
-   **SqlTriggerContext**:**SqlTriggerContext** CLR トリガー内からオブジェクトが取得のみできます。 このオブジェクトでは、トリガーを起動した操作や、更新された列のマップについての情報を提供します。 詳細については、 **SqlTriggerContext**オブジェクトを参照してください[SqlTriggerContext オブジェクト](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)します。  
  
-   **IsAvailable**:**IsAvailable**プロパティはコンテキスト可用性を確認するために使用します。  
  
-   **WindowsIdentity**:**WindowsIdentity**プロパティを使用して、呼び出し元の Windows id を取得します。  
  
## <a name="determining-context-availability"></a>コンテキスト可用性の判断  
 クエリ、 **SqlContext**クラスを現在実行中のコードがインプロセスで実行されているかどうか。 これを行うには、確認、 **IsAvailable**のプロパティ、 **SqlContext**オブジェクト。 **IsAvailable**プロパティは読み取り専用、および返します**True**内で呼び出し元のコードが実行されている場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]おり、他**SqlContext**メンバーにアクセスできます。 場合、 **IsAvailable**プロパティが返す**False**、他のすべての**SqlContext**メンバーをスロー、 **InvalidOperationException**使用されている場合、. 場合**IsAvailable**返します**False**をされている接続オブジェクトを開く"コンテキスト接続 = true"では、接続文字列が失敗します。  
  
## <a name="retrieving-windows-identity"></a>Windows ID の取得  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内で実行されている CLR コードは、常に、プロセス アカウントのコンテキストで呼び出されます。 代わりに、呼び出し元ユーザーの id を使用して特定の操作を行う必要がある場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を介して偽装トークンを取得する必要が、プロセス id で、 **WindowsIdentity** のプロパティ**SqlContext**オブジェクト。 **WindowsIdentity**プロパティが返す、 **WindowsIdentity**インスタンスを表す、[!INCLUDE[msCoName](../../includes/msconame-md.md)]を使用して、クライアントが認証された場合は null か、呼び出しの Windows id [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]認証します。 マークされたアセンブリだけ**EXTERNAL_ACCESS**または**UNSAFE**アクセス許可がこのプロパティにアクセスできます。  
  
 取得した後、 **WindowsIdentity**オブジェクト、呼び出し元はクライアントのアカウントを借用でき、ユーザーに代わって操作を実行します。  
  
 呼び出し元の id を利用のみ**SqlContext.WindowsIdentity**ストアド プロシージャまたは関数の実行を開始したクライアントが Windows 認証を使用して、サーバーに接続されているかどうか。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証が使用されている場合、このプロパティは NULL になり、コードでは呼び出し元ユーザーの権限を借用することはできません。  
  
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
  
## <a name="see-also"></a>関連項目  
 [SqlPipe オブジェクト](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)   
 [SqlTriggerContext オブジェクト](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqltriggercontext-object.md)   
 [CLR トリガー](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [ADO.NET に対する SQL Server インプロセス固有の拡張機能](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
