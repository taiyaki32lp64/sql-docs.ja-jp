---
title: データ処理拡張機能の配置 | Microsoft Docs
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: e5c0b5a9-1386-47cb-aade-96653ecfaa54
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3e8c86c1ba590ab574e7afe351b3e29c2c918b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194062"
---
# <a name="deploying-a-data-processing-extension"></a>データ処理拡張機能の配置
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のデータ処理拡張機能は、作成して [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ライブラリにコンパイルした後、レポート サーバーおよびレポート デザイナーで検出できるようにする必要があります。 これは、適切なディレクトリに拡張機能をコピーし、適切な [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 構成ファイルにエントリを追加するだけで簡単に行うことができます。  
  
## <a name="configuration-file-extension-element"></a>構成ファイルの Extension 要素  
 レポート サーバーまたはレポート デザイナーに配置するデータ処理拡張機能は、構成ファイルに **Extension** 要素として入力する必要があります。 構成ファイルは、レポート サーバーの場合は RSReportServer.config、レポート デザイナーの場合は RSReportDesigner.config です。  
  
 次の表では、データ処理拡張機能の **Extension** 要素の属性について説明します。  
  
|属性|[説明]|  
|---------------|-----------------|  
|**[名前]**|拡張機能の一意な名前。たとえば、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ処理拡張機能に対して "SQL"、OLE DB データ処理拡張機能に対して "OLEDB"。 **Name** 属性の最大文字数は 255 文字です。 名前は、構成ファイルの **Extension** 要素内にあるすべてのエントリの間で一意にする必要があります。|  
|**型**|アセンブリの名前と共に完全修飾名前空間を含むコンマ区切りの一覧。|  
|**[表示]**|**false** の値は、データ処理拡張機能がユーザー インターフェイスに表示されないことを示します。 この属性が指定されない場合、既定値は **true**になります。|  
  
 RSReportServer.config ファイルまたは RSReportDesigner.config ファイルの詳細については、「[Reporting Services 構成ファイル](../../../reporting-services/report-server/reporting-services-configuration-files.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[データ処理拡張機能をレポート サーバーに配置する方法](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-a-report-server.md)|レポート サーバーにデータ処理拡張機能を配置する方法について説明します。|  
|[データ処理拡張機能をレポート デザイナーに配置する方法](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md)|レポート デザイナーにデータ処理拡張機能を配置する方法について説明します。|  
  
## <a name="see-also"></a>参照  
 [Reporting Services の拡張機能](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [データ処理拡張機能の実装](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
