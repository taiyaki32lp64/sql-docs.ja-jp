---
title: SQLSetStmtOption (デスクトップ データベース ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: 98db9631-eb9b-4962-abe4-96f495133a5d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 20043c96771bf888defa2c8fbeb028aaa18f5abc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905342"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (デスクトップ データベース ドライバー)

|*fOption*|コメント|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|非同期処理がサポートされていません。 SQL_ASYNC_ENABLE fOption は SQLSTATE S1C00 を返します (ドライバーに対応していない)。|  
|SQL_KEYSET_SIZE|混在しているために、唯一の有効なキーセットのサイズは 0、および動的カーソルはサポートされていません。 この値が他の任意の数に設定されている場合は 0 に変更して、呼び出しは SQL_SUCCESS_WITH_INFO および SQLSTATE 01S02 を返します (オプションの値が変更されました)。|  
|SQL_MAX_ROWS|唯一の有効な行セットのサイズは、デスクトップ データベース ドライバーが返される行の数の制限をサポートしていないために、0 です。 この値が他の任意の数に設定されている場合は 0 に変更して、呼び出しは SQL_SUCCESS_WITH_INFO および SQLSTATE 01S02 を返します (オプションの値が変更されました)。|  
|SQL_QUERY_TIMEOUT|サポートされていません。|  
|SQL_ROW_NUMBER|サポートされていません。|  
|SQL_SIMULATE_CURSOR|サポートされていません。|
