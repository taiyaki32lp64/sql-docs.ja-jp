---
title: テーブル サイズの見積もり | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- pages [SQL Server], space
- space [SQL Server], tables
- row size [SQL Server]
- size [SQL Server], tables
- column size [SQL Server]
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- clustered indexes, table size
- disk space [SQL Server], tables
- space allocation [SQL Server], table size
- designing databases [SQL Server], estimating size
- reserved free rows per page [SQL Server]
- calculating table size
ms.assetid: 15c17c92-616f-402e-894b-907a296efe5f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 403e0af44fc1db7efaf674d02ed0e3b94e81a5b6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62916876"
---
# <a name="estimate-the-size-of-a-table"></a>テーブル サイズの見積もり
  次の手順を実行して、テーブルにデータを格納するために必要な領域を見積もることができます。  
  
1.  「 [ヒープ サイズの見積もり](estimate-the-size-of-a-heap.md) 」または「 [クラスター化インデックスのサイズの見積もり](estimate-the-size-of-a-clustered-index.md)」の説明に従って、ヒープまたはクラスター化インデックスに必要な領域を計算します。  
  
2.  「 [非クラスター化インデックスのサイズの算出](estimate-the-size-of-a-nonclustered-index.md)」に記載されている手順に従って、非クラスター化インデックスごとに必要な領域を計算します。  
  
3.  手順 1. と手順 2. で計算した値を加算します。  
  
## <a name="see-also"></a>関連項目  
 [データベース サイズの見積もり](estimate-the-size-of-a-database.md)   
 [ヒープ サイズの見積もり](estimate-the-size-of-a-heap.md)   
 [クラスター化インデックスのサイズの見積もり](estimate-the-size-of-a-clustered-index.md)   
 [非クラスター化インデックスのサイズの算出](estimate-the-size-of-a-nonclustered-index.md)  
  
  
