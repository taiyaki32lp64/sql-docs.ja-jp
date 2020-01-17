---
title: '[構成] ダイアログ ボックス | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.SSIS.SSMS.ISPROJECTPROP.PARAMETERS.F1
- SQL12.SSIS.SSMS.ISPROJECTPROP.REFERENCES.F1
- sql12.dts.designer.configure.f1
ms.assetid: 10183c8d-b1be-420f-972a-96ea97d4f4d8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9361e08722ae832c9e671cd8b83caa51bddaf4f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62836114"
---
# <a name="configure-dialog-box"></a>[構成] ダイアログ ボックス
  パッケージとプロジェクトのパラメーター、接続マネージャー、および環境への参照を構成するには、 **[構成]** ダイアログ ボックスを使用します。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [[構成] ダイアログ ボックスを開く](#open_dialog)  
  
-   [[パラメーター] ページのオプションの設定](#parameter)  
  
-   [[参照] ページのオプションの設定](#references)  
  
##  <a name="open_dialog"></a> [構成] ダイアログ ボックスを開く  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]から [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに接続します。  
  
     SSISDB データベースをホストする [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続されます。  
  
2.  オブジェクト エクスプローラーで、ツリーを展開して、 **[Integration Services カタログ]** ノードを表示します。  
  
3.  **[SSISDB]** ノードを展開します。  
  
4.  構成するパッケージまたはプロジェクトが格納されているフォルダーを展開します。  
  
5.  パッケージまたはプロジェクトを右クリックし、 **[構成]** をクリックします。  
  
##  <a name="parameter"></a> [パラメーター] ページのオプションの設定  
 パラメーターの名前と値を表示したり、値を変更するには、 **[パラメーター]** ページを使用します。  
  
 **[スコープ]** ボックスの一覧から、 **[パラメーター]** タブと **[接続マネージャー]** タブに表示されるパラメーターのスコープを選択します。  
  
 **[パラメーター]** タブのオプションの一覧を次に示します。  
  
 **コンテナー**  
 パラメーターを含むオブジェクトを一覧表示します。  
  
 **名前**  
 パラメーター名を一覧表示します。  
  
 **Value**  
 パラメーター値を一覧表示します。 **[パラメーター値の設定]** ダイアログ ボックスの値を変更するには、参照ボタンをクリックします。  
  
 **[接続マネージャー]** タブのオプションの一覧を次に示します。このタブは、接続マネージャーのプロパティの値を変更するときに使用します。 パラメーターは、SSIS サーバー上でプロパティ用に自動的に生成されます。  
  
 **コンテナー**  
 接続マネージャーを含むオブジェクトを一覧表示します。  
  
 **名前**  
 接続マネージャーの名前を一覧表示します。  
  
 **プロパティ名**  
 接続マネージャーのプロパティの名前を一覧表示します。  
  
 **[値]**  
 接続マネージャーのプロパティに割り当てられた値を一覧表示します。 **[パラメーター値の設定]** ダイアログ ボックスの値を変更するには、参照ボタンをクリックします。 リテラル値を入力するか、使用する値を含んでいる環境変数をマップするか、パッケージの既定値を使用することができます。  
  
##  <a name="references"></a> [参照] ページのオプションの設定  
 環境への参照を追加および削除したり、環境プロパティにアクセスするには、 **[参照]** ページを使用します。  
  
 環境は、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置したプロジェクトに含まれるパッケージのランタイム値を示します。  
  
 **環境**  
 環境を一覧表示します。  
  
 **環境フォルダー**  
 環境を含むフォルダーを一覧表示します。  
  
 **[ファイル]**  
 **[環境のプロパティ]** ダイアログ ボックスを開く場合にクリックします。  
  
 **[追加]**  
 環境への参照を追加する場合にクリックします。 **[環境の参照]** ダイアログ ボックスで、環境をクリックして **[OK]** をクリックします。  
  
 **SSISDB** ノードの下の任意のプロジェクト フォルダーに含まれている環境を選択できます。  
  
 **[削除]**  
 **[参照]** 領域に表示されている環境を選択し、 **[削除]** をクリックします。  
  
  
