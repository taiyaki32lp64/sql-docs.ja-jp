---
title: SQLGetTypeInfo (dBASE ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetTypeInfo
ms.assetid: 6e9ce02b-97c7-4c1a-91e0-829df7459c84
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43319f7f23741a1533321c9369077d42a2484395
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898750"
---
# <a name="sqlgettypeinfo-dbase-driver"></a>SQLGetTypeInfo (dBASE ドライバー)
> [!NOTE]  
>  このトピックでは、dBASE ドライバー固有の情報を提供します。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
 によって生成されたテーブルの型 (TYPE_NAME) の名前が返される**SQLGetTypeInfo**データ ソースで最もよく使用する名前になります。  
  
 SQL_ALL_EXCEPT_LIKE が返されます、検索可能な列で、バイトのカウンター、Double、1 つ、Long、Short データ型。 (LIKE 機能は、値を比較を実行し、ODBC 標準変換関数を使用する文字に変換することで実現できます)。
