---
title: '[パッケージのプロパティ] ダイアログ ボックス | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.ispackageprop.general.f1
- sql12.ssis.ssms.packageproperties.f1
ms.assetid: a70acbf4-5f5c-4606-8ce4-8eb3684233de
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ab3cdf0079d0c01d95b73339e1fce8960658f93a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62836336"
---
# <a name="package-properties-dialog-box"></a>[パッケージのプロパティ] ダイアログ ボックス
  **[パッケージのプロパティ]** ダイアログ ボックスでは、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに格納されているパッケージのプロパティを表示できます。  
  
 詳細については、「[Integration Services &#40;SSIS&#41; Packages](integration-services-ssis-server-and-catalog.md)」(Integration Services &#40;SSIS&#41; のパッケージ) を参照してください。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [[パッケージのプロパティ] ダイアログ ボックスを開く](#open_dialog)  
  
-   [オプションの構成](#options)  
  
##  <a name="open_dialog"></a> [パッケージのプロパティ] ダイアログ ボックスを開く  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]から [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに接続します。  
  
     SSISDB データベースをホストする [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続されます。  
  
2.  オブジェクト エクスプローラーで、ツリーを展開して、 **[Integration Services カタログ]** ノードを表示します。  
  
3.  **[SSISDB]** ノードを展開します。  
  
4.  プロパティを表示するパッケージが格納されているフォルダーを展開します。  
  
5.  パッケージを右クリックし、 **[プロパティ]** をクリックします。  
  
##  <a name="options"></a> オプションの構成  
 **[全般]** ページでは、選択されているパッケージのプロパティを表示できます。  
  
 **[全般]** ページに表示されるすべてのプロパティは読み取り専用です。  
  
 **名前**  
 パッケージの名前が表示されます。  
  
 **[Identifier]**  
 パッケージ ID を一覧表示します。  
  
 **エントリ ポイント**  
 値 `True` は、パッケージが直接起動されることを示します。 値 `False` は、パッケージ実行タスクを使用して、パッケージが別のパッケージによって起動されることを示します。 既定値は `True` です。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] で親パッケージと子パッケージの両方に対してこのプロパティを設定するには、ソリューション エクスプローラーでパッケージを右クリックし、 **[エントリ ポイント パッケージ]** をクリックします。  
  
 **[説明]**  
 省略可能なパッケージの説明が表示されます。  
  
  
