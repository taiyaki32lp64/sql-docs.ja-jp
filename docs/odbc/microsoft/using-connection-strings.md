---
title: 接続文字列の使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC]
- connecting to data source [ODBC], Visual FoxPro
- Visual FoxPro data source [ODBC], connecting
ms.assetid: 57634960-47e9-49bf-95c1-6e3702ac8166
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 496fe10fbf49f4d712127e2e4122c50fa20ba2be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044584"
---
# <a name="using-connection-strings"></a>接続文字列の使用
Visual FoxPro データ ソースに接続する接続文字列を使用することができます。  
  
 たとえば、TasTrade データ ソースとデータ ソースに関連付けられている排他の現在の設定の上書きに接続するには、文字列を使用します。  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 一連の属性のキーワードと値、接続文字列に含めることができます、次を参照してください。 [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)します。  
  
 接続文字列の構文の詳細については、次を参照してください。 [SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md)で、 *ODBC プログラマ リファレンス*します。
