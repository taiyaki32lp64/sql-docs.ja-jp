---
title: サーバーカーソルを使用する |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, cursors
- cursors [ODBC], server cursors
- ODBC cursors, server cursors
- server cursors [SQL Server]
ms.assetid: 8a6d99b7-10b8-4474-8639-4914b25ba170
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7ca1f7e2e5115920558e8550f5564a56aea5790b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784440"
---
# <a name="using-server-cursors"></a>サーバー カーソルの使用
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC アプリケーションが ODBC カーソルの属性のいずれかを既定値以外に設定すると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、同じ種類の API サーバーカーソルを実装するようにサーバーに要求します。 API サーバー カーソルを使用すると、クライアント側のメモリを解放でき、クライアントとサーバー間のネットワーク トラフィックを大幅に削減できます。  
  
 API サーバー カーソルの潜在的な欠点は、現時点では、すべての SQL ステートメントをサポートしているわけではないことです。 次の機能は、API サーバー カーソルでは実行できません。  
  
-   複数の結果セットを返すバッチまたはストアド プロシージャ  
  
-   COMPUTE 句、COMPUTE BY 句、FOR BROWSE 句、または INTO 句を伴う SELECT ステートメント  
  
-   リモート ストアド プロシージャを参照する EXECUTE ステートメント  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続している場合、サーバー カーソルを使用してこのような特性のステートメントを実行すると、カーソルは既定の結果セットに変換されます。 以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続している場合は、エラーになります。  
  
## <a name="see-also"></a>参照  
 [カーソルの実装方法](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
