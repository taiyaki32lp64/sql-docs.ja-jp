---
title: 配信拡張機能のコードのデバッグ | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], debugging
- debugging delivery extensions [Reporting Services]
- troubleshooting [Reporting Services], delivery extensions
ms.assetid: a7d959da-5005-4a50-aca7-2cef36aa9947
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1abe30a462e8bf303b0171dbeeb82c407c80ca2a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193742"
---
# <a name="debugging-delivery-extension-code"></a>配信拡張機能のコードのデバッグ
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] には、配信拡張機能コードを分析してエラーを探すのに役立ついくつかのデバッグ ツールが用意されています。 最適なデバッグ ツールは、使用する目的によって異なります。 この例では [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]を使用します。  
  
#### <a name="to-debug-your-delivery-extension-code"></a>配信拡張機能のコードをデバッグするには  
  
1.  [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] を起動し、配信拡張機能のプロジェクトを開きます。  
  
2.  プロジェクトをビルドし、配信拡張機能アセンブリとその .pdb ファイルをレポート サーバーとレポート マネージャーに配置します。 配置の詳細については、「[配信拡張機能の配置](../../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)」を参照してください。  
  
3.  サブスクリプション ユーザー インターフェイスを記述してレポート マネージャーを拡張した場合は、[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] で配信拡張機能のコードを開いたまま、Internet Explorer を開いてレポート マネージャーに移動します。 レポート マネージャーのサブスクリプション ユーザー インターフェイスを配置していない場合は、クライアント アプリケーションを開き、そこから SOAP API を使用して配信拡張機能を呼び出します。  
  
4.  [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] および配信拡張機能のプロジェクトに移動し、コードにブレーク ポイントを設定します。  
  
5.  配信拡張機能プロジェクトのウィンドウをアクティブにしたまま、 **[デバッグ]** メニューの **[プロセスにアタッチ]** をクリックします。  
  
     **[プロセスにアタッチ]** ダイアログが開きます。  
  
6.  プロセスの一覧から aspnet_wp.exe プロセス (アプリケーションを IIS 6.0 に配置している場合は w3wp.exe ) を選択し、 **[アタッチ]** をクリックします。  
  
7.  配信拡張機能を使用して新しいサブスクリプションを定義します。 通常は、レポート マネージャーまたは SOAP API を使用します。 これにより、デバッガーが呼び出され、ブレーク ポイントに対応するコードが実行されます。  
  
8.  **F11** キーを使用してコードを実行します。 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] を使用したデバッグの詳細については、[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] のマニュアルを参照してください。  
  
## <a name="see-also"></a>参照  
 [配信拡張機能の実装](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
