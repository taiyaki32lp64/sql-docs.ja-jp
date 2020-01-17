---
title: マルチ スレッド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], thread-safe
- thread-safe drivers [ODBC]
- multithreaded applications [ODBC]
ms.assetid: cdfebdf5-12ff-4e28-8055-41f49b77f664
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1eaa07ce22436bc8bfae215c0431480081ee0f06
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086352"
---
# <a name="multithreading"></a>マルチスレッド
マルチ スレッドのオペレーティング システムでは、ドライバーは、スレッド セーフである必要があります。 つまり、アプリケーションは 1 つ以上のスレッドで同じハンドルを使用する場合があります。 ドライバーに固有では、これを実現する方法と、ドライバーがしようとすると同時に 2 つの異なるスレッドで同じハンドルを使用するシリアル化する可能性があります。  
  
 通常、アプリケーションは、非同期処理ではなく複数のスレッドを使用します。 アプリケーションは、別のスレッドを作成します。、ODBC 関数を呼び出すおよびメイン スレッドで処理を続行します。 ではなく、非同期関数を常にポーリングする場合、SQL_ATTR_ASYNC_ENABLE ステートメント属性を使用する場合と同様、アプリケーションは、[完了] 新しく作成されたスレッドを単にさせることができます。  
  
 ステートメント ハンドルをそのまま使用し、1 つのスレッドで実行している関数を呼び出すことでキャンセルできます**SQLCancel**同じステートメントでは、別のスレッドから処理します。 ドライバーの使用をシリアル化しないが**SQLCancel** 、この方法で保証はありません呼び出す**SQLCancel**他のスレッドで実行されている関数が実際にキャンセルされます。
