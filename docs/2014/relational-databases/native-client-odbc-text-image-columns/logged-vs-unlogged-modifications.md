---
title: ログに変更ログを取らない |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- logged vs. nonlogged modifications [SQL Server Native Client]
- columns [ODBC]
- ODBC data types, image columns
- nonlogged vs. logged modifications
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 20aa5b27-4a2c-46e7-8356-beb0eebf4b7e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c722d5360ad01e7e95508c2219ceb674de381286
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63195134"
---
# <a name="logged-vs-unlogged-modifications"></a>ログに記録される変更と記録されない変更
  アプリケーションが要求を[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC ドライバー ログではなく**テキスト**、 **ntext**、および**イメージ**変更します。 ただし、このオプションの使用には注意が必要です。 そのような状況だけのために使用する必要があります、**テキスト**、 **ntext**、または**イメージ**データが重要でないと、データの所有者がデータを回復する機能のトレードオフを許容できます。高いパフォーマンス。  
  
 ログ記録**テキスト**、 **ntext**、および**イメージ**変更が呼び出すことによって制御される[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)で、 *属性*パラメーターを SQL_SOPT_SS _ TEXTPTR_LOGGING に設定し、 *ValuePtr* SQL_TL_ON または SQL_TL_OFF に設定します。  
  
## <a name="see-also"></a>関連項目  
 [text 列と image 列の管理](managing-text-and-image-columns.md)  
  
  
