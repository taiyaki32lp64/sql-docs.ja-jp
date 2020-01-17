---
title: 表示拡張機能の実装 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- rendering extensions [Reporting Services]
- custom rendering extensions [Reporting Services]
- transformations [Reporting Services]
- extensions [Reporting Services], rendering
- rendering extensions [Reporting Services], implementing
ms.assetid: 4a5c64f5-2391-4597-ba3f-81d265b23703
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a72144df0f560feb6da0b954cbd7053832d46c87
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193707"
---
# <a name="implementing-a-rendering-extension"></a>表示拡張機能の実装
  表示拡張機能は、レポート サーバーのコンポーネントまたはモジュールで、レポートのデータとレイアウト情報をデバイス固有の形式に変換します。 SQL Server Reporting Services には 6 種類の表示拡張機能 (HTML、Excel、Word、CSV (Text)、XML、Image、PDF) があります。 追加の表示拡張機能を作成して、他の形式でレポートを生成できます。  
  
> [!NOTE]  
>  どの表示拡張機能を利用できるかは、RSReportServer.config ファイルのインストール済み拡張機能の一覧で確認できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [表示拡張機能の概要](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のカスタム表示機能の記述方法について説明します。  
  
 [IRenderingExtension インターフェイスの実装](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)  
 表示拡張機能の属性について説明します。  
  
 [表示拡張機能の配置](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
 レポート サーバーに表示拡張機能を配置する方法について説明します。  
  
 [表示拡張機能の削除](../../../reporting-services/extensions/rendering-extension/removing-a-rendering-extension.md)  
 レポート サーバーから表示拡張機能を削除する方法について説明します。  
  
## <a name="see-also"></a>参照  
 [Reporting Services の拡張機能](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services 拡張機能ライブラリ](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
