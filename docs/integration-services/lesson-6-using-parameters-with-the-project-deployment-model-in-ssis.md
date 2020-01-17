---
title: 'レッスン 6: SSIS でプロジェクト配置モデルを持つパラメーターを使用する | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f6370319091d4326adbe2d11d1f92e19cd88695a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71282644"
---
# <a name="lesson-6-use-parameters-with-the-project-deployment-model-in-ssis"></a>レッスン 6: SSIS でプロジェクト配置モデルを持つパラメーターを使用する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



SQL Server 2012 では、Integration Services サーバーにプロジェクトを配置できる新しい配置モデルが導入されました。 Integration Services サーバーを使用すると、パッケージの管理、パッケージの実行、およびパッケージに合わせたランタイム値の構成を行うことができます。  
  
このレッスンでは、「[レッスン 5: パッケージ配置モデルの SSIS パッケージ構成を追加する](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)」で作成したパッケージを、パッケージ配置モデルを使用するように変更します。 構成値をパラメーターに置換して、サンプル データの場所を指定します。 または、チュートリアルに含まれている、レッスン 5 を完了した状態のパッケージをコピーすることもできます。  
  
Integration Services プロジェクト変換ウィザードを使用し、プロジェクトをプロジェクト配置モデルに変換します。 このモデルでは、構成値ではなく、パラメーターを使用して Directory プロパティを設定します。 このレッスンでは、新規プロジェクト配置モデルに既存の SSIS パッケージを変換するための手順について部分的に説明します。  
  
パッケージを再実行すると、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーでは、パラメーターを使用して変数の値が入力されます。 その後、変数によって Directory プロパティが更新されます。 パッケージでは、新しいパラメーターによって指定されたデータ フォルダーのファイルが反復処理されます。  
  
> [!NOTE]
> まだ行っていない場合は、[レッスン 1 の前提条件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)を参照してください。
    
## <a name="lesson-tasks"></a>このレッスンの作業  
このレッスンの内容は次のとおりです。  
  
1.  [ステップ 1:レッスン 5 のパッケージをコピーする](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [手順 2:プロジェクトをプロジェクト配置モデルに変換する](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [ステップ 3:レッスン 6 のパッケージをテストする](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [手順 4:レッスン 6 のパッケージを配置する](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>レッスンの開始  
[ステップ 1:レッスン 5 のパッケージをコピーする](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
