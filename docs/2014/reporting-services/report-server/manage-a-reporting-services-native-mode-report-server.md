---
title: Reporting Services ネイティブ モードのレポート サーバーの管理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services Configuration tool
- configuration options [Reporting Services]
- report servers [Reporting Services], configuring
ms.assetid: 6ca03a09-d6a8-4c93-ba12-1c99dcbfb618
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: da2eb97e5ce57a2e6a82dda3e264b33e1e3a3b11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103788"
---
# <a name="manage-a-reporting-services-native-mode-report-server"></a>Reporting Services ネイティブ モードのレポート サーバーの管理
  ここでは、Reporting Services 構成マネージャーを使用してネイティブ モードのレポート サーバー インスタンスを構成する手順について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 このセクションのトピックは、必要な手順をより簡単に見つけることができるようにカテゴリ別に分類されています。 最初のセクションでは、ネイティブ モードのレポート サーバーの基本的な構成タスクに関するトピックについて紹介します。 2 番目のセクションでは、詳細な構成に関するトピックについて紹介します。 3 番目のセクションでは、SharePoint 統合モードで実行されるレポート サーバーの構成に関するトピックについて紹介します。  
  
### <a name="basic-configuration"></a>基本構成  
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
 Reporting Services の構成ツールを開始するための手順を説明します。  
  
 [サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)  
 レポート サーバー サービス用のアカウントとパスワードの情報を指定する方法について説明します。  
  
 [レポート サーバーのサービス プリンシパル名 (SPN) の登録](register-a-service-principal-name-spn-for-a-report-server.md)  
 Kerberos 認証を使用するネットワーク上でドメイン ユーザー アカウントで実行されるレポート サーバーの SPN を手動で登録する方法について説明します。  
  
 [URL の構成 &#40;SSRS 構成マネージャー&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)  
 レポート サーバー Web サービスおよびレポート マネージャーへのアクセスに使用する 1 つ以上の URL の設定方法について説明します。  
  
 [ネイティブ モード レポート サーバー データベースの作成 &#40;SSRS 構成マネージャー&#41;](../install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)  
 レポート サーバー データベースを作成するための手順を説明します。 この手順は、Reporting Services のインストールの配置に必要です。  
  
### <a name="advanced-or-optional-configuration"></a>詳細な構成または省略可能な構成  
 [ネイティブ モード レポート サーバーのスケールアウト配置の構成 (SSRS 構成マネージャー)](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
 レポート サーバー データベースを共有するための複数のレポート サーバーの構成手順を説明します。  
  
 [レポート サーバー電子メール配信用に構成&#40;SSRS 構成マネージャー&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)  
 電子メール配信用のレポート サーバーを構成する手順を説明します。  
  
 [レポート サーバー アクセスに対するファイアウォールの構成](configure-a-firewall-for-report-server-access.md)  
 レポート サーバーの要求の受信と応答の送信に使用されるポートを開く方法について説明します。  
  
 [ローカル管理用のネイティブ モードのレポート サーバー (SSRS) の構成](configure-a-native-mode-report-server-for-local-administration-ssrs.md)  
 http://localhost を使用してレポート マネージャーまたはレポート サーバーに接続するために必要な追加手順について説明します。  
  
 [リモート管理用のレポート サーバーの構成](configure-a-report-server-for-remote-administration.md)  
 リモートのレポート サーバー インスタンスに接続したり別のコンピューターから構成したりすることができるようにインスタンスを構成する方法について説明します。  
  
 [Reporting Services 機能の有効化と無効化](turn-reporting-services-features-on-or-off.md)  
 使用しない機能を Reporting Services から削除する方法について説明します。  
  
 [リモート エラーの有効化 (Reporting Services)](enable-remote-errors-reporting-services.md)  
 リモート サーバーで発生するエラー状態に関する追加情報を返すように、レポート サーバーのサーバー プロパティを設定する方法について説明します。  
  
## <a name="see-also"></a>関連項目  
 [レポート サーバーを構成および管理する &#40;SSRSネイティブ モード&#41;](configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [レポート サーバーの構成と管理 (Reporting Services SharePoint モード)](../configure-administer-report-server-reporting-services-sharepoint-mode.md)  
  
  
