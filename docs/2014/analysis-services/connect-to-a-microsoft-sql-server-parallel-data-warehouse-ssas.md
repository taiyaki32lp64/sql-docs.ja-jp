---
title: Microsoft SQL Server 並列データ ウェアハウス (SSAS) への接続 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connsqlparadatawh.f1
ms.assetid: 98c879ee-7257-40c9-bc85-6766bd3b4885
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7ab10518ff976562665317a75574ee2070be0d8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087200"
---
# <a name="connect-to-a-microsoft-sql-server-parallel-data-warehouse-ssas"></a>[Microsoft SQL Server 並列データ ウェアハウスへの接続] (SSAS)
  **テーブルのインポート ウィザード**のこのページを使用すると、Microsoft SQL Server 並列データ ウェアハウス (PDW) に接続するための設定を指定できます。 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]からウィザードにアクセスするには、 **[モデル]** メニューの **[データ ソースからのインポート]** をクリックします。  
  
 SQL Server PDW は、非常にスケーラブルなアプライアンスであり、超並列処理によって低コストで優れたパフォーマンスを提供します。 SQL Server PDW の詳細については、Web サイト「 [SQL Server 2008 R2 並列データ ウェアハウス](https://go.microsoft.com/fwlink/?LinkId=150895)」を参照してください。 データ ウェアハウスには、SQL Server 認証を使用して接続します。 データ ソースに接続するには、適切なプロバイダーがコンピューターにインストールされている必要があります。  
  
> [!NOTE]  
>  このページでデータベースを選択する際には、現在のユーザーの資格情報が使用されます。 ただし、[権限借用情報] ページで指定されたユーザーに、選択したデータベースの読み取り権限がないと、インポートは成功しません。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 **接続の表示名**  
 このデータ ソース接続の一意の名前を入力します。 このフィールドは必須です。  
  
 **サーバー名**  
 接続するサーバーの名前または IP アドレスを入力します。  
  
 **ユーザー名**  
 データベース接続に使用するユーザー名を指定します。  
  
 このユーザー名は、データ ソースの接続文字列を構築するときに使用されます。 [テーブルのプロパティ] ウィンドウおよびインポート ウィザードでデータのプレビューまたはフィルター処理を行う際も、これらの資格情報が使用されます。 データをインポートまたは更新する際には、これらの資格情報は使用されず、[権限借用情報] ページで指定された Windows の資格情報が使用されます。  
  
 **Password**  
 データベース接続に使用するパスワードを指定します。  
  
 **パスワードを保存します。**  
 **[パスワード]** ボックスに入力したパスワードを保存するかどうかを指定します。  
  
 **データベース名**  
 データベースを一覧から選択します。  
  
 **詳細設定**  
 **[詳細プロパティの設定]** ダイアログ ボックスを使用して追加の接続プロパティを設定します。 詳細については、「[[詳細プロパティの設定] (SSAS)](set-advanced-properties-ssas.md)」を参照してください。  
  
 **[接続テスト]**  
 現在の設定を使用して、データ ソースに対する接続の確立を試みます。 メッセージが表示され、接続に成功したかどうかが示されます。  
  
  
