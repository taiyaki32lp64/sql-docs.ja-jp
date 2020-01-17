---
title: 手順 3:パッケージとその他のファイルの追加 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a7e6ec9c-d31d-4613-9525-8947a7b358f7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7db3e293c95b358d78e445e6b7534f90ea7b9310
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62892134"
---
# <a name="step-3-adding-packages-and-other-files"></a>手順 3:パッケージとその他のファイルの追加
  このタスクでは、既存のパッケージ、個々のパッケージをサポートする補助ファイル、および Readme を、前のタスクで作成した Deployment Tutorial プロジェクトに追加します。 たとえば、パッケージのデータを含んでいる XML データ ファイルや、プロジェクトのすべてのパッケージに関する Readme 情報を提供するテキスト ファイルを追加します。  
  
 パッケージをテスト環境または運用環境に配置するとき、通常はデータ ファイルを配置に含めるのではなく、テスト バージョンまたは運用バージョンのデータ ファイルまたはデータベースにアクセスできるように、構成ファイルでデータ ソースへのパスを更新します。 このチュートリアルでは、手順を説明する目的で、データ ファイルをパッケージの配置に含めます。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のサンプルをインストールすると、パッケージとパッケージで使用されるサンプル データがインストールされます。 Deployment Tutorial プロジェクトに次のパッケージを追加します。  
  
-   **DataTransfer。** フラット ファイルからデータを抽出し、列の値を評価して、条件に応じてデータセット内で行を維持し、データを AdventureWorks データベースのテーブルに読み込む基本パッケージです。  
  
-   **LoadXMLData。** XML データ ファイルからデータを抽出し、列の値を評価して集計し、AdventureWorks データベースのテーブルにデータを読み込むデータ転送パッケージです。  
  
 これらのパッケージの配置をサポートするために、次の付属ファイルを Deployment Tutorial プロジェクトに追加します。  
  
|[パッケージ]|ファイル|  
|-------------|----------|  
|DataTransfer|NewCustomers.txt|  
|LoadXMLData|orders.xml および orders.xsd|  
  
 また、Readme も追加します。これは、Deployment Tutorial プロジェクトに関する情報を提供するテキスト ファイルです。  
  
 次の手順で使用するパスでは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のサンプルが既定の場所である [!INCLUDE[ssSampPathIS](../includes/sssamppathis-md.md)]にインストールされていることを前提としています。 サンプルを別の場所にインストールした場合は、手順でその場所を使用してください。  
  
 次のタスクでは、DataTransfer パッケージと LoadXMLData パッケージに構成を追加します。 構成はすべて XML ファイルで保存され、システム環境変数を使用して、これらのファイルの場所を指定します。 構成ファイルを作成して、プロジェクトに追加します。  
  
### <a name="to-add-packages-to-the-deployment-tutorial-project"></a>Deployment Tutorial プロジェクトにパッケージを追加するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] がまだ開いていない場合は、 **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[Microsoft SQL Server]** の順にポイントして、 **[SQL Server Data Tools]** をクリックします。  
  
2.  **[ファイル]** メニューの **[開く]** をクリックし、 **[プロジェクト/ソリューション]** をクリックします。次に、 **[Deployment Tutorial]** フォルダーをクリックして **[開く]** をクリックし、 **Deployment Tutorial.sln**をダブルクリックします。  
  
3.  ソリューション エクスプローラーで、[Deployment Tutorial] を右クリックして **[追加]** をクリックし、 **[既存のパッケージ]** をクリックします。  
  
4.  **[既存のパッケージのコピーを追加]** ダイアログ ボックスの **[パッケージの場所]** で、 **[ファイル システム]** をクリックします。  
  
5.  参照ボタン ( **[...]** ) をクリックして、C:\Program Files\Microsoft SQL Server\100\Samples\Integration ServicesTutorial\Deploying Packages\Completed Packages に移動し、**DataTransfer.dtsx** をクリックして **[開く]** をクリックします。  
  
6.  **[OK]** をクリックします。  
  
7.  手順 3. ～ 6. を繰り返して LoadXMLData.dtsx を追加します。このパッケージは C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Completed Packages にあります。  
  
### <a name="to-add-ancillary-files-to-the-deployment-tutorial-project"></a>Deployment Tutorial プロジェクトに付属ファイルを追加するには  
  
1.  ソリューション エクスプローラーで、[Deployment Tutorial] を右クリックして **[追加]** をクリックし、 **[既存の項目]** をクリックします。  
  
2.  **[既存の項目の追加 - Deployment Tutorial]** ダイアログ ボックスで C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deployment Packages\Sample Data に移動し、orders.xml、orders.xsd、および NewCustomers.txt を選択して、 **[追加]** をクリックします。  
  
3.  **[既存の項目の追加 - Deployment Tutorial]** ダイアログ ボックスで C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deployment Packages\\に移動し、Readme.txt を選択して、 **[追加]** をクリックします。  
  
4.  [ファイル] メニューの **[すべてを保存]** をクリックします。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [手順 4:パッケージ構成の追加](../integration-services/lesson-1-4-adding-package-configurations.md)  
  
![Integration Services のアイコン (小)](media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
  
