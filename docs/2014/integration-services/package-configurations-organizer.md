---
title: パッケージ構成オーガナイザー |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.packageconfigurationorganizer.f1
helpviewer_keywords:
- Package Configurations Organizer dialog box
ms.assetid: f20ae6cb-9e6a-4d24-88ff-d7a903a4e8d3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d5313118f7949818d341a47744a69cf13c43dbc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056965"
---
# <a name="package-configurations-organizer"></a>[パッケージ構成オーガナイザー]
  **[パッケージ構成オーガナイザー]** ダイアログ ボックスを使用すると、パッケージ構成を有効にし、現在のパッケージの構成の一覧を表示して、構成の優先読み込み順序を指定できます。  
  
> [!NOTE]  
>  パッケージ配置モデルの構成を使用できます。 パラメーターは、プロジェクト配置モデルの構成の代わりに使用します。 プロジェクト配置モデルを使用すると、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーに [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを配置できます。 配置モデルの詳細については、「 [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。  
  
 複数の構成で同じプロパティを更新した場合、構成の一覧内で上の方にある構成の値は、一覧内で下の方にある構成の値に置き換えられます。 パッケージを実行するときに使用される値は、プロパティに最後に読み込まれた値です。 また、パッケージで XML 構成ファイルなどの直接構成と環境変数などの間接構成の組み合わせを使用している場合は、直接構成の場所を指す間接構成を一覧の上の方に置く必要があります。  
  
> [!NOTE]  
>  パッケージ構成を優先順序で読み込むと、 **[パッケージ構成オーガナイザー]** ダイアログ ボックスに表示された一覧の上から下へと構成が読み込まれます。 ただし、実行時にパッケージ構成が優先順序で読み込まれるとは限りません。 具体的には、親のパッケージ構成は他の種類の構成の後に読み込まれます。  
  
 パッケージ オブジェクトのプロパティの値は、パッケージ構成によって実行時に更新されます。 パッケージが読み込まれると、パッケージの開発時に設定された値は、構成の値に置き換えられます。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、さまざまな種類の構成がサポートされます。 たとえば、複数の構成を含むことができる XML ファイルや、単一の構成を含む環境変数を使用できます。 詳細については、「[パッケージ構成](../../2014/integration-services/package-configurations.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[パッケージの構成を有効にする]**  
 パッケージで使用する構成を選択します。  
  
 **[構成名]**  
 構成の名前を表示します。  
  
 **[構成の種類]**  
 構成を格納する場所の種類を表示します。  
  
 **[構成文字列]**  
 構成値を格納する場所を表示します。 場所には、ファイルのパス、環境変数の名前、親パッケージ変数の名前、レジストリ キー、または [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] テーブルの名前を使用できます。  
  
 **[対象になるオブジェクト]**  
 構成を更新するオブジェクトの名前を表示します。 構成が XML 構成ファイルまたは SQL Server テーブルである場合は、構成に複数のオブジェクトを含むことができるため、この列は空白になります。  
  
 **[対象になるプロパティ]**  
 構成によって変更されるプロパティの名前を表示します。 構成の種類が複数の構成をサポートしている場合、この列は空白になります。  
  
 **[追加]**  
 パッケージ構成ウィザードを使用して構成を追加します。  
  
 **[編集]**  
 パッケージ構成ウィザードを再実行することにより、既存の構成を編集します。  
  
 **[削除]**  
 構成を選択してから、 **[削除]** をクリックします。  
  
 **矢印**  
 構成を選択し、上矢印および下矢印を使用して、構成を一覧の上または下に移動します。 構成は、一覧に表示された順序で読み込まれます。  
  
## <a name="see-also"></a>関連項目  
 [パッケージ構成を作成する](../../2014/integration-services/create-package-configurations.md)  
  
  
