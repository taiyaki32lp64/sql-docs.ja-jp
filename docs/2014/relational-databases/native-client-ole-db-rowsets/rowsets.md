---
title: 行セット |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], about rowsets
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets
- OLE DB rowsets, about rowsets
- rowsets [OLE DB]
ms.assetid: 5e7b3cbe-3670-4e18-8172-2226e0b6b142
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c78f634f78cdcd970c1d731071a291930cf00ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206650"
---
# <a name="rowsets"></a>行セット
  行セットとは、データの列を含む行の集まりです。 行セットは、すべての OLE DB データ プロバイダーが表形式で結果セット データを公開できるようにするための重要な機能を持つオブジェクトです。  
  
 コンシューマーでは **IDBCreateSession::CreateSession** メソッドを使用してセッションを作成した後、そのセッションで **IOpenRowset** インターフェイスまたは **IDBCreateCommand** インターフェイスのいずれかを使用して行セットを作成できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、これらのインターフェイスの両方がサポートされます。 ここでは、これら両方のメソッドについて説明します。  
  
-   **IOpenRowset::OpenRowset** メソッドを呼び出して行セットを作成します。  
  
     この操作は、1 つのテーブル全体について行セットを作成することと同じです。 このメソッドは、1 つのベース テーブルのすべての行を含む行セットを開き、その行セットを返します。 **OpenRowset** の引数の 1 つは、行セットの作成元となるテーブルを識別するテーブル ID です。  
  
-   **IDBCreateCommand::CreateCommand** メソッドを呼び出して、コマンド オブジェクトを作成します。  
  
     コマンド オブジェクトでは、プロバイダーがサポートするコマンドが実行されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、SELECT ステートメントなどの任意の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントやストアド プロシージャへの呼び出しをコンシューマーで指定できます。 コマンド オブジェクトを使用して行セットを作成する手順は次のとおりです。  
  
    1.  コンシューマーは、セッションの **IDBCreateCommand::CreateCommand** メソッドを呼び出してコマンド オブジェクトを取得し、そのコマンド オブジェクトの **ICommandText** インターフェイスを要求します。 この **ICommandText** インターフェイスで、実際のコマンド テキストが設定および取得されます。 コンシューマーは、**ICommandText::SetCommandText** メソッドを呼び出して、テキスト コマンドにコマンドを設定します。  
  
    2.  ユーザーがコマンドの **ICommand::Execute** メソッドを呼び出します。 コマンドの実行時に構築される行セット オブジェクトには、コマンドから返される結果セットが含まれます。  
  
 コンシューマーは、**ICommandProperties** インターフェイスを使用して、**ICommand::Execute** インターフェイスで実行されるコマンドから返される行セットのプロパティを取得または設定できます。 最も一般的に要求されるプロパティは、行セットでサポートする必要のあるインターフェイスです。 コンシューマーはインターフェイスだけでなく、行セットやインターフェイスの動作を変更するプロパティも要求できます。  
  
 コンシューマーは **IRowset::Release** メソッドを使用して行セットを解放します。 行セットを解放すると、コンシューマーがその行セットに保持しているすべての行ハンドルも解放されます。 ただし、行セットを解放してもアクセサーは解放されません。 **IAccessor** インターフェイスがある場合は、それを解放する必要があります。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [IOpenRowset を使用した行セットの作成](creating-a-rowset-with-iopenrowset.md)  
  
-   [ICommand::Execute を使用した行セットの作成](creating-rowsets-with-icommand-execute.md)  
  
-   [行セットのプロパティと動作](rowset-properties-and-behaviors.md)  
  
-   [行セットと SQL Server カーソル](rowsets-and-sql-server-cursors.md)  
  
-   [行のフェッチ](fetching-rows.md)  
  
-   [IRow による 1 行のフェッチ](fetching-a-single-row-with-irow.md)  
  
-   [ブックマーク](bookmarks.md)  
  
-   [行セット内のデータの更新](updating-data-in-rowsets.md)  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
