---
title: '[パラメーター値の設定] ダイアログ ボックス | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ce9c2201-4e9a-4495-948f-b68deeaa7955
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5e5bfe3faf83b0873a8b47c348df9cfd8138dacb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771638"
---
# <a name="set-parameter-value-dialog-box"></a>[パラメーター値の設定] ダイアログ ボックス
  プロジェクトとパッケージのパラメーターと接続マネージャーのプロパティの値を設定するには、 **[パラメーター値の設定]** ダイアログ ボックスを使用します。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [[パラメーター値の設定] ダイアログ ボックスを開く](#open_dialog)  
  
-   [オプションの構成](#option)  
  
##  <a name="open_dialog"></a> [パラメーター値の設定] ダイアログ ボックスを開く  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]から [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに接続します。  
  
     SSISDB データベースをホストする [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続されます。  
  
2.  オブジェクト エクスプローラーで、ツリーを展開して、 **[Integration Services カタログ]** ノードを表示します。  
  
3.  **[SSISDB]** ノードを展開します。  
  
4.  パッケージまたはプロジェクトを右クリックして **[構成]** をクリックし、 **[パラメーター]** タブまたは **[接続マネージャー]** タブの参照ボタンをクリックします。  
  
##  <a name="option"></a> オプションの構成  
 **パラメーター**  
 パラメーター名を一覧表示します。  
  
 **型**  
 パラメーター値のデータ型を一覧表示します。  
  
 **[説明]**  
 パラメーターのオプションの説明を表示します。  
  
 **値の編集**  
 パラメーター値を編集する場合に選択します。  
  
 **パッケージの既定値を使用する**  
 パッケージに保存されている既定のパラメーター値を使用する場合に選択します。  
  
 **環境変数を使用する**  
 環境に保存されている変数値を使用する場合に選択します。この変数値はプロジェクトまたはパッケージによって参照されます。 環境参照をプロジェクトまたはパッケージに追加するには、 **[構成]** ダイアログ ボックスを使用します。 詳細については、「 [[構成] ダイアログ ボックス](configure-dialog-box.md)」を参照してください。  
  
  
