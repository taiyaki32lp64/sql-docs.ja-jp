---
title: 手順 2:プロジェクトをプロジェクト配置モデルに変換する | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 80964293-f1f5-4da7-b1fb-00ab8c30c1c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0563ceff3185f856692292884fe63e79c16e4216
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295881"
---
# <a name="lesson-6-2-convert-the-project-to-the-project-deployment-model"></a>レッスン 6-2:プロジェクトをプロジェクト配置モデルに変換する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



ここでは、Integration Services プロジェクトの変換ウィザードを使用して、プロジェクトをプロジェクト配置モデルに変換します。  
  
1.  **[プロジェクト]** メニューの **[プロジェクト配置モデルに変換]** を選択します。  
  
2.  **[Integration Services プロジェクトの変換ウィザードの概要]** **ページで**、手順を確認して **[次へ]** を選択します。  
  
3.  **[パッケージの選択]** ページの **[パッケージ]** の一覧で、 **[Lesson 6.dtsx]** を除くすべてのチェック ボックスをオフにし、 **[次へ]** を選択します。  
  
4.  **[プロジェクトのプロパティの指定]** ページで **[次へ]** を選択します。  
  
5.  **[パッケージ実行タスクの更新]** ページで **[次へ]** を選択します。  
  
6.  **[構成の選択]** ページで、 **[Lesson 6.dtsx]** パッケージが**構成**の一覧で選択されていることを確認し、 **[次へ]** を選択します。  
  
7.  **[パラメーターの作成]** ページで **[Lesson 6.dtsx]** パッケージが選択されていることを確認します。  **[構成プロパティ]** で **[スコープ]** が **[パッケージ]** になっていることを確認し、 **[次へ]** を選択します。  
  
8.  **[パラメーターの構成]** ページで、 **[名前]** と **[値]** の値が、レッスン 5 で変数と構成値に指定した名前と値と同じであることを確認し、 **[次へ]** を選択します。  
  
9. **[確認]** ページの **[概要]** ウィンドウで、ウィザードでは、変換される**プロパティ**を設定する目的で構成ファイルの情報が使用されたことに注意してください。  
  
10. **[変換]** を選択します。  
  
    変換の完了後、プロジェクトを保存するまで変更内容は保存されませんという警告メッセージが表示されます。 **[OK]** を選択し、警告ダイアログを閉じます。  
  
11. **Integration Services プロジェクトの変換ウィザード**で **[閉じる]** を選択します。  
  
12. **SQL Server Data Tools** で **[ファイル]** メニューを選択し、 **[保存]** を選択して変換済みのパッケージを保存します。  
  
13. **[パラメーター]** タブを選択し、**VarFolderName** のパラメーターがパッケージに含まれていることを確認します。 そのパラメーター値は、レッスン 5 の構成ファイルの **New Sample Data** フォルダーに指定されたものと同じパスです。  
  
## <a name="go-to-next-task"></a>次のタスクに進む
[ステップ 3:レッスン 6 のパッケージをテストする](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
  
  
