---
title: ブックマークによるスクロール |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
- scrolling rows [ODBC]
ms.assetid: 4862f098-41a4-4bd2-894e-f71bb97f9bc0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d27c46407e2994960af4f6abddd6cdc6f08ec852
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055538"
---
# <a name="scrolling-by-bookmark"></a>ブックマークによるスクロール
持つ行をフェッチするときに**SQLFetchScroll**アプリケーションは、開始行を選択するため、単位としてブックマークを使用することができます。 これは、現在のカーソルの位置に依存しないので、絶対アドレスの形式になります。 アプリケーションの呼び出し、ブックマークが設定された行にスクロールする**SQLFetchScroll**で、 *FetchOrientation* SQL_FETCH_BOOKMARK の。 この操作には、SQL_ATTR_FETCH_BOOKMARK_PTR ステートメント属性によって示されるブックマークが使用されます。 結果として、そのブックマークによって識別される行で始まる行セットが返されます。 アプリケーションでこの操作のオフセットを指定することができます、 *FetchOffset*への呼び出しの引数**SQLFetchScroll**します。 内の数を追加することで返された行セットの最初の行が決定されますオフセットを指定した場合、 *FetchOffset*ブックマークによって識別される行の数の引数。 このように使用、 *FetchOffset* ODBC 2 を使用すると、引数がサポートされていません *。x*ドライバーは、アプリケーションを呼び出すと**SQLFetchScroll** 、ODBC 2 *。x*ドライバー *FetchOrientation*に SQL_FETCH_BOOKMARK、設定、 *FetchOffset*引数を 0 に設定する必要があります。
