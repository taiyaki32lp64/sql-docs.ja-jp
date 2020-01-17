---
title: 標準のゲートウェイ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], gateways
- standard gateways [ODBC]
- gateways [ODBC]
ms.assetid: b8341492-2141-4bab-80bd-f2752223079e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8120f3cda584240b0b58ed5d6758621b18fe44d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070477"
---
# <a name="standard-gateway"></a>標準のゲートウェイ
A*ゲートウェイ*は別のように 1 つの DBMS を原因となるソフトウェアの一部です。 つまり、ゲートウェイ、プログラミング インターフェイス、SQL の文法とデータ ストリームを 1 つの DBMS のプロトコルとプログラミング インターフェイス、SQL の文法に変換されます受け取りデータ ストリームの非表示の DBMS のプロトコル。 たとえば、Microsoft® SQL Server™ を使用するアプリケーション データにアクセスできます DB2 マイクロ Decisionware DB2 ゲートウェイ; 経由この製品により、DB2 から SQL Server のようになります。 ゲートウェイを使用している場合は、ターゲット データベースごとに別のゲートウェイを書き込む必要があります。  
  
 ゲートウェイは、Dbms のアーキテクチャの違いによる制限は、標準化に適した候補では。 ただし、すべての Dbms プログラミング インターフェイスを標準化する場合は、SQL 文法、およびデータ ストリーム プロトコルが DBMS が、標準として選択するのには、1 つの DBMS のでしょうか。 確かに商用の DBMS ベンダーを競合企業の製品を標準化することに同意する可能性はありません。 その場合、標準的なプログラミング インターフェイス、SQL の文法とのデータ ストリーム プロトコルを開発すると、ゲートウェイは必要ありません。
