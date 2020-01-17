---
title: SQLProcedures |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0001f1d6e45e855b884028a595a2b61263c2e58
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046686"
---
# <a name="sqlprocedures"></a>SQLProcedures
  すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャは値を返します。 **SQLProcedures**に結果セット列 PROCEDURE_TYPE を報告します。  
  
 **SQLProcedures**値が存在するかどうかに関係なく SQL_SUCCESS を返します*CatalogName、SchemaName,* または*ProcName*パラメーター。 **SQLFetch** SQL_NO_DATA が返されるこれらのパラメーターに無効な値を使用する場合。  
  
 **SQLProcedures**静的サーバー カーソルで実行できます。 実行しようとすると、 **SQLProcedures**更新可能な (動的またはキーセット) カーソルでは、カーソルの種類が変更されたことを示す SQL_SUCCESS_WITH_INFO を返します。  
  
 **SQLProcedures**名前に一致するすべてのプロシージャに関する情報を返します*ProcName*され、現在のユーザーによってまたは現在のユーザーが付与されている VIEW DEFINITION 権限で実行できます。  
  
## <a name="see-also"></a>関連項目  
 [SQLProcedures 関数](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API 実装の詳細](odbc-api-implementation-details.md)  
  
  
