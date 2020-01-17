---
title: 作成して、スレッドの終了 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b97f29ad06c4ed961f3cee571b0ca7b8d9c0b774
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002084"
---
# <a name="creating-and-terminating-threads"></a>スレッドの作成と終了
ODBC を使用するマルチ スレッド アプリケーションは、Microsoft® Visual で呼び出す必要がありますC++® ランタイム ライブラリ関数 **_beginthread**と **_endthread** (または **_beginthreadex**と **_endthreadex**) を作成して、ODBC ドライバー マネージャーを呼び出すスレッドを終了します。 アプリケーションが Microsoft Windows NT® 関数を呼び出す場合**CreateThread**と**EndThread**代わりに、ドライバー マネージャーと一部の ODBC ドライバーは、C ランタイムを呼び出すため、リークが発生するメモリ関数呼び出すことによって作成されたスレッドでは機能しません**CreateThread**します。 詳細については、Microsoft Windows® ドキュメントを参照してください。
