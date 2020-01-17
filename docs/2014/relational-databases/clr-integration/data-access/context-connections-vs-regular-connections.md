---
title: 通常の接続とコンテキスト接続 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- context connections [CLR integration]
- regular connections [CLR integration]
ms.assetid: a1dead02-be88-4b16-8cb2-db1284856764
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f4255e17f7cd76cf402c10d84b015a1324d7d6f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874042"
---
# <a name="regular-vs-context-connections"></a>通常の接続とコンテキスト接続
  リモート サーバーに接続している場合は、常に、コンテキスト接続ではなく通常の接続を使用します。 ストアド プロシージャや関数を実行している同一サーバーに接続する必要がある場合は、ほとんどの場合、コンテキスト接続を使用します。 コンテキスト接続には、同一のトランザクション領域で実行され、再認証が不要であるなどの利点があります。  
  
 また、コンテキスト接続を使用すると、通常、パフォーマンスが向上し、リソースの使用が抑えられます。 コンテキスト接続では、TRANSACT-SQL ステートメントを送信し、結果を受信するネットワーク プロトコルとトランスポート層をバイパスして、「直接」サーバーと通信できるように、内のプロセスのみに接続です。 認証プロセスも同様に迂回されます。 次の図に、`SqlClient` マネージド プロバイダーの主要なコンポーネントと、通常の接続を使用する場合とコンテキスト接続を使用する場合の、さまざまなコンポーネント相互の通信方法を示します。  
  
 ![コードのコンテキストと通常の接続のパス。](../../../database-engine/dev-guide/media/clrintdataaccess.gif "コンテキストと通常の接続のコード パス。")  
  
 コンテキスト接続で使用するコード パスは、通常の接続よりも短く、関連するコンポーネントの数も少ないので、サーバーへの要求とサーバーからの結果の取得が通常の接続よりも速くなることが期待できます。 サーバーでのクエリの実行時間は、どちらの接続でも同じです。  
  
 同じサーバーに対して通常の接続を別に開く必要が生じる場合もあります。 たとえば、上で説明されている、コンテキスト接続を使用して制限があり、[標準モードとコンテキスト接続に関する制限事項](context-connections-and-regular-connections-restrictions.md)します。  
  
## <a name="see-also"></a>関連項目  
 [コンテキスト接続](context-connection.md)  
  
  
