---
title: SQLAllocStmt のマッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLAllocStmt
- SQLAllocStmt function [ODBC], mapping
ms.assetid: a2449dbb-1b6c-4b49-81b9-ebdddd4442fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf79d3ef813e87e785cea588cfc1d6e3eed44ee4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064990"
---
# <a name="sqlallocstmt-mapping"></a>SQLAllocStmt のマッピング
アプリケーションを呼び出すと**SQLAllocStmt** ODBC を通じて*3.x*ドライバーへの呼び出し。  
  
```  
SQLAllocStmt(hdbc, phstmt)  
```  
  
 マップされて**SQLAllocHandle**ドライバー マネージャーによってドライバーとして次のとおりです。  
  
```  
SQLAllocHandle(SQL_HANDLE_STMT, InputHandle, OutputHandlePtr)  
```  
  
 *InputHandle*に設定*hdbc*と*OutputHandlePtr*設定*phstmt*します。
