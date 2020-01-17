---
title: 手順 3:パッケージとその他のファイルの追加 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: a7e6ec9c-d31d-4613-9525-8947a7b358f7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: be3dcb5bd42624ee943db4393809e2889808a11e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283837"
---
# <a name="lesson-1-3---adding-packages-and-other-files"></a>レッスン 1-3 - パッケージとその他のファイルの追加

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このタスクでは、既存のパッケージ、個々のパッケージをサポートする補助ファイル、および Readme を、前のタスクで作成した Deployment Tutorial プロジェクトに追加します。 たとえば、パッケージのデータを含んでいる XML データ ファイルや、プロジェクトのすべてのパッケージに関する Readme 情報を提供するテキスト ファイルを追加します。  
  
パッケージをテスト環境または運用環境に配置するとき、通常はデータ ファイルを配置に含めるのではなく、テスト バージョンまたは運用バージョンのデータ ファイルまたはデータベースにアクセスできるように、構成ファイルでデータ ソースへのパスを更新します。 このチュートリアルでは、手順を説明する目的で、データ ファイルをパッケージの配置に含めます。  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のサンプルをインストールすると、パッケージとパッケージで使用されるサンプル データがインストールされます。 Deployment Tutorial プロジェクトに次のパッケージを追加します。  
  
-   **DataTransfer。** フラット ファイルからデータを抽出し、列の値を評価して、条件に応じてデータセット内で行を維持し、データを AdventureWorks データベースのテーブルに読み込む基本パッケージです。  
  
-   **LoadXMLData。** XML データ ファイルからデータを抽出し、列の値を評価して集計し、AdventureWorks データベースのテーブルにデータを読み込むデータ転送パッケージです。  
  
これらのパッケージの配置をサポートするために、次の付属ファイルを Deployment Tutorial プロジェクトに追加します。  
  
|[パッケージ]|ファイル|  
|-----------|--------|  
|DataTransfer|NewCustomers.txt|  
|LoadXMLData|orders.xml および orders.xsd|  
  
また、Readme も追加します。これは、Deployment Tutorial プロジェクトに関する情報を提供するテキスト ファイルです。  
  
次の手順で使用するパスでは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のサンプルが既定の場所である [!INCLUDE[ssSampPathIS](../includes/sssamppathis-md.md)]にインストールされていることを前提としています。 サンプルを別の場所にインストールした場合は、手順でその場所を使用してください。  
  
次のタスクでは、DataTransfer パッケージと LoadXMLData パッケージに構成を追加します。 構成はすべて XML ファイルで保存され、システム環境変数を使用して、これらのファイルの場所を指定します。 構成ファイルを作成して、プロジェクトに追加します。  
  
### <a name="to-add-packages-to-the-deployment-tutorial-project"></a>Deployment Tutorial プロジェクトにパッケージを追加するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] がまだ開いていない場合は、 **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[Microsoft SQL Server]** の順にポイントして、 **[SQL Server Data Tools]** をクリックします。  
  
2.  **[ファイル]** メニューの **[開く]** をクリックし、 **[プロジェクト/ソリューション]** をクリックします。次に、 **[Deployment Tutorial]** フォルダーをクリックして **[開く]** をクリックし、 **Deployment Tutorial.sln**をダブルクリックします。  
  
3.  ソリューション エクスプローラーで、Deployment Tutorial を右クリックして  **追加** をクリックし、**既存のパッケージ** をクリックします。  
  
4.  **[既存のパッケージのコピーを追加]** ダイアログ ボックスの **[パッケージの場所]** で、 **[ファイル システム]** をクリックします。  
  
5.  参照ボタン ( **[...]** ) をクリックして、C:\Program Files\Microsoft SQL Server\100\Samples\Integration ServicesTutorial\Deploying Packages\Completed Packages に移動し、**DataTransfer.dtsx** をクリックして **[開く]** をクリックします。  
  
6.  **[OK]** をクリックします。  
  
7.  手順 3. ～ 6. を繰り返して LoadXMLData.dtsx を追加します。このパッケージは C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Completed Packages にあります。  
  
### <a name="to-add-ancillary-files-to-the-deployment-tutorial-project"></a>Deployment Tutorial プロジェクトに付属ファイルを追加するには  
  
1.  ソリューション エクスプローラーで、Deployment Tutorial を右クリックして  **追加** をクリックし、**既存の項目** をクリックします。  
  
2.  **[既存の項目の追加 - Deployment Tutorial]** ダイアログ ボックスで C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deployment Packages\Sample Data に移動し、orders.xml、orders.xsd、および NewCustomers.txt を選択して、 **[追加]** をクリックします。  
  
3.  **[既存の項目の追加 - Deployment Tutorial]** ダイアログ ボックスで C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deployment Packages\\に移動し、Readme.txt を選択して、 **[追加]** をクリックします。  
  
4.  ファイル メニューの  **すべてを保存** をクリックします。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
[手順 4:パッケージ構成の追加](../integration-services/lesson-1-4-adding-package-configurations.md)  
  
  
  
