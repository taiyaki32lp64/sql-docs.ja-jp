---
title: 同時実行モデル (Visual FoxPro ODBC ドライバー) のサポート |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 597d1022fa6946e0ae768cb9600a3f4534c67a25
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080689"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>サポートされているコンカレンシー モデル (Visual FoxPro ODBC ドライバー)
Visual FoxPro ODBC ドライバーをサポートしています*読み取り専用の同時実行*します。 アプリケーションが呼び出すことができます[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) SQL_CONCUR_READ_ONLY の SQL_CONCURRENCY オプションを使用します。  
  
 詳細についてを参照してください、 [ODBC プログラマーズ リファレンス](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="read-only-concurrency"></a>読み取り専用の同時実行  
 カーソルは更新できません。  
  
## <a name="row-versioning"></a>行のバージョン管理 (row versioning)  
 基本的にタイムスタンプ サポート、更新時にでは、行のバージョンを比較します。
