---
title: 非同期操作
description: .NET Framework で使用されている非同期モデルに基づいて設計された API を使用し、非同期データベース操作を実行する方法について説明します。
ms.date: 09/30/2019
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 79cde936328476408fabb3df7a6bff8d983ace1c
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452322"
---
# <a name="asynchronous-operations"></a>非同期操作

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

コマンドの実行など、一部のデータベース操作は、完了までにかなりの時間がかかる場合があります。 このような場合、シングルスレッドアプリケーションは、他の操作をブロックし、コマンドが終了するまで待機してから、独自の操作を続行する必要があります。 これに対して、実行時間の長い操作をバックグラウンド スレッドに割り当てることができると、フォアグラウンド スレッドが途中でブロックされることがなくなります。 たとえば、Windows アプリケーションでは、実行時間の長い操作をバックグラウンドスレッドに委任すると、操作の実行中にユーザーインターフェイススレッドの応答性を維持できます。  
  
.NET には、開発者がバックグラウンドスレッドを利用し、ユーザーインターフェイスや優先順位の高いスレッドを解放して <xref:Microsoft.Data.SqlClient.SqlCommand> クラスの他の操作を実行するために使用できる、いくつかの標準的な非同期デザインパターンが用意されています。 具体的には、<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>、<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A>、および <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> メソッドを <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>、<xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A>、および <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A> メソッドと組み合わせて使用することにより、非同期のサポートが提供されます。  
  
> [!NOTE]
>  非同期プログラミングは、.NET の中核となる機能です。 開発者が使用できるさまざまな非同期手法の詳細については、「[同期メソッドの非同期呼び出し](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)」を参照してください。  
  
ADO.NET 機能で非同期手法を使用しても特別な考慮事項はありませんが、マルチスレッドアプリケーションを作成する利点と落とし穴に注意することが重要です。 このセクションの後の例では、マルチスレッド機能を組み込んだアプリケーションを構築する際に考慮する必要がある重要な問題について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
[コールバックを使用する Windows アプリケーション](windows-applications-callbacks.md)  
非同期コマンドを安全に実行し、フォームとその内容との対話を別のスレッドから正しく処理する方法を示す例を示します。  
  
[待機ハンドルを使用する ASP.NET アプリケーション](aspnet-apps-use-wait-handles.md)  
ASP.NET ページから複数の同時実行コマンドを実行する方法を示す例を示します。待機ハンドルを使用して、すべてのコマンドの完了時に操作を管理します。  
  
[コンソール アプリケーションでのポーリング](poll-console-applications.md)  
ポーリングを使用して、コンソールアプリケーションからの非同期コマンドの実行が完了するまで待機する例を示します。 この手法は、クラスライブラリまたはユーザーインターフェイスを持たない他のアプリケーションでも有効です。  
  
## <a name="next-steps"></a>次の手順
- [SQL Server と ADO.NET](index.md)
- [同期メソッドの非同期呼び出し](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)
