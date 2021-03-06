---
title: データ プロバイダー |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data providers [ADO]
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 877b9f25-60c4-4ab6-8052-2c28a3849e89
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c3b8a4ac0da80303a63bd62f7b4d6f51faab1fb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692940"
---
# <a name="data-providers"></a>データ プロバイダー
データ プロバイダーは、SQL データベース、インデックス付きのシーケンシャル ファイル、スプレッドシート、ドキュメント ストア、およびメール ファイルなどのデータのさまざまなソースを表します。 プロバイダーは、行セットと呼ばれる共通の抽象化を一様に分布を使用してデータを公開します。  
  
 ADO では、強力で柔軟ないくつかの異なるデータ プロバイダーのいずれかに接続し、指定されたプロバイダーの特定の機能に関係なく、同じプログラミング モデルを公開するためにします。 ただし、各データ プロバイダーは、一意であるためにがデータ プロバイダーによって異なりますが、アプリケーションが ADO と対話する方法。  
  
 機能と、OLE DB Provider for Microsoft SQL Server データベースへのアクセスに使用される、SQL Server の機能が大きく異なるため、Microsoft OLE DB Provider for ファイルへのアクセスに使用されるインターネット Publishing はたとえば、Web サーバーに保存します。
