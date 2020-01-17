---
title: 既定の C データ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b9e0a9b8e85967ce46344e824c03e74fe3552e7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130013"
---
# <a name="default-c-data-types"></a>既定の C データ型
アプリケーションで SQL_C_DEFAULT を指定する場合**SQLBindCol**、 **SQLGetData**、または**SQLBindParameter**ドライバーは、その入力バッファーまたは出力の C データ型が前提としています。列またはパラメーターのバッファーをバインドする対象の SQL データ型に対応します。  
  
> [!IMPORTANT]  
>  相互運用可能なアプリケーションでは、SQL_C_DEFAULT を使用する必要があります。 これらは、常を使用しているバッファーの C 型を指定する必要があります。 これは、ドライバーが次の理由で既定の C 型を常に正しく判断できないためです。  
  
-   DBMS が、SQL データ型の列またはパラメーターを昇格する場合、ドライバーは元の SQL データ型の列またはパラメーターを特定できません。 そのため、対応する既定の C データ型を判断できません。  
  
-   ドライバーを決定できない場合かどうかは、特定の列またはパラメーターが署名済み、これが、大文字と小文字は多くの場合、ドライバーが判断できない、DBMS によって処理される対応する既定の C データを入力するかどうかする必要がある付きまたは署名なし。  
  
     SQL_C_DEFAULT がプログラミングの利便性としてのみ提供される、ため、アプリケーションが実際の C データ型を指定する場合の機能を失うしていません。  
  
 各 SQL データ型の既定の C データ型を示す表が含まれている[SQL から C データ型への変換データ](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)、この付録で後述します。
