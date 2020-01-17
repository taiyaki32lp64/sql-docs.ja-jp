---
title: トランザクション分離レベルの設定 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: 64a037f0-5065-4f45-9669-6710404a540c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e59db823f8b84edfb5c92f2d142c8238449e3323
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107580"
---
# <a name="setting-the-transaction-isolation-level"></a>トランザクション分離レベルの設定
トランザクション分離レベルを設定するには、アプリケーションは、SQL_ATTR_TXN_ISOLATION 接続属性を使用します。 データ ソースが要求された分離レベルをサポートしていない場合、ドライバーまたはデータ ソースはより高いレベルを設定できます。 どのようなトランザクション分離レベルでデータ ソースを決定するをサポートし、既定の分離レベルは、アプリケーションを呼び出す**SQLGetInfo** SQL_TXN_ISOLATION_OPTION と SQL_DEFAULT_TXN_ISOLATION オプションそれぞれします。  
  
 トランザクション分離レベルは、データベースのデータの整合性を最大限に保護を提供します。 シリアル化可能なトランザクションはできない他のトランザクションによって影響を受けることが保証し、データベースの整合性を維持するために保証します。  
  
 ただしより高いレベルのトランザクション分離はアプリケーションがリリースされるデータのロックを待機する必要がある機会が増えるためパフォーマンスが低下を生じることができます。 アプリケーションでは、次の場合にパフォーマンスを向上する分離のレベルを指定できます。  
  
-   場合ことを保証できる他のトランザクションが存在しないことは、アプリケーションのトランザクションに干渉する可能性があります。 このような状況では、小規模な会社の 1 人のユーザーが 1 台のコンピューターの個人データを含む dBASE ファイルを保持する場合など、限られた環境でのみが発生し、これらのファイルを共有しません。  
  
-   速度が精度およびすべてのエラーよりもより重要な場合は、小さい可能性があります。 たとえば、会社、多くの小規模な販売することとの大きな売り上げはまれであるとします。 開いているすべての売上の合計値を推定するトランザクションでは、Read Uncommitted 分離レベルを安全に使用可能性があります。 トランザクションが開かれたり閉じられたりするは、その後、注文が含まれますがロールバックし、これらは通常どうしし、ことが、このような順序が発生するたびにブロックされていないために、トランザクションがはるかに高速になります。  
  
 詳細については、次を参照してください。[オプティミスティック同時実行制御](../../../odbc/reference/develop-app/optimistic-concurrency.md)します。
