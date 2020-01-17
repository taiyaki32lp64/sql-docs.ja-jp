---
title: 行 (パーティション ウィザード) の制限 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.typefilterexpression.f1
ms.assetid: eec8da8f-eab4-4ac4-a81d-995c814f88ca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 59bff3eac690b7352b75d02bd7b266dfa8f303f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070211"
---
# <a name="restrict-rows-partition-wizard"></a>[行の制限] (パーティション ウィザード)
  **[行の制限]** ページを使用すると、指定したテーブルから取得、集計されて、パーティションに含まれる行を制限できます。  
  
> [!NOTE]  
>  このページは、 **[基になる情報の指定]** ページでテーブルを 1 つ選択した場合にのみ表示されます。  
  
> [!CAUTION]  
>  他のパーティションで使用されている **[基になる情報の指定]** ページの **[使用できるテーブル]** でテーブルを指定した場合は、 **[行の制限]** ページでクエリを指定するか、キューブでリスクの複製データを指定する必要があります。  
  
## <a name="options"></a>および  
 **行を制限するクエリを指定します。**  
 **[クエリ]** ボックスに、行を制限するクエリを入力します。  
  
 このオプションを選択していて **[クエリ]** が空の場合、以前に選択したテーブルからすべての列と行を取得する SQL ステートメントと共に、オプションが設定されます。  
  
 **クエリ**  
 パーティションの処理時に、テーブルから行を取得する場合に使用される SQL ステートメントを、入力または変更します。  
  
> [!IMPORTANT]  
>  WHERE 句を指定することにより、レコードのサブセットをこのパーティションで使用できます。 複数のパーティションが 1 つのファクト テーブルに基づいている場合は、データを複製しないでください。  
  
 **[確認]**  
 **[クエリ]** のステートメントが有効な SQL ステートメントであることを確認します。  
  
## <a name="see-also"></a>関連項目  
 [パーティション (Analysis Services - 多次元データ)](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
