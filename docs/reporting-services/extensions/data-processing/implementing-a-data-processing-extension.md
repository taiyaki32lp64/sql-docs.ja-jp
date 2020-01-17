---
title: データ処理拡張機能の実装 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- data sources [Reporting Services], data processing extensions
- data processing extensions [Reporting Services]
- extensions [Reporting Services], data processing
ms.assetid: 8dc2b44e-5ad9-411d-a29f-7213e29321a9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 96458c62500794d06633299da57b4eccea9810da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193924"
---
# <a name="implementing-a-data-processing-extension"></a>データ処理拡張機能の実装
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のデータ処理拡張機能を使用することによって、データ ソースに接続し、データを取得できます。 データ処理拡張機能は、データ ソースとデータセット間のブリッジとしても機能します。 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のデータ処理拡張機能は、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] データ プロバイダー インターフェイスのサブセットと似ています。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [データ処理拡張機能の概要](../../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] のカスタム データ処理拡張機能の記述方法について説明します。  
  
 [データ処理拡張機能を実装する準備](../../../reporting-services/extensions/data-processing/preparing-to-implement-a-data-processing-extension.md)  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] データ処理拡張機能を実装する場合と特定のインターフェイスを実装する必要がある場合に使用できるインターフェイスについて説明します。  
  
 [データ処理拡張機能ライブラリの作成](../../../reporting-services/extensions/data-processing/creating-a-data-processing-extension-library.md)  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] データ処理拡張機能の名前空間の割り当て、およびライブラリ DLL へのデータ処理拡張機能のコンパイルについて説明します。  
  
 [データ処理拡張機能の Connection クラスの実装](../../../reporting-services/extensions/data-processing/implementing-a-connection-class-for-a-data-processing-extension.md)  
 接続の属性、およびデータ処理拡張機能の独自の **Connection** クラスを実装する方法について説明します。  
  
 [データ処理拡張機能の Command クラスの実装](../../../reporting-services/extensions/data-processing/implementing-a-command-class-for-a-data-processing-extension.md)  
 コマンドの属性と、データ処理拡張機能の独自の **Command** クラスを実装する方法について説明します。  
  
 [データ処理拡張機能の DataReader クラスの実装](../../../reporting-services/extensions/data-processing/implementing-a-datareader-class-for-a-data-processing-extension.md)  
 データ リーダーの属性と、データ処理拡張機能の独自の **DataReader** クラスを実装する方法について説明します。  
  
 [Reporting Services での外部データセットの使用](../../../reporting-services/extensions/data-processing/using-an-external-dataset-with-reporting-services.md)  
 カスタム **DataSet** オブジェクトをレポート サーバーで使用するために公開する方法について説明します。  
  
 [データ処理拡張機能の配置](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)  
 データ処理拡張機能を展開する方法について説明します。  
  
 [データ処理拡張機能コードのデバッグ](../../../reporting-services/extensions/data-processing/debugging-data-processing-extension-code.md)  
 データ処理拡張機能のコードをデバッグする方法について説明します。  
  
 完全に実装されたデータ処理拡張機能の例については、「[SQL Server Reporting Services Product Samples](https://go.microsoft.com/fwlink/?LinkId=177889)」 (SQL Server Reporting Services 製品サンプル) を参照してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services の拡張機能](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services 拡張機能ライブラリ](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
