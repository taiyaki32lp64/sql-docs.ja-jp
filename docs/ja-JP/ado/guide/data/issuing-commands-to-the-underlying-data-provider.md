---
title: 基になるデータ プロバイダーにコマンドを発行する |Microsoft ドキュメント
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f217bd606dbc61db26430840c3b8dcdb79274d9d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>基になるデータ プロバイダーにコマンドを発行します。
図形で始まっていない任意のコマンドは、データ プロバイダーにを介して渡されます。 これは、"SHAPE {プロバイダー コマンド}"の形式で図形コマンドの発行に相当します。 これらのコマンドは*いない*を生成する必要がある、**レコード セット**です。 たとえば、"図形 {ドロップ テーブル MyTable} は完全に有効な図形コマンドでは、データ プロバイダーは、DROP TABLE をサポートするいると仮定した場合です。  
  
 この機能は、通常のプロバイダー コマンドと同じ接続とトランザクションを共有する図形コマンドの両方をによりします。  
  
## <a name="see-also"></a>参照  
 [データ シェイプの例](../../../ado/guide/data/data-shaping-example.md)   
 [図形の正式な文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般的な Shape コマンド](../../../ado/guide/data/shape-commands-in-general.md)