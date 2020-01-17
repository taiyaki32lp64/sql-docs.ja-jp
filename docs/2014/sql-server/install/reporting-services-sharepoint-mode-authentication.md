---
title: Reporting Services SharePoint モード認証 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade SharePoint Mode [Reporting Services]
- SharePoint integration
- SharePoint Mode
ms.assetid: 2c19794a-dd55-4fe5-b901-6dd93e9f6beb
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ff0a4f38bf9ee7d9c27fbc07308084ed3272f95d
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952101"
---
# <a name="reporting-services-sharepoint-mode-authentication"></a>Reporting Services SharePoint モード認証
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードの **[Reporting Services SharePoint モード認証]** ページを使用すると、現在の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インストールで使用されるサービス アカウントの資格情報を指定できます。 資格情報は新しい SharePoint アプリケーション プールの作成に使用されます。 また、1 つの新しい [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint サービス アプリケーションが作成されます。 サービス アプリケーション名には前の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンス名が含まれます。  
  
## <a name="options"></a>および  
  
-   **[SSRS アプリケーション プールのアカウント名]** オプションは読み取り専用です。 値はアップグレード中の既存の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インストールからの現在の値で自動的に設定されます。  
  
-   アプリケーション プール アカウントのパスワードが不要な場合、 **[SSRS アプリケーション プール アカウントのパスワード]** オプションは無効になります。 たとえば、"NT Authority\NetworkService" のようになります。 アプリケーション プール アカウントのパスワードが必要な場合、正しいパスワードを入力するまでアップグレードは続行できません。  
  
 詳細については、「 [Reporting Services のアップグレードと移行](https://go.microsoft.com/fwlink/?LinkID=245628)」 (https://go.microsoft.com/fwlink/?LinkID=245628) を参照してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services のアップグレードと移行](https://go.microsoft.com/fwlink/?LinkID=245628)  
  
  
