---
title: 手順 1:レッスン 4 のパッケージをコピーする | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 8aa7d690-4649-4c0a-ac6f-9504637ee426
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 17a72f7d11a2ed743bbede2852b6336ce808a75d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295929"
---
# <a name="lesson-5-1-copy-the-lesson-4-package"></a>レッスン 5-1:レッスン 4 のパッケージをコピーする

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



ここでは、レッスン 4 で作成した **Lesson 4.dtsx** パッケージのコピーを作成します。 レッスン 4 を終了していない場合は、チュートリアルに含まれている、レッスン 4 を完了した状態のパッケージをプロジェクトに追加し、作業用のコピーを作成することもできます。 レッスン 5 の残りの実習では、このパッケージの新しいコピーを使用します。  
  
## <a name="create-the-lesson-5-package"></a>レッスン 5 のパッケージを作成する  
  
完了したレッスン 4 をコピーする場合は、この手順を使用します。  レッスン 4 のサンプルをコピーするには、次のセクションを参照してください。

1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools がまだ開いていない場合は、 **[開始]**  >  **[すべてのプログラム]**  >  **[Microsoft SQL Server 2017]** の順に選択し、次に **[SQL Server Data Tools]** を選択します。

2.  **[ファイル]** メニューで、 **[開く]**  >  **[プロジェクト/ソリューション]** の順に選択し、 **[SSIS Tutorial]** フォルダーを選択し、 **[開く]** を選択します。  次に、 **[SSIS Tutorial.sln]** をダブルクリックします。

3.  **ソリューション エクスプローラー**で、 **[Lesson 4.dtsx]** を右クリックし、 **[コピー]** を選択します。

4.  **ソリューション エクスプローラー**で、 **[SSIS パッケージ]** を右クリックし、 **[貼り付け]** を選択します。

    コピーしたパッケージの既定の名前は、**Lesson 4.dtsx** です。

5.  **ソリューション エクスプローラー**で **[Lesson 4.dtsx]** をダブルクリックし、パッケージを開きます。

6.  **[制御フロー]** デザイン画面の背景上で任意の場所を右クリックし、 **[プロパティ]** を選択します。

7.  **[プロパティ]** ウィンドウで、**Name** プロパティを **Lesson 5** に変更します。

8.  **ID** プロパティのボックスを選択し、ドロップダウン矢印を選択し、 **[\<新しい ID の生成>]** を選択します。

## <a name="add-the-completed-lesson-4-package"></a>レッスン 4 を完了した状態のパッケージを追加する

1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools を開き、SSIS Tutorial プロジェクトを開きます。

2.  **ソリューション エクスプローラー**で **[SSIS パッケージ]** を右クリックし、 **[既存のパッケージを追加]** を選択します。

3.  **[既存のパッケージのコピーを追加]** ダイアログ ボックスの **[パッケージの場所]** で、 **[ファイル システム]** をクリックします。

4.  参照ボタン **[...]** を選択し、ご利用のコンピューター上の **Lesson 4.dtsx** に移動して、 **[開く]** を選択します。

5.  前のセクションの手順 3 から 8 の説明に従って、レッスン 4 パッケージをコピーして貼り付けます。
  
## <a name="go-to-next-task"></a>次のタスクに進む  
[手順 2:パッケージ構成の有効化と構成](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
