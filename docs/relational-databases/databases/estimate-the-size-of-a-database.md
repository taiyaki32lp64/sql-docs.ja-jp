---
title: データベース サイズの見積もり | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- space allocation [SQL Server], database size
- calculating database size
- increasing database size
- database size [SQL Server], estimating
- predicting database size
- size [SQL Server], databases
- estimating database size
- designing databases [SQL Server], estimating size
ms.assetid: 5b240161-eba4-44b0-946c-61a8fc00fc8c
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9a11d6d83b4c2c56d6448431028beec89265a0d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67934481"
---
# <a name="estimate-the-size-of-a-database"></a>データベース サイズの見積もり
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  データベースをデザインするときは、データを格納したときにデータベースのサイズがどのくらい大きくなるかを見積もる必要性が生じる場合があります。 データベースのサイズを見積もると、次の目的に必要なハードウェア構成の決定に役立ちます。  
  
-   アプリケーションが必要とするパフォーマンスの実現。  
  
-   データとインデックスの格納に必要となる適切な量の物理ディスク領域の確保。  
  
 データベースのサイズを見積もると、データベースのデザインを改良する必要があるかどうかを判断する場合にも役立ちます。 たとえば、見積もったデータベースのサイズが大きすぎて組織内で実装できず、正規化の必要性があるとわかる場合があります。 逆に、見積もったサイズが予想より小さい場合もあります。 この場合は、データベースを非正規化してクエリのパフォーマンスを向上させることができます。  
  
 データベースのサイズを見積もるには、各テーブルのサイズを個別に見積もり、それぞれの値を合計します。 テーブルのサイズは、テーブルにインデックスが含まれているかどうかにより異なり、インデックスが含まれている場合はそのインデックスの種類によって異なります。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[テーブル サイズの見積もり](../../relational-databases/databases/estimate-the-size-of-a-table.md)|テーブルおよび関連付けられたインデックスにデータを格納するために必要な領域を見積もる手順や計算方法について説明します。|  
|[ヒープ サイズの見積もり](../../relational-databases/databases/estimate-the-size-of-a-heap.md)|ヒープにデータを格納するために必要な領域を見積もる手順や計算方法について説明します。 ヒープとは、クラスター化インデックスを含まないテーブルのことです。|  
|[クラスター化インデックスのサイズの見積もり](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)|クラスター化インデックスにデータを格納するために必要な領域を見積もる手順や計算方法について説明します。|  
|[非クラスター化インデックスのサイズの算出](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)|非クラスター化インデックスにデータを格納するために必要な領域を見積もる手順や計算方法について説明します。|  
  
  
