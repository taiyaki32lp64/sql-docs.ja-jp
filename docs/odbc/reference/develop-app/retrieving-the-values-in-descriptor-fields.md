---
title: 記述子フィールドの値を取得する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 55d7017c659ca4d0b8094ed4a665d27c10b355f7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020450"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>記述子フィールドの値の取得
アプリケーションが呼び出すことができます**SQLGetDescField**記述子レコードの 1 つのフィールドを取得します。 **SQLGetDescField** ODBC では、定義されているすべての記述子フィールドをドライバーで定義されたフィールドも、アプリケーションにアクセスします。  
  
 **SQLGetDescRec**呼び出すデータ型に影響する複数の記述子フィールドの設定と列またはパラメーターのデータのストレージを取得することができます。
