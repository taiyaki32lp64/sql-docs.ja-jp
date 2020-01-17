---
title: 記述子を明示的に割り当てられた |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- explicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: f590251d-56a6-4d58-a405-9e85e68fbc47
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5808265a9ab70b9947cea64fef790497c7229da8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069927"
---
# <a name="explicitly-allocated-descriptors"></a>明示的に割り当てられた記述子
アプリケーションでは、データベースに接続されている、いつでも接続でのアプリケーション記述子を明示的に割り当てることができます。 ステートメントの属性の処理を使用して、その記述子ハンドルを指定することによって**SQLSetStmtAttr**アプリケーションは、アプリケーションを暗黙的に割り当てられているを対応する代わりにその記述子を使用するドライバーに指示記述子。 アプリケーションでは、別の実装記述子を指定できません。  
  
 アプリケーションでは、1 つ以上のステートメントを使用して、明示的に割り当てられた記述子を関連付けることができます。 アプリケーションが実際には、データベースに接続されている場合にのみ、記述子は、明示的に割り当てられた記述子を指定できます。 アプリケーションまたは解放できます。 このような記述子、明示的に暗黙的にその接続を解放しています。
