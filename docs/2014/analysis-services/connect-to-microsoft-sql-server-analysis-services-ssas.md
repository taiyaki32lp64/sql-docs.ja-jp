---
title: Microsoft SQL Server Analysis Services (SSAS) への接続 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connsqlserveras.f1
ms.assetid: 7f3244ee-b690-471c-893d-68e361c2d416
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fe8eee02d019b5cf68e257b3fac4266a18ead795
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087027"
---
# <a name="connect-to-microsoft-sql-server-analysis-services-ssas"></a>[Microsoft SQL Server Analysis Service への接続] (SSAS)
  このページで、**テーブルのインポート ウィザード**Microsoft SQL Server Analysis Services キューブまたは SharePoint でホストされている PowerPivot ブックからデータをインポートする設定を指定することができます。 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]からウィザードにアクセスするには、 **[モデル]** メニューの **[データ ソースからのインポート]** をクリックします。  
  
 データ ソースに接続するには、適切なプロバイダーがコンピューターにインストールされている必要があります。  
  
> [!NOTE]  
>  このページでデータベースを選択する際には、現在のユーザーの資格情報が使用されます。 ただし、[権限借用情報] ページで指定されたユーザーに、選択したデータベースの読み取り権限がないと、インポートは成功しません。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 **接続の表示名**  
 このデータ ソース接続の一意の名前を入力します。 このフィールドは必須です。  
  
 **サーバー名またはファイル名**  
 次のいずれかを入力します。  
  
-   SQL Server Analysis Services サーバーが接続に使用する名前または IP アドレスを入力します。  
  
     ピリオド (.)、(local)、または localhost を使用すると、ローカル サーバーを指定できます。  
  
-   SharePoint にパブリッシュする PowerPivot ブックの URL を入力します。  
  
 **[Windows 認証を使用する]**  
 SQL Server Analysis Services サーバーへの接続に Windows 認証を使用するかどうかを指定します。  
  
 Windows 認証モードを使用すると、ユーザーは Windows ユーザー アカウントを使用して接続できます。 可能であれば、Windows 認証を使用します。  
  
 Windows 認証を使用した場合、[テーブルのプロパティ] ウィンドウおよびインポート ウィザードでデータのプレビューまたはフィルター処理を行う際に、現在のユーザーの資格情報が使用されます。 データをインポートまたは更新する際には、これらの資格情報は使用されず、[権限借用情報] ページで指定された Windows の資格情報が使用されます。  
  
 **[SQL Server 認証を使用する]**  
 SQL Server Analysis Services サーバーへの接続に SQL Server 認証を使用するかどうかを指定します。  
  
 SQL Server 認証の場合、SQL Server は、SQL Server ログイン アカウントが設定されているかどうか、指定されたパスワードが以前に記録されたパスワードと一致しているかどうかを確認することで認証を行います。  
  
 SQL Server 認証は、データ ソースの接続文字列を構築するときに使用されます。 [テーブルのプロパティ] ウィンドウおよびインポート ウィザードでデータのプレビューまたはフィルター処理を行う際も、これらの資格情報が使用されます。 データをインポートまたは更新する際には、これらの資格情報は使用されず、[権限借用情報] ページで指定された Windows の資格情報が使用されます。  
  
 **ユーザー名**  
 データベース接続に使用するユーザー名を指定します。 このオプションは、Windows 認証を使用した接続を選択した場合のみ使用できます。  
  
 **Password**  
 データベース接続に使用するパスワードを指定します。 このオプションは、SQL Server 認証を使用した接続を選択した場合にのみ編集できます。  
  
 **パスワードを保存します。**  
 **[パスワード]** ボックスに入力したパスワードを保存するかどうかを指定します。 このオプションは、SQL Server 認証を使用した接続を選択した場合にのみ使用できます。  
  
 **データベース名**  
 データベースを一覧から選択します。  
  
 **詳細設定**  
 **[詳細プロパティの設定]** ダイアログ ボックスを使用して追加の接続プロパティを設定します。 詳細については、「[[詳細プロパティの設定] (SSAS)](set-advanced-properties-ssas.md)」を参照してください。  
  
 **[接続テスト]**  
 現在の設定を使用して、データ ソースに対する接続の確立を試みます。 接続が正常に確立されたかどうかを示すメッセージが表示されます。  
  
  
