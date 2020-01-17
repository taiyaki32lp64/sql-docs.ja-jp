---
title: データソースからの切断 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- disconnecting [ODBC]
- ODBC applications, disconnecting
- SQLDisconnect function
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLFreeHandle function
- ODBC data sources, disconnecting
- SQL Server Native Client ODBC driver, data sources
- ODBC functions
- SQL Server Native Client ODBC driver, connections
ms.assetid: 65b0267d-b2ab-4a59-83f2-436d90cfbf79
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d5a7cb061c308508b0ab5d489dcabb4b25f93883
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784751"
---
# <a name="disconnecting-from-a-data-source"></a>データ ソースからの切断
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  アプリケーションでデータソースの使用が完了すると、 **Sqldisconnect**が呼び出されます。 **Sqldisconnect**は、接続に割り当てられているすべてのステートメントを解放し、データソースからドライバーを切断します。 切断後、アプリケーションは[Sqlfreehandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md)を呼び出して接続ハンドルを解放できます。 終了する前に、アプリケーションは**Sqlfreehandle**を呼び出して環境ハンドルを解放します。  
  
 切断後は、割り当てられていた接続ハンドルを再利用して、別のデータ ソースに接続したり、同じデータ ソースに再接続したりできます。 切断してから後で再接続するか、接続した状態を維持するかを決める際、アプリケーションの作成者は各操作の相対コストを考慮する必要があります。 接続メディアによっては、データ ソースに接続し、接続した状態を維持するのに比較的コストがかかる場合があります。 両者を比較検討する場合は、アプリケーションで同じデータ ソースに追加操作が行われる可能性やタイミングについて想定することも必要です。 また、アプリケーションで複数の接続が必要になる場合もあります。  
  
## <a name="see-also"></a>参照  
 [SQL Server &#40;ODBC との通信&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
