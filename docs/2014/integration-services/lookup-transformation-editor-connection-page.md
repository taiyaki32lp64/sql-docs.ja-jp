---
title: 参照変換エディター ([接続] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.referencetable.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: e90d6b69-5a26-43c5-8433-5c3c9588e08c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7985f713093e839d258a0c9b80bb5d4e6e58f37f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057949"
---
# <a name="lookup-transformation-editor-connection-page"></a>[参照変換エディター] ([接続] ページ)
  **[参照変換エディター]** ダイアログ ボックスの **[接続]** ページを使用して、接続マネージャーを選択します。 OLE DB 接続マネージャーを選択する場合は、参照データセットを生成するためのクエリ、テーブル、またはビューも選択します。  
  
 参照変換の詳細については、「 [Lookup Transformation](data-flow/transformations/lookup-transformation.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[参照変換エディター]** ダイアログ ボックスの [全般] ページで **[フル キャッシュ]** および **[キャッシュ接続マネージャー]** を選択すると、次のオプションを使用できます。  
  
 **[フル キャッシュ]**  
 既存のキャッシュ接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 新しい接続を作成するには、 **[キャッシュ接続マネージャー エディター]** ダイアログ ボックスを使用します。  
  
 **[参照変換エディター]** ダイアログ ボックスの [全般] ページで **[フル キャッシュ]** 、 **[部分キャッシュ]** 、 **[キャッシュなし]** 、および **[OLE DB 接続マネージャー]** を選択すると、次のオプションを使用できます。  
  
 **[キャッシュなし]**  
 一覧から既存の OLE DB 接続マネージャーを選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[OLE DB 接続マネージャーの構成]** ダイアログ ボックスを使用して、新しい接続を作成します。  
  
 **[テーブルまたはビューを使用する]**  
 既存のテーブルまたはビューを一覧から選択するか、 **[新規作成]** をクリックして新しいテーブルを作成します。  
  
> [!NOTE]  
>  **[参照変換エディター]** の **[詳細設定]** ページで SQL ステートメントを指定する場合、ここで選択したテーブル名はその SQL ステートメントでオーバーライドおよび置換されます。 詳細については、「 [[参照変換エディター] &#40;[詳細設定] ページ&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)」を参照してください。  
  
 **[新規作成]**  
 **[テーブルの作成]** ダイアログ ボックスを使用して新しいテーブルを作成します。  
  
 **[SQL クエリの結果を使用する]**  
 既存のクエリの参照、新しいクエリの構築、クエリ構文のチェック、およびクエリ結果のプレビューを行うには、このオプションを選択します。  
  
 **[クエリの作成]**  
 **[クエリ ビルダー]** を使用して、実行する Transact-SQL ステートメントを作成します。これは、データを参照することによってクエリを作成するグラフィカルなツールです。  
  
 **[参照]**  
 ファイルとして保存されている既存のクエリを参照します。  
  
 **[クエリの解析]**  
 クエリ構文をチェックします。  
  
 **プレビュー**  
 **[クエリ結果のプレビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 結果は 200 行まで表示されます。  
  
## <a name="external-resources"></a>外部リソース  
 blogs.msdn.com のブログ「 [キャッシュ モードの参照](https://go.microsoft.com/fwlink/?LinkId=219518) 」  
  
## <a name="see-also"></a>参照  
 [[参照変換エディター] &#40;[全般] ページ&#41;](general-page-of-integration-services-designers-options.md)   
 [[参照変換エディター] &#40;[列] ページ&#41;](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [[参照変換エディター] &#40;[詳細設定] ページ&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [[参照変換エディター] &#40;[エラー出力] ページ&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)   
 [あいまい参照変換](data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  
