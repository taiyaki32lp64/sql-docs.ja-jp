---
title: カスタム レポート アイテムの実装要件 | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom report items
ms.assetid: cfacd816-00d6-4a3d-be72-1bba6f7f6886
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0000e0c7a5933003544de22b60a8adc4d9c59c82
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2019
ms.locfileid: "74684442"
---
# <a name="custom-report-item-implementation-requirements"></a>カスタム レポート アイテムの実装要件
  このトピックでは、カスタム レポート アイテムの開発と配置の前提条件について説明します。  
  
## <a name="development-and-deployment-requirements"></a>開発と配置の要件  
 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のカスタム レポート アイテムを開発するには、次の条件が必要です。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]および[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]を使用してを実行しているサーバーへの管理アクセス。  
  
-   [!INCLUDE[vsprvsext](../../includes/vsprvsext-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]以上のソフトウェア開発キット (SDK) がインストールされている。  
  
-   
  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK ドキュメントへのアクセス権を持つこと。  
  
-   コンポーネントの作成および [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のコンポーネント モデル名前空間について理解していること。 詳細については、msdn.microsoft.com の「コンポーネントの作成」および「Visual Studio のコンポーネント モデルの名前空間」を参照してください。  
  
## <a name="language-and-namespace-requirements"></a>言語と名前空間の要件  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] カスタム レポート アイテムは、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] を完全にサポートしています。 任意の .NET 準拠の言語を使用してカスタム レポート アイテムを開発できます。  
  
 
  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] には、反復的なコーディング、デバッグ、テストのサイクルを簡素化および高速化し、開発を容易にするための多数のツールと機能が備わっています。 
  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK には、[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] コンパイラと C# コンパイラ、および関連ツールが含まれています。  
  
-   カスタム レポート アイテムは、`Microsoft.ReportDesigner` 名前空間と <xref:Microsoft.ReportingServices.Interfaces> 名前空間を使用します。 これらは、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の一部としてインストールされた Microsoft.ReportingServices.Designer.DLL アセンブリと Microsoft.ReportingServices.Interfaces.DLL アセンブリに格納されています。  
  
-   カスタム レポート アイテムのデザイン時コンポーネントは、<xref:System.ComponentModel> 内の [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 名前空間からインターフェイスを実装する必要があります。 
  <xref:System.ComponentModel> は、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK ドキュメントに記載されています。  
  
> [!IMPORTANT]  
>  既定では、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と共にインストールされますが、[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK はインストールされません。 SDK がコンピューターにインストールされておらず、SDK ドキュメントがオンライン ブック コレクションにも含まれていない場合、このセクションの SDK コンテンツへのリンクは機能しません。 
  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK をインストールしたら、「[SQL Server の製品ドキュメントの追加または削除](../../2014-toc/index.yml)」の手順に従って、SDK ドキュメントをオンライン ブック コレクションと目次に追加できます。  
  
## <a name="see-also"></a>参照  
 [カスタムレポートアイテムの実行時コンポーネントの作成](creating-a-custom-report-item-run-time-component.md)   
 [カスタムレポートアイテムのデザイン時コンポーネントの作成](creating-a-custom-report-item-design-time-component.md)   
 [カスタムレポートアイテムを配置する方法](how-to-deploy-a-custom-report-item.md)   
 [カスタム レポート アイテムのクラス ライブラリ](custom-report-item-class-libraries.md)  
  
  
