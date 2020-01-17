---
title: 行セット |Microsoft Docs
description: OLE DB Driver for SQL Server の行セット
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], about rowsets
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets
- OLE DB rowsets, about rowsets
- rowsets [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 23d07cd93ada1d1eeae36b4e4ed104906feef88d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015371"
---
# <a name="rowsets"></a>行セット
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  行セットとは、データの列を含む行の集まりです。 行セットは、すべての OLE DB データ プロバイダーが表形式で結果セット データを公開できるようにするための重要な機能を持つオブジェクトです。  
  
 コンシューマーでは **IDBCreateSession::CreateSession** メソッドを使用してセッションを作成した後、そのセッションで **IOpenRowset** インターフェイスまたは **IDBCreateCommand** インターフェイスのいずれかを使用して行セットを作成できます。 SQL Server 用の OLE DB ドライバーは、これらのインターフェイスの両方をサポートしています。 ここでは、これら両方のメソッドについて説明します。  
  
-   **IOpenRowset::OpenRowset** メソッドを呼び出して行セットを作成します。  
  
     この操作は、1 つのテーブル全体について行セットを作成することと同じです。 このメソッドは、1 つのベース テーブルのすべての行を含む行セットを開き、その行セットを返します。 **OpenRowset** の引数の 1 つは、行セットの作成元となるテーブルを識別するテーブル ID です。  
  
-   **IDBCreateCommand::CreateCommand** メソッドを呼び出して、コマンド オブジェクトを作成します。  
  
     コマンド オブジェクトでは、プロバイダーがサポートするコマンドが実行されます。 OLE DB Driver for SQL Server では、SELECT ステートメントなどの任意の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントやストアド プロシージャへの呼び出しをコンシューマーで指定できます。 コマンド オブジェクトを使用して行セットを作成する手順は次のとおりです。  
  
    1.  コンシューマーは、セッションの **IDBCreateCommand::CreateCommand** メソッドを呼び出してコマンド オブジェクトを取得し、そのコマンド オブジェクトの **ICommandText** インターフェイスを要求します。 この **ICommandText** インターフェイスで、実際のコマンド テキストが設定および取得されます。 コンシューマーは、**ICommandText::SetCommandText** メソッドを呼び出して、テキスト コマンドにコマンドを設定します。  
  
    2.  ユーザーがコマンドの **ICommand::Execute** メソッドを呼び出します。 コマンドの実行時に構築される行セット オブジェクトには、コマンドから返される結果セットが含まれます。  
  
 コンシューマーは、**ICommandProperties** インターフェイスを使用して、**ICommand::Execute** インターフェイスで実行されるコマンドから返される行セットのプロパティを取得または設定できます。 最も一般的に要求されるプロパティは、行セットでサポートする必要のあるインターフェイスです。 コンシューマーはインターフェイスだけでなく、行セットやインターフェイスの動作を変更するプロパティも要求できます。  
  
 コンシューマーは **IRowset::Release** メソッドを使用して行セットを解放します。 行セットを解放すると、コンシューマーがその行セットに保持しているすべての行ハンドルも解放されます。 ただし、行セットを解放してもアクセサーは解放されません。 **IAccessor** インターフェイスがある場合は、それを解放する必要があります。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [IOpenRowset を使用した行セットの作成](../../oledb/ole-db-rowsets/creating-a-rowset-with-iopenrowset.md)  
  
-   [ICommand::Execute を使用した行セットの作成](../../oledb/ole-db-rowsets/creating-rowsets-with-icommand-execute.md)  
  
-   [行セットのプロパティと動作](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
-   [行セットと SQL Server カーソル](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)  
  
-   [行のフェッチ](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
-   [IRow による 1 行のフェッチ](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
-   [ブックマーク](../../oledb/ole-db-rowsets/bookmarks.md)  
  
-   [行セット内のデータの更新](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server のプログラミング](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
