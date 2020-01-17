---
title: 'レッスン 5: パッケージ配置モデルの SSIS パッケージ構成を追加する| Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d3b3ccea56d367e7870826b39830e415e26bb2ac
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295909"
---
# <a name="lesson-5-add-ssis-package-configurations-for-the-package-deployment-model"></a>レッスン 5: パッケージ配置モデルの SSIS パッケージ構成を追加する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



パッケージ構成を使用すれば、開発環境の外部からランタイムのプロパティと変数を設定できます。 この構成により、配置と配信が容易で柔軟なパッケージを開発できます。 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、次の種類の構成が用意されています。  
  
-   XML 構成ファイル  
  
-   環境変数  
  
-   レジストリ エントリ  
  
-   親パッケージ変数  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] テーブル  
  
このレッスンでは、パッケージ配置モデルを使用し、パッケージ構成を活用するようにサンプル [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを変更します。このパッケージは「[レッスン 4: SSIS でエラー フロー リダイレクションを追加する](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)」で作成したものです。 チュートリアルに含まれている、レッスン 4 を完了した状態のパッケージをコピーすることもできます。 

パッケージ構成ウィザードを使用し、Foreach ループ コンテナーの **Directory** プロパティを更新する XML 構成を作成します。 **Directory** プロパティにマップされているパッケージ レベル変数を使用します。 構成ファイルを作成したら、変数の値を開発環境外から新しいサンプル データ フォルダー パスに変更します。 パッケージを再度実行すると、構成ファイルによって変数の値が生成されます。さらに、この変数は **Directory** プロパティを更新します。 パッケージはその後、元のハードコードではなく、新しいデータ フォルダーでファイルを反復処理します。  
  
> [!NOTE]
> まだ行っていない場合は、[レッスン 1 の前提条件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)を参照してください。
  
## <a name="lesson-tasks"></a>このレッスンの作業  
このレッスンの内容は次のとおりです。  
  
-   [ステップ 1:レッスン 4 のパッケージをコピーする](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [手順 2:パッケージ構成の有効化と構成](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [ステップ 3:Directory プロパティの構成値の変更](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [手順 4:レッスン 5 のパッケージをテストする](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>レッスンの開始  
  
-   [ステップ 1:レッスン 4 のパッケージをコピーする](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
  
  
