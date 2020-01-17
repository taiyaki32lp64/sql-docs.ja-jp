---
title: 'レッスン 3: パッケージのインストール |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 87bc4d82-39d8-424f-886f-98cf1e4bb07a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b15b19bfc7f04c96bb955207c6631706380063fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057868"
---
# <a name="lesson-3-installing-packages"></a>レッスン 3: パッケージのインストール
  「[レッスン 2: 配置バンドルを作成する](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)、配置ユーティリティの構築、および項目を格納するために、配置バンドルを作成することは、別のコンピューターにパッケージをインストールする必要があります。 また、配置バンドルのファイル リストを確認し、配置ユーティリティの構築時に作成されたマニフェスト ファイルの内容も調べました。  
  
 このレッスンでは、配置バンドルを目的のコンピューターにコピーし、パッケージ インストール ウィザードを実行して、そのコンピューターにパッケージ、パッケージの依存関係、および補助ファイルをインストールします。 パッケージは **msdb** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースにインストールされ、その他の項目はファイル システムにインストールされます。 パッケージのインストールが完了すると、パッケージ実行ユーティリティを使用して [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] からパッケージを実行し、配置をテストします。  
  
 **このレッスンの推定所要時間:** 30 分  
  
## <a name="lesson-tasks"></a>このレッスンの作業  
 このレッスンの内容は次のとおりです。  
  
-   [ステップ 1: 配置バンドルのコピー](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
-   [手順 2:パッケージ インストール ウィザードの実行](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
-   [ステップ 3:配置したパッケージのテスト](../integration-services/lesson-3-3-testing-the-deployed-packages.md)  
  
## <a name="start-the-lesson"></a>レッスンの開始  
 [ステップ 1: 配置バンドルのコピー](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
![Integration Services のアイコン (小)](media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
  
