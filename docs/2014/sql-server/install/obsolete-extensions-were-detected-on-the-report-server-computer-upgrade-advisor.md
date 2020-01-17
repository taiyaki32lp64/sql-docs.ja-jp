---
title: 古い拡張機能がレポートサーバーコンピューターで検出されました (アップグレードアドバイザー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 40d245a2-0631-470e-81b3-1feb47e028cb
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 18f90bd6c551a6240a49eed9a0ec39723851bce1
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952076"
---
# <a name="obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor"></a>互換性のために残されている拡張機能がレポート サーバー コンピューターで検出された (アップグレード アドバイザー)
  アップグレード アドバイザーによって、現在のリリースでは使用できない表示拡張機能が 1 つ以上検出されました。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード。|  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>説明  
 このリリースで提供が中止されている拡張機能を 1 つ以上使用するようにレポート サーバーが構成されています。 廃止された拡張機能は次のとおりです。  
  
-   HTML OWC 表示拡張機能  
  
-   HTML 3.2 表示拡張機能  
  
 アップグレードを続行できますが、サポートされていない機能はアップグレード後のレポート サーバーで使用できません。  
  
 これらの拡張機能が必要な場合は、これらの要件に対する代替ソリューションが見つかるまで、アップグレードしないでください。 同一または同様の機能を提供するカスタム表示拡張機能を取得またはビルドする必要が生じることがあります。  
  
## <a name="corrective-action"></a>修正措置  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に現在含まれている一連の機能を評価して、サポートされている機能がユーザーの要件を満たすかどうかを判断します。  
  
## <a name="see-also"></a>関連項目  
 [アップグレードに関する&#40;問題の Reporting Services アップグレードアドバイザー&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
