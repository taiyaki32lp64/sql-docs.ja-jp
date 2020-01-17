---
title: 配置ユーティリティを使用してパッケージの展開 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], installing
- installing packages
- dependencies [Integration Services]
- deploying packages [Integration Services], installing
ms.assetid: eaf4b56e-2023-4d17-971c-703031da758c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 73b71e83f3b0f0f895b2cc5b8fd3495fb4893a32
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059623"
---
# <a name="deploy-packages-by-using-the-deployment-utility"></a>配置ユーティリティを使用してパッケージを配置する
  配置ユーティリティを構築し、その配置ユーティリティが構築されたコンピューター以外のコンピューターに [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトのパッケージをインストールする場合は、最初に配置フォルダーを目的のコンピューターにコピーする必要があります。  
  
 配置フォルダーのパスは、配置ユーティリティを作成した [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトの DeploymentOutputPath プロパティで指定されます。 既定のパスは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを基準とする bin\Deployment です。 詳細については、「 [配置ユーティリティを作成する](../../2014/integration-services/create-a-deployment-utility.md)」を参照してください。  
  
 パッケージ インストール ウィザードを使用してパッケージをインストールします。 ウィザードを起動し、配置フォルダーをサーバーにコピーしてから、配置ユーティリティ ファイルをダブルクリックします。 このファイルは、\<プロジェクト名>.SSISDeploymentManifest という名前で、インストール先のコンピューターの配置フォルダーにあります。  
  
> [!NOTE]  
>  配置するパッケージのバージョンによっては、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の異なるバージョンがサイド バイ サイドでインストールされている場合にエラーが発生する可能性があります。 このエラーが発生するのは、.SSISDeploymentManifest ファイル名拡張子が [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]のすべてのバージョンで同じであるためです。 このファイルをダブルクリックすると、最後にインストールしたバージョンの [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]のインストーラー (dtsinstall.exe) が呼び出されますが、配置ユーティリティ ファイルとはバージョンが異なる場合があります。 この問題を回避するには、コマンド ラインから正しいバージョンの dtsinstall.exe を実行し、配置ユーティリティ ファイルのパスを指定します。  
  
 パッケージ インストール ウィザードを使用すると、手順に従ってパッケージをファイル システムまたは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]にインストールできます。 インストールは、次の方法で構成できます。  
  
-   パッケージをインストールする場所の種類と場所を選択します。  
  
-   パッケージの依存関係をインストールする場所を選択します。  
  
-   パッケージがターゲット サーバーにインストールされた後に、パッケージを検証します。  
  
 パッケージのファイル ベースの依存関係は、必ずファイル システムにインストールされます。 パッケージをファイル システムにインストールする場合、依存関係は、パッケージ用に指定したのと同じフォルダーにインストールされます。 パッケージを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]にインストールする場合は、ファイル ベースの依存関係を格納するフォルダーを指定できます。  
  
 パッケージに含まれている構成をインストール先のコンピューター用に合わせて変更したい場合は、ウィザードを使ってプロパティの値を更新できます。  
  
 パッケージ インストール ウィザードを使ってパッケージをインストールする方法に加えて、 **dtutil** コマンド プロンプト ユーティリティを使ってパッケージをコピーおよび移動する方法があります。 詳細については、「 [dtutil ユーティリティ](dtutil-utility.md)」を参照してください。  
  
### <a name="to-deploy-packages-to-an-instance-of-sql-server"></a>SQL Server のインスタンスにパッケージを配置するには  
  
1.  ターゲット コンピューターの配置フォルダーを開きます。  
  
2.  \<プロジェクト名>.SSISDeploymentManifest という名前のマニフェスト ファイルをダブルクリックしてパッケージ インストール ウィザードを起動します。  
  
3.  **[SSIS パッケージの配置]** ページで、 **[SQL Server に配置]** オプションを選択します。  
  
4.  必要に応じて、ターゲット サーバーにパッケージがインストールされた後で検証を行う場合は、 **[インストール後にパッケージを検証する]** を選択します。  
  
5.  **[インストール先の SQL Server の指定]** ページで、パッケージをインストールする [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスを指定し、認証モードを選択します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証を選択する場合は、ユーザー名とパスワードを入力する必要があります。  
  
6.  **[インストール フォルダーの選択]** ページで、パッケージの依存関係をインストールするファイル システムのフォルダーを指定します。  
  
7.  パッケージに構成が含まれる場合は、[パッケージの構成] ページで構成を編集して、 **[値]** の一覧の値を更新できます。  
  
8.  インストール後にパッケージの検証を行うように選択した場合、配置したパッケージの検証結果が表示されます。  
  
## <a name="see-also"></a>参照  
 [パッケージの配置&#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)  
  
  
