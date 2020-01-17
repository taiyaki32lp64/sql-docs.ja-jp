---
title: SQLDriverConnect (Excel ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Excel Driver
ms.assetid: 285cb1ea-f461-4596-97f2-fc57af05dede
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e38f2f513b7da2c9342470ba75e2ee11b3d7e52a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053905"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect (Excel ドライバー)
> [!NOTE]  
>  このトピックでは、Excel ドライバー固有の情報を提供します。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 **SQLDriverConnect**データ ソース (DSN) を作成することがなく、ドライバーに接続することができます。  
  
 すべてのドライバーの接続文字列では、次のキーワードがサポートされています。**DSN**、 **DBQ**、および**FIL**します。  
  
 次の表は、各ドライバーでは、接続に必要な最小のキーワードを示しています。 と併用キーワード/値ペアの例を示します**SQLDriverConnect**します。 DRIVERID 値の一覧については、次を参照してください。 [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)します。  
  
> [!NOTE]  
>  For Microsoft Excel 3.0 または 4.0 driver DBQ または DefaultDir を指定しない場合、ドライバーは、現在のディレクトリに接続します。  
  
|Driver|必要なキーワード|使用例|  
|------------|-----------------------|--------------|  
|3\.0 または 4.0、Microsoft Excel|ドライバー、DriverID|ドライバー {0} Microsoft Excel ドライバー (*.xls)} を = です。DBQ c:\temp; を =DriverID 278 を =|  
|Microsoft Excel 5.0/7.0|ドライバー、DriverID、DBQ|ドライバー {0} Microsoft Excel ドライバー (*.xls)} を = です。DBQ=c:\temp\sample.xls;DriverID 22 を =|  
|Microsoft Excel 97 以降|ドライバー、DriverID、DBQ|ドライバー {0} Microsoft Excel ドライバー (*.xls)} を = です。DBQ=c:\temp\sample.xls;DriverID 790 を =|
