---
title: レッスン 3:SSIS パッケージのインストール | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 87bc4d82-39d8-424f-886f-98cf1e4bb07a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5f325c9322d9194ff9dfb99dcf5bcae902a59faa
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295979"
---
# <a name="lesson-3-install-ssis-packages"></a>レッスン 3:SSIS パッケージのインストール

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


「[レッスン 2: SSIS で配置バンドルを作成する](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)」では、配置ユーティリティを構築し、配置バンドルを作成しました。配置バンドルには、別のコンピューターにパッケージをインストールする際に必要となるアイテムが含まれています。 また、配置バンドルのファイル リストを確認し、配置ユーティリティの構築時に作成されたマニフェスト ファイルの内容も調べました。  
  
このレッスンでは、配置バンドルを目的のコンピューターにコピーし、パッケージ インストール ウィザードを実行して、そのコンピューターにパッケージ、パッケージの依存関係、および補助ファイルをインストールします。 パッケージは **msdb** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースにインストールされ、その他の項目はファイル システムにインストールされます。 パッケージのインストールが完了すると、パッケージ実行ユーティリティを使用して [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] からパッケージを実行し、配置をテストします。  
  
**このレッスンの推定所要時間:** 30 分  
  
## <a name="lesson-tasks"></a>このレッスンの作業  
このレッスンの内容は次のとおりです。  
  
-   [ステップ 1:配置バンドルのコピー](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
-   [手順 2:パッケージ インストール ウィザードの実行](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
-   [ステップ 3:配置したパッケージのテスト](../integration-services/lesson-3-3-testing-the-deployed-packages.md)  
  
## <a name="start-the-lesson"></a>レッスンの開始  
[ステップ 1:配置バンドルのコピー](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
  
  
