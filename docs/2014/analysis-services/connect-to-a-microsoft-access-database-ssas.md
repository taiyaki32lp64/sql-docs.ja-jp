---
title: Microsoft Access データベース (SSAS) への接続 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connaccessdb.f1
ms.assetid: 9fa81839-dd8b-41d3-915e-c774a707ed53
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 95d40cc0a6da642fe92f46a86308da348d5cc040
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087296"
---
# <a name="connect-to-a-microsoft-access-database-ssas"></a>[Microsoft Access データベースへの接続] (SSAS)
  **テーブルのインポート ウィザード**のこのページを使用すると、Microsoft Access データベースに接続するための設定を指定できます。 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]からウィザードにアクセスするには、 **[モデル]** メニューの **[データ ソースからのインポート]** をクリックします。  
  
 Microsoft Access データベースに接続するには、適切な ACE プロバイダーがコンピューターにインストールされている必要があります。 詳細については、「[サポートされているデータ ソース &#40;SSAS テーブル&#41;](tabular-models/data-sources-supported-ssas-tabular.md)」を参照してください。  
  
> [!NOTE]  
>  このページでファイルを選択する際には、現在のユーザーの資格情報が使用されます。 ただし、[権限借用情報] ページで指定されたユーザーに、選択したファイルの読み取り権限がないと、インポートは成功しません。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 **接続の表示名**  
 このデータ ソース接続の一意の名前を入力します。 このフィールドは必須です。  
  
 **データベース名**  
 Microsoft Access データベース ファイルの完全なパスを指定します。  
  
 **[参照]**  
 使用可能な Microsoft Access データベース ファイルがある場所に移動します。  
  
 **ユーザー名**  
 データベース接続に使用するユーザー名を指定します。  
  
 **Password**  
 データベース接続に使用するパスワードを指定します。  
  
 **パスワードを保存します。**  
 **[パスワード]** ボックスに入力したパスワードを保存するかどうかを指定します。  
  
 **詳細設定**  
 **[詳細プロパティの設定]** ダイアログ ボックスを使用して追加の接続プロパティを設定します。  
  
 **[接続テスト]**  
 現在の設定を使用して、データ ソースに対する接続の確立を試みます。 接続が正常に確立されたかどうかを示すメッセージが表示されます。  
  
  
