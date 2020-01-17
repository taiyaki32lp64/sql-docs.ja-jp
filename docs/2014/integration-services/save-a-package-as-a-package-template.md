---
title: パッケージをパッケージ テンプレートとして保存する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- reusing packages
- templates [Integration Services]
ms.assetid: efe66cec-3933-4f6e-8d35-fe3d300de66c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 76349c0ca91f24a6d8d7942a89eb9683a91b573d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056340"
---
# <a name="save-a-package-as-a-package-template"></a>パッケージをパッケージ テンプレートとして保存する
  このトピックでは、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で新しい Integration Services パッケージを作成する際に、カスタム パッケージをテンプレートとして指定および使用する方法について説明します。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトに新しいパッケージを追加する場合に、既定で、新しいパッケージを作成するパッケージ テンプレートを使用します。 この既定のテンプレートを置き換えることはできませんが、新しいテンプレートを追加することはできます。  
  
 テンプレートとして、複数のパッケージを指定できます。 カスタム パッケージをテンプレートとして実装するには、そのパッケージをあらかじめ作成しておく必要があります。  
  
 カスタム パッケージをテンプレートとして使用してパッケージを作成すると、新しいパッケージの名前と GUID は、テンプレートと同じになります。 パッケージを区別するには、`Name` プロパティの値を更新して、`ID` プロパティの新しい GUID を生成する必要があります。 詳細については、「 [SQL Server データ ツールでのパッケージの作成](create-packages-in-sql-server-data-tools.md) 」および「 [パッケージのプロパティを設定する](set-package-properties.md)」を参照してください。  
  
### <a name="to-designate-a-custom-package-as-a-package-template"></a>カスタム パッケージをパッケージ テンプレートとして指定するには  
  
1.  ファイル システムで、テンプレートとして使用するパッケージを指定します。  
  
2.  パッケージを DataTransformationItems フォルダーにコピーします。 既定では、このフォルダーは、C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject にあります。  
  
3.  テンプレートとして使用する各パッケージについて、手順 1. と手順 2. を繰り返します。  
  
### <a name="to-use-a-custom-package-as-a-package-template"></a>カスタム パッケージをパッケージ テンプレートとして使用するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、パッケージを作成する [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、プロジェクトを右クリックして **[追加]** をポイントし、**[新しい項目]** をクリックします。  
  
3.  **[新しい項目の追加 - \<プロジェクト名>]** ダイアログ ボックスで、テンプレートとして使うパッケージをクリックします。  
  
     テンプレートの一覧には、"新しい SSIS パッケージ" という名前の既定のパッケージ テンプレートがあります。 パッケージ テンプレートとして使用できるテンプレートは、パッケージ アイコンで示されます。  
  
4.  **[追加]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server データ ツールでのパッケージの作成](create-packages-in-sql-server-data-tools.md)   
 [Integration Services &#40;SSIS&#41; パッケージ](../../2014/integration-services/integration-services-ssis-packages.md)  
  
  
