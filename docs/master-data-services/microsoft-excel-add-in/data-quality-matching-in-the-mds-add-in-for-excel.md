---
title: Excel 用 MDS アドインでのデータ品質照合 | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: be78d051-0d56-46d3-bb89-327e218dadd6
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 32e22f93dff6edb90c89896fca3495d27ac34dc0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68092398"
---
# <a name="data-quality-matching-in-the-mds-add-in-for-excel"></a>Excel 用 MDS アドインでのデータ品質照合

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  後で、MDS リポジトリにさらにデータを追加する場合があります。 データを追加する前に、新しいデータと既に MDS で管理されているデータを比較することは、重複するデータや不正確なデータの追加を避けるために役立ちます。  
  
 MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の Data Quality Services (DQS) 機能を使用して、類似するデータを照合します。 アドインの照合機能を使用すると、類似するレコードがグループ化され、結果の精度を表すスコアが表示されます。 DQS によって提供される照合機能の詳細については、「 [データ照合](../../data-quality-services/data-matching.md)」を参照してください。  
  
## <a name="workflow-for-data-quality-matching"></a>データ品質照合のワークフロー  
 MDS [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]で DQS を使用する場合、次のワークフローを使用します。  
  
1.  MDS によって管理されるデータの一覧を取得して、MDS によって管理されていないデータの一覧と結合します。 詳細については、「 [データの結合 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md)」を参照してください。  
  
2.  DQS ナレッジを使用して、結合した一覧のデータを比較します。 詳細については、「 [類似データの照合 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)」を参照してください。  
  
3.  DQS で見つかった類似性について詳細を確認するには、詳細列を表示します。  
  
4.  結果を確認し、MDS リポジトリに追加する必要があるデータと重複しているデータを判別します。  
  
5.  新しいデータと更新されたデータを MDS リポジトリにパブリッシュします。  
  
## <a name="knowledge-bases"></a>ナレッジ ベース  
 アドインで提供される照合結果は、DQS ナレッジ ベースに基づいています。  
  
-   既定のナレッジ ベース (DQS データ) は、DQS のインストール時に作成されます。 (Data Quality Client で既定のナレッジ ベースに照合ポリシーを追加せずに) 既定のナレッジ ベースを使用する場合は、ワークシート内の列をナレッジ ベース内のドメインにマップしてから、選択したドメインに重み値を割り当てる必要があります。  
  
-   Data Quality Client を使用して、照合ポリシーと共にナレッジ ベースを作成するか、既定のナレッジ ベースに照合ポリシーを追加することができます。 この場合、重み値は既に作成済みの照合ポリシーによって決定されるので、列をドメインにマップするだけで済みます。 詳細については、「 [Create a Matching Policy](../../data-quality-services/create-a-matching-policy.md)」をご参照ください。  
  
 サポート技術情報の詳細については、「 [DQS のナレッジ ベースとドメイン](../../data-quality-services/dqs-knowledge-bases-and-domains.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|外部データを MDS によって管理されるデータと結合して、比較できるようにします。|[データの結合 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md)|  
|DQS ナレッジを使用して、データの類似性を見つけます。|[類似データの照合 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [概要:Excel からデータをインポートする&#40;MDS アドインの Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [データ照合](../../data-quality-services/data-matching.md)  
  
  
