---
title: パラメーター値の配列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 9b572c5b-1dfe-40af-bebd-051548ab6d90
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1e65928cd078a3f05032f4e4fb400e3e2eb1f27a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077069"
---
# <a name="arrays-of-parameter-values"></a>パラメーター値の配列
アプリケーション パラメーターの配列を渡すと便利です。 などのパラメーターとパラメーター化された配列を使用して**挿入**ステートメントでは、アプリケーションでは、行の数を一度に挿入できます。 配列を使用するいくつかの利点があります。 最初に、(データ ソースでは、パラメーター配列はネイティブにサポートしている) 場合、ステートメントの多くのデータが 1 つのパケットで送信されるため、ネットワーク トラフィックが減少します。 次に、一部のデータ ソースには、配列を同じ数の個別の SQL ステートメントを実行するよりも高速化を使用して SQL ステートメントを実行できます。 最後に、画面のデータのケースでは多くの場合に、配列内のデータが格納されている場合、アプリケーションでバインドできますすべての行に単一の呼び出しで、特定の列**SQLBindParameter**し、1 つのステートメントを実行して更新します。  
  
 残念ながら、多くのデータ ソースは、パラメーター配列をサポートします。 ただし、ドライバーはパラメーター値のセットごとに、SQL ステートメントを実行することによって、パラメーター配列をエミュレートできます。 これは、ドライバーは、パラメーター セットごとに 1 回実行することを計画するステートメントを準備できますし、ために、速度の増加につながることができます。 単純なアプリケーション コードにも生じる可能性があります。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [パラメーターのバインディング配列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [パラメーターの配列の使用](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
