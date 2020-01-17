---
title: 診断レコード |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- handles [ODBC], diagnostic records
- header records [ODBC]
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 92c73f9b-3ed7-410d-9cec-2771004aae60
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 90133b4a18876c52b9b6b6bffbe4c8c02c953e07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039879"
---
# <a name="diagnostic-records"></a>診断レコード
接続、ステートメント、および記述子ハンドルは、各環境では、関連付けられている*診断レコード*します。 これらのレコードには、最後に呼び出される特定のハンドルを使用する関数についての診断情報が含まれます。 レコードは、そのハンドルを使用して、別の関数が呼び出されたときだけに置き換えられます。 いつでも格納できる診断レコードの数に制限はありません。  
  
 診断レコードの 2 種類があります。*ヘッダー レコード*と 0 個以上*状態レコード*します。 ヘッダー レコードはレコード 0 です。状態レコードは、レコード 1 以降。 診断レコードは、数のヘッダー レコードと状態レコードが異なりますが、個別のフィールドで構成されます。 さらに、ODBC コンポーネントは、独自の診断レコードのフィールドを定義できます。  
  
 構造を実際にするためには必要はありませんが、診断レコードは、構造体として考えることができます、ドライバーが診断情報を格納する方法は、ドライバー固有です。  
  
 診断レコードのフィールドが取得されます**SQLGetDiagField**します。 SQLSTATE、ネイティブ エラー番号、および状態レコードの診断メッセージ フィールドに 1 回の呼び出しで取得できる**SQLGetDiagRec**します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ヘッダー レコード](../../../odbc/reference/develop-app/header-record.md)  
  
-   [状態レコード](../../../odbc/reference/develop-app/status-records.md)
