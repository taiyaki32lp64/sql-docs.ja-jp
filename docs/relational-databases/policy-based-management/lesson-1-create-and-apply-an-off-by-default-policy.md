---
title: レッスン 1:"既定でオフ" ポリシーの作成と適用
description: SQL Server でポリシーベース管理に "既定でオフ" ポリシーを作成して適用する方法について説明するチュートリアル。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.technology: security
ms.prod_service: database-engine
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d31367db-b7db-44c4-8df2-f1240474cf78
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1bff30a7270be7b47e5bf718d07d5386951042f1
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558007"
---
# <a name="lesson-1-create-and-apply-an-off-by-default-policy"></a>レッスン 1:"既定でオフ" ポリシーの作成と適用
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
ポリシー ベースの管理ポリシーを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の複数のインスタンス、複数のインスタンス オブジェクト、1 つのサーバー インスタンス、複数のデータベース、または複数のデータベース オブジェクトを管理できます。 データベース管理者は、特定のサーバーでデータベース メールが有効化されないようにすることができます。 このレッスンでは、このようなサーバー オプションを設定する条件およびポリシーを作成し、 サーバーがこのポリシーに準拠しているかどうかを確認するためにサーバーをテストします。 次に、このポリシーを使用してサーバーを再構成し、サーバーがポリシーに準拠するようにします。  

## <a name="prerequisites"></a>前提条件
このチュートリアルを完了するには、SQL Server Management Studio と SQL Server を実行しているサーバーへのアクセスが必要です。 

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールします。
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads) をインストールする。
  
## <a name="create-the-mail-off-condition"></a>メールをオフ条件の作成

1.  オブジェクト エクスプローラーで、 **[管理]** 、 **[ポリシー管理]** 、 **[ファセット]** の順に展開し、 **[セキュリティ構成]** を右クリックして **[新しい条件]** をクリックします。  

    ![新しい条件](Media/lesson-1-create-and-apply-an-off-by-default-policy/new-surface-area-condition.png)
  
2.  **[新しい条件の作成]** ダイアログ ボックスで、 **[名前]** ボックスに「 **メールをオフ**」と入力します。   
    1. **[ファセット]** ボックスで、 **[セキュリティ構成]** ファセットが選択されていることを確認します。
    1. **[式]** 領域の **[フィールド]** ボックスで **\@DatabaseMailEnabled** を選択し、 **[演算子]** ボックスで **=** を選択して、 **[値]** ボックスで **[False]** を選択します。  
    1. **[説明]** ページで条件の説明を入力し、 **[OK]** をクリックして条件を作成します。  

    ![メールをオフ条件](Media/lesson-1-create-and-apply-an-off-by-default-policy/mail-off-condition.png) 
  
## <a name="create-the-off-by-default-policy"></a>既定でオフ ポリシーの作成  
  
1.  オブジェクト エクスプローラーで、 **[セキュリティ構成]** を右クリックし、 **[新しいポリシー]** をクリックします。  
  
2.  **[新しいポリシーの作成]** ダイアログ ボックスで、 **[名前]** ボックスに「 **既定でオフ**」と入力します。 
    1. **[有効]** チェック ボックスはオフのままにします。 **[有効]** チェック ボックスは自動ポリシーに適用され、このポリシーは要求時に実行されます。
    1. **[条件の確認]** チェック ボックスを下にスクロールして **[セキュリティ構成]** 領域を表示し、確認する条件として **[メールをオフ]** を選択します。
    1. サーバー スコープのポリシーなので、 **[対象]** ボックスは空白になります。 
    1. **[評価モード]** チェック ボックスで、 **[要求時]** を評価モードとして選択します。
    1. **[サーバーの制限]** チェック ボックスで **[なし]** を選択します。
    1. **[説明]** ページでポリシーの説明を入力します。  

    ![既定でオフ ポリシー](Media/lesson-1-create-and-apply-an-off-by-default-policy/off-by-default-policy.png)
  
9. 説明のページの **[追加のヘルプ ハイパーリンク]** 領域で、ポリシーの Web ページへのハイパーリンクを指定できます。 **[表示するテキスト]** ボックスに、ハイパーリンクに表示するテキストを入力します。
    1. **[アドレス]** ボックスに、会社の IT 部門のホーム ページなどのヘルプ ページへのハイパーリンクを入力します。
    1. Web ページを開いてアドレスを確認するには、 **[リンクのテスト]** をクリックします。
    1. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

    ![既定でオフ ポリシーの Web リンク](Media/lesson-1-create-and-apply-an-off-by-default-policy/off-by-default-policy-web-link.png)


## <a name="configure-server-to-run-off-by-default-policy"></a>既定でオフ ポリシーを実行するためのサーバーの構成 

1.  オブジェクト エクスプローラーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス名を右クリックし、 **[ポリシー]** をポイントして、 **[評価]** をクリックします。  

    ![ポリシーの評価](Media/lesson-1-create-and-apply-an-off-by-default-policy/evaluate-policy.png)
  
2.  **[ポリシーの評価]** ダイアログ ボックスで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の別のインスタンスから、またはファイルからポリシーを選択できます。 この手順では、 **[ソース]** を [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに設定したままにしてください。  
    1. **[ポリシー]** セクションで、 **[既定でオフ]** ポリシーを選択します。
    1. サーバーがポリシーに準拠しているかどうかを確認するには、 **[評価]** をクリックします。
    1. **[結果]** 領域では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] がポリシーに準拠している場合にチェック マークの付いた緑の円が表示されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] がポリシーに準拠していない場合は、X の付いた赤い円が表示されます。 

   ![既定でオフ ポリシーの評価](Media/lesson-1-create-and-apply-an-off-by-default-policy/evaluate-off-by-default-policy.png)

  
6.  **[対象の詳細]** 領域では、エラーが発生すると、 **[メッセージ]** 列に詳細情報が表示されます。 **[メッセージ]** 列では、 **[表示]** をクリックすると、確認された各ファセット プロパティの確認結果を示すレポートが表示されます。 

    ![ポリシーの評価結果の表示](Media/lesson-1-create-and-apply-an-off-by-default-policy/view-results-of-policy-evaluation.png)
  
7.  ページの下部にポリシーの説明が表示され、 **[追加のヘルプ]** セクションにポリシーに対して構成したハイパーリンクが表示されます。 メッセージ ハイパーリンクをクリックすると、ポリシー作成時に指定した Web ページが開きます。   

1.  ブラウザーを閉じ、 **[結果の詳細ビュー]** ダイアログ ボックスを閉じます。  

1. サーバーが準拠していない場合に、データベース メールを無効にするには、 **[評価の結果]** ページで **[適用]** をクリックします。  
  
10. **[結果の詳細ビュー]** と **[ポリシーの評価]** の両方のダイアログ ボックスを閉じます。   

   
## <a name="next-lesson"></a>次のレッスン  
[レッスン 2:名前付け基準ポリシーの作成と適用](../../relational-databases/policy-based-management/lesson-2-create-and-apply-a-naming-standards-policy.md)  
  
  
  
