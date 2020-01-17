---
title: データベースへのアクセスをネットワーク |Microsoft Docs
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
- network database access [ODBC]
- standardizing database access [ODBC], network
ms.assetid: f31dd938-e992-436b-b613-145c23973064
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f8eaebca02ef3987e3613b5dd896e0f7c130086
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938034"
---
# <a name="network-database-access"></a>ネットワーク データベース アクセス
ネットワーク経由でデータベースにアクセスするには、さまざまなコンポーネントをそれぞれから独立しており、下に、プログラミング インターフェイスが存在する必要があります。 次の図は、これらのコンポーネントについて示しています。  
  
 ![ネットワーク経由でデータベースにアクセスするコンポーネント](../../odbc/reference/media/pr04.gif "pr04")  
  
 各コンポーネントの詳細説明に従います。  
  
-   **プログラミング インターフェイス**プログラミング インターフェイスに、アプリケーションによって行われた呼び出しは、このセクションで前述したようです。 これらのインターフェイス (SQL、SQL が埋め込まれたモジュール、およびコールレベル インターフェイス) は、通常は、ANSI または ISO 標準に基づいているが、各 DBMS に一般的に固有です。  
  
-   **Data Stream Protocol**データ ストリーム プロトコルには、DBMS とそのクライアントの間で転送されるデータのストリームがについて説明します。 たとえば、プロトコルは、ストリームの残りの部分に含まれる内容を記述する最初のバイトを必要があります。 SQL ステートメントを実行すると、返されたエラー値、またはデータが返されます。 このフラグは、ストリーム内のデータの残りの部分の形式が決まります。 たとえば、フラグ、2 バイトの整数のエラー コード、2 バイトの整数ではエラー メッセージの長さ、およびエラー メッセージはエラー ストリームが含まれます。  
  
     データのストリーム プロトコルは、論理プロトコルでは、基になるネットワークで使用されるプロトコルに依存しません。 そのため、1 つのデータ ストリームのプロトコルは、多くの異なるネットワークに一般に使用できます。 データ ストリーム プロトコルは、通常ベンダーがおよび、特定の DBMS を使用する最適化されています。  
  
-   **通信メカニズムをプロセス間**プロセス間通信 (IPC) メカニズムは 1 つのプロセス間で通信するプロセスです。 例には、名前付きパイプ、TCP/IP ソケット、および DECnet ソケットが含まれます。 IPC メカニズムの選択は、オペレーティング システムと使用されているネットワークによって制限されます。  
  
-   **ネットワーク プロトコル**ネットワーク プロトコルがネットワーク経由でのデータ ストリームの転送に使用します。 これはデータを実装するために使用される IPC メカニズムをサポートしていますが、プロトコルとファイル転送などの基本的なネットワーク操作をサポートしているストリームし、プリンターの共有のプラミング検討できます。 ネットワーク プロトコルは、NetBEUI、TCP/IP、DECnet、SPX/IPX などされ、各ネットワークに固有です。
