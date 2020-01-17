---
title: SQLDescribeCol および SQLColAttribute |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], and SQLDescribeCol
- SQLDescribeCol function [ODBC], and SQLColAttribute
- result sets [ODBC], metadata
- retrieving result set meta data [ODBC]
- metadata [ODBC], result set
ms.assetid: c2ca442c-03a8-4e0f-9e67-b300bb15962f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d602368475c6f1326cc615453116e898b1c1892f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107444"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol および SQLColAttribute
**SQLDescribeCol**と**SQLColAttribute**結果セットのメタデータの取得に使用されます。 これら 2 つの関数の違いは**SQLDescribeCol**同じの 5 つの中の情報 (列の名前、データ型、有効桁数、スケール、および null 値許容属性) は常に返します**SQLColAttribute** 、単一のアプリケーションによって要求された情報を返します。 ただし、 **SQLColAttribute**列の大文字小文字の区別を含む、メタデータの豊富な機能の選択範囲を返す、サイズ、更新、および検索機能を表示できます。  
  
 特に、データのみが表示される、多くのアプリケーションによって返されるメタデータのみを必要と**SQLDescribeCol**します。 これらのアプリケーションが高速化を使用する**SQLDescribeCol**より**SQLColAttribute**情報が 1 回の呼び出しで返されるためです。 特に、データを更新する他のアプリケーションによって返される追加のメタデータを必要と**SQLColAttribute**のため両方の関数を使用します。 さらに、 **SQLColAttribute**ドライバー固有のメタデータをサポートしています。 詳細については、次を参照してください。[ドライバー固有のデータ型、記述子の種類、情報の種類、診断型、および属性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)します。  
  
 アプリケーションは、ステートメントが準備または実行された後で、結果セットの上にあるカーソルが閉じられる前であればいつでも結果セットのメタデータを取得できます。 ステートメントが準備されてから実行されるまでの間に、結果セットのメタデータを必要とするアプリケーションはほとんどありません。 可能であれば、アプリケーションではステートメントが実行されるまでメタデータの取得を待機する必要があります。データソースによっては、準備済みステートメントのメタデータを返すことができず、ドライバーでこの機能をエミュレートするのには時間がかかる場合が多いためです。 例えば、ドライバーは **SELECT** ステートメントの **WHERE** 句を **WHERE 1 = 2** 句に置き換えて、結果のステートメントを実行することによって、0 行の結果セットを生成することがあります。  
  
 メタデータは、データ ソースから取得する高価な多くの場合。 このため、ドライバーは、サーバーから取得するメタデータの結果の上にカーソルが設定されている限り開いている保持をキャッシュする必要があります。 また、アプリケーションでは、絶対に必要なメタデータのみを要求する必要があります。
