---
title: スクロール可能なカーソルの種類 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 210b66a800670f033508f903b18778f88ddd4c8b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061635"
---
# <a name="scrollable-cursor-types"></a>スクロール可能なカーソルの種類
4 つの種類のスクロール可能なカーソルは、静的、動的、キーセット ドリブン、混合。 静的カーソルはほとんどまたはまったく変更を検出しますが、比較的負荷の実装には。 動的カーソルはすべての変更を検出しますが、実装にコストがかかります。 カーソルのキーセット ドリブン、混合は、動的カーソルよりも少ない費用でが、ほとんどの変更を検出する間にあります。  
  
 スクロール可能なカーソルの種類ごとの特性を定義する、次の用語が使用されます。  
  
-   **独自の更新、削除、および挿入します。** 更新、削除、および呼び出しを使用するか、カーソルによって行われた挿入**SQLBulkOperations**または**SQLSetPos**または位置指定の delete ステートメントまたは更新します。  
  
-   **更新プログラムの他、削除、および挿入します。** 更新、削除、およびしない同じトランザクション内でその他の操作によって行われたものも含め、カーソルによって行われた挿入、他のトランザクションによるものおよび他のアプリケーションによって行われたものです。  
  
-   **メンバーシップ。** 結果セット内の行のセット。  
  
-   **順序。** 順序は、カーソルによって行が返されます。  
  
-   **値。** 結果セットの各行の値。  
  
 更新、削除、およびデータを挿入する方法については、次を参照してください。[更新データの概要](../../../odbc/reference/develop-app/updating-data-overview.md)します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ODBC 静的カーソル](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [ODBC 動的カーソル](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [キーセット ドリブン カーソル](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [混合カーソル](../../../odbc/reference/develop-app/mixed-cursors.md)
