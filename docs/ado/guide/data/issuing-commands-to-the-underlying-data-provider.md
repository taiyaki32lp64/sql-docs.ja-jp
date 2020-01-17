---
title: 基になるデータ プロバイダーへのコマンドの発行 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02a861daa78b798c1b19b5fc2607cfcaf0ce5968
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924946"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>基になるデータ プロバイダーにコマンドを発行する
図形で始まらない任意のコマンドは、データ プロバイダーに渡されます。 これは、「図形 {0} プロバイダー コマンド}」形式での図形のコマンドを実行するのと同じです。 これらのコマンドは*いない*を生成する必要がある、**レコード セット**します。 たとえば、"形状 {ドロップ テーブル MyTable} は完全に有効な図形コマンドでは、データ プロバイダーは、DROP TABLE をサポートするいると仮定した場合です。  
  
 この機能により、通常プロバイダー コマンドと同じ接続とトランザクションを共有する図形のコマンドの両方ができます。  
  
## <a name="see-also"></a>関連項目  
 [データ シェイプの例](../../../ado/guide/data/data-shaping-example.md)   
 [Shape の正式文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般的な Shape コマンド](../../../ado/guide/data/shape-commands-in-general.md)
