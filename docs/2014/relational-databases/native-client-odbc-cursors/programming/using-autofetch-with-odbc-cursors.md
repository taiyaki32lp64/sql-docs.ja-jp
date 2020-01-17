---
title: Autofetch と ODBC カーソル |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, autofetch
- autofetch option
- cursors [ODBC], autofetch
ms.assetid: 57bd55f4-8945-4d8d-9f58-d30c81d2a514
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 343975c2c6ad39c67dcd10c0d55886d21e69f3f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62711560"
---
# <a name="using-autofetch-with-odbc-cursors"></a>autofetch と ODBC カーソルの併用
  インスタンスに接続されているときに[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、任意のサーバー カーソルの種類を使用する場合、autofetch オプションをサポートしています。 Autofetch では、 **SQLExecute**または**SQLExecDirect**カーソルを開く関数にも、暗黙の型は、 [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)(SQL_FIRST) 関数。 バインドされたアプリケーション変数に、最初の行セットを構成する行がステートメント実行の一環として返されるので、ネットワーク経由でのサーバーとのやり取りが減少します。 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md)ときはサポートされていません、autofetch オプションが有効になります。 結果セットの列をプログラム変数にバインドする必要があります。  
  
 アプリケーションでは、ドライバー固有の SQL_SOPT_SS_CURSOR_OPTIONS ステートメント属性を SQL_CO_AF に設定することにより autofetch を要求します。  
  
## <a name="see-also"></a>参照  
 [カーソル プログラミングの詳細&#40;ODBC&#41;](cursor-programming-details-odbc.md)  
  
  
