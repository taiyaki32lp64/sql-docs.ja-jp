---
title: コマンドを実行する |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- commands [SQL Server Native Client]
- OLE DB, executing commands
- sessions [SQL Server Native Client]
- OLE DB extensions for XML
- SQL Server Native Client OLE DB provider, command execution
ms.assetid: bb0b3cbf-fe45-46ba-b2ec-c5a39e3c7081
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f4c641495f2232bd0710e810716459d29a7f357a
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761738"
---
# <a name="executing-a-command"></a>コマンドの実行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  データソースへの接続が確立されると、コンシューマーは**IDBCreateSession:: CreateSession**メソッドを呼び出してセッションを作成します。 セッションは、コマンド、行セット、またはトランザクションのファクトリとして動作します。  
  
 個別のテーブルやインデックスを直接操作するには、**IOpenRowset** インターフェイスを要求します。 **IOpenRowset::OpenRowset** メソッドは、1 つのベース テーブルまたはベース インデックスからのすべての行が含まれる行セットを開いて返します。  
  
 SELECT \* FROM Authors などのコマンドを実行するには、**IDBCreateCommand** インターフェイスを要求します。 コンシューマーは、 **IDBCreateCommand:: createcommand**メソッドを実行して、コマンドオブジェクトを作成し、 **ICommandText**インターフェイスの要求を行うことができます。 **ICommandText:: SetCommandText**メソッドを使用して、実行するコマンドを指定します。  
  
 コマンドを実行するには、**Execute** コマンドを使用します。 コマンドには、任意の SQL ステートメントやプロシージャ名を指定できます。 コマンドを実行しても、必ず結果セット (行セット) オブジェクトが得られるわけではありません。 SELECT * FROM Authors などのコマンドでは、結果セットが得られます。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client OLE DB プロバイダー アプリケーションの作成](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
