---
title: データ処理拡張機能コードのデバッグ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- debugging data processing extensions [Reporting Services]
- troubleshooting [Reporting Services], data processing extensions
- data processing extensions [Reporting Services], debugging
ms.assetid: e963e205-9ae0-446d-97df-028a1d2727d9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: adecc79256f49aeca9532e50119675515b9939dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63164364"
---
# <a name="debugging-data-processing-extension-code"></a>データ処理拡張機能コードのデバッグ
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] には、データ処理拡張機能コードを分析してエラーを探すのに役立ついくつかのデバッグ ツールが用意されています。 最適なデバッグ ツールは、使用する目的によって異なります。 この例では [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)]を使用します。  
  
#### <a name="to-debug-your-data-processing-extension-code"></a>データ処理拡張機能コードをデバッグするには  
  
1.  [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] を起動し、データ処理拡張機能プロジェクトを開きます。  
  
2.  プロジェクトを構築し、データ処理拡張機能アセンブリと付随する .pdb ファイルをレポート デザイナーに配置します。 展開の詳細については、次を参照してください。[方法。レポート デザイナーにデータ処理拡張機能を配置](deploying-a-data-processing-extension-to-report-designer.md)します。  
  
3.  データ処理拡張機能コードを [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] で開いたまま、別の [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] ウィンドウで新しいレポート プロジェクトを開きます。  
  
4.  データ処理拡張機能プロジェクトを含む [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] のウィンドウに移動し、コードにブレーク ポイントを設定します。  
  
5.  データ処理拡張機能プロジェクト ウィンドウを開いたまま、 **[デバッグ]** メニューの **[プロセスにアタッチ]** をクリックします。  
  
     **[プロセスにアタッチ]** ダイアログが開きます。  
  
6.  プロセスの一覧から、レポート プロジェクトに対応する devenv.exe プロセスを選択して、 **[アタッチ]** をクリックします。  
  
7.  レポート プロジェクトの **[レポート データ]** タブを使用して、レポート データ ソースを定義します。 通常、汎用クエリ デザイナーを使用してカスタム データ ソースへのクエリを実行します。 これにより、デバッガーが呼び出され、ブレーク ポイントに対応するコードが実行されます。  
  
8.  F11 キーを使用してコードを実行します。 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] を使用したデバッグの詳細については、[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] のマニュアルを参照してください。  
  
## <a name="see-also"></a>参照  
 [データ処理拡張機能の配置](deploying-a-data-processing-extension.md)   
 [Reporting Services の拡張機能](../reporting-services-extensions.md)   
 [データ処理拡張機能の実装](implementing-a-data-processing-extension.md)   
 [Reporting Services 拡張機能ライブラリ](../reporting-services-extension-library.md)  
  
  
