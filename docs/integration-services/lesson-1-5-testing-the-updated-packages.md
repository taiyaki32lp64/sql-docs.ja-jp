---
title: 手順 5:更新したパッケージのテスト | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 683e52e5-1c7e-49ab-9ffe-6a450a1c5776
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e90af0ecf9972b7365f42fcc307181c4d657e3c5
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296107"
---
# <a name="lesson-1-5---testing-the-updated-packages"></a>レッスン 1-5 - 更新したパッケージのテスト

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


次のレッスンでは、目的のコンピューターにチュートリアル パッケージをインストールするときに使用する配置バンドルを作成しますが、その前にパッケージをテストする必要があります。 この作業では、Deployment Tutorial プロジェクトに追加して構成を拡張したパッケージ DataTransfer.dtsx および LoadXMLData を実行します。  
  
パッケージを実行すると、パッケージ内の各実行ファイルが完了したときに緑色になります。 実行ファイルのすべてが緑色になると、パッケージの実行に成功したことを表します。 **[進行状況]** タブでパッケージ実行の進み具合を見ることもできます。  
  
パッケージの実行に失敗した場合は、次のレッスンに進む前に修正する必要があります。  
  
### <a name="to-run-the-datatransfer-package"></a>DataTransfer パッケージを実行するには  
  
1.  ソリューション エクスプローラーで [DataTransfer.dtsx] をクリックします。  
  
2.  **[デバッグ]** メニューの **[デバッグ開始]** をクリックします。  
  
3.  パッケージの実行が完了したら、 **[デバッグ]** メニューの **[デバッグの停止]** をクリックします。  
  
### <a name="to-run-the-loadxmldata-package"></a>LoadXMLData パッケージを実行するには  
  
1.  ソリューション エクスプローラーで [LoadXMLData.dtsx] をクリックします。  
  
2.  **[デバッグ]** メニューの **[デバッグ開始]** をクリックします。  
  
3.  パッケージの実行が完了したら、 **[デバッグ]** メニューの **[デバッグの停止]** をクリックします。  
  
## <a name="next-lesson"></a>次のレッスン  
[レッスン 2:SSIS での配置バンドルの作成](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)  
  
  
  
