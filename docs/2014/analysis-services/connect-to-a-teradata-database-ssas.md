---
title: Teradata データベース (SSAS) への接続 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connterradb.f1
ms.assetid: 875ad4a3-a2b3-4b68-8c1c-6507e9f25b4d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dc6712598452b1957857509e6b3ff6f659a16c4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087186"
---
# <a name="connect-to-a-teradata-database-ssas"></a>[Teradata データベースへの接続] (SSAS)
  **テーブルのインポート ウィザード**のこのページを使用すると、Teradata データベースに接続するための設定を指定できます。 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]からウィザードにアクセスするには、 **[モデル]** メニューの **[データ ソースからのインポート]** をクリックします。  
  
 データ ソースに接続するには、適切なプロバイダーがコンピューターにインストールされている必要があります。  
  
> [!NOTE]  
>  このページでデータベースを選択する際には、現在のユーザーの資格情報が使用されます。 ただし、[権限借用情報] ページで指定されたユーザーに、選択したデータベースの読み取り権限がないと、インポートは成功しません。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 **接続の表示名**  
 このデータ ソース接続の一意の名前を入力します。 このフィールドは必須です。  
  
 **サーバー名**  
 接続するサーバー インスタンスの名前を入力または選択します。  
  
 **ユーザー名**  
 データベース接続に使用するユーザー名を指定します。  
  
 このユーザー名は、データ ソースの接続文字列を構築するときに使用されます。 [テーブルのプロパティ] ウィンドウおよびインポート ウィザードでデータのプレビューまたはフィルター処理を行う際も、これらの資格情報が使用されます。 データをインポートまたは更新する際には、これらの資格情報は使用されず、[権限借用情報] ページで指定された Windows の資格情報が使用されます。  
  
 **Password**  
 データベース接続に使用するパスワードを指定します。  
  
 **パスワードを保存します。**  
 **[パスワード]** ボックスに入力したパスワードを保存する必要があるかどうかを指定します。  
  
 **詳細設定**  
 **[詳細プロパティの設定]** ダイアログ ボックスを使用して追加の接続プロパティを設定します。 詳細については、「[[詳細プロパティの設定] (SSAS)](set-advanced-properties-ssas.md)」を参照してください。  
  
 **[接続テスト]**  
 現在の設定を使用して、データ ソースに対する接続の確立を試みます。 接続が正常に確立されたかどうかを示すメッセージが表示されます。  
  
  
