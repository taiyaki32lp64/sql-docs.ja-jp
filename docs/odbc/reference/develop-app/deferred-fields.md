---
title: フィールドを遅延 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], deferred fields
- deferred fields [ODBC]
ms.assetid: 5abeb9cc-4070-4f43-a80d-ad6a2004e5f3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2c229d31941d5cef0da253545cecd7d1496ee4a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076821"
---
# <a name="deferred-fields"></a>遅延フィールド
値*フィールドを遅延*設定されているが、ドライバーは、遅延の影響用の変数のアドレスを保存する場合は使用しません。 ドライバー、アプリケーション パラメーター記述子への呼び出し時に、変数の内容を使用して**SQLExecDirect**または**SQLExecute**します。 アプリケーションの追加行記述子では、ドライバーはフェッチ時に、変数の内容を使用します。  
  
 次に、遅延のフィールドを示します。  
  
-   記述子レコードの SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR フィールドです。  
  
-   アプリケーション記述子レコードの SQL_DESC_OCTET_LENGTH_PTR フィールドです。  
  
-   複数行のフェッチの場合、記述子のヘッダー フィールドの SQL_DESC_ARRAY_STATUS_PTR と SQL_DESC_ROWS_PROCESSED_PTR フィールド。  
  
 記述子が割り当てられると、各記述子レコードのフィールドの遅延が最初に含まれる null 値にします。 Null 値の意味は次のとおりです。  
  
-   SQL_DESC_ARRAY_STATUS_PTR に null 値がある場合は、このコンポーネントの行ごとの診断情報を返す複数行のフェッチは失敗します。  
  
-   SQL_DESC_DATA_PTR が null の値を持つ場合、レコードは連結ではありません。  
  
-   ARD の SQL_DESC_OCTET_LENGTH_PTR フィールドは、null 値を持つ、ドライバーでは、その列の長さの情報は返されません。  
  
-   場合は、APD の SQL_DESC_OCTET_LENGTH_PTR フィールドに null 値があり、ユーザーがパラメーターは文字の文字列は、ドライバーは、文字列が null 終端であると仮定します。 出力の動的パラメーターのこのフィールドに null 値により、ドライバー、長さ情報を返します。 (SQL_DESC_TYPE フィールドが文字の文字列パラメーターを表していない場合、SQL_DESC_OCTET_LENGTH_PTR フィールドは無視されます。)  
  
 アプリケーションの割り当てを解除またはドライバーの読み取りまたは書き込みに時間と、フィールドとそれらを関連付けます時間の間の遅延のフィールドに使用される変数を破棄する必要がありますできません。
