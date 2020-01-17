---
title: ADO net 変換元エディター ([接続マネージャー] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetsource.connection.f1
ms.assetid: 7de3f438-bdd6-49b5-937a-47369e754943
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f3d9d2270603c3f38189478ccaaf48510085907f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061688"
---
# <a name="ado-net-source-editor-connection-manager-page"></a>[ADO NET 変換元エディター] ([接続マネージャー] ページ)
  **[ADO NET 変換元エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、変換元の [!INCLUDE[vstecado](../includes/vstecado-md.md)] 接続マネージャーを選択できます。 さらにこのページを使用して、データベースのテーブルやビューを選択できます。  
  
 ADO NET 変換元の詳細については、「 [ADO NET Source](data-flow/ado-net-source.md)」を参照してください。  
  
 **[接続マネージャー] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、ADO NET 変換元を含む [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、ADO NET 変換元をダブルクリックします。  
  
3.  **[ADO NET 変換元エディター]** で、 **[接続マネージャー]** をクリックします。  
  
## <a name="static-options"></a>静的オプション  
 **ADO.NET 接続マネージャー**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[ADO.NET の接続マネージャーの構成]** ダイアログ ボックスを使用して、新しい接続マネージャーを作成します。  
  
 **[データ アクセス モード]**  
 ソースからデータを選択する方法を指定します。  
  
|オプション|説明|  
|------------|-----------------|  
|[テーブルまたはビュー]|[!INCLUDE[vstecado](../includes/vstecado-md.md)] データ ソースのテーブルまたはビューからデータを取得します。|  
|[SQL コマンド]|SQL クエリを使用して、 [!INCLUDE[vstecado](../includes/vstecado-md.md)] データ ソースからデータを取得します。|  
  
 **プレビュー**  
 **[データ ビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 **プレビュー** では、最大で 200 行を表示できます。  
  
> [!NOTE]  
>  データをプレビューするときに、CLR ユーザー定義型を含む列にはデータが表示されません。 その代わりに、\<値が大きすぎて表示できません> または System.Byte[] が値として表示されます。 前者は、 [!INCLUDE[vstecado](../includes/vstecado-md.md)] プロバイダーを使用してデータ ソースにアクセスする場合に表示されます。後者は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client プロバイダーを使用している場合に表示されます。  
  
## <a name="data-access-mode-dynamic-options"></a>データ アクセス モードの動的オプション  
  
### <a name="data-access-mode--table-or-view"></a>[データ アクセス モード] = [テーブルまたはビュー]  
 **[テーブル名またはビュー名]**  
 データ ソースで使用できるテーブルまたはビューの一覧から、テーブルまたはビューの名前を選択します。  
  
### <a name="data-access-mode--sql-command"></a>[データ アクセス モード] = [SQL コマンド]  
 **[SQL コマンド テキスト]**  
 SQL クエリのテキストを入力し、 **[クエリの作成]** をクリックしてクエリを作成するか、 **[参照]** をクリックしてクエリ テキストを含むファイルを指定します。  
  
 **[クエリの作成]**  
 SQL クエリを視覚的に作成するには、 **[クエリ ビルダー]** ダイアログ ボックスを使用します。  
  
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、SQL クエリのテキストが含まれているファイルを指定します。  
  
## <a name="see-also"></a>参照  
 [[ADO NET 変換元エディター] ([列] ページ)](../../2014/integration-services/ado-net-source-editor-columns-page.md)   
 [[ADO NET 変換元エディター] ([エラー出力] ページ)](../../2014/integration-services/ado-net-source-editor-error-output-page.md)   
 [ADO.NET 接続マネージャー](connection-manager/ado-net-connection-manager.md)  
  
  
