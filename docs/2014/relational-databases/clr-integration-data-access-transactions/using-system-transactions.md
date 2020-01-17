---
title: System.Transactions の使用 |Microsoft Docs
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
- TransactionScope class
- Dispose method
- System.Transactions namespace
ms.assetid: 79656ce5-ce46-4c5e-9540-cf9869bd774b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e39106ea1c4077d1aee90cedc17c5af07503a136
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919532"
---
# <a name="using-systemtransactions"></a>System.Transactions の使用
  `System.Transactions` 名前空間では、ADO.NET と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR (共通言語ランタイム) 統合に完全に統合される新しいトランザクション フレームワークが提供されます。 `System.Transactions.TransactionScope` クラスは、接続を分散トランザクションに暗黙に参加させることで、コード ブロックをトランザクション対応にします。 `Complete` でマークされたコード ブロックの最後には、`TransactionScope` メソッドを呼び出す必要があります。 プログラムの実行がコード ブロックから離れる際には `Dispose` メソッドが呼び出され、このとき `Complete` メソッドが呼び出されなければ、トランザクションの続行が中止されます。 コードがスコープから離れるような例外がスローされると、このトランザクションは中止されたと見なされます。  
  
 `using` ブロックを使用することで、`Dispose` オブジェクトで `TransactionScope` ブロックの終了時に必ず `using` メソッドを呼び出すようにすることをお勧めします。 `TransactionScope` の既定のタイムアウトは 1 分なので、保留中のトランザクションのコミットまたはロールバックに失敗すると、パフォーマンスが大幅に低下する場合があります。 `using` ステートメントを使用しない場合は、`Try` ブロック内のすべての処理を実行し、`Dispose` ブロックで `Finally` メソッドを明示的に呼び出す必要があります。  
  
 `TransactionScope` 内で例外が発生すると、トランザクションには一貫性がないことを示すマークが付けられ、破棄されます。 `TransactionScope` が破棄されると、トランザクションはロールバックされます。 例外が発生しなければ、参加しているトランザクションがコミットされます。  
  
 `TransactionScope` は、ローカルおよびリモート データ ソース、または外部リソース マネージャーにアクセスするときのみ使用してください。 これは、`TransactionScope` が常にトランザクションを昇格してしまうからです。コンテキスト接続内のみで使用した場合でさえ、そのようになります。  
  
> [!NOTE]  
>  既定では、`TransactionScope` クラスは、`System.Transactions.Transaction.IsolationLevel` が `Serializable` であるトランザクションを作成します。 アプリケーションによっては、分離レベルを低くして、アプリケーション内の競合を回避することを検討する必要があります。  
  
> [!NOTE]  
>  リモート サーバーに対する分散トランザクション内では、大量のデータベース リソースが消費されるため、更新、挿入、および削除だけを実行することをお勧めします。 操作がローカル サーバーで実行される場合は、分散トランザクションは必要なく、ローカル トランザクションで十分です。 SELECT ステートメントは、不必要にデータベース リソースをロックすることがあります。また、選択に多くのトランザクションを要する場合もあります。 データベース以外の作業は、トランザクション処理を行う他のリソース マネージャーを必要とする場合を除き、トランザクションのスコープ外で行う必要があります。 トランザクションのスコープ内で例外が発生するとトランザクションのコミットは回避されますが、`TransactionScope` クラスには、トランザクションのスコープ外でユーザー コードによって行われた変更をロールバックする機能はありません。 トランザクションのロールバック時に操作が必要である場合は、`System.Transactions.IEnlistmentNotification` インターフェイスの独自の実装を作成し、明示的にトランザクションに参加する必要があります。  
  
## <a name="example"></a>例  
 `System.Transactions` を使用するには、System.Transactions.dll ファイルへの参照が必要です。  
  
 次のコードでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 2 つの異なるインスタンスに対して昇格可能なトランザクションを作成する方法を説明します。 これらのインスタンスは、2 つの異なる `System.Data.SqlClient.SqlConnection` オブジェクトで表され、`TransactionScope` ブロックにラップされます。 このコードでは、`TransactionScope` ステートメントを使用して `using` ブロックを作成し、最初の接続を開きます。これにより、トランザクションは `TransactionScope` に自動参加します。 最初、トランザクションは完全な分散トランザクションではなく、軽量トランザクションとして参加します。 このコードでは、条件ロジックが存在することを前提としています (説明を簡単にするために、このロジックは省略しています)。 必要な場合のみ 2 番目の接続を開き、`TransactionScope` に参加させます。 2 番目の接続が開かれると、トランザクションは完全な分散トランザクションに自動的に昇格します。 その後、`TransactionScope.Complete` を呼び出し、トランザクションをコミットします。 その接続の `using` ステートメントが終了すると、2 つの接続が破棄されます。 `TransactionScope.Dispose` の `TransactionScope` メソッドは、その `using` での `TransactionScope` ブロックの終了時に自動的に呼び出されます。 `TransactionScope` ブロックのどこかで例外がスローされた場合は、`Complete` が呼び出されません。また、分散トランザクションは、`TransactionScope` が破棄される際にロールバックされます。  
  
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
  
## <a name="see-also"></a>参照  
 [CLR 統合とトランザクション](../native-client-ole-db-transactions/transactions.md)  
  
  
