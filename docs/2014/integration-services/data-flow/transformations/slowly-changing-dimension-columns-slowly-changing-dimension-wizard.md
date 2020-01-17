---
title: '[緩やかに変化するディメンションの列] (緩やかに変化するディメンション ウィザード) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.scdsupport.f1
ms.assetid: 36de99d5-5368-48e0-b876-17e9c6862c6c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c49f0ce7498215d5758557fba4c67740dca1239e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770671"
---
# <a name="slowly-changing-dimension-columns-slowly-changing-dimension-wizard"></a>[緩やかに変化するディメンションの列] (緩やかに変化するディメンション ウィザード)
  **[緩やかに変化するディメンションの列]** ダイアログ ボックスを使用すると、緩やかに変化するディメンションの各列に対して変更の種類を選択できます。  
  
 このウィザードの詳細については、「 [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[ディメンション列]**  
 ディメンション列を一覧から選択します。  
  
 **[変更の種類]**  
 **[固定属性]** を選択するか、変化する属性の 2 つのうちのいずれかを選択します。 列の値を変更しない場合は **[固定属性]** を使用します。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] は、変更をエラーとして扱います。 **[変化する属性]** を使用して、既存の値を変更後の値で上書きします。 **[履歴属性]** を使用して、変更後の値を新しいレコードに保存し、前のレコードを期限切れにすることができます。  
  
 **[削除]**  
 ディメンション列を選択し、 **[削除]** をクリックして、マップされた列の一覧から削除します。  
  
## <a name="see-also"></a>関連項目  
 [緩やかに変化するディメンション ウィザードを使用して出力を構成する](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
