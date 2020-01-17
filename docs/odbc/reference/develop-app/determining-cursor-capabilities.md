---
title: カーソル機能の決定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], capabilities
- cursors [ODBC], scrollable
ms.assetid: 35be486c-8f2d-4cec-beb8-df14151abfef
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14715e40cd99f3f1a03c2ae19e825705a8376e30
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039997"
---
# <a name="determining-cursor-capabilities"></a>カーソル機能の決定
次の 4 つのオプションで**SQLGetInfo**カーソルの種類がサポートされており、機能について説明します。  
  
-   SQL_CURSOR_SENSITIVITY します。 カーソルが別のカーソルによって行われた変更に影響するかどうかを示します。  
  
-   SQL_SCROLL_OPTIONS します。 サポートされているカーソルの種類 (順方向専用、静的、キーセット ドリブン、動的、または混合) を示します。 すべてのデータ ソースには、順方向専用カーソルをサポートする必要があります。  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1、または SQL_STATIC_CURSOR_ATTRIBUTES1 (によって、カーソルの種類)。 スクロール可能なカーソルでサポートされるフェッチの型を一覧表示します。 戻り値のビットは、フェッチの型に対応して**SQLFetchScroll**します。  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 または SQL_STATIC_CURSOR_ATTRIBUTES2 (によって、カーソルの種類)。 静的およびキーセット ドリブン カーソルは、独自の更新、削除、および挿入を検出できるかどうかを示します。  
  
 アプリケーションは、実行時にカーソル機能を呼び出すことによって決定できます**SQLGetInfo**でこれらのオプション。 汎用アプリケーション、これは一般的です。 カーソル機能も決定できますアプリケーションの開発とハード コードされた使用中に、アプリケーションにします。 これは、垂直方向およびカスタム アプリケーションでよく行われますが、ODBC カーソル ライブラリなどのクライアント側のカーソルの実装を使用する汎用アプリケーションで行うこともできます。
