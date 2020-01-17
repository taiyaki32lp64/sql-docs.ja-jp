---
title: Excel 接続マネージャー | Microsoft Docs
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 58b73e5bd1f82d619f00e50d554d2043196d7884
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298546"
---
# <a name="excel-connection-manager"></a>Excel 接続マネージャー

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Excel 接続マネージャーを使用すると、パッケージは [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel ブック ファイルに接続できます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に含まれる Excel ソースと Excel 変換先は、Excel 接続マネージャーを使用します。  
 
> [!IMPORTANT]
> Excel ファイルへの接続、および Excel から、または Excel へのデータの読み込みに関する制限事項と既知の問題については、「[Load data from or to Excel with SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)」 (SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む) を参照してください。

 Excel 接続マネージャーをパッケージに追加するときに、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] により、実行時に Excel 接続として解決される接続マネージャーを作成し、接続マネージャーのプロパティを設定して、接続マネージャーをパッケージの **Connections** コレクションに追加します。  
  
 接続マネージャーの **ConnectionManagerType** プロパティは、 **EXCEL**に設定されます。  
  
## <a name="configure-the-excel-connection-manager"></a>Excel 接続マネージャーの構成  
 Excel 接続マネージャーは、次の方法で構成できます。  
  
-   Excel ブック ファイルのパスを指定します。  
  
-   ファイルの作成に使用した Excel のバージョンを指定します。  
  
-   選択したワークシート内または範囲内の最初の行に、列名が格納されているかどうかを示します。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、「 [Excel 接続マネージャー](../../integration-services/connection-manager/excel-connection-manager-editor.md)」を参照してください。  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
## <a name="excel-connection-manager-editor"></a>Excel 接続マネージャー
  **[Excel 接続マネージャー]** ダイアログ ボックスを使用すると、既存または新規の [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] ブック ファイルへの接続を追加できます。  
  
### <a name="options"></a>オプション  
 **[Excel ファイル パス]**  
 既存または新規の Excel ブック ファイルのパスおよびファイル名を入力します。  
   
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、Excel ファイルが存在するフォルダー、または新しいファイルを作成するフォルダーを指定します。  
  
 **[Excel バージョン]**  
 ファイルを作成するために使用した Microsoft Excel のバージョンを指定します。  
  
 **[先頭行に列名を含める]**  
 選択されているワークシートのデータの 1 行目に列名が含まれているかどうかを指定します。 このオプションの既定値は **[true]** です。  
  
## <a name="related-tasks"></a>Related Tasks  
[SQL Server Integration Services (SSIS) を使用して Excel から、または Excel にデータを読み込む](../load-data-to-from-excel-with-ssis.md)  
[Excel ソース](../data-flow/excel-source.md)  
[Excel 変換先](../data-flow/excel-destination.md)
