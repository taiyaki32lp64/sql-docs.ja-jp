---
title: 推定ディメンション メンバー (緩やかに変化するディメンション ウィザード) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.inferrdim.f1
ms.assetid: 809e395f-2e10-48ff-8860-56403f130628
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6b8510ebf2b5499dfa9e90a80a49a8241543c4ff
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291274"
---
# <a name="inferred-dimension-members-slowly-changing-dimension-wizard"></a>[推定ディメンション メンバー] (緩やかに変化するディメンション ウィザード)

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **[推定ディメンション メンバー]** ダイアログ ボックスを使用すると、推定メンバーを使用するためのオプションを指定できます。 推定メンバーは、まだ読み込まれていないディメンション メンバーをファクト テーブルで参照するときに使用されます。 推定メンバーのデータが読み込まれると、新しいレコードを作成する代わりに、既存のレコードを更新できます。  
  
 このウィザードの詳細については、「 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)」を参照してください。  
  
## <a name="options"></a>オプション  
 **[推定メンバー サポートを有効にする]**  
 推定メンバーを有効にすることを選択した場合は、次のどちらかのオプションを選択する必要があります。  
  
 **[変化する型を持つすべての列を NULL とする]**  
 新しい推定メンバー レコード内で、変化する型を持つすべての列に NULL 値を入力するかどうかを指定します。  
  
 **[現在のレコードが推定メンバーであるかどうかの識別にブール型の列を使用する]**  
 現在のレコードが推定メンバーであるかどうかを示すために、既存のブール型の列を使用するかどうかを指定します。  
  
 **[推定メンバー インジケーター]**  
 上記の、推定メンバーであるかどうかの識別にブール型の列を使用することを選択した場合は、一覧から列を選択します。  
  
## <a name="see-also"></a>参照  
 [緩やかに変化するディメンション ウィザードを使用して出力を構成する](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
