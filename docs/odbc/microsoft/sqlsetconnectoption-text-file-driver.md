---
title: SQLSetConnectOption (テキスト ファイル ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Text File Driver
- text file driver [ODBC], SQLSetConnectOption
ms.assetid: b631a20c-2f60-4102-a61d-93b8780a4620
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 32c4a0219b049ee66a38d6c7c10295245dd48ebc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905484"
---
# <a name="sqlsetconnectoption-text-file-driver"></a>SQLSetConnectOption (テキスト ファイル ドライバー)
> [!NOTE]  
>  このトピックでは、テキスト ファイル ドライバー固有の情報を提供します。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
|fOption|解説|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption SQL_MODE_READ_ONLY または SQL_MODE_READ_WRITE のいずれかに設定できます。 ただし、SQL_ACCESS_MODE が SQL_MODE_READ_ONLY に設定されている場合、ドライバーは更新を禁止できません。|  
|SQL_AUTOCOMMIT|テキストのドライバーでは、トランザクションをサポートしていないため SQL_AUTOCOMMIT に設定されています (既定の状態) でのみサポートします。|  
|SQL_CURRENT_QUALIFIER|サポートされています。|  
|SQL_LOGIN_TIMEOUT|サポートされていません。|  
|SQL_OPT_TRACE|サポートされています。|  
|SQL_OPT_TRACEFILE|サポートされています。|  
|SQL_PACKET_SIZE|サポートされていません。|  
|SQL_QUIET_MODE|サポートされていません。|  
|SQL_TRANSLATE_DLL|サポートされていません。|  
|SQL_TRANSLATION_OPTION|サポートされていません。|  
|SQL_TXN_ISOLATION|サポートされていません。|
