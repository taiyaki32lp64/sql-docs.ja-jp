---
title: 手順 1:新しい Integration Services プロジェクトを作成する | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: f14521b5-941e-443b-8f5e-385f98e37fbf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 74e56788741b36e68884db823fa46eb24856081e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296124"
---
# <a name="lesson-1-1-create-a-new-integration-services-project"></a>レッスン 1-1:新しい Integration Services プロジェクトを作成する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] でパッケージを作成するには、まず [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを作成する必要があります。 このサンプル プロジェクトには、データ変換ソリューションを構成するデータ ソース、データ ソース ビュー、パッケージのテンプレートが含まれています。  
  
この [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] チュートリアルで作成するパッケージは、ロケール依存型データの値を解釈します。 コンピューターが地域オプション **[英語 (米国)]** を使用するように構成されていない場合は、パッケージ内で追加のプロパティを設定する必要があります。 

レッスン 2 - 6 で使用するパッケージは、このレッスンで作成したパッケージからコピーされます。  
  
> [!NOTE]  
> まだ行っていない場合は、[レッスン 1 の前提条件](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)を参照してください。

## <a name="create-a-new-integration-services-project"></a>新しい Integration Services プロジェクトを作成する  
  
1.  Windows の **[スタート]** メニューで、**Visual Studio (SSDT)** を検索して選択します。  
  
2.  Visual Studio で、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択して、新しい [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを作成します。  
  
3.  **[新しいプロジェクト]** ダイアログ ボックスの **[インストール済み]** で **[ビジネス インテリジェンス]** を展開し、 **[テンプレート]** ペインで **[Integration Services プロジェクト]** を選択します。  
  
4.  **[名前]** ボックスに表示されている既定の名前を「 **SSIS Tutorial**」に変更します。 既に存在するフォルダーを使用するには、 **[ソリューションのディレクトリを作成]** チェック ボックスをオフにします。  
  
5.  既定の場所をそのまま使用するか、 **[参照]** を選択して使用するフォルダーを指定します。 **[プロジェクトの場所]** ダイアログ ボックスで、フォルダーを選択し、 **[フォルダーの選択]** を選択します。  
  
6.  **[OK]** を選択します。  
  
    既定では、**Package.dtsx** という名前の空のパッケージが作成され、**SSIS パッケージ**の下のプロジェクトに追加されます。  
  
7.  **ソリューション エクスプローラー**で **[Package.dtsx]** を右クリックし、 **[名前の変更]** を選択して、既定のパッケージ名を **Lesson 1.dtsx** に変更します。  
  
## <a name="go-to-next-task"></a>次の実習に進む
[手順 2:フラット ファイル接続マネージャーを追加し、構成する](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
