---
title: SQLFreeHandle |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2320ec5059535702d8fb203b32a316b49821b20c
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73786836"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  手動コミットモードでは、トランザクションが開いているステートメントハンドルで**Sqlfreehandle**を呼び出すと、データベースに対する保留中の変更がロールバックされます。 ステートメントハンドルで**Sqlfreehandle**を呼び出すと、開いているカーソルが常に閉じられ、保留中の結果は破棄され、ステートメントハンドルに関連付けられているすべてのリソースが解放されます。  
  
## <a name="see-also"></a>参照  
 [Sqlfreehandle 関数](https://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
