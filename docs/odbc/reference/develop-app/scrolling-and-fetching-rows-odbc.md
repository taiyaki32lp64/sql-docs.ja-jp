---
title: スクロールとフェッチ (ODBC) の行 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- fetches [ODBC], scrollable cursors
- cursors [ODBC], scrollable
- scrolling rows [ODBC]
ms.assetid: c43764cb-5841-4b89-9dc0-984a7488b3c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b326ed0c4e9a196904aa0f5c60b705243ef3bd97
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061581"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>行のスクロールとフェッチ (ODBC)
スクロール可能なカーソルを使用して、アプリケーションが呼び出す**SQLFetchScroll** cursor および fetch の行を配置します。 **SQLFetchScroll**相対スクロールをサポートしています (次へ、prior、および相対*n*行)、絶対のスクロール (first、last、および行の*n*)、およびブックマークで位置指定します。 *FetchOrientation*と*FetchOffset*引数**SQLFetchScroll**次の図に示すように、フェッチする行セットを指定します。  
  
 ![次に、前に、最初と最後の行セットのフェッチ](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **次に、前に、最初と最後の行セットをフェッチしています**  
  
 ![絶対、相対パス、およびブックマークが設定された行セットをフェッチ](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **絶対、相対パス、およびブックマークが設定された行セットをフェッチしています**  
  
 **SQLFetchScroll**指定された行にカーソルを配置し、その行で始まる行セットの行を返します。 指定した行セットには、結果セットの末尾が重なっている場合、部分的な行セットが返されます。 重なっている場合、結果の先頭は、指定した行セットの設定、結果の最初の行セット通常セットが返されます。詳細については、次を参照してください。、 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)関数の説明。  
  
 場合によっては、アプリケーションがすべてのデータを取得せずにカーソルを配置しようとする可能性があります。 たとえば、行が存在するかどうかをテスト、だけせず、ネットワーク経由でその他のデータ行のブックマークを取得したりすること可能性があります。 これを行うには、SQL_RD_OFF に SQL_ATTR_RETRIEVE_DATA ステートメント属性を設定します。 このステートメントの属性の設定に関係なく、ブックマーク列 (存在する場合) にバインドされた変数を常に更新します。  
  
 アプリケーションを呼び出して、行セットの取得が完了したら**SQLSetPos**を行セットの行セットまたは更新の行にある特定の行に配置します。 使用しての詳細については**SQLSetPos**を参照してください[SQLSetPos によるデータの更新](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)します。  
  
> [!NOTE]  
>  ODBC 2 では、スクロールがサポートされています。*x*によってドライバー **SQLExtendedFetch**します。 詳細については、次を参照してください[ブロック カーソル、スクロール可能なカーソル、および下位互換性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)で付録 g:。旧バージョンとの互換性のためのガイドラインをドライバーです。
