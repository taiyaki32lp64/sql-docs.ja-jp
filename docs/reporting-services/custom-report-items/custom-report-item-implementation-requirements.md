---
title: カスタム レポート アイテムの実装要件 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-report-items
ms.topic: reference
helpviewer_keywords:
- custom report items
ms.assetid: cfacd816-00d6-4a3d-be72-1bba6f7f6886
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e25938d690d6e1046d1d0e75ae5a4952b05d4615
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594516"
---
# <a name="custom-report-item-implementation-requirements"></a>カスタム レポート アイテムの実装要件
  このトピックでは、カスタム レポート アイテムの開発と配置の前提条件について説明します。  
  
## <a name="development-and-deployment-requirements"></a>開発と配置の要件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のカスタム レポート アイテムを開発するには、次の条件が必要です。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] および [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] を使用) を実行するサーバーへの管理アクセス権を持っていること。  
  
-   [!INCLUDE[vsprvsext](../../includes/vsprvsext-md.md)] 以上と [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ソフトウェア開発キット (SDK) がインストールされていること。  
  
-   [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK ドキュメントへのアクセス権を持つこと。  
  
-   コンポーネントの作成および [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のコンポーネント モデル名前空間について理解していること。  
  
## <a name="language-and-namespace-requirements"></a>言語と名前空間の要件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] カスタム レポート アイテムは、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] を完全にサポートしています。 任意の .NET 準拠の言語を使用してカスタム レポート アイテムを開発できます。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] には、反復的なコーディング、デバッグ、テストのサイクルを簡素化および高速化し、開発を容易にするための多数のツールと機能が備わっています。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK には、[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] コンパイラと C# コンパイラ、および関連ツールが含まれています。  
  
-   カスタム レポート アイテムでは、**Microsoft.ReportDesigner** および <xref:Microsoft.ReportingServices.Interfaces> 名前空間を使用します。 これらは、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の一部としてインストールされた Microsoft.ReportingServices.Designer.DLL アセンブリと Microsoft.ReportingServices.Interfaces.DLL アセンブリに格納されています。  
  
-   カスタム レポート アイテムのデザイン時コンポーネントは、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 内の <xref:System.ComponentModel> 名前空間からインターフェイスを実装する必要があります。 <xref:System.ComponentModel> は、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK ドキュメントに記載されています。  

## <a name="see-also"></a>参照  
 [カスタム レポート アイテムの実行時コンポーネントの作成](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [カスタム レポート アイテムのデザイン時コンポーネントの作成](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [カスタム レポート アイテムを配置する方法](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)   
 [カスタム レポート アイテムのクラス ライブラリ](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
  
  
