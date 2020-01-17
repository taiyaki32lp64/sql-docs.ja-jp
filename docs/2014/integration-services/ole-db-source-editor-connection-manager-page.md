---
title: OLE DB ソース エディター ([接続マネージャー] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbsourceadapter.connection.f1
helpviewer_keywords:
- OLE DB Source Editor
ms.assetid: 53699902-8699-4547-b56b-a5b2079e98b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 22b7c9ea4012655043cac7eb7f3d432ef1e2e854
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057047"
---
# <a name="ole-db-source-editor-connection-manager-page"></a>[OLE DB ソース エディター] ([接続マネージャー] ページ)
  **[OLE DB ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、ソースの OLE DB 接続マネージャーを選択できます。 さらにこのページを使用して、データベースのテーブルやビューを選択できます。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 2007 を使用するデータ ソースからデータを読み込むには、OLE DB ソースを使用します。 Excel ソースを使用して Excel 2007 データ ソースからデータを読み込むことはできません。 詳細については、「 [Configure OLE DB Connection Manager](configure-ole-db-connection-manager.md)」 (OLE DB 接続マネージャーの構成) を参照してください。  
>   
>  [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 2003 以前のバージョンを使用するデータ ソースからデータを読み込むには、Excel ソースを使用します。 詳細については、「[[Excel ソース エディター] ([接続マネージャー] ページ)](../../2014/integration-services/excel-source-editor-connection-manager-page.md)」を参照してください。  
  
> [!NOTE]  
>  `CommandTimeout`の OLE DB ソースのプロパティでは使用できません、 **OLE DB ソース エディター**を使用して設定できますが、**高度なエディター**します。 このプロパティの詳細については、「 [OLE DB Custom Properties](data-flow/ole-db-custom-properties.md)」(OLE DB のカスタム プロパティ) の Excel ソースのセクションを参照してください。  
  
 OLE DB ソースの詳細については、「 [OLE DB Source](data-flow/ole-db-source.md)」を参照してください。  
  
## <a name="open-the-ole-db-source-editor-connection-manager-page"></a>OLE DB ソース エディターを開く ([接続マネージャー] ページ)  
  
1.  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で、OLE DB ソースを [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]パッケージに追加します。  
  
2.  ソース コンポーネントを右クリックし、 **[編集]** をクリックします。  
  
3.  **[接続マネージャー]** をクリックします。  
  
## <a name="static-options"></a>静的オプション  
 **[キャッシュなし]**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[OLE DB 接続マネージャーの構成]** ダイアログ ボックスを使用して、新しい接続マネージャーを作成します。  
  
 **[データ アクセス モード]**  
 ソースからデータを選択する方法を指定します。  
  
|オプション|説明|  
|------------|-----------------|  
|[テーブルまたはビュー]|OLE DB データベースのテーブルまたはビューからデータを取得します。|  
|[テーブル名またはビュー名の変数]|テーブル名またはビュー名を変数で指定します。<br /><br /> **関連情報:** [パッケージで変数を使用する](../../2014/integration-services/use-variables-in-packages.md)|  
|[SQL コマンド]|SQL クエリを使用して、OLE DB データ ソースからデータを取得します。|  
|[変数からの SQL コマンド]|SQL クエリ テキストを変数で指定します。|  
  
 **プレビュー**  
 **[データ ビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 **プレビュー** では、最大で 200 行を表示できます。  
  
> [!NOTE]  
>  データをプレビューするときに、CLR ユーザー定義型を含む列にはデータが表示されません。 その代わりに、\<値が大きすぎて表示できません> または System.Byte[] が値として表示されます。 前者は、SQL OLE DB プロバイダーを使用してデータ ソースにアクセスする場合に表示されます。後者は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client プロバイダーを使用している場合に表示されます。  
  
## <a name="data-access-mode-dynamic-options"></a>データ アクセス モードの動的オプション  
  
### <a name="data-access-mode--table-or-view"></a>[データ アクセス モード] = [テーブルまたはビュー]  
 **[テーブル名またはビュー名]**  
 データ ソースで使用できるテーブルまたはビューの一覧から、テーブルまたはビューの名前を選択します。  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>[データ アクセス モード] = [テーブル名またはビュー名の変数]  
 **[変数名]**  
 テーブル名またはビュー名を含む変数を選択します。  
  
### <a name="data-access-mode--sql-command"></a>[データ アクセス モード] = [SQL コマンド]  
 **[SQL コマンド テキスト]**  
 SQL クエリのテキストを入力し、 **[クエリの作成]** をクリックしてクエリを作成するか、 **[参照]** をクリックしてクエリ テキストを含むファイルを指定します。  
  
 **パラメーター**  
 クエリ テキスト内でパラメーターのプレースホルダーとして "?" を使用することにより、 パラメーター化クエリを入力した場合は、 **[クエリ パラメーターの設定]** ダイアログ ボックスを使用して、クエリ入力パラメーターをパッケージ変数にマップします。  
  
 **Build query**  
 SQL クエリを視覚的に作成するには、 **[クエリ ビルダー]** ダイアログ ボックスを使用します。  
  
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、SQL クエリのテキストが含まれているファイルを指定します。  
  
 **[クエリの解析]**  
 クエリ テキストの構文を検査します。  
  
### <a name="data-access-mode--sql-command-from-variable"></a>データ アクセス モードが [変数からの SQL コマンド] の場合  
 **[変数名]**  
 SQL クエリのテキストを含む変数を選択します。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [OLE DB ソース エディター ([列] ページ)](../../2014/integration-services/ole-db-source-editor-columns-page.md)   
 [OLE DB ソース エディター ([エラー出力] ページ)](../../2014/integration-services/ole-db-source-editor-error-output-page.md)   
 [OLE DB ソースを使用してデータを抽出する](data-flow/extract-data-by-using-the-ole-db-source.md)   
 [OLE DB 接続マネージャー](connection-manager/ole-db-connection-manager.md)  
  
  
