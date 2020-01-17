---
title: ハードウェア構成
description: Analytics Platform System (APS) アプライアンスハードウェアは、ビジネス要件に応じて適切な量の処理とストレージを購入できるように、スケーラブルなユニットを使用して構築されています。 アプライアンスは、並列データウェアハウスのストレージを数テラバイトから6ペタバイトを超えるデータにスケーリングします。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ee16045931da345f06c141597ccd25d19a36dea7
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401132"
---
# <a name="hardware-configurations---analytics-platform-system"></a>ハードウェア構成-分析プラットフォームシステム
Analytics Platform System (APS) ハードウェアは、ビジネス要件に応じて適切な量の処理とストレージを購入できるように、スケーラブルなユニットを使用して構築されています。 アプライアンスは SQL Server Parallel Data Wareouse (PDW) 用のストレージを数テラバイトから6ペタバイトを超えるデータにスケーリングします。  
  
## <a name="contents"></a>内容  
  
-   [1つのラック構成](#section1)  
  
-   [マルチラック構成](#section2)  

  
## <a name="section1"></a>1つのラック構成  
アプライアンスの最初のラックには、PDW を実行するために必要なコンポーネントが含まれています。 最小アプライアンス構成は、ラックとネットワークに基本スケールユニットを加えたものです。 これらの図は、アプライアンスの最初のラックを構成できる方法を示しています。 ハードウェアベンダーによっては、最初のラックに 2 ~ 9 個のコンピューティングノードを含めることができます。  
  
### <a name="first-rack-configurations---dell"></a>最初のラック構成-DELL  
DELL アプライアンスの最小構成には、3つのコンピューティングノードがあります。 1つ目のラックに最大2つのデータスケールユニットを追加して、合計9個のコンピューティングノードを作成することができます。  
  
![Dell の最初のラック構成](media/first-rack-configurations-dell.png "Dell の最初のラック構成")  
  
### <a name="first-rack-configurations---hpe"></a>最初のラック構成-HPE  
HPE アプライアンスの最小構成には、2つのコンピューティングノードがあります。 1つ目のラックに最大3つのデータスケールユニットを追加して、合計8個のコンピューティングノードを作成することができます。  
  
![Hpe の HPE の最初のラック構成](media/first-rack-configurations-hpe.png "HPE の最初のラック構成")  
  
## <a name="section2"></a>マルチラック構成  
PDW に容量を追加するには、必要に応じて追加のラック & ネットワークコンポーネントと共にデータスケールユニットを追加して、適切な電源、ネットワーク、およびラックのインフラストラクチャを提供できます。 各追加のラック & には、パッシブホストが必要です。  
  
各ハードウェアベンダーは、アプライアンスの容量を指定して、追加できるデータスケールユニットの数を指定します。 少なくとも20% のパフォーマンスへのアップグレードを確認するには、十分なデータスケールユニットを追加することをお勧めします。 たとえば、既に20個のデータスケールユニットを持つアプライアンスに1つのデータスケールユニットを追加すると、パフォーマンスが低下する可能性があります。 純利益は、コストと労力に価値がありません。  
  
### <a name="scale-out-example---hpe"></a>Scale out の例-HPE  
この図は、20個のコンピューティングノードを含む3つのラック HP アプライアンスを示しています。  
  
![20個のコンピューティングノードを持つ HPE アプライアンス](media/scale-out-hpe.png "20個のコンピューティングノードを持つ HPE アプライアンス")  
  
### <a name="scale-out-example---dell-quanta"></a>Scale Out の例-DELL、クォンタム  
この図は、21個のコンピューティングノードを含む3ラックの DELL またはクォンタムのアプライアンスを示しています。  
  
![21個のコンピューティングノードを含む Dell アプライアンス](media/scale-out-dell.png "21個のコンピューティングノードを含む Dell アプライアンス")  
 
