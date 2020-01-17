---
title: 手順 2:プロジェクトをプロジェクト配置モデルに変換する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 80964293-f1f5-4da7-b1fb-00ab8c30c1c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1ba6dcb7052fed3d209dd87f55789a99df24116c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767354"
---
# <a name="step-2-converting-the-project-to-the-project-deployment-model"></a>手順 2:プロジェクトをプロジェクト配置モデルに変換する
  ここでは、Integration Services プロジェクトの変換ウィザードを使用して、プロジェクトをプロジェクト配置モデルに変換します。  
  
### <a name="converting-the-project-to-the-project-deployment-model"></a>プロジェクトをプロジェクト配置モデルに変換する  
  
1.  [プロジェクト] メニューの [プロジェクト配置モデルに変換] をクリックします。  
  
2.  [Integration Services プロジェクトの変換ウィザードの概要] ページで、手順を確認して [次へ] をクリックします。  
  
3.  [パッケージの選択] ページの [パッケージ] の一覧で、[Lesson 6.dtsx] を除くすべてのチェック ボックスをオフにし、[次へ] をクリックします。  
  
4.  [プロジェクトのプロパティの指定] ページで [次へ] をクリックします。  
  
5.  [パッケージ実行タスクの更新] ページで [次へ] をクリックします。  
  
6.  [構成の選択] ページで、[Lesson 6.dtsx] パッケージが構成の一覧で選択されていることを確認し、[次へ] をクリックします。  
  
7.  [パラメーターの作成] ページの構成プロパティの一覧で、[Lesson 6.dtsx] パッケージが選択され、[スコープ] が [パッケージ] に設定されていることを確認し、[次へ] をクリックします。  
  
8.  [パラメーターの構成] ページで、[名前と値] の値が、レッスン 5 で変数と構成値に指定した名前および値と同じであることを確認し、[次へ] をクリックします。  
  
9. [確認] ページの [概要] ウィンドウで、ウィザードは、構成ファイルの情報を使用して変換するプロパティを設定することに注意してください。  
  
10. [変換] をクリックします。  
  
     変換が完了すると、プロジェクトが Visual Studio に保存されるまで変更が保存されないことを警告するメッセージ表示されます。 警告ダイアログで [OK] をクリックします。  
  
11. Integration Services プロジェクトの変換ウィザードで [閉じる] をクリックします。  
  
12. SQL Server Data Tools で [ファイル] メニューをクリックし、[保存] をクリックして変換されたパッケージを保存します。  
  
13. [パラメーター] タブをクリックし、パッケージが VarFolderName のパラメーターに含まれ、値がレッスン 5 の構成ファイルの新しいサンプル データ フォルダーに指定されたパスと同じであることを確認します。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [ステップ 3:レッスン 6 パッケージのテスト](lesson-6-3-testing-the-lesson-6-package.md)  
  
  
