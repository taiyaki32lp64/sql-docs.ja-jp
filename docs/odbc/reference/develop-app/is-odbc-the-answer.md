---
title: ODBC が正解ですか? | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], ODBC
ms.assetid: bfa5e6ee-5979-42a9-be6f-a84d1ee7a54c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e325793a7b703c445be836f6f427645acda3370
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138849"
---
# <a name="is-odbc-the-answer"></a>ODBC が正解ですか?
相互運用性の問題を詳しく調べる前に、次の質問を考慮してください。必要があります、アプリケーションを使用して ODBC まったくでしょうか。 ODBC でのガイド、奇妙な疑問があるかもしれませんが、実際には、正当な 1 つ。 ODBC は、ネイティブ データベース Api を完全に置き換える設計されていません。 またそれがすべての環境でデータベースへのアクセスを提供するように設計。 データベースに共通のインターフェイスを提供するように設計されたし、アプリケーション プログラマの詳細を複数のデータベースへのリンクを管理することから解放するためのものがします。  
  
 カスタム アプリケーションは、ネイティブ データベース Api の主要な候補です。 主な理由は、カスタム アプリケーションが多くの場合、1 つの DBMS を使用し、相互運用できるようにする必要があるないことです。 ネイティブ データベース Api は特定の DBMS の機能を公開する ODBC よりも優れたジョブを実行して、ODBC によって公開されない機能を公開する可能性があります。 さらに、カスタム アプリケーションの開発者を通常に、DBMS のネイティブのデータベース API を使い慣れているため、理由はほとんどありませんを ODBC を参照してください。 ただし、一部の Dbms のことと、ODBC は、ネイティブ データベース API に注意してください。 興味深いは。  
  
 したがってアプリケーション ODBC の候補となるでしょうか。 最適な候補は、1 つ以上の DBMS を使用するアプリケーションです。 これには、ジェネリックと垂直方向のほぼすべてのアプリケーションが含まれます。 多数のカスタム アプリケーションも含まれています。 たとえば、いくつかの異なる Dbms を使用するカスタム アプリケーションは、はるかに簡単で、複数のネイティブ Api を使用したよりも ODBC を使って記述するクリーナーです。 ODBC で記述されたカスタム アプリケーションが簡単に移行するように 1 つの DBMS 間を移動する、会社やさまざまな Dbms に対して同じアプリケーションをデプロイします。
