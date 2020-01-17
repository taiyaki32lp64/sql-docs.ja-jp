---
title: 手順 1:作業フォルダーと環境変数の作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 45091ba2-ea3d-4399-9814-489d812b42cc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 08de88d45b31e4c00c9ce5a7790405c6da1542a2
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284134"
---
# <a name="lesson-1-1---creating-working-folders-and-environment-variables"></a>レッスン 1-1 - 作業フォルダーと環境変数の作成

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このタスクでは、この後のチュートリアル タスクで使用する作業フォルダー (C:\DeploymentTutorial) と新しいシステム環境変数 (`DataTransfer` および `LoadXMLData`) を作成します。  
  
作業フォルダーは、C ドライブのルートにあります。 別のドライブまたは場所を使用する必要がある場合は、変更してかまいません。 ただし、この場所を書き留めておいて、チュートリアルで DeploymentTutorial 作業フォルダーの場所が参照されたときに、該当する場所を使用する必要があります。  
  
この後のレッスンでは、ファイル システムに保存されているパッケージを msdb [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースの sysssispackages テーブルに配置します。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージは別のコンピューターに配置するのが理想的です。 これが不可能な場合でも、パッケージをローカル コンピューターの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスに配置してこのチュートリアルを実行すれば、多くのことを学習できます。 ローカル コンピューターと配置先コンピューターで使用する環境変数には同じ変数名が付いていますが、変数に格納される値は異なります。 たとえば、ローカル コンピューターでは、環境変数 `DataTransfer` の値は C:\DeploymentTutorial フォルダーを参照しています。一方、ターゲット コンピューターでは、環境変数 `DataTransfer` は C:\DeploymentTutorialInstall フォルダーを参照しています。  
  
ローカル コンピューターに配置する場合は、1 つのセットの環境変数を作成するだけで済みます。ただし、ローカルの配置を行う前に、環境変数を適切な値に更新する必要があります。  
  
パッケージを別のコンピューターに配置する場合は、2 つのセットの環境変数を作成する必要があります。1 つはローカル コンピューター用で、もう 1 つは配置先コンピューター用です。 現時点では、ソース コンピューター用の変数のみを作成できます。配置先コンピューター用の変数は後で作成しますが、配置先コンピューターにパッケージをインストールする前に、このコンピューターでフォルダーと環境変数が使用可能になっている必要があります。  
  
### <a name="to-create-the-local-working-folder"></a>ローカルの作業フォルダーを作成するには  
  
1.  [スタート] メニューを右クリックし、[エクスプローラー] をクリックします。  
  
2.  **[ローカル ディスク (C:)]** をクリックします。  
  
3.  **[ファイル]** メニューの **[新規作成]** をポイントし、 **[フォルダー]** をクリックします。  
  
4.  新規フォルダーの名前を「 **DeploymentTutorial**」に変更します。  
  
### <a name="to-create-local-environment-variables"></a>ローカルの環境変数を作成するには  
  
1.  **[スタート]** ボタンをクリックし、 **[コントロール パネル]** をクリックします。  
  
2.  コントロール パネルで、 **[システム]** をダブルクリックします。  
  
3.  **[システムのプロパティ]** ダイアログ ボックスで、 **[詳細設定]** タブをクリックし、 **[環境変数]** をクリックします。  
  
4.  **[環境変数]** ダイアログ ボックスの **[システム環境変数]** フレームで、 **[新規]** をクリックします。  
  
5.  **[新しいシステム変数]** ダイアログ ボックスで、 **[変数名]** ボックスに「 **DataTransfer** 」と入力し、 **[変数値]** ボックスに「 **C:\DeploymentTutorial\datatransferconfig.dtsconfig** 」と入力します。  
  
6.  **[OK]** をクリックします。  
  
7.  **[新規]** を再びクリックし、 **[変数名]** ボックスに「 **LoadXMLData** 」と入力し、 **[変数値]** ボックスに「 **C:\DeploymentTutorial\loadxmldataconfig.dtsconfig** 」と入力します。  
  
8.  **[OK]** をクリックして **[環境変数]** ダイアログ ボックスを閉じます。  
  
9. **[OK]** をクリックして **[システムのプロパティ]** ダイアログ ボックスを閉じます。  
  
10. 必要に応じて、コンピューターを再起動します。 コンピューターを再起動しない場合、新しい変数の名前はパッケージ構成ウィザードには表示されませんが、この変数を使用することはできます。  
  
### <a name="to-create-destination-environment-variables"></a>配置先の環境変数を作成するには  
  
1.  **[スタート]** ボタンをクリックし、 **[コントロール パネル]** をクリックします。  
  
2.  コントロール パネルで、 **[システム]** をダブルクリックします。  
  
3.  **[システムのプロパティ]** ダイアログ ボックスで、 **[詳細設定]** タブをクリックし、 **[環境変数]** をクリックします。  
  
4.  **[環境変数]** ダイアログ ボックスの **[システム環境変数]** フレームで、 **[新規]** をクリックします。  
  
5.  **[新しいシステム変数]** ダイアログ ボックスで、 **[変数名]** ボックスに「 **DataTransfer** 」と入力し、 **[変数値]** ボックスに「 **C:\DeploymentTutorialInstall\datatransferconfig.dtsconfig** 」と入力します。  
  
6.  **[OK]** をクリックします。  
  
7.  **[新規]** を再びクリックし、 **[変数名]** ボックスに「 **LoadXMLData** 」と入力し、 **[変数値]** ボックスに「 **C:\DeploymentTutorialInstall\loadxmldataconfig.dtsconfig** 」と入力します。  
  
8.  **[OK]** をクリックして **[環境変数]** ダイアログ ボックスを閉じます。  
  
9. **[OK]** をクリックして **[システムのプロパティ]** ダイアログ ボックスを閉じます。  
  
10. 必要に応じて、コンピューターを再起動します。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
[手順 2:配置プロジェクトの作成](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
  
  
