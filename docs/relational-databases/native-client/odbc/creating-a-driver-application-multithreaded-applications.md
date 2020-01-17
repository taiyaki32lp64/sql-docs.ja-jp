---
title: マルチスレッドアプリケーション |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- threads [SQL Server], multithreaded applications
- ODBC applications, multithreaded applications
- asynchronous operations [SQL Server Native Client]
- SQL Server Native Client ODBC driver, multithreaded applications
- multithreaded applications [SQL Server Native Client]
ms.assetid: d352c91a-6e08-4e50-9f3e-a37892d9c2cc
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e7a2a778f4af4c39e53942401e0de93997afbb64
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761249"
---
# <a name="creating-a-driver-application---multithreaded-applications"></a>ドライバー アプリケーションの作成 - マルチスレッド アプリケーション
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーはマルチスレッド ドライバーです。 マルチスレッド アプリケーションは、非同期呼び出しを使用して複数の ODBC 呼び出しを処理するための代替手段として作成されます。 あるスレッドが同期 ODBC 呼び出しを実行すると、その呼び出しへの応答を待機するために最初のスレッドがブロックされている間に、他のスレッドの処理を実行できます。 このモデルは、ネットワーク トラフィックなどのオーバーヘッドが取り除かれるので、非同期呼び出しを実行するよりも効率的です。また、ODBC 関数を繰り返し呼び出して SQL_STILL_EXECUTING が返されるかどうかをテストするよりも効率的です。  
  
 それでも、非同期モードは、依然として効果的な処理方法です。 マルチスレッド モデルによるパフォーマンスの向上は、非同期アプリケーションを書き直すほどのものではありません。 ユーザーが DB-Library 非同期モデルを使用する DB-Library アプリケーションを ODBC アプリケーションに変換する場合は、ODBC 非同期モデルに変換する方が容易です。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client ODBC ドライバー アプリケーションの作成](../../../relational-databases/native-client/odbc/creating-a-driver-application.md)  
  
  
