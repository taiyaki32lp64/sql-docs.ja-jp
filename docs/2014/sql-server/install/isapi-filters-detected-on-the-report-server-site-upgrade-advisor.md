---
title: レポートサーバーサイトで検出された ISAPI フィルター (アップグレードアドバイザー) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- ISAPI filters
- report servers [Reporting Services], upgrade issues
ms.assetid: dd30560d-9e16-47c7-ba68-a9743a657e4e
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a2b811955839eb22e3325d64c55454b92a6b1b8c
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952442"
---
# <a name="isapi-filters-detected-on-the-report-server-site-upgrade-advisor"></a>ISAPI フィルターがレポート サーバー サイトで検出された (アップグレード アドバイザー)
  アップグレード アドバイザーによって、レポート サーバー仮想ディレクトリおよびレポート マネージャー仮想ディレクトリをホストする Web サイトで 1 つ以上の ISAPI フィルターが検出されました。 ISAPI フィルターは [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]ではサポートされていません。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブです。|  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>[説明]  
 アップグレードする前に、Web サイトの ISAPI フィルターが [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーションで使用されているかどうかを確認します。 ISAPI フィルターが必要でない場合、レポート サーバーをアップグレードできます。 セットアップでは、既定の URL が作成され、IIS で実行される ISAPI フィルターはサポートされません。 ISAPI フィルターが必要な場合は、ISAPI フィルターをホストする別の方法 (ISA Server の使用や、IIS での ISAPI フィルターのホストの継続など) を把握してからアップグレードしてください。 レポート サーバーでは、シナリオによっては、ISAPI フィルターの代わりとして ASP.NET HTTPModules がサポートされます。 詳細については、MSDN で ASP.NET のマニュアルを参照してください。  
  
## <a name="corrective-action"></a>修正措置  
 配置に必要な ISAPI フィルターをホストするための個別のソリューションを評価し、使用します。  
  
## <a name="see-also"></a>参照  
 [アップグレードに関する&#40;問題の Reporting Services アップグレードアドバイザー&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
