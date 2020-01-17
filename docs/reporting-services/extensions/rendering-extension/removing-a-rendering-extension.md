---
title: 表示拡張機能の削除 | Microsoft Docs
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0ee3563074e2379061006b72f55dab99f80094cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193456"
---
# <a name="removing-a-rendering-extension"></a>表示拡張機能の削除
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 表示拡張機能を削除する場合は、 **%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<インスタンス名>\Reporting Services\ReportServer** フォルダーにある、rsreportserver.config ファイルから表示拡張機能の **Extension** 要素を削除するだけです。 レポート サーバーに加えてレポート デザイナーにもエントリを作成した場合は、[RSReportDesigner 構成ファイル](../../../reporting-services/report-server/rsreportdesigner-configuration-file.md)からも **Extension** 要素を削除します。 構成情報を削除した後は、表示拡張機能をコンポーネントに使用できません。  
  
## <a name="see-also"></a>参照  
 [Reporting Services 構成ファイル](../../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [表示拡張機能の実装](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [表示拡張機能の概要](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [IRenderingExtension インターフェイスの実装](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [拡張機能のセキュリティに関する考慮事項](../../../reporting-services/extensions/security-considerations-for-extensions.md)   
 [表示拡張機能の配置](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
  
