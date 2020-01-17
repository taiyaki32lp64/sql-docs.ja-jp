---
title: System.Transactions の使用 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TransactionScope class
- Dispose method
- System.Transactions namespace
ms.assetid: 79656ce5-ce46-4c5e-9540-cf9869bd774b
author: rothja
ms.author: jroth
ms.openlocfilehash: a9b99842a92649a42e9a0a42e6732368dc5e06ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081350"
---
# <a name="using-systemtransactions"></a>System.Transactions の使用
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **System.Transactions**名前空間は、ADO.NET に完全に統合される新しいトランザクション フレームワークを提供し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]共通言語ランタイム (CLR) 統合します。 **System.Transactions.TransactionScope**クラスは、分散トランザクション内の接続を暗黙的に参加して、コード ブロックをトランザクション。 呼び出す必要があります、**完了**によってマークされたメソッドのコード ブロックの末尾に、 **TransactionScope**します。 **Dispose**プログラムの実行が中止された場合、トランザクションの原因と、コード ブロックを離れるときに、メソッドが呼び出される、**完了**メソッドは呼び出されません。 コードがスコープから離れるような例外がスローされると、このトランザクションは中止されたと見なされます。  
  
 取り入れることをお勧めします、**を使用して**ことを確認するブロック、 **Dispose**でメソッドが呼び出される、 **TransactionScope**オブジェクトと、 **を使用して**。ブロックを終了します。 コミットまたは保留中のトランザクションのロールバックに失敗したことができます重大なパフォーマンスが低下するための既定のタイムアウト、 **TransactionScope**は 1 分です。 使用しない場合、**を使用して**ステートメントでは、すべての処理を実行する必要があります、**お試しください**をブロックし、明示的に呼び出す、 **Dispose**メソッドで、**最後に**ブロックします。  
  
 内で例外が発生した場合、 **TransactionScope**トランザクションが不整合としてマークされているし、破棄されます。 戻るときに、 **TransactionScope**が破棄されました。 例外が発生しなければ、参加しているトランザクションがコミットされます。  
  
 **TransactionScope**ローカルおよびリモート データ ソースまたは外部リソース マネージャーにアクセスしている場合にのみ使用する必要があります。 これは、ため**TransactionScope**によって常に昇格するには、トランザクション コンテキスト接続内でのみ使用されている場合でもです。  
  
> [!NOTE]  
>  **TransactionScope**でトランザクションを作成するクラス、 **System.Transactions.Transaction.IsolationLevel**の**Serializable**既定。 アプリケーションによっては、分離レベルを低くして、アプリケーション内の競合を回避することを検討する必要があります。  
  
> [!NOTE]  
>  リモート サーバーに対する分散トランザクション内では、大量のデータベース リソースが消費されるため、更新、挿入、および削除だけを実行することをお勧めします。 操作がローカル サーバーで実行される場合は、分散トランザクションは必要なく、ローカル トランザクションで十分です。 SELECT ステートメントは、不必要にデータベース リソースをロックすることがあります。また、選択に多くのトランザクションを要する場合もあります。 データベース以外の作業は、トランザクション処理を行う他のリソース マネージャーを必要とする場合を除き、トランザクションのスコープ外で行う必要があります。 トランザクションのスコープ内での例外には、トランザクションのコミットが防止されますが、 **TransactionScope**クラスには用意されていません、トランザクションのスコープの外部で行った変更をロールバックして、コードの自体。 独自の実装を記述する必要があります、トランザクションがロールバック時に、何らかのアクションを実行する必要がある場合、 **System.Transactions.IEnlistmentNotification**インターフェイス、およびトランザクションに明示的に参加します。  
  
## <a name="example"></a>例  
 使用する**System.Transactions**、System.Transactions.dll ファイルへの参照があります。  
  
 次のコードでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 2 つの異なるインスタンスに対して昇格可能なトランザクションを作成する方法を説明します。 これらのインスタンスが 2 つの異なるによって表される**System.Data.SqlClient.SqlConnection**オブジェクトでラップされている、 **TransactionScope**ブロックします。 コードを作成、 **TransactionScope**ブロックと一緒に、**を使用して**ステートメントでは、自動的に参加させることで、最初の接続を開くと、 **TransactionScope**。 最初、トランザクションは完全な分散トランザクションではなく、軽量トランザクションとして参加します。 このコードでは、条件ロジックが存在することを前提としています (説明を簡単にするために、このロジックは省略しています)。 必要な場合は、2 番目の接続を開きますに参加させます、 **TransactionScope**します。 2 番目の接続が開かれると、トランザクションは完全な分散トランザクションに自動的に昇格します。 コードが呼び出され、 **TransactionScope.Complete**、トランザクションをコミットします。 コードを終了するときに 2 つの接続の破棄、**を使用して**接続のステートメント。 **TransactionScope.Dispose**のメソッド、 **TransactionScope**の終了時に自動的に呼び出されますが、**を使用して**のブロック、 **TransactionScope**します。 任意の時点で例外がスローされたかどうか、 **TransactionScope**ブロック、**完了**が呼び出されませんの分散トランザクションはロールバックとき、 **TransactionScope**が破棄されています。  
  
 Visual Basic  
  
```  
Using transScope As New TransactionScope()  
    Using connection1 As New SqlConnection(connectString1)  
        ' Opening connection1 automatically enlists it in the   
        ' TransactionScope as a lightweight transaction.  
        connection1.Open()  
  
        ' Do work in the first connection.  
  
        ' Assumes conditional logic in place where the second  
        ' connection will only be opened as needed.  
        Using connection2 As New SqlConnection(connectString2)  
            ' Open the second connection, which enlists the   
            ' second connection and promotes the transaction to  
            ' a full distributed transaction.  
            connection2.Open()  
  
            ' Do work in the second connection.  
  
        End Using  
    End Using  
  
    ' Commit the transaction.  
    transScope.Complete()  
End Using  
```  
  
 C#  
  
```  
using (TransactionScope transScope = new TransactionScope())  
{  
    using (SqlConnection connection1 = new   
       SqlConnection(connectString1))  
    {  
        // Opening connection1 automatically enlists it in the   
        // TransactionScope as a lightweight transaction.  
        connection1.Open();  
  
        // Do work in the first connection.  
  
        // Assumes conditional logic in place where the second  
        // connection will only be opened as needed.  
        using (SqlConnection connection2 = new   
            SqlConnection(connectString2))  
        {  
            // Open the second connection, which enlists the   
            // second connection and promotes the transaction to  
            // a full distributed transaction.   
            connection2.Open();  
  
            // Do work in the second connection.  
        }  
    }  
    //  The Complete method commits the transaction.  
    transScope.Complete();  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [CLR 統合とトランザクション](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
