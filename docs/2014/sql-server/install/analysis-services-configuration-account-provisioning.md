---
title: Analysis Services の構成 - アカウントの準備 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services configuration
- account provisioning
ms.assetid: 169b1af2-6fe2-467f-8ca4-919f24c620ce
author: heidisteen
ms.author: heidist
manager: craigg
ms.openlocfilehash: 033c1ec1b0ad478e525f3ea9e8f172c5e5e31eef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096796"
---
# <a name="analysis-services-configuration---account-provisioning"></a>Analysis Services の構成 - アカウントの準備
  このページを使用すると、サーバー モードを設定し、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] への無制限アクセスを必要とするユーザーまたはサービスに管理権限を付与することができます。 セットアップでは、ローカル Windows グループ BUILTIN\Administrators が、インストールするインスタンスの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サーバー管理者ロールに自動的に追加されません。 サーバー管理者ロールにローカルの Administrators グループを追加する場合は、そのグループを明示的に指定する必要があります。  
  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] をインストールする場合は、[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ファームでの [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] サーバーの配置に責任を負う SharePoint ファーム管理者またはサービス管理者に管理権限を付与してください。 詳細については[!INCLUDE[ssGeminiMTS](../../includes/ssgeminimts-md.md)]インストールおよびサービス アカウントの要件を参照してください。 [SharePoint と SQL Server BI 機能のインストール&#40;PowerPivot と Reporting Services&#41;](../../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)します。  
  
## <a name="options"></a>および  
 **[サーバー モード]** - サーバー モードでは、サーバーに配置できる Analysis Services データベースの種類を指定します。 セットアップ中に指定したサーバー モードを後で変更することはできません。 各モードは互いに排他的です。そのため、従来の OLAP ソリューションとテーブル モデル ソリューションの両方をサポートする場合は、それぞれ異なるモードで構成した 2 つの Analysis Services のインスタンスが必要になります。  
  
 **[管理者の指定]** - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのサーバー管理者を少なくとも 1 人指定する必要があります。 指定したユーザーまたはグループは、インストールする [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスのサーバー管理者ロールのメンバーになります。 これらは、ソフトウェアをインストールするコンピューターと同じドメインの Windows ドメイン ユーザー アカウントである必要があります。  
  
> [!NOTE]  
>  ユーザー アカウント制御 (UAC) は Windows セキュリティ機能であり、管理操作または管理アプリケーションの承認を管理者が実行前に明示的に行う必要があります。 UAC は既定でオンになっているため、高度な特権を必要とする特定の操作について許可するよう求めるメッセージが表示されます。 UAC を構成して既定の動作を変更することも、特定のプログラム用に UAC をカスタマイズすることもできます。 UAC および UAC 構成の詳細については、「[User Account Control Step by Step Guide](https://go.microsoft.com/fwlink/?linkid=196350)」(Windows ユーザー アカウント制御手順ガイド) と「[User Account Control (Wikipedia)](https://go.microsoft.com/fwlink/?linkid=196351)」(ユーザー アクセス制御) を参照してください。  
  
## <a name="see-also"></a>参照  
 [サービス アカウントの構成&#40;Analysis Services&#41;](../../../2014/analysis-services/instances/configure-service-accounts-analysis-services.md)   
 [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
  
  
