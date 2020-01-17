---
title: レポートサーバーへの直接参照 (アップグレードアドバイザー) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3d2814a4-318a-45ed-b093-1e852fab561f
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 6945828b2eba829c32d717c13393c9fbda4fc43e
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952211"
---
# <a name="direct-browsing-to-report-server-upgrade-advisor"></a>レポート サーバーの直接参照 (アップグレード アドバイザー)
  アップグレードアドバイザーによって、レポートサーバーの仮想ディレクトリを直接参照している [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の現在のインストールが検出されました。  
  
||  
|-|  
|SharePoint モード[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **[!INCLUDE[applies](../../includes/applies-md.md)]** ます。|  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>[説明]  
 アップグレードアドバイザーによって、レポートサーバーの仮想ディレクトリを直接参照している [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の現在のインストールが検出されました。たとえば、 **http://\<server name >/ReportServer**などです。 このような直接参照は現在のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ではサポートされていません。  
  
> [!NOTE]  
>  この規則は警告であり、アップグレードはブロックされません。  
  
## <a name="corrective-action"></a>修正措置  
 ドキュメントライブラリの SharePoint ユーザーインターフェイスを使用して参照するか、 **http://\<サーバー名 >/SharePoint サイト >/_vti_bin/reportserver**を使用します。  
  
  
