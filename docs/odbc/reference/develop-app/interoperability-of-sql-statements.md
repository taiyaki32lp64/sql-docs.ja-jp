---
title: SQL ステートメントの相互運用性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC]
- interoperability of SQL statements [ODBC], about interoperability
ms.assetid: 3b24c499-829c-4e65-90cf-a3a0f6d0a186
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ed366acde11778342387d3bcb152a6619a6a3778
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138868"
---
# <a name="interoperability-of-sql-statements"></a>SQL ステートメントの相互運用性
アプリケーションの残りの部分のようには、SQL ステートメントは相互運用可能なまたは特定の DBMS を指定できます。 どのように相互運用可能な SQL ステートメントの選択は、アプリケーションの残りの部分のようにする必要があるとアプリケーションの種類によって異なります。 カスタム アプリケーションは、1 つまたは場合によって 2 つの Dbms の機能を利用する、通常は設計されているために、相互運用可能な SQL ステートメントを使用する可能性が低下します。 汎用アプリケーションは、さまざまな Dbms を使用するよう設計されていますので、相互運用可能な SQL ステートメントを使用します。 垂直方向のアプリケーションは、通常どこかに間には、特定のレベルの機能の要求が、それ以外の場合 相互運用可能な SQL ステートメントを使用しています。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [SQL 文法の選択](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [相互運用可能な SQL ステートメントの構築](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
