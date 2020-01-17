---
title: CLR データベース オブジェクトからのデータ アクセス |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], data access
- routines [CLR integration]
- data access [CLR integration]
- ADO.NET [CLR integration]
- internal data access [CLR integration]
- common language runtime [SQL Server], ADO.NET
- database objects [CLR integration], data access
- managed code [SQL Server], database objects
- .NET Data Access Provider for SQL Server [CLR integration]
- managed code [SQL Server], data access
- SqlClient provider
- in-process data access providers [CLR integration]
ms.assetid: 9a0f4dee-71c1-42e9-a85e-52382807010f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4561c7b8979a919ea144bab6d9b42f722b089e48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874079"
---
# <a name="data-access-from-clr-database-objects"></a>CLR データベース オブジェクトからのデータ アクセス
  共通言語ランタイム (CLR) のルーチンのインスタンスに格納されているデータにアクセスする簡単に[!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)]でこれを実行する、リモート インスタンスに格納されているデータだけでなく。 ルーチンからどのデータにアクセスできるかは、コードが実行されているユーザー コンテキストによって決まります。 .NET Framework Data Provider for を使用して CLR データベース オブジェクトからのデータにアクセス[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]マネージ クライアントと中間層アプリケーションからのデータ。 このため、クライアント アプリケーションや中間層アプリケーションでは、ADO.NET と `SqlClient` の知識を活用できます。  
  
> [!NOTE]  
>  ユーザー定義型メソッドとユーザー定義関数では、既定ではデータ アクセスの実行が許可されていません。 UDT (ユーザー定義型) メソッドやユーザー定義関数からの読み取り専用データ アクセスを可能にするには、`DataAccess` または `SqlMethodAttribute` の `SqlFunctionAttribute` プロパティを `DataAccessKind.Read` に設定する必要があります。 UDT またはユーザー定義関数によるデータ変更操作は許可されません。この操作を実行しようとすると、実行時に例外がスローされます。  
  
 ここでは、CLR データベース オブジェクト内からデータにアクセスする際の機能や動作の具体的な違いについて説明します。 ADO.NET の機能の詳細については、.NET Framework SDK に付属の ADO.NET のドキュメントを参照してください。  
  
 次の表は、このセクションのトピックを一覧表示します。  
  
 [コンテキスト接続](context-connection.md)  
 SQL Server へのコンテキスト接続について説明します。  
  
 [接続の権限借用と資格情報](impersonation-and-credentials-for-connections.md)  
 接続の権限借用および接続の資格情報について説明します。  
  
 [ADO.NET に対する SQL Server インプロセス固有の拡張機能](../../clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
 プロセス内の固有の `SqlPipe`、`SqlContext`、`SqlTriggerContext`、および `SqlDataRecord` の各オブジェクトについて説明します。  
  
 [CLR 統合とトランザクション](../../native-client-ole-db-transactions/transactions.md)  
 System.Transactions 名前空間で提供される新しいトランザクション フレームワークを ADO.NET および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CLR 統合と統合する方法について説明します。  
  
 [CLR データベース オブジェクトからの XML シリアル化](../../../database-engine/dev-guide/xml-serialization-from-clr-database-objects.md)  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内部で CLR データベース オブジェクトの XML シリアル化のシナリオを有効にする方法について説明します。  
  
  
