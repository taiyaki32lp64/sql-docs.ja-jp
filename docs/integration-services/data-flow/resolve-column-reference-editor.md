---
title: 列参照解決エディター | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.resolvereferences.preview.F1
- sql13.dts.designer.resolvereferences.mapper.F1
ms.assetid: bb3ee33c-79c4-4c76-a82f-71581b4a60f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4340dfcaa7807616ccd8c3cdf4e504d0e33423c0
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298115"
---
# <a name="resolve-column-reference-editor"></a>列参照解決エディター

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  入力パスが接続されていない場合、またはパスにマップ解除された列が存在する場合、対応するデータ パスの横にエラー アイコンが表示されます。 列参照エラーの解決を簡素化するために、参照の解決エディターを使用して、マップ解除された出力列を、実行ツリーのすべてのパスのマップ解除された入力列とリンクできます。 また、参照の解決エディターでは、解決されているパスを示すためにパスが強調表示されます。  
  
> [!NOTE]  
>  入力パスが接続されていない場合でもコンポーネントを編集できます。  
  
 すべての列参照が解決された後、他のデータ パス エラーが存在しなければ、データ パスの横にエラー アイコンが表示されなくなります。  
  
## <a name="options"></a>オプション  
 **マップ解除された出力列 (変換元)**     
 現在マップされていない上流パスの列。  
  
**マップされた列 (変換元)**     
 下流パスから列にマップされた上流パスの列。  
  
**マップされた列 (変換先)**     
 下流パスから列にマップされた上流パスの列。  
  
**マップ解除された入力列 (変換先)**     
 現在マップされていない下流パスの列。  
  
**[マップ解除された入力列の削除]**  
 [マップ解除された入力列の削除] をオンにすると、データ パスの変換先でマップ解除された列が無視されます。 \[変更のプレビュー] ボタンには、[OK] ボタンを押したときに行われる変更の一覧が表示されます。  
  
  
