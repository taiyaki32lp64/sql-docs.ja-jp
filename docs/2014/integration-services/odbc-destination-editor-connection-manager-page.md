---
title: Odbc 入力先エディター ([接続マネージャー] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcdest.connection.f1
ms.assetid: f6d9c6c2-e4c4-468b-9e0d-af7b9609614d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 281bbda38a6711efd4e2ffae7afbfa17d689254b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057206"
---
# <a name="odbc-destination-editor-connection-manager-page"></a>[ODBC 変換先エディター]\([接続マネージャー] ページ)
  **[ODBC 入力先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、入力先の ODBC 接続マネージャーを選択できます。 さらにこのページを使用して、データベースのテーブルやビューを選択できます。  
  
 ODBC 入力先の詳細については、「 [ODBC Destination](data-flow/odbc-destination.md)」を参照してください。  
  
 **[ODBC 入力先エディター] の [接続マネージャー] ページを開くには**  
  
## <a name="task-list"></a>タスク一覧  
  
-   [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]で、ODBC 入力先を含む [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] パッケージを開きます。  
  
-   **[データ フロー]** タブで、ODBC 入力先をダブルクリックします。  
  
-   **[ODBC 入力先エディター]** で、 **[接続マネージャー]** をクリックします。  
  
## <a name="options"></a>および  
  
### <a name="connection-manager"></a>[ODBC 入力元エディター]  
 既存の ODBC 接続マネージャーを一覧から選択するか、[新規作成] をクリックして新しい接続を作成します。 ODBC でサポートされているデータベースへの接続を選択または入力できます。  
  
### <a name="new"></a>ボタンを使用して新しい  
 **[新規作成]** をクリックします。 新しい接続マネージャーを作成できる **[ODBC 接続マネージャーの構成エディター]** ダイアログ ボックスが開きます。  
  
### <a name="data-access-mode"></a>[データ アクセス モード]  
 データを入力先に読み込む方法を選択します。 次の表に示すオプションがあります。  
  
|オプション|説明|  
|------------|-----------------|  
|[テーブル名 - バッチ]|バッチ モードで動作する ODBC 入力先を構成するには、このオプションを選択します。 このオプションを選択した場合は、次のオプションを指定できます。|  
||**[テーブル名またはビュー名]** : 使用できるテーブルまたはビューを一覧から選択します。<br /><br /> この一覧には、最初の 1,000 個のテーブルのみが含まれます。 データベースに 1,000 を超えるテーブルがある場合、テーブル名の最初の文字を入力するか、名前の一部の入力にワイルドカード (\*) を使用すると、目的のテーブルが表示されます。<br /><br /> **[バッチ サイズ]** : 一括読み込みのバッチのサイズを入力します。 これは、バッチとして読み込まれる行数です。|  
|[テーブル名 - 行ごと]|一度に 1 行ずつ、入力先テーブルに各行を挿入するように ODBC 入力先を構成するには、このオプションを選択します。 このオプションを選択した場合は、次のオプションを指定できます。|  
||**[テーブル名またはビュー名]** : 使用できるテーブルまたはビューを一覧のデータベースから選択します。<br /><br /> この一覧には、最初の 1,000 個のテーブルのみが含まれます。 データベースに 1,000 を超えるテーブルがある場合、テーブル名の最初の文字を入力するか、名前の一部の入力にワイルドカード (*) を使用すると、目的のテーブルが表示されます。|  
  
### <a name="preview"></a>[プレビュー]  
 **[プレビュー]** をクリックすると、選択したテーブルのデータが最大で 200 行表示されます。  
  
## <a name="see-also"></a>参照  
 [ODBC 入力先のカスタム プロパティ](data-flow/odbc-destination-custom-properties.md)   
 [[ODBC 変換先エディター] &#40;[マッピング] ページ&#41;](../../2014/integration-services/odbc-destination-editor-mappings-page.md)   
 [ODBC 変換先エディター &#40;[エラー出力] ページ&#41;](../../2014/integration-services/odbc-destination-editor-error-output-page.md)  
  
  
