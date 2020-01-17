---
title: 固定属性と変化する属性のオプション (緩やかに変化するディメンション ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.attriboption.f1
ms.assetid: c841345c-7d03-452f-9379-1c8c464f029c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3e54fc003f2bb61a5e94f521ddb1a0221261610e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291431"
---
# <a name="fixed-and-changing-attribute-options-slowly-changing-dimension-wizard"></a>[固定属性と変化する属性のオプション] (緩やかに変化するディメンション ウィザード)

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **[固定属性と変化する属性のオプション]** ダイアログ ボックスを使用すると、固定属性と変化する属性において変更に応答する方法を指定します。  
  
 このウィザードの詳細については、「 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)」を参照してください。  
  
## <a name="options"></a>オプション  
 **[固定属性]**  
 固定属性の場合は、固定属性で変更が検出された場合に、タスクが失敗するかどうかを示します。  
  
 **[変化する属性]**  
 変化する属性の場合は、変化する属性で変更が検出された場合に、現在のレコードに加え、古いレコードや有効期限が切れたレコードをタスクが変更するかどうかを指定します。 有効期限が切れたレコードとは、履歴属性の変更 (種類 2 の変更) によって新しいレコードに置き換えられたレコードのことです。 このオプションを選択すると、リレーショナル データ ウェアハウスで構築された多次元オブジェクトに処理要件が追加される可能性があります。  
  
## <a name="see-also"></a>参照  
 [緩やかに変化するディメンション ウィザードを使用して出力を構成する](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
