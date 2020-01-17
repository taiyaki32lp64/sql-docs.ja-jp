---
title: SQLSetScrollOptions (デスクトップ データベース ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Desktop Database Drivers
ms.assetid: 51d643ed-015b-4639-969a-9491d9875aca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0adedfb69cd4a7b5cf195916747687826805e8bf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905390"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (デスクトップ データベース ドライバー)
SQL_CONCUR_READ_ONLY では、転送と静的カーソルはサポートされます。  
  
 キーセット ドリブン カーソルのみがサポートされている、 *fConcurrency* SQL_CONCUR_LOCK の引数。  
  
 *FConcurrency* SQL_CONCUR_ROWVER の引数はサポートされていません。  
  
 動的カーソルと混合カーソルはサポートされていません。
