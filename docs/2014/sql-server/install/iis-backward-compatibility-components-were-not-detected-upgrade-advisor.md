---
title: IIS の旧バージョンとの互換性コンポーネントが検出されませんでした (アップグレードアドバイザー) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- IIS [Reporting Services]
ms.assetid: e794185a-0a77-480a-9aea-d09f8760a6b8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: dbf5686d4a947cb8629675368c59c8039c93835e
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952504"
---
# <a name="iis-backward-compatibility-components-were-not-detected-upgrade-advisor"></a>IIS の下位互換コンポーネントが検出されない (アップグレード アドバイザー)
  新しい [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] URL を作成するためにセットアップで使用する情報を提供する IIS コンポーネントと設定が、アップグレード アドバイザーで検出されませんでした。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のネイティブ モード。|  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>[説明]  
 IIS にはレポート サーバー仮想ディレクトリおよびレポート マネージャー仮想ディレクトリに関する情報を提供するコンポーネントが含まれており、これらのコンポーネントがレポート サーバー コンピューターにインストールされていません。 アップグレードを続行できますが、レポート サーバーまたはレポート マネージャーの URL は、アップグレードで再作成されません。  
  
## <a name="corrective-action"></a>修正措置  
 アップグレードの完了後、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用してレポート サーバーまたはレポート マネージャーの URL を設定します。 IIS マネージャーを使用して、不要になった仮想ディレクトリを削除します。  
  
 詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンラインブックの「 [Configure a URL &#40;&#41; SSRS Configuration Manager](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) 」を参照してください。  
  
## <a name="see-also"></a>参照  
 [アップグレードに関する&#40;問題の Reporting Services アップグレードアドバイザー&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
