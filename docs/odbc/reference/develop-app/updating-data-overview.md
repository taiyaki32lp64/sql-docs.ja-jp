---
title: データの概要の更新 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0701218b5ef489d1f8962ffadc9409986a0c36c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942810"
---
# <a name="updating-data-overview"></a>データの概要の更新
SQL ステートメントを実行するか、呼び出すことによって、アプリケーションでデータを更新できる**SQLSetPos**または**SQLBulkOperations**します。 **UPDATE**、**DELETE**、および**INSERT**ステートメントは、データ ソース上で直接実行し、通常、ドライバーによってサポートされます。 更新プログラムを検索する delete ステートメントを変更する行の仕様を含めることができます。 更新プログラムの配置、および delete ステートメントと**SQLSetPos**カーソルを介して、データ ソースに対して動作し、はあまり広くサポートされています。  
  
 カーソルが、このセクションで説明する方法を使用して結果セットに加えられた変更を検出できるかどうかは、カーソルの実装方法の種類によって異なります。 順方向専用カーソルでは、行を再確認いませんし、そのため、変更は検出されません。 スクロール可能なカーソルが変更を検出するかどうかについては、次を参照してください。[スクロール可能なカーソル](../../../odbc/reference/develop-app/scrollable-cursors.md)します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [UPDATE、DELETE、INSERT ステートメント](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [位置指定の UPDATE および DELETE ステートメント](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [位置指定の UPDATE および DELETE ステートメントのシミュレート](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [影響を受ける行数の決定](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [SQLSetPos によるデータの更新](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [SQLBulkOperations によるデータの更新](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [長い形式のデータ、SQLSetPos および SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
