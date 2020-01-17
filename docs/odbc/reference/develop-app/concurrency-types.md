---
title: 同時実行の種類 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- locking concurrency control [ODBC]
- optimistic concurrency [ODBC]
- read-only concurrency control [ODBC]
ms.assetid: 46762ae5-17dd-4777-968e-58156f470fe1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 63d7c7dce51fe4f514232cfd0d5ae2e5abeb5b70
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083181"
---
# <a name="concurrency-types"></a>コンカレンシーの種類
削減カーソルの同時実行の問題を解決するためには、ODBC は、4 種類のカーソルの同時実行を公開します。  
  
-   **読み取り専用**カーソルからデータを読み取ることができますが、更新ことはできません、またはデータを削除します。 これは、既定の同時実行の種類です。 DBMS は、Repeatable Read と Serializable 分離レベルを適用する行をロックが書き込みロックではなく読み取りロックを使用できます。 これは、結果、他のトランザクションは、データを読み取るには少なくともできるため、高い同時実行性。  
  
-   **ロック**カーソルは更新または削除の結果セット内の行かどうかを確認するために必要なロックの最下位のレベルを使用します。 通常、この結果、Repeatable Read および Serializable トランザクション分離レベルで特に、非常に低い同時実行レベル。  
  
-   **行のバージョンを使用してオプティミスティック同時実行とオプティミスティック同時実行制御の値を使用して**カーソルはオプティミスティック同時実行制御を使用します。更新または最後の読み取り以降に変更されていない場合にのみ行を削除します。 変更を検出するために行バージョンまたは値を比較します。 カーソルは更新または行を削除できるようになりますが、同時実行がロックを使用する場合よりも大幅に上回ってことの保証はありません。 詳細については、次のセクションを参照してください。[オプティミスティック同時実行制御](../../../odbc/reference/develop-app/optimistic-concurrency.md)します。  
  
 アプリケーションでは、また、ステートメント属性 SQL_ATTR_CONCURRENCY を使用するカーソルが同時実行の種類を指定します。 呼び出しがサポートされる種類を判断する**SQLGetInfo** SQL_SCROLL_CONCURRENCY オプションを使用します。
