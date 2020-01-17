---
title: 記述子フィールドの初期化 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- initializing descriptor fields [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1da157cb-8ea9-4a56-983b-1c45650217c5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c78162bcf0421fee609abe5fcacf9613e0f8020b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138938"
---
# <a name="initialization-of-descriptor-fields"></a>記述子フィールドの初期化
アプリケーションの行記述子は、割り当て済みフィールドが表示される初期値に記載されている[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)します。 SQL_DESC_TYPE フィールドの初期値は、SQL_DEFAULT です。 これは、データベースのデータ、アプリケーションに提示するための標準的な処理を提供します。 アプリケーションは、記述子レコードのフィールドを設定して、データの処理が異なるを指定する場合があります。  
  
 記述子のヘッダーの SQL_DESC_ARRAY_SIZE の初期値は 1 です。 アプリケーションでは、複数行のフェッチを有効にするには、このフィールドを変更できます。  
  
 既定値の概念は、ird フィールドに対して無効です。 関連付けられている準備または実行されたステートメントがある場合にのみ、アプリケーションは、ird フィールドへのアクセスを得ることができます。  
  
 ドライバーが自動的に入力されたら、IPD 後にのみ、IPD の特定のフィールドが定義されます。 ない場合は、定義はありません。 これらのフィールドは SQL_DESC_CASE_SENSITIVE、SQL_DESC_FIXED_PREC_SCALE、SQL_DESC_TYPE_NAME、SQL_DESC_UNSIGNED、および SQL_DESC_LOCAL_TYPE_NAME です。
