---
title: SharePoint 共有サービスがサイドバイサイドでインストールされている Microsoft SQL Server Reporting Services (アップグレードアドバイザー) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6ae1017e-129b-4702-9ea7-00ac9b024062
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 529e07dc7beed8dc37741f6c9dab0b0b080d4898
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952693"
---
# <a name="microsoft-sql-server-reporting-services-sharepoint-shared-service-is-installed-side-by-side-upgrade-advisor"></a>Microsoft SQL Server Reporting Services SharePoint 共有サービスがサイド バイ サイドでインストールされている (アップグレード アドバイザー)
  アップグレードアドバイザーによって、SharePoint 共有サービスが以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]とサイドバイサイドでインストールされている [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] が検出されました。  
  
||  
|-|  
|SharePoint モード[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **[!INCLUDE[applies](../../includes/applies-md.md)]** ます。|  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>[説明]  
 Sharepoint 共有サービスが SharePoint 共有サービスアーキテクチャに基づいていない以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] とサイドバイサイドでインストールされている [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] が、アップグレードアドバイザーによって検出されました。 新旧両方の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint 関連テクノロジがサイド バイ サイドでコンピューターにインストールされているため、アップグレードはブロックされます。  
  
## <a name="corrective-action"></a>修正措置  
 アップグレードを続行するには、既存の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インストールのうちの 1 つをアンインストールする必要があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のインストールのうちの 1 つを削除した後、アップグレード アドバイザーを再実行して、他にアップグレードに関する問題がないことを確認します。  
  
  
