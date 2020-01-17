---
title: 機能のサポートと可変性の確認 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: ff45f220-9b8b-4c44-82f8-a8e9913fffea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 21495e538a554a477336d1a92926c11fe762c5af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062660"
---
# <a name="checking-feature-support-and-variability"></a>機能のサポートと可変性の確認
アプリケーションの通常の呼び出し機能のサポートと可変性を確認する**SQLGetInfo**、 **SQLGetFunctions**、および**SQLGetTypeInfo**します。 開始点としては、ドライバーの API と SQL 文法の適合性レベルです。 これらには、さまざまなレベルの機能サポートについて説明します。 アプリケーションを呼び出して**SQLGetInfo**サポートまたは必要な機能のばらつきを判断するには、他のオプションと**SQLGetFunctions**を決定する関数かどうか、返されたを超える必要があります準拠レベルはサポートされていると**SQLGetTypeInfo**をどのような SQL データ型がサポートされているかを判断します。  
  
 アプリケーションが呼び出すことによって、ステートメントまたは接続属性がサポートされているかどうかを判断することができます**SQLSetStmtAttr**または**SQLSetConnectAttr**属性を持つ。 関数が SQL_SUCCESS または SQL_SUCCESS_WITH_INFO を返す場合、属性はサポートされています。SQLSTATE HYC00 SQL_ERROR を返す場合 (省略可能な機能は実装されていません)、属性がサポートされていません。  
  
 アプリケーションには、呼び出すことによって、ドライバーに接続する前に、限られた量が決定することも**SQLDrivers**します。
