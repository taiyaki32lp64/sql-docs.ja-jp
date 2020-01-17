---
title: LIKE 述語のエスケープ文字 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate [ODBC]
- escape sequences [ODBC], LIKE predicate
ms.assetid: 185d6109-48cf-4981-bc40-ec2a4a90cafc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 20310c60759aea17d61b9252fd73d226567a7a54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027231"
---
# <a name="like-predicate-escape-character"></a>LIKE 述語のエスケープ文字
**LIKE**述語、パーセント記号 (%)一致する 0 個以上の任意の文字、およびアンダー スコア (\_) では、任意の 1 文字と一致します。 実際のパーセント記号の一致またはでアンダー スコア、**LIKE**述語、エスケープ文字はアンダー スコアまたはパーセント記号の前に取得する必要があります。 エスケープ シーケンスを定義する、**LIKE**述語のエスケープ文字とは。  
  
 **{escape '** *エスケープ文字* **'}**  
  
 場所*エスケープ文字*はデータ ソースでサポートされる任意の文字。  
  
 などの詳細についてはエスケープ シーケンスを参照してください[エスケープ シーケンスのような](../../../odbc/reference/appendixes/like-escape-sequence.md)付録 c:SQL 文法。  
  
 たとえば、次の SQL ステートメントは、「AAA %」文字で始まる名前、同じ結果セットの顧客の作成します。 最初のステートメントでは、エスケープ シーケンス構文を使用します。 2 番目のステートメントでは、Microsoft® Access 固有の構文を使用して、相互運用可能なではありません。 2 番目のパーセントが各文字に注意してください**LIKE**述語は、0 個以上の任意の文字に一致するワイルドカード文字です。  
  
```  
SELECT Name FROM Customers WHERE Name LIKE '\%AAA%' {escape '\'}  
  
SELECT Name FROM Customers WHERE Name LIKE '[%]AAA%'  
```  
  
 確認するかどうか、**LIKE**述語のエスケープ文字がデータ ソースでサポートされている、アプリケーションを呼び出す**SQLGetInfo** SQL_LIKE_ESCAPE_CLAUSE オプションを使用します。
