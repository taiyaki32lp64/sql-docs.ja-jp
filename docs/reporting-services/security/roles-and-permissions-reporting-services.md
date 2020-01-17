---
title: ロールとアクセス許可 (Reporting Services) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- access controls [Reporting Services]
- permissions [Reporting Services], about permissions
- security [Reporting Services], identity and access control
- authentication [Reporting Services]
- permissions [Reporting Services]
- security [Reporting Services], role-based
- identity [Reporting Services]
ms.assetid: eea655fe-43ed-418d-8233-b288a8f4daa4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2fc536de2312bc9adf1cba103ffde0999a83609e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570664"
---
# <a name="roles-and-permissions-reporting-services"></a>ロールと権限 (Reporting Services)
  Reporting Services では、認証サブシステムとロールベースの承認モデルを提供しています。 認証モデルと承認モデルは、レポート サーバーがネイティブ モードで実行されているか、SharePoint モードで実行されているかで異なります。 レポート サーバーが SharePoint 配置の一部として存在している場合、SharePoint の権限によってレポート サーバーへのアクセス権を持つユーザーが決定されます。  
  
## <a name="identity-and-access-control-for-native-mode"></a>ネイティブ モードの ID およびアクセス制御  
 既定の認証は、Windows 認証および統合セキュリティに基づいています。 レポート サーバーが異なる認証要求に応答できるように認証設定を変更したり、既定のセキュリティ機能を、指定したカスタム認証拡張機能に置き換えたりすることができます。  
  
 承認は、プリンシパルに割り当てるロールに基づいています。 各ロールは、一連の関連タスクで構成されており、タスクは関連操作で構成されています。 たとえば、 **レポートの管理** タスクでは、レポートの表示、レポートの追加、レポートの更新、レポートの削除、レポートのスケジュール設定、レポート プロパティの更新という、レポート サーバーの操作へのアクセス権が付与されます。  
  
## <a name="identity-and-access-control-for-sharepoint-mode"></a>SharePoint モードの ID およびアクセス制御  
 SharePoint 統合モードでは、要求がレポート サーバーに到達する前に、認証と承認が SharePoint サイトで処理されます。 認証の構成方法に応じて、SharePoint サイトからの要求には、セキュリティ トークンまたは信頼されたユーザー名が含まれます。 SharePoint のユーザーおよびグループに設定した権限によって、SharePoint ライブラリに配置されているレポート サーバー アイテムへのアクセスが承認されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [ネイティブ モードのレポート サーバーに対する権限の許可](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
 コンテンツおよび操作へのアクセスを提供するロールベースの承認モデルについて説明します。  
  
 [SharePoint サイトのレポート サーバー アイテムに対する権限の付与](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
 SharePoint グループ、権限レベル、および権限を使用してレポート サーバーへのアクセスを制御する方法を説明します。  
  
## <a name="see-also"></a>参照  
 [レポート サーバーでの認証](../../reporting-services/security/authentication-with-the-report-server.md)   
 [ネイティブ モードのレポート サーバーに対する権限の許可](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
