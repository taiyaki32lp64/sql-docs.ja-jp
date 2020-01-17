---
title: 記述子ハンドル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application parameter descriptor [ODBC]
- automatically allocated descriptors [ODBC]
- implementation row descriptor [ODBC]
- descriptor handles [ODBC]
- handles [ODBC], descriptor
- implementation parameter descriptor [ODBC]
- apd [ODBC]
- ard [ODBC]
- explicitly allocated descriptors [ODBC]
- ipd [ODBC]
- ird [ODBC]
- application row descriptor [ODBC]
ms.assetid: 7741035c-f3e7-4c89-901e-fe528392f67d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 24e3d4c87f3bc461a339a6cb635d64f20dc73e20
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106161"
---
# <a name="descriptor-handles"></a>記述子ハンドル
A*記述子*SQL ステートメントのパラメーターであるか、結果セットの列を記述するメタデータのコレクションは、アプリケーションまたはドライバーによって表示される (とも呼ばれる、*実装*)。 そのため、記述子では 4 つのロールを入力できます。  
  
-   **アプリケーション パラメーター記述子 (APD)。** アドレス、長さ、C データ型など、SQL ステートメントのパラメーターにバインドされているアプリケーション バッファーについての情報が含まれています。  
  
-   **実装パラメーター記述子 (IPD)。** SQL データ型、長さ、null 値の許容など、SQL ステートメント内のパラメーターについて説明します。  
  
-   **アプリケーションの行記述子 (ARD)。** アドレス、長さ、C データ型などの結果セット内の列にバインドされているアプリケーション バッファーについての情報が含まれています。  
  
-   **実装行記述子 (IRD)。** SQL データ型、長さ、null 値許容属性などの結果セット内の列について説明します。  
  
 (1 つそれぞれの役割を担う) 4 つの記述子は、ステートメントが割り当てられるときに自動的に割り当てられます。 これらと呼ばれます。*記述子を自動的に割り当てられた*とそのステートメントに関連付けられた常にします。 アプリケーションは、の記述子を割り当てることができますも**SQLAllocHandle**します。 これらと呼ばれます。*記述子を明示的に割り当てられた*します。 接続上に割り当てられたされ、これらのステートメントで APD または ARD の役割を実行するには、その接続で 1 つまたは複数のステートメントを関連付けることができます。  
  
 ODBC のほとんどの操作は、記述子の明示的なを使用しなくても、アプリケーションで実行できます。 ただし、記述子では、いくつかの操作の便利なショートカットを提供します。 たとえば、アプリケーションは、バッファーの 2 つの異なるセットからデータを挿入する必要があるとします。 バッファーの最初のセットを使用する繰り返しを呼び出す場合と**SQLBindParameter**内のパラメーターにバインドして、**挿入**ステートメントし、ステートメントを実行します。 バッファーの 2 番目のセットを使用するには、このプロセスを繰り返しますになります。 または、バインディング記述子が 1 つのバッファーの最初のセットをバッファー記述子を別の 2 番目のセットをそのセットアップできます。 バインドのセットの間には、アプリケーションを呼び出すことは単純に**SQLSetStmtAttr** APD としてステートメントを使用して、正しい記述子に関連付けるとします。  
  
 記述子の詳細については、次を参照してください。[型の記述子](../../../odbc/reference/develop-app/types-of-descriptors.md)します。
