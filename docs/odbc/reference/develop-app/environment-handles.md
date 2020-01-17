---
title: 環境ハンドル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 409b2c14282238766457d349287f65d90fe463b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114319"
---
# <a name="environment-handles"></a>環境ハンドル
*環境*はデータにアクセスするためのグローバル コンテキストは、環境に関連付けられているなど、本質的にグローバルに適用されるすべての情報。  
  
-   環境の状態  
  
-   現在の環境レベルの診断  
  
-   環境に現在割り当てられている接続の処理  
  
-   環境の各属性の現在の設定  
  
 ODBC ドライバー マネージャー (ドライバー) を実装するコード内では、環境ハンドルは、この情報を格納する構造体を識別します。  
  
 環境ハンドルは、ODBC アプリケーションで頻繁には使用されません。 呼び出しで常に使用する**SQLDataSources**と**SQLDrivers**への呼び出しで使用されることと**SQLAllocHandle**、 **SQLEndTran**、**SQLFreeHandle**、 **SQLGetDiagField**、および**SQLGetDiagRec**します。  
  
 ODBC ドライバー マネージャー (ドライバー) を実装するコードの各部分には、1 つまたは複数の環境ハンドルが含まれています。 たとえば、ドライバー マネージャーは、それに接続されている各アプリケーションの別の環境ハンドルを保持します。 使用して環境ハンドルが割り当てられた**SQLAllocHandle**およびに解放された**SQLFreeHandle**します。
