---
title: プロジェクトまたはソリューションとしてスクリプトを保存する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 72dfd37f-dbe7-4d1d-bda6-7eb54c7922d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6d17dd44f597d7b3ddfce574670e9e6bfd55f908
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62753045"
---
# <a name="save-scripts-as-projects-or-solutions"></a>プロジェクトまたはソリューションとしてスクリプトを保存する
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio を使い慣れている開発者であれば、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のソリューション エクスプローラーにもすぐに慣れることができます。 業務を支援するスクリプトはスクリプト プロジェクトにグループ化することができ、スクリプト プロジェクトはソリューションとしてまとめて管理できます。 スクリプト プロジェクトまたはソリューションに格納したスクリプトは、グループとして一括して開けるほか、Visual SourceSafe などのソース管理製品にまとめて保存することができます。 スクリプト プロジェクトは、スクリプトを適切に実行するための接続情報を保持し、テキスト ファイルなどの非スクリプト ファイルを保持することもできます。  
  
 次の実習では、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースにクエリを実行する短いスクリプトを作成し、スクリプト プロジェクトとソリューションに格納します。  
  
## <a name="using-script-projects-and-solutions"></a>スクリプト プロジェクトとソリューションの使用  
  
#### <a name="to-create-a-script-project-and-solution"></a>スクリプト プロジェクトとソリューションを作成するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]を開き、オブジェクト エクスプローラーを使用してサーバーに接続します。  
  
2.  **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。 **[新しいプロジェクト]** ダイアログ ボックスが開きます。  
  
3.  **[名前]** ボックスに「 **StatusCheck**」と入力し、 **[テンプレート]** で **[SQL Server スクリプト]** をクリックして、 **[OK]** をクリックします。新しいソリューションとスクリプト プロジェクトが開きます。  
  
4.  ソリューション エクスプローラーで **[接続]** を右クリックし、 **[新しい接続]** をクリックします。 **[サーバーへの接続]** ダイアログ ボックスが開きます。  
  
5.  **[サーバー名]** ボックスにサーバー名を入力します。  
  
6.  **[オプション]** をクリックし、 **[接続プロパティ]** タブをクリックします。  
  
7.  **[データベースへの接続]** ボックスで [サーバーの参照] をクリックし、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースを選択して、 **[接続]** をクリックします。 指定したデータベースを含む接続情報がプロジェクトに追加されます。  
  
8.  [プロパティ] ウィンドウが表示されない場合は、ソリューション エクスプローラーで新しい接続をクリックし、F4 キーを押します。 接続のプロパティが表示され、 **初期データベース** が [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]であることなどの接続情報が示されます。  
  
9. ソリューション エクスプローラーで接続を右クリックし、 **[新しいクエリ]** をクリックします。 **SQLQuery1.sql** という名前の新しいクエリが作成され、サーバー上の [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースに接続されます。さらに、スクリプト プロジェクトにこのクエリが追加されます。  
  
10. クエリ エディターに次のクエリを入力します。ここでは、期限が設けられており、まだ開始日に至っていない作業命令の数を調べます (チュートリアル ウィンドウからコードをコピーして、貼り付けることができます)。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT COUNT(WorkOrderID)  
    FROM Production.WorkOrder  
    WHERE DueDate < StartDate;  
  
    ```  
  
    > [!NOTE]  
    >  クエリを入力するスペースが足りない場合は、Shift + Alt + Enter キーを押して全画面モードに切り替えてください。  
  
11. ソリューション エクスプローラーで **SQLQuery1**を右クリックし、 **[名前の変更]** をクリックします。 型**Check Workorders.sql**クエリと ENTER キーを押して新しい名前として。  
  
12. ソリューションとスクリプト プロジェクトを保存するには、 **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [概要:ソリューションとスクリプト プロジェクト](lesson-3-4-summary-solutions-and-script-projects.md)  
  
  
