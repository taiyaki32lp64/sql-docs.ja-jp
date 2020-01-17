---
title: SQL Server メッセージの結果 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3383dcd08ed5910d949608e521b3cd23f37aace8
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73790154"
---
# <a name="sql-server-message-results"></a>SQL Server のメッセージ結果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントでは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー行セット、または実行時に影響を受ける行の数が生成されません。  
  
-   PRINT  
  
-   重大度が 10 以下の RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 上記のステートメントでは、行セットや行数の結果が返されるのではなく、ステートメントから 1 つ以上の情報メッセージが返されるか、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から情報メッセージが返されます。 正常に実行されると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは S_OK を返し、メッセージは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーコンシューマーが使用できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは S_OK を返し、多くの [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの実行後、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーメンバー関数のコンシューマー実行に従って、1つまたは複数の情報メッセージを使用できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーコンシューマーがクエリテキストを動的に指定できるようにするには、リターンコードの値に関係なく、すべてのメンバー関数の実行後にエラーインターフェイスを確認し、返された IRowset の有無を確認する必要があります。または**IMultipleResults**インターフェイス参照、または影響を受ける行の数。  
  
## <a name="see-also"></a>参照  
 [エラー](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
