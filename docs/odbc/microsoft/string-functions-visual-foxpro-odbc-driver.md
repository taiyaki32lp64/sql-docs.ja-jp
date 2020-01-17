---
title: 文字列関数 (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC string functions [ODBC]
- string functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], string functions
- FoxPro ODBC driver [ODBC], string functions
ms.assetid: 1974fd26-ef0d-45d5-860b-298917c8e9c3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db1fbaffbee0f74625f4a11cad3b961f194e3829
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948776"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>文字列関数 (Visual FoxPro ODBC ドライバー)
次の表に、Visual FoxPro ODBC ドライバーでサポートされている ODBC の文字列操作関数ODBC 構文から同じ関数の場合、Visual FoxPro の文法が異なる場合は、Visual FoxPro のと同じですが一覧表示されます。  
  
|ODBC の文法|Visual FoxPro の文法|  
|------------------|---------------------------|  
|ASCII *(string_exp)*|ASC *(string_exp)*|  
|CHAR *(コード)*|CHR *(string_exp)*|  
|CONCAT *(string_exp1 string_exp2)*|*string_exp1 + string_exp2*|  
|違い *(string_exp1 string_exp2)*||  
|挿入 *(string_exp1、開始、長さ、string_exp2)*|STUFF *(string_exp1、開始、長さ、string_exp2)*|  
|LCASE *(string_exp)*|LOWER *(string_exp)*|  
|左 *(string_exp 数)*||  
|長さ *(string_exp)*|LEN *(string_exp)*|  
|LTRIM *(string_exp)*||  
|繰り返し *(string_exp 数)*|レプリケート *(string_exp 数)*|  
|置換 *(string_exp1、string_exp2、string_exp3)*|STRTRAN *(string_exp1、string_exp2、string_exp3)*|  
|右 *(string_exp 数)*||  
|RTRIM *(string_exp)*||  
|SOUNDEX *(string_exp)*||  
|領域 *(数)*||  
|部分文字列 *(string_exp、開始、長さ)*|SUBSTR *(string_exp、開始、長さ)*|  
|UCASE *(string_exp)*|上限 *(string_exp)*|
