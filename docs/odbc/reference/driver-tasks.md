---
title: ドライバーでの処理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], tasks
ms.assetid: 184c795a-c2e8-4d20-9902-12e60b2f0e45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e2ed50ac3f9e914953abdd64907199a5f978af2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915460"
---
# <a name="driver-tasks"></a>ドライバーでの処理
ドライバーによって実行される特定のタスクは次のとおりです。  
  
-   接続して、データ ソースから切断しています。  
  
-   ドライバー マネージャーによってオフ関数のエラーを確認しています。  
  
-   トランザクションを開始します。これは、アプリケーションに対して透過的です。  
  
-   実行のデータ ソースを SQL ステートメントを送信しています。 ドライバーは DBMS 固有の sql; ODBC SQL を変更する必要があります。多くの場合、これは、DBMS に固有の SQL を使用した ODBC で定義されたエスケープ句を置き換えるに制限されています。  
  
-   データを送信し、アプリケーションによって指定されたデータ型を変換する場合など、データ ソースからデータを取得します。  
  
-   ODBC SQLSTATEs DBMS 固有のエラーにマップします。
