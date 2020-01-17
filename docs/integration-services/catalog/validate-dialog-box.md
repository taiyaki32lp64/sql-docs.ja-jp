---
title: '[検証] ダイアログ ボックス | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.isprojectvalidate.f1
- sql13.ssis.ssms.ispackagevalidate.f1
ms.assetid: 134e14ce-4f8d-4a20-889a-918014c841d8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 049bb90dddf4bbfb03b222a675bd4008eb83cc14
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294870"
---
# <a name="validate-dialog-box"></a>[検証] ダイアログ ボックス

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **のプロジェクトまたはパッケージの一般的な問題を確認するには、** [検証] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ダイアログ ボックスを使用します。  
  
 問題がある場合は、ダイアログ ボックスの上部にメッセージが表示されます。 それ以外の場合は、上部に "準備完了" と表示されます。  
  
 **目的に合ったトピックをクリックしてください**  
  
-   [[検証] ダイアログ ボックスを開く](#open_dialog)  
  
-   [[全般] ページのオプションの設定](#general)  
  
##  <a name="open_dialog"></a> [検証] ダイアログ ボックスを開く  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]から [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに接続します。  
  
     SSISDB データベースをホストする [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続されます。  
  
2.  オブジェクト エクスプローラーで、ツリーを展開して、 **[Integration Services カタログ]** ノードを表示します。  
  
3.  **[SSISDB]** ノードを展開します。  
  
4.  検証するプロジェクトまたはパッケージが格納されているフォルダーを展開します。  
  
5.  プロジェクトまたはパッケージを右クリックし、 **[検証]** をクリックします。  
  
##  <a name="general"></a> [全般] ページのオプションの設定  
 **環境**  
 プロジェクトまたはパッケージの検証に使用する環境を選択します。  
  
 **32 ビット ランタイム**  
 32 ビット ランタイムを使用してパッケージを実行する場合に選択します。  
  
 **[パラメーター]** タブには、プロジェクトまたはパッケージの検証に使用するパラメーターの値が表示されます。 [パラメーター] タブのオプションを次に示します。  
  
 **コンテナー**  
 パラメーターを含むオブジェクトを一覧表示します。  
  
 **パラメーター**  
 パラメーターの名前を一覧表示します。  
  
 **Value**  
 パラメーター値を一覧表示します。  
  
 **[接続マネージャー]** タブには、プロジェクトまたはパッケージの検証に使用する接続マネージャーのプロパティ値が表示されます。  
  
 **[接続マネージャー]** タブのオプションを次に示します。  
  
 **コンテナー**  
 接続マネージャーを含むオブジェクトを一覧表示します。  
  
 **[名前]**  
 接続マネージャーの名前を一覧表示します。  
  
 **プロパティ名**  
 接続マネージャーのプロパティの名前を一覧表示します。  
  
 **Value**  
 接続マネージャーのプロパティに割り当てられた値を一覧表示します。  
  
  
