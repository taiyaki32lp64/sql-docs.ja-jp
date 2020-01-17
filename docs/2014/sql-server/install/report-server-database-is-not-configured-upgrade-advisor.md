---
title: レポートサーバーデータベースが構成されていない (アップグレードアドバイザー) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: b964300c-b220-4244-9fa6-c0c6a57760f6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: bb5dd5968930319532a29ff7c3909c36af99b3a0
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952109"
---
# <a name="report-server-database-is-not-configured-upgrade-advisor"></a>レポート サーバー データベースが構成されていない (アップグレード アドバイザー)
  レポート サーバーの構成が不完全であるためアップグレードがブロックされます。 レポート サーバー データベースが構成されていません。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint モード。|  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>説明  
 セットアップでアップグレードできるのは、完全に構成されているレポート サーバー インスタンスだけです。 続行するには、レポートサーバーデータベースを構成するか、Microsoft Windows の**コントロールパネル**を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストールからレポートサーバー機能を削除する必要があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を削除すると、その他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントをアップグレードできるようになります。  
  
## <a name="corrective-action"></a>修正措置  
 レポート サーバー データベースを構成していない場合、レポート サーバーは使用できないので、アップグレード前に削除する必要があります。  
  
 @No__t-0 のアンインストールの詳細については、「 [2012 Reporting Services のアンインストール](https://technet.microsoft.com/library/hh479745.aspx\(v=sql.11\))」を参照してください。 このトピックでは、特定のバージョンをアンインストールする方法について説明しています。アンインストールする手順は以前のバージョンでも同様です。  
  
## <a name="see-also"></a>関連項目  
 [アップグレードに関する&#40;問題の Reporting Services アップグレードアドバイザー&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
