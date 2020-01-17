---
title: 記述子のコピー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d41cd744d39113c556c4ee8bc17411b7992e596
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002143"
---
# <a name="copying-descriptors"></a>記述子のコピー
**SQLCopyDesc**記述子が 1 つのフィールドを別の識別子にコピーする関数が呼び出されます。 フィールドは、IRD ではなく、アプリケーション記述子をまたは、IPD にのみコピーできます。 フィールドは、任意の型記述子からコピーすることができます。 ソースとターゲットの両方の記述子に対して定義されているフィールドのみがコピーされます。 **SQLCopyDesc**記述子の割り当ての種類を変更できないため、SQL_DESC_ALLOC_TYPE フィールドはコピーされません。 コピーしたフィールドは、既存のフィールドを上書きします。  
  
 1 つのステートメント ハンドルで、ARD は、別のステートメント ハンドルで APD として使用できます。 これにより、アプリケーション、アプリケーション レベルでデータをコピーせずにテーブル間の行をコピーします。 これを行うには、テーブルのフェッチされた行を表す行記述子は、INSERT ステートメントのパラメーターのパラメーターの記述子として再利用されます。 SQL_MAX_CONCURRENT_ACTIVITIES 情報の種類は、この操作が成功するための 1 より大きくなければなりません。
