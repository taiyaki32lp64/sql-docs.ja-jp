---
title: SQL Server のインストール計画 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, planning
ms.assetid: b1d56f2f-603f-48f2-b902-c715f14a6db9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b1baf29a88ff25eb278271719680d1979940c590
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211495"
---
# <a name="planning-a-sql-server-installation"></a>SQL Server のインストール計画
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をインストールするには、次の手順を実行します。  
  
-   インストール要件、システム構成チェック、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールに関するセキュリティ上の考慮事項を確認します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを実行し、新しいバージョンをインストールするか、新しいバージョンへのアップグレードを行います。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を構成します。  
  
 どのインストール方法を使用するかにかかわらず、個人として、または組織を代表して、ソフトウェア ライセンス条項に同意するかどうかを確認する必要があります。ただし、ソフトウェアの使用に別の契約 ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] ボリューム ライセンス契約、ISV や OEM とのサード パーティ契約など) が適用される場合を除きます。  
  
 ライセンス条項は、セットアップのユーザー インターフェイスで確認し、同意することができます。 /Q または /QS パラメーターを使用した自動インストールでは、/IAcceptSQLServerLicenseTerms パラメーターを指定する必要があります。 ライセンス条項は、「 [マイクロソフト ソフトウェア ライセンス条項](https://go.microsoft.com/fwlink/?LinkID=148209)」で別途確認できます。  
  
> [!NOTE]  
>  ソフトウェアの入手方法 ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] のボリューム ライセンスを通じて入手した場合など) によっては、ソフトウェアの使用に追加の条件が課されることがあります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [SQL Server インストールの新機能](../../../2014/sql-server/install/what-s-new-in-sql-server-installation.md)  
 このトピックでは、今バージョンの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]でのインストールに関する、新しい機能や強化された機能について説明します。  
  
 [SQL Server 2014 のインストールに必要なハードウェアおよびソフトウェア](hardware-and-software-requirements-for-installing-sql-server.md)  
 このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のインスタンスのインストールおよび実行に必要な最低限のハードウェア要件とソフトウェア要件について説明します。  
  
 [SQL Server インストールにおけるセキュリティの考慮事項](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
 このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール前と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインストール後で考慮する必要があるセキュリティのベスト プラクティスについて説明します。  
  
 [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
 このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のこのリリースにおける既定のサービス構成、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール時およびインストール後に設定できる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの構成オプションについて説明します。  
  
 [ネットワーク プロトコルとネットワーク ライブラリ](../../../2014/sql-server/install/network-protocols-and-network-libraries.md)  
 このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のこのリリースにおけるネットワーク プロトコルの既定の構成と、利用可能な構成オプションについて説明します。  
  
 [SQL Server の複数のバージョンおよびインスタンスの使用](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の複数のバージョンおよびインスタンスのインストールに関する考慮事項について説明します。  
  
 [SQL Server のローカル言語版](../../../2014/sql-server/install/local-language-versions-in-sql-server.md)  
 このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のローカライズ版について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [SQL Server 2014 のインストール](../../database-engine/install-windows/install-sql-server.md)  
 このセクションでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の各種インストール オプションについて概説します。  
  
 [SQL Server 2014 の BI 機能をインストールします。](install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップのドキュメントのこのセクションでは、Microsoft BI プラットフォームの一部である [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能のインストール方法について説明します。  
  
 [SQL Server 2014 へのアップグレード](../../database-engine/install-windows/upgrade-sql-server.md)  
 このセクションでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のバージョンのインスタンスを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にアップグレードする方法について概説します。  
  
 [SQL Server 2014 のアンインストール](uninstall-sql-server.md)  
 このセクションでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の既存のインスタンスを完全にアンインストールし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を再インストールできるようにシステムを準備する方法について説明します。  
  
 [SQL Server フェールオーバー クラスターのインストール](../failover-clusters/install/sql-server-failover-cluster-installation.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ ドキュメントのこのセクションでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターをインストールして構成する方法について説明します。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server 2014 のインストールのクイック スタート](../../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)   
 [コマンド プロンプトから SQL Server 2014 をインストールします。](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [高可用性ソリューション &#40;SQL Server&#41;](../failover-clusters/high-availability-solutions-sql-server.md)   
 [フェールオーバー クラスタリングをインストールする前に](../failover-clusters/install/before-installing-failover-clustering.md)   
 [アップグレードする SQL Server 2014 のインストール ウィザードを使用して&#40;セットアップ&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
