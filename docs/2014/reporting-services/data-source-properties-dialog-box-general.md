---
title: データ ソースのプロパティ ダイアログ ボックスで、全般 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasourceproperties.general.f1
- "10120"
ms.assetid: 44b5edd3-5c11-4d3d-91b8-5871aa0572ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9f918d6583f01473e061792406821b13a4856cea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109475"
---
# <a name="data-source-properties-dialog-box-general"></a>[全般] ([データ ソースのプロパティ] ダイアログ ボックス)
  **[データ ソースのプロパティ]** ダイアログ ボックスの **[全般]** を選択すると、レポート内のデータ ソースに関する接続情報を表示および変更できます。  
  
## <a name="options"></a>および  
 **名前**  
 データ ソースの名前を入力します。 データ ソース名はレポート内で一意である必要があります。 既定では、DataSource1 または DataSource2 などの一般的な名前がデータ ソースに割り当てられます。  
  
 **埋め込み接続**  
 共有データ ソースを使用しない場合は、このオプションを選択します。  
  
 **型**  
 データ処理拡張機能を選択します。 一覧には、登録されているすべての拡張機能が表示されます。  
  
 **[接続文字列]**  
 データ ソースの接続文字列を入力します。 **[編集]** をクリックして、 **[接続のプロパティ]** ダイアログ ボックスで接続文字列を生成します。 式を編集するには、 **式** ( *[fx]* ) ボタンをクリックします。  
  
 **共有データ ソース参照を使用します。**  
 共有データ ソースにリンクする場合は、このオプションを選択します。 ドロップダウン リストから共有データ ソースを選択します。 選択したデータ ソースを編集する場合は、 **[編集]** をクリックします。 **[共有データ ソース参照を使用する]** が選択されている場合、 **[型]** および **[接続文字列]** は使用できません。  
  
 **クエリの処理時に、1 つのトランザクションを使用します。**  
 このデータ ソースを使用するデータセットが、データベースに対する単一のトランザクションで処理されるように指定する場合は、このオプションを選択します。 同じデータ ソースを使用するサブレポートのトランザクションを含めるには、 **[プロパティ]** ペインのサブレポートの **[その他]** のプロパティ セクションで、 **[MergeTransactions]** を **[True]** に設定します。  
  
## <a name="see-also"></a>参照  
 [レポートにデータを追加&#40;レポート ビルダーおよび SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [埋め込みまたは共有データ ソースを作成&#40;SSRS&#41;](../../2014/reporting-services/create-an-embedded-or-shared-data-source-ssrs.md)   
 [データ接続、データ ソース、および Reporting Services の接続文字列](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [[資格情報] ([データ ソースのプロパティ] ダイアログ ボックス)](../../2014/reporting-services/data-source-properties-dialog-box-credentials.md)  
  
  
