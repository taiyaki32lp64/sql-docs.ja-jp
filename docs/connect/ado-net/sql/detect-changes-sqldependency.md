---
title: SqlDependency を使用した変更の検出
description: クエリの結果が最初に受信したものと異なる場合を検出する方法を示します。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: e6a58316-f005-4477-92e1-45cc2eb8c5b4
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 2d2c4c48a9085fa83d6104233be5f2e1c6b11318
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452247"
---
# <a name="detecting-changes-with-sqldependency"></a>SqlDependency を使用した変更の検出

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

<xref:Microsoft.Data.SqlClient.SqlDependency> オブジェクトは <xref:Microsoft.Data.SqlClient.SqlCommand> に関連付けることができ、クエリの結果が最初に取得したものと異なる場合を検出するために使用されます。 また、`OnChange` イベントにデリゲートを割り当てることもできます。これは、関連付けられたコマンドの結果が変更されたときに発生します。 コマンドを実行する前に、<xref:Microsoft.Data.SqlClient.SqlDependency> をコマンドに関連付ける必要があります。 <xref:Microsoft.Data.SqlClient.SqlDependency> の `HasChanges` プロパティを使用して、データが最初に取得されてからクエリの結果が変更されたかどうかを判断することもできます。

## <a name="security-considerations"></a>セキュリティに関する考慮事項

依存関係インフラストラクチャは、特定のコマンドの基になるデータが変更されたことを示す通知を受信するために <xref:Microsoft.Data.SqlClient.SqlDependency.Start%2A> が呼び出されたときに開かれる <xref:Microsoft.Data.SqlClient.SqlConnection> に依存します。 クライアントが `SqlDependency.Start` への呼び出しを開始する機能は、<xref:Microsoft.Data.SqlClient.SqlClientPermission> およびコードアクセスセキュリティ属性を使用して制御されます。 詳細については、「[クエリ通知の有効化](enable-query-notifications.md)」を参照してください。

### <a name="example"></a>例

次の手順では、依存関係を宣言し、コマンドを実行し、結果セットが変更されたときに通知を受け取る方法について説明します。

1. サーバーへの `SqlDependency` 接続を開始します。

2. サーバーに接続して Transact-sql ステートメントを定義する <xref:Microsoft.Data.SqlClient.SqlConnection> および <xref:Microsoft.Data.SqlClient.SqlCommand> オブジェクトを作成します。

3. 新しい `SqlDependency` オブジェクトを作成するか、既存のオブジェクトを使用して、`SqlCommand` オブジェクトにバインドします。 内部的には、これによって <xref:Microsoft.Data.Sql.SqlNotificationRequest> オブジェクトが作成され、必要に応じて command オブジェクトにバインドされます。 この通知要求には、この `SqlDependency` オブジェクトを一意に識別する内部識別子が含まれています。 また、クライアントリスナーがまだアクティブになっていない場合は開始します。

4. イベントハンドラーを、`SqlDependency` オブジェクトの `OnChange` イベントにサブスクライブします。

5. `SqlCommand` オブジェクトの `Execute` メソッドのいずれかを使用して、コマンドを実行します。 コマンドは通知オブジェクトにバインドされているため、サーバーは通知を生成する必要があることを認識し、キュー情報は依存関係キューを指します。

6. サーバーへの `SqlDependency` 接続を停止します。

その後、基になるデータがユーザーによって変更された場合、Microsoft SQL Server はその変更に対して保留中の通知があることを検出し、によって作成された基になる `SqlConnection` を通じて、処理され、クライアントに転送される通知を送信します。`SqlDependency.Start` を呼び出しています。 クライアントリスナーは、無効化メッセージを受信します。 次に、クライアントリスナーは、関連付けられている `SqlDependency` オブジェクトを特定し、`OnChange` イベントを発生させます。

次のコードフラグメントは、サンプルアプリケーションの作成に使用するデザインパターンを示しています。

```csharp
void Initialization()
{
    // Create a dependency connection.
    SqlDependency.Start(connectionString, queueName);
}

void SomeMethod()
{
    // Assume connection is an open SqlConnection.

    // Create a new SqlCommand object.
    using (SqlCommand command=new SqlCommand(
        "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers",
        connection))
    {

        // Create a dependency and associate it with the SqlCommand.
        SqlDependency dependency=new SqlDependency(command);
        // Maintain the reference in a class member.

        // Subscribe to the SqlDependency event.
        dependency.OnChange+=new
           OnChangeEventHandler(OnDependencyChange);

        // Execute the command.
        using (SqlDataReader reader = command.ExecuteReader())
        {
            // Process the DataReader.
        }
    }
}

// Handler method
void OnDependencyChange(object sender,
   SqlNotificationEventArgs e )
{
  // Handle the event (for example, invalidate this cache entry).
}

void Termination()
{
    // Release the dependency.
    SqlDependency.Stop(connectionString, queueName);
}
```

## <a name="next-steps"></a>次の手順
- [SQL Server でのクエリ通知](query-notifications-sql-server.md)
