---
title: SQL Server メッセージの結果 |Microsoft Docs
description: SQL Server のメッセージ結果
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 05d731f418bad21f9e8ec32c620b352c5663994a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994921"
---
# <a name="sql-server-message-results"></a>SQL Server のメッセージ結果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントでは、OLE DB Driver for SQL Server の行セットや、ステートメント実行時に処理された行カウントは生成されません。  
  
-   PRINT  
  
-   重大度が 10 以下の RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 上記のステートメントでは、行セットや行数の結果が返されるのではなく、ステートメントから 1 つ以上の情報メッセージが返されるか、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] から情報メッセージが返されます。 正常に実行されると、SQL Server の OLE DB ドライバーから S_OK が返され、SQL Server コンシューマーの OLE DB ドライバーでメッセージを使用できるようになります。  
  
 SQL Server の OLE DB ドライバーは S_OK を返し、多く[!INCLUDE[tsql](../../../includes/tsql-md.md)]のステートメントの実行後、または SQL Server メンバー関数の OLE DB ドライバーのコンシューマー実行に従って、1つまたは複数の情報メッセージを使用できます。  
  
 OLE DB Driver for SQL Server のコンシューマーがクエリ テキストの動的な指定を許可する場合、メンバー関数を実行するたびにエラー インターフェイスをチェックする必要があります。このチェックは、リターン コードの値、返される **IRowset** インターフェイス参照や **IMultipleResults** インターフェイス参照の有無、および処理された行数に関係なく行う必要があります。  
  
## <a name="see-also"></a>参照  
 [エラー](../../oledb/ole-db-errors/errors.md)  
  
  
