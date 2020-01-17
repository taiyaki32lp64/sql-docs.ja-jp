---
title: レッスン 3:SSIS でのログ記録の追加 | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 64cd24cc-ba8e-4bd7-b10b-6b80d8b04af6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6ebbc82f5570fb97d7b1169563bfde7c67f5be0d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296020"
---
# <a name="lesson-3-add-logging-with-ssis"></a>レッスン 3:SSIS でのログ記録の追加

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、パッケージの実行を監視し、問題を解決するためのログ機能があります。このログを使用して、タスクやコンテナー イベントを追跡できます。 ログ記録には柔軟性があります。 ログ記録はパッケージ レベルで有効にするか、パッケージ内の個々のタスクやコンテナーで有効にすることができます。 ログを記録するイベントを複数選択すると、1 つのパッケージに対して複数のログが作成されます。  
  
ログは、ログ プロバイダーによって作成されます。 ログ プロバイダーごとに、異なる書式、および異なるファイル形式でログ情報を書き分けることができます。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、次のログ プロバイダーを使用できます。  
  
-   テキスト ファイル  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]  
  
-   Windows イベント ログ  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   XML ファイル  
  
このレッスンでは、「[レッスン 2: SSIS でのループの追加](../integration-services/lesson-2-adding-looping-with-ssis.md)」で作成したパッケージのコピーを作成します。 この新しいパッケージを操作しながら、パッケージの実行中に特定のイベントを監視するログ記録を追加および構成します。 前のレッスンで完了していないものがある場合は、このチュートリアルに含まれる、完了しているレッスン 2 のパッケージをコピーすることもできます。  

> [!NOTE]
> まだ行っていない場合は、[レッスン 1 の前提条件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)を参照してください。

## <a name="lesson-tasks"></a>このレッスンの作業  
このレッスンの内容は次のとおりです。  
  
-   [ステップ 1:レッスン 2 のパッケージのコピー](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [ステップ 2:ログ記録の追加および構成](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
-   [ステップ 3:レッスン 3 のパッケージのテスト](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>レッスンの開始  
[ステップ 1:レッスン 2 のパッケージのコピー](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
