---
title: Irow::getcolumns を使用して |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b26d13fd5e1158c93118de3efb495469ff0d8f6b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62938630"
---
# <a name="using-irowgetcolumns"></a>IRow::GetColumns の使用
  **IRow** の実装では、列に対して順方向専用の順次アクセスを実行できます。 **IRow::GetColumns** を 1 回だけ呼び出して、行内のすべての列にアクセスすることができます。また、行内の複数の列にアクセスするたびに、毎回 **IRow::GetColumns** を呼び出すこともできます。  
  
 **IRow::GetColumns** を複数回呼び出す場合は、呼び出しが重ならないようにする必要があります。 たとえば、1 回目に **IRow::GetColumns** を呼び出すときに列 1、2、3 を取得する場合、2 回目に **IRow::GetColumns** を呼び出すときには列 4、5、6 を取得する必要があります。 **IRow::GetColumns** の呼び出しが重なると、状態フラグ (DBCOLUMNACCESS の dwstatus フィールド) が DBSTATUS_E_UNAVAILABLE に設定されます。  
  
## <a name="see-also"></a>参照  
 [IRow による 1 行のフェッチ](fetching-a-single-row-with-irow.md)  
  
  
