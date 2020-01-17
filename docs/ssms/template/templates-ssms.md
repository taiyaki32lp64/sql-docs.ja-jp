---
title: SQL Server Management Studio でテンプレートを使用する
description: SSMS でのテンプレートの使用に関するチュートリアルです。
keywords: SQL Server, SSMS, SQL Server Management Studio, テンプレート
author: MashaMSFT
ms.author: mathoma
ms.topic: tutorial
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
helpviewer_keywords:
- templates [SQL Server], SQL Server Management Studio
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.custom: ''
ms.date: 03/13/2018
ms.openlocfilehash: b3df46f3536c488ff863287a0efb26ed7063ffc2
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266635"
---
# <a name="use-templates-in-sql-server-management-studio"></a>SQL Server Management Studio でテンプレートを使用する

このチュートリアルでは、SQL Server Management Studio (SSMS) で使用できる作成済みの Transact-SQL (T-SQL) テンプレートについて説明します。 この記事では、次の方法を学習します。

## <a name="prerequisites"></a>Prerequisites

このチュートリアルを実行するには、SQL Server Management Studio と、SQL Server へのアクセスが必要です。

* [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールする。

* [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads) をインストールする。

## <a name="use-template-browser"></a>テンプレート ブラウザーを使用する

このセクションでは、テンプレート ブラウザーの場所を探して使う方法を説明します。

1. SQL Server Management Studio を開きます。

2. **[表示]** メニューの **[テンプレート ブラウザー]** を選択します (Ctrl + Alt + T)。

    ![テンプレート ブラウザーを開く](media/templates-ssms/templatebrowser.png)

    テンプレート ブラウザーの下部には、最近使ったテンプレートが表示されます。

3. 対象のノードを展開します。 テンプレートを右クリックして、 **[開く]** を選びます。

    ![テンプレートを開く](media/templates-ssms/opentemplate.png)

    テンプレート名をダブルクリックして開くこともできます。

4. 新しいクエリ ウィンドウが開きます。 T-SQL スクリプトは既に設定されています。

5. 必要に応じてテンプレートを変更し、 **[実行]** を選んでクエリを実行します。

    ![DB テンプレートを作成する](media/templates-ssms/createdbtemplate.png)

## <a name="edit-an-existing-template"></a>既存のテンプレートを編集する

テンプレート ブラウザーでは、既存のテンプレートを編集することもできます。  

1. テンプレート ブラウザーで、操作するテンプレートに移動します。

2. テンプレートを右クリックして、 **[編集]** を選びます。

    ![テンプレートを編集する](media/templates-ssms/edittemplate.png)

3. 開いたクエリ ウィンドウで、必要な変更を加えます。

4. テンプレートを保存するには、 **[ファイル]**  >  **[保存]** (Ctrl + S) の順に選択します。

5. クエリ ウィンドウを閉じます。

6. テンプレートをもう一度開きます。 編集内容が表示されます。

## <a name="locate-templates-on-disk"></a>ディスク上のテンプレートを探す

テンプレートが開いたら、ディスク上にあるテンプレートを探すことができます。

1. テンプレート ブラウザーで、テンプレートを選択し、 **[編集]** を選びます。

2. **[クエリ タイトル]** を右クリックしてから、 **[1 つ上のフォルダーを開く]** を選択します。 エクスプローラーが開き、テンプレートが格納されているディスク上の場所が示されます。 

   ![ディスク上のテンプレート](media/templates-ssms/templatesondisk.png)
  
## <a name="create-a-new-template"></a>新しいテンプレートを作成する

テンプレート ブラウザーで新しいテンプレートを作成することもできます。 以下の手順では、新しいフォルダーを作成し、そのフォルダーに新しいテンプレートを作成する方法を示します。 これらの手順を使用して、既存のフォルダーにカスタム テンプレートを作成することもできます。 

1. テンプレート ブラウザーを開きます。

2. **[SQL Server テンプレート]** を右クリックし、 **[新規]**  >  **[フォルダー]** の順に選択します。

3. このフォルダーの名前を「**カスタム テンプレート**」に設定します。

    ![カスタム テンプレート フォルダーを作成する](media/templates-ssms/creatingcustomtemplate.png)

4. 新しく作成したカスタム テンプレート フォルダーを右クリックし、 **[新規]**  >  **[テンプレート]** の順に選択します。 テンプレートの名前を入力します。

    ![カスタム テンプレートを作成する](media/templates-ssms/createnewtemplate.png)

5. 作成したテンプレートを右クリックして、 **[編集]** を選びます。 新しいクエリ ウィンドウが開きます。

6. 保存する T-SQL テキストを入力します。

7. **[ファイル]** メニューの **[保存]** を選択します。

8. 既存のクエリ ウィンドウを閉じて、新しいカスタム テンプレートを開きます。

## <a name="next-steps"></a>次の手順

SSMS に慣れ親しむには、実践的な経験を積むのが最も効果的です。 以下の "*チュートリアル*" と "*操作方法*" に関する記事は、SSMS 内で使用できるさまざまな機能を使用するのに役立ちます。  以下の記事では、SSMS のコンポーネントを管理する方法と、頻繁に使用する機能にアクセスする方法が説明されています。

* [インスタンスに接続してクエリを実行する](../tutorials/connect-query-sql-server.md)
* [スクリプトの作成](../tutorials/scripting-ssms.md)
* [SSMS を構成する](../tutorials/ssms-configuration.md)
* [SSMS を使用するための追加のヒントとテクニック](../tutorials/ssms-tricks.md)