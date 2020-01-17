---
title: Word デバイス情報設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Word [Reporting Services]
- device information settings [Reporting Services], Word
ms.assetid: 28146498-fae7-4b13-b47f-6ec05aa8e057
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ddd145c5073003a8dc189e3ed9b1bbb25dc11d09
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096929"
---
# <a name="word-device-information-settings"></a>Word デバイス情報設定
  次の表は、 [!INCLUDE[ofprword](../includes/ofprword-md.md)] 形式で表示するためのデバイス情報設定を示しています。  
  
|設定|値|  
|-------------|-----------|  
|`AutoFit`|`False`。 Word のすべての表で AutoFit が `false` に設定されます。<br /><br /> `True`。 設定されている AutoFit`true`すべて Word の表でします。<br /><br /> `Never`。 Word の表で AutoFit 値が設定されず、動作が Word の既定値に戻ります。<br /><br /> `Default`。 各論理ページごとに、物理的な描画領域 (余白を除いた物理ページの幅) よりも幅の狭い表で AutoFit が設定されます。|  
|`ExpandToggles`|表示と非表示の切り替えが可能なすべてのアイテムを完全に展開した状態で表示するかどうかを示します。 既定値は `false` です。|  
|`FixedPageWidth`|DOC ファイルに書き込まれるページの幅がレポート本文内で最大のページの幅に合わせて拡大されるかどうかを示します。 既定値は `false` です。|  
|**OmitHyperlinks**|ハイパーリンク アクションが設定されているすべてのアイテムでそのアクションを省略するかどうかを示します。 既定値は `false`|  
|`OmitDrillthroughs`|ドリルスルー アクションが設定されているすべてのアイテムでそのアクションを省略するかどうかを示します。 既定値は `false`|  
  
## <a name="see-also"></a>参照  
 [表示拡張機能にデバイス情報設定を渡す](report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md)   
 [RSReportServer.Config で表示拡張機能パラメーターをカスタマイズする](customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [テクニカル リファレンス (SSRS)](../../2014/reporting-services/technical-reference-ssrs.md)  
  
  
