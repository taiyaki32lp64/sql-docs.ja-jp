---
title: 状態遷移の確認 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b337d317092ad6ae20cc91236d69c1314de96bce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107284"
---
# <a name="state-transition-checks"></a>状態遷移の確認
ドライバー マネージャーは、環境、接続、またはステートメントの状態が呼び出される関数に適していることを確認します。 などの接続が割り当て済みである必要があります状態**SQLConnect**が呼び出されます。 ステートメントが準備済みである必要があります状態**SQLExecute**が呼び出されます。 ドライバー マネージャーは、状態遷移のエラーの SQL_ERROR を返します。
