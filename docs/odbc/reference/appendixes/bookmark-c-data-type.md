---
title: Bookmark C データ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], bookmark C data type
- pseudo-type identifiers [ODBC], bookmark C data type
- data types [ODBC], pseudo-type identifiers
- bookmarks [ODBC]
- bookmark C data type [ODBC]
ms.assetid: add88e48-ada3-4c0c-a5ac-e78903d3ff41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86488da93470a61a54638e9c60e6e1795a9da4dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125752"
---
# <a name="bookmark-c-data-type"></a>Bookmark C データ型
ブックマークの C データ型では、ブックマークを取得するアプリケーション。 ブックマーク C 型は可変長; できるブックマークの値を取得する場合のみ使用されます。他のデータ型に変換する必要がありますされません。 アプリケーションの取得と設定のいずれかから結果の列 0 ブックマーク**SQLBulkOperations** SQL_ADD の操作)、(で**SQLFetch**、 **SQLFetchScroll**、または**SQLGetData**します。 詳細については、次を参照してください。[ブックマーク](../../../odbc/reference/develop-app/bookmarks-odbc.md)します。  
  
 次の表の値*CType*ブックマーク C データ型では、ブックマーク C データ型、およびこのデータの定義を実装する ODBC C データ型を SQL から入力します。H.  
  
> [!NOTE]
>  SQL_C_BOOKMARK のデータ型は非推奨とされました。 ODBC *3.x*アプリケーションは SQL_C_BOOKMARK を使用しないでください。 ODBC *3.x*ドライバーは ODBC を使って作業する場合にのみ、SQL_C_BOOKMARK をサポートする必要があります*2.x*を使用するアプリケーション。 ドライバー マネージャーが、ODBC を使って、アプリケーションが動作する際に、SQL_C_BOOKMARK に SQL_C_VARBOOKMARK をマップ*2.x*ドライバー。  
  
|C 型識別子|ODBC C の typedef|C 型|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(非推奨)|ブックマーク|符号なし long int|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|
