---
title: ブロック カーソルの使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 2aad7d6b-216e-47e7-b3cb-f95ad096f21a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 529b71540b4abde5fce868975fcbf2749e31dc8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135541"
---
# <a name="using-block-cursors"></a>ブロック カーソルの使用
ブロック カーソルのサポートは、ODBC 3 に組み込まれています。*x*します。 **SQLFetch** ODBC 3 で呼び出されると、複数行のフェッチに対してのみ使用できます *。x*場合は、ODBC 2 *。x*アプリケーション呼び出し**SQLFetch**単一行、順方向専用カーソルのみが開きます。 ODBC 3 時にします。*x*アプリケーション呼び出し**SQLFetch** 、ODBC 2 *。x*ドライバー、ドライバーをサポートしない限り、1 行を返します、 **SQLExtendedFetch**します。 詳細については、次を参照してください[ブロック カーソル、スクロール可能なカーソル、および下位互換性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)で付録 g:。旧バージョンとの互換性のためのガイドラインをドライバーです。  
  
 ブロック カーソルを使用するアプリケーション行セットのサイズを設定、バインド、行セットのバッファー (前のセクションで説明) に従って、必要に応じてセット SQL_ATTR_ROWS_FETCHED_PTR とし、SQL_ATTR_ROW_STATUS_PTR ステートメント属性、および呼び出し**SQLFetch**または**SQLFetchScroll**を行のブロックをフェッチします。 アプリケーションは行セットのサイズを変更したり、新しい行セットのバッファーをバインド (呼び出して**SQLBindCol**バインド オフセットを指定するか) の行がフェッチされた後も。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [行セット サイズ](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [フェッチされた行の数と状態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData およびブロック カーソル。ブロック カーソル](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
