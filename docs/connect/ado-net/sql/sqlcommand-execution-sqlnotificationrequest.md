---
title: SqlCommand の実行と SqlNotificationRequest
description: SqlCommand オブジェクトを構成してクエリ通知を操作する方法を示します。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 1776f48f-9bea-41f6-83a4-c990c7a2c991
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 892f11e2d81e3a0733a1f0747c0b72c72ebc79fc
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451939"
---
# <a name="sqlcommand-execution-with-a-sqlnotificationrequest"></a>SqlCommand の実行と SqlNotificationRequest

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

<xref:Microsoft.Data.SqlClient.SqlCommand> は、データがサーバーからフェッチされた後にデータが変更された場合に通知を生成するように構成できます。また、クエリを再度実行した場合は、結果セットが異なることがあります。 これは、サーバー上でカスタム通知キューを使用する場合や、ライブオブジェクトを保持しない場合に便利です。

## <a name="creating-the-notification-request"></a>通知要求を作成しています

<xref:Microsoft.Data.Sql.SqlNotificationRequest> オブジェクトを使用して、`SqlCommand` オブジェクトにバインドすることによって通知要求を作成できます。 要求が作成されると、`SqlNotificationRequest` オブジェクトは不要になります。 キューに対して任意の通知を照会し、適切に応答することができます。 通知は、アプリケーションがシャットダウンされ、その後再起動された場合でも発生する可能性があります。

コマンドに通知を関連付けて実行した場合、元の結果セットに何らかの変更が生じると、通知要求で構成した SQL Server キューにメッセージが送信されます。

SQL Server のキューをポーリングしメッセージを解釈する方法は、アプリケーションごとに固有なものになります。 アプリケーションは、メッセージの内容に基づいてキューのポーリングと応答を行います。

> [!NOTE]
> <xref:Microsoft.Data.SqlClient.SqlDependency> で SQL Server 通知要求を使用する場合は、既定のサービス名を使用するのではなく、独自のキュー名を作成します。

<xref:Microsoft.Data.Sql.SqlNotificationRequest> 用の新しいクライアント側セキュリティ要素はありません。 これは主にサーバー機能であり、ユーザーが通知を要求するために必要な特別な特権をサーバーが作成しています。

### <a name="example"></a>例

次のコードフラグメントは、<xref:Microsoft.Data.Sql.SqlNotificationRequest> を作成し、<xref:Microsoft.Data.SqlClient.SqlCommand> に関連付ける方法を示しています。

```csharp
// Assume connection is an open SqlConnection.
// Create a new SqlCommand object.
SqlCommand command=new SqlCommand(
 "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", connection);

// Create a SqlNotificationRequest object.
SqlNotificationRequest notificationRequest=new SqlNotificationRequest();
notificationRequest.id="NotificationID";
notificationRequest.Service="mySSBQueue";

// Associate the notification request with the command.
command.Notification=notificationRequest;
// Execute the command.
command.ExecuteReader();
// Process the DataReader.
// You can use Transact-SQL syntax to periodically poll the
// SQL Server queue to see if you have a new message.
```

## <a name="next-steps"></a>次の手順
- [SQL Server でのクエリ通知](query-notifications-sql-server.md)
