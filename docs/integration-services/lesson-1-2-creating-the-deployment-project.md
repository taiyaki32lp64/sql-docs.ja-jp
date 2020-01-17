---
title: 手順 2:配置プロジェクトの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 59990fe2-7036-4e9c-8efc-6ece9e66eda7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 26803904c22953b919c568b2798ecf02ad6a94a7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283755"
---
# <a name="lesson-1-2---creating-the-deployment-project"></a>レッスン 1-2 - 配置プロジェクトの作成

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]では、配置可能な単位は [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトになります。 パッケージを配置するには、まず新しい [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを作成し、すべてのパッケージと、これらのパッケージと共に配置する補助ファイルをそのプロジェクトに追加する必要があります。  
  
### <a name="to-create-the-integration-services-project"></a>Integration Services プロジェクトを作成するには  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[Microsoft SQL Server]** の順にポイントしてから、[SQL Server] の **[SQL Server Data Tools]** をクリックします。  
  
2.  新しい **プロジェクトを作成するため、** [ファイル] **メニューの**[新規作成] **をポイントし、** [プロジェクト] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] をクリックします。  
  
3.  **[新しいプロジェクト]** ダイアログ ボックスの **[テンプレート]** ペインで、 **[Integration Services プロジェクト]** をクリックします。  
  
4.  **[名前]** ボックスに表示されている既定の名前を「 **Deployment Tutorial**」に変更します。 必要に応じて、 **[ソリューションのディレクトリを作成]** チェック ボックスをオフにします。  
  
5.  既定の場所をそのまま使用するか、 **[参照]** をクリックして使用するフォルダーを指定します。  
  
6.  **[プロジェクトの場所]** ダイアログ ボックスで、目的のフォルダーをクリックして **[開く]** をクリックします。  
  
7.  **[OK]** をクリックします。  
  
8.  既定では、Package.dtsx という名前の空のパッケージが作成され、プロジェクトに追加されます。 ただし、このパッケージはここでは使用しません。代わりに既存のパッケージをプロジェクトに追加します。 プロジェクト内のすべてのパッケージを配置に含めるので、Package.dtsx は削除してください。 削除するには、Package.dtsx を右クリックし、 **[削除]** をクリックします。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
[ステップ 3:パッケージとその他のファイルの追加](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
## <a name="see-also"></a>参照  
[Integration Services (SSIS) プロジェクト](~/integration-services/integration-services-ssis-projects-and-solutions.md)  
  
  
  

