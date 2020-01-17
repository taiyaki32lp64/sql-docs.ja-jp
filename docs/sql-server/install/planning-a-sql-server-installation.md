---
title: SQL Server のインストール計画 | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: quickstart
helpviewer_keywords:
- installing SQL Server, planning
ms.assetid: b1d56f2f-603f-48f2-b902-c715f14a6db9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 94cdaba9319ed683dafcf3e8e29903b1d1957100
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019829"
---
# <a name="planning-a-sql-server-installation"></a>SQL Server のインストール計画
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をインストールするには、次の手順を実行します。  
  
-   インストール要件、システム構成チェック、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストールに関するセキュリティ上の考慮事項を確認します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを実行し、新しいバージョンをインストールするか、新しいバージョンへのアップグレードを行います。 アップグレードの前に、「[SQL Server をアップグレードする](../../database-engine/install-windows/upgrade-sql-server.md)」をご確認ください。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を構成します。  
  
 どのインストール方法を使用するかにかかわらず、個人として、または組織を代表して、ソフトウェア ライセンス条項に同意するかどうかを確認する必要があります。ただし、ソフトウェアの使用に別の契約 ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] ボリューム ライセンス契約、ISV や OEM とのサード パーティ契約など) が適用される場合を除きます。  
  
 ライセンス条項は、セットアップのユーザー インターフェイスで確認し、同意することができます。 無人インストール (`/Q` または `/QS` パラメーターを使用) には、`/IAcceptSQLServerLicenseTerms` パラメーターを含める必要があります。 「[Microsoft SQL Server ライセンス条項および情報](https://www.microsoft.com/Licensing/product-licensing/sql-server.aspx)」で、ライセンス条項を個別にダウンロードして確認することができます。 ボリューム ライセンス条項については、「[Licensing Terms and Documentation](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53)」 (ライセンス条項とドキュメント) を参照してください。 SQL Server の以前のバージョンについては、「[マイクロソフト ソフトウェア ライセンス条項](https://go.microsoft.com/fwlink/?LinkID=148209)」を参照してください。  
  
> [!NOTE]  
>  ソフトウェアの入手方法 ( [!INCLUDE[msCoName](../../includes/msconame-md.md)] のボリューム ライセンスを通じて入手した場合など) によっては、ソフトウェアの使用に追加の条件が課されることがあります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [SQL Server インストールの新機能](../../sql-server/install/what-s-new-in-sql-server-installation.md)  
 この記事では、このバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でのインストールに関する、新しい機能や強化された機能について説明します。  
  
 [SQL Server のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
 この記事では、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインスタンスのインストールおよび実行に必要な最低限のハードウェア要件とソフトウェア要件について説明します。  
  
 [SQL Server インストールにおけるセキュリティの考慮事項](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
 この記事では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール前と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール後で考慮する必要があるセキュリティのベスト プラクティスについて説明します。  
  
 [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
 この記事では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のこのリリースにおける既定のサービス構成、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール時とインストール後に設定できる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスの構成オプションについて説明します。  
  
 [ネットワーク プロトコルとネットワーク ライブラリ](../../sql-server/install/network-protocols-and-network-libraries.md)  
 この記事では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のこのリリースにおけるネットワーク プロトコルの既定の構成と、利用可能な構成オプションについて説明します。  
  
 [SQL Server の複数のバージョンおよびインスタンスの使用](../../sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
 この記事では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のバージョンおよびインスタンスのインストールに関する考慮事項について説明します。  
  
 [SQL Server のローカル言語版](../../sql-server/install/local-language-versions-in-sql-server.md)  
 この記事では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカライズ版について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [SQL Server のインストール](../../database-engine/install-windows/install-sql-server.md)  
 このセクションでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各種インストール オプションについて概説します。  
  
 [SQL Server のビジネス インテリジェンス機能のインストール](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップのドキュメントのこのセクションでは、Microsoft BI プラットフォームの一部である [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能のインストール方法について説明します。  
  
 [SQL Server のアップグレード](../../database-engine/install-windows/upgrade-sql-server.md)  
 このセクションでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の以前のバージョンのインスタンスを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にアップグレードする方法について概説します。  
  
 [SQL Server のアンインストール](../../sql-server/install/uninstall-sql-server.md)  
 このセクションでは、 [!INCLUDE[ssNoversion](../../includes/ssnoversion-md.md)] の既存のインスタンスを完全にアンインストールし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を再インストールできるようにシステムを準備する方法について説明します。  
  
 [SQL Server フェールオーバー クラスターのインストール](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ ドキュメントのこのセクションでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターをインストールして構成する方法について説明します。  
  
## <a name="see-also"></a>参照  
 [コマンド プロンプトからの SQL Server のインストール](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [高可用性ソリューション &#40;SQL Server&#41;](../../database-engine/sql-server-business-continuity-dr.md)   
 [フェールオーバー クラスタリングをインストールする前に](../../sql-server/failover-clusters/install/before-installing-failover-clustering.md)   
 [インストール ウィザードを使用した SQL Server のアップグレード &#40;セットアップ&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
