---
title: Integration Services (SSIS) サーバー |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], managing
- managing packages [Integration Services]
ms.assetid: 6d667bba-7c25-492a-8f4d-70ebaca28f40
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 02966721d1fdfd1c1d3051510e0dd68ed26dcbc3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771738"
---
# <a name="integration-services-ssis-server"></a>Integration Services (SSIS) サーバー
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]でパッケージをデザインしてテストしたら、パッケージを含むプロジェクトを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーは、`SSISDB` データベースをホストする [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスです。 データベースには、パッケージ、プロジェクト、パラメーター、権限、サーバーのプロパティ、および運用履歴というオブジェクトが格納されます。  
  
 `SSISDB` データベース内のオブジェクト情報は、パブリック ビューに対してクエリを実行することで公開されます。 また、データベースには、オブジェクトを管理するために呼び出すことができるストアド プロシージャも用意されています。  
  
 プロジェクトを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置するには、まず `SSISDB` カタログを作成する必要があります。  
  
 SSISDB カタログの機能の概要については、「[SSIS カタログ](ssis-catalog.md)」を参照してください。  
  
## <a name="high-availability"></a>高可用性  
 他のユーザー データベースと同様に、`SSISDB` データベースでデータベース ミラーリングとレプリケーションをサポートします。 ミラーリングとレプリケーションの詳細については、「[データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)」を参照してください。  
  
 SSIS と AlwaysOn 可用性グループを利用して SSISDB とそのコンテンツの高可用性を実現することもできます。 詳細については、Matt Masson による blogs.msdn.com のブログ記事「 [SSIS と AlwaysOn](https://go.microsoft.com/fwlink/?LinkId=255873)」を参照してください。  
  
##  <a name="ssms"></a> SQL Server Management Studio の Integration Services サーバー  
 `SSISDB` データベースをホストする [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続している場合、オブジェクト エクスプローラーに、次のオブジェクトが表示されます。  
  
-   **SSISDB データベース**  
  
     `SSISDB`データベースのもと、**データベース**オブジェクト エクスプ ローラーでノード。 ビューに対してクエリを実行し、ストアド プロシージャを呼び出して、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーとサーバーに格納されているオブジェクトを管理できます。  
  
-   **統合サービス カタログ**  
  
     **[Integration Services カタログ]** ノードには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトおよび環境のフォルダーが存在します。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [SSIS カタログの作成](../create-the-ssis-catalog.md)  
  
-   [Integration Services サーバー上のパッケージの一覧を表示する](view-the-list-of-packages-on-the-integration-services-server.md)  
  
-   [Integration Services サーバーへのプロジェクトの配置](../deploy-projects-to-integration-services-server.md)  
  
-   [SQL Server Management Studio を使用した SSIS サーバーでのパッケージの実行](../run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 blogs.msdn.com のブログ エントリ「 [SSIS と AlwaysOn](https://go.microsoft.com/fwlink/?LinkId=255873)」。  
  
  
