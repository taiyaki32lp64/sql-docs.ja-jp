---
title: ODBC アーキテクチャ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], components
- ODBC architecture [ODBC]
ms.assetid: 2604f492-587b-4a51-9876-59a7870b3ef2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 781a214d3ca059a442680c332d79aad48914976c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111222"
---
# <a name="odbc-architecture"></a>ODBC アーキテクチャ
ODBC アーキテクチャでは、次の 4 つのコンポーネントがあります。  
  
-   **アプリケーション**SQL ステートメントを送信し、結果を取得する処理と呼び出しの ODBC 関数を実行します。  
  
-   **ドライバー マネージャー**読み込みとアンロードのドライバー、アプリケーションの代わりです。 プロセスの ODBC 関数では、呼び出しまたはドライバーに渡します。  
  
-   **ドライバー**プロセス ODBC 関数呼び出し、特定のデータ ソースへの SQL 要求を送信して、アプリケーションに結果を返します。 必要に応じて、ドライバーは、要求が関連付けられている DBMS でサポートされる構文に準拠しているように、アプリケーションの要求を変更します。  
  
-   **データ ソース**にアクセスし、次のように関連付けられているオペレーティング システム、DBMS のデータから構成されています。 ユーザーが、(ある場合) のネットワーク プラットフォーム、DBMS にアクセスするために使用します。  
  
 ODBC アーキテクチャについては、次の点に注意してください。 これにより、アプリケーションは同時に 1 つ以上のデータ ソースからデータにアクセスする最初では、複数のドライバーとデータ ソースが存在できます。 2 つの場所で ODBC API を使用する 2 番目に、: アプリケーションと、ドライバー マネージャーの間、およびドライバー マネージャーと各ドライバー間。 ドライバー マネージャーとドライバーの間のインターフェイスとして呼ば、*サービス プロバイダー インターフェイス、* または*SPI*します。 ODBC では、アプリケーション プログラミング インターフェイス (API) と、サービス プロバイダー インターフェイス (SPI) は、同じです。つまり、ドライバー マネージャーと各ドライバーは、同じ関数を同じインターフェイスを持っています。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [アプリケーション](../../odbc/reference/applications.md)  
  
-   [ドライバー マネージャー](../../odbc/reference/the-driver-manager.md)  
  
-   [ドライバー](../../odbc/reference/drivers.md)  
  
-   [データ ソース](../../odbc/reference/data-sources.md)
