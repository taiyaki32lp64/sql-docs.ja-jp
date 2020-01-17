---
title: SQLColAttributes (Paradox ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLColAttributes
ms.assetid: bbeef024-d470-4d28-b61b-26997ef41007
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9b7d5967108d605d6b7426dcd662507a49037108
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132664"
---
# <a name="sqlcolattributes-paradox-driver"></a>SQLColAttributes (Paradox ドライバー)
> [!NOTE]  
>  このトピックでは、Paradox ドライバー固有の情報を提供します。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
|属性|コメント|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|LONGVARBINARY データ、SQL_COLUMN_DISPLAY_SIZE は 2 時間列の最大長いない列の最大長です。|  
|SQL_OWNER_NAME|空の文字列 ("") の所有者名がサポートされていないために、この列に返されます。|  
|SQL_QUALIFIER_NAME|ディレクトリへのパスが返されます。|  
|SQL_COLUMN_SEARCHABLE|LONGVARBINARY および LONGVARCHAR 列は、SQL_UNSEARCHABLE として報告されます。<br /><br /> 固定長および可変長のバイナリおよび文字データ型は LONGVARBINARY および LONGVARCHAR がない場合でも、検索可能です。|  
  
> [!NOTE]  
>  上記はによって返される属性の完全な一覧ではない**SQLColAttributes**します。
