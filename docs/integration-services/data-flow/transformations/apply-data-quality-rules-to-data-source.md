---
title: データ ソースにデータ品質ルールを適用する | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a965e8f2-004d-4ccc-8523-a185b35b26e2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7e81d5b1c85b1a2105e0e9a54c11c63bd5c25344
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291754"
---
# <a name="apply-data-quality-rules-to-data-source"></a>データ ソースにデータ品質ルールを適用する

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Data Quality Services (DQS) を使用して、DQS クレンジング変換をデータ ソースに接続することで、パッケージ データ フロー内のデータを修正できます。 DQS の詳細については、「 [Data Quality Services の概念](../../../data-quality-services/data-quality-services-concepts.md)」を参照してください。 変換の詳細については、「 [DQS クレンジング変換](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)」を参照してください。  
  
 DQS クレンジング変換によってデータを処理すると、データ品質プロジェクトが Data Quality Server に作成されます。 データ品質クライアントを使用してプロジェクトを管理します。 詳細については、「[データ品質プロジェクトを開く、ロックを解除する、名前を変更する、削除する](../../../data-quality-services/open-unlock-rename-and-delete-a-data-quality-project.md)」を参照してください。  
  
### <a name="to-correct-data-in-the-data-flow"></a>データ フロー内のデータを修正するには  
  
1.  パッケージを作成します。  
  
2.  DQS クレンジング変換を追加し、構成します。 詳細については、「 [[DQS クレンジング変換エディター] ダイアログ ボックス](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation-editor-dialog-box.md)」を参照してください。  
  
3.  データ ソースに DQS クレンジング変換を接続します。  
  
  
