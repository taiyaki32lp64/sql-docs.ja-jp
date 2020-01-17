---
title: Reporting Services のセキュリティと保護 | Microsoft Docs
ms.date: 08/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services]
- Reporting Services, security
ms.assetid: 270075c5-bf12-4467-a775-abbda3d954a5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 03234369ed7422433b35a5e3d296f6db1d1b2223
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570658"
---
# <a name="reporting-services-security-and-protection"></a>Reporting Services のセキュリティと保護
  このセクションでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]のセキュリティ機能について説明します。 また、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]でサポートされている承認モデルと認証プロバイダーについても説明します。  
  
## <a name="extended-protection-for-authentication"></a>認証の拡張保護 (Extended Protection for Authentication)  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]以降では、認証の拡張保護がサポートされています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能により、認証の拡張保護に対するチャネル バインドとサービス バインドの使用がサポートされます。 この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能は、拡張保護がサポートされているオペレーティング システムで使用する必要があります。 詳細については、「 [Reporting Services での認証の拡張保護](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)」をご覧ください。  
  
## <a name="authentication-and-authorization"></a>認証と承認  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、レポート サーバーで認証を行うためのさまざまな認証の種類が、ユーザーおよびクライアント アプリケーションに提供されます。 レポート サーバーの適切な認証の種類を使用すると、組織で必要とされる適切なレベルのセキュリティを実現できます。 詳細については、「 [レポート サーバーでの認証](../../reporting-services/security/authentication-with-the-report-server.md)」を参照してください。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、レポート サーバー カタログ内のコンテンツへのユーザー アクセス (つまり、アクセスできるユーザーとそのユーザーがアクセスできるコンテンツ、およびアクセス方法) を制御するためのロールと権限も使用されます。 詳細については、「[ロールと権限 (Reporting Services)](../../reporting-services/security/roles-and-permissions-reporting-services.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|リンク|  
|-----------------------|-----------|  
|レポート サーバーへのクライアント接続を保護するための Secure Socket Layer (SSL) の構成|[ネイティブ モードのレポート サーバーでの SSL 接続の構成](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)|  
  
  
