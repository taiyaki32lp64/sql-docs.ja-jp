---
title: コミット モードの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a43a78ad9453f65d9b12595851bd622f720b409a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094223"
---
# <a name="setting-the-commit-mode"></a>コミット モードの設定
アプリケーションでは、SQL_ATTR_AUTOCOMMIT 接続属性を持つ、トランザクション モードを指定します。 既定では ODBC トランザクション自動コミット モードでは (場合を除き、 **SQLSetConnectAttr**と**SQLSetConnectOption**はサポートされていませんはほとんどありません)。 自動コミット モードに手動コミット モードから自動的に切り替え、接続での任意の開いているトランザクションをコミットします。
