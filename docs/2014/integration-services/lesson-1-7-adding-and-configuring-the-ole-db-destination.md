---
title: 手順 7:追加して、OLE DB 変換先の構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 442c841d-d528-4bf0-8724-7156f909ee50
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 97b155852a0d6941cff4da0bdd4565e08dc63e79
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767561"
---
# <a name="step-7-adding-and-configuring-the-ole-db-destination"></a>手順 7:OLE DB 変換先の追加と構成
  前回までの実習で、フラット ファイル ソースからデータを抽出し、変換先との互換性のある形式にデータを変換できるパッケージを作成しました。 次は、変換したデータを実際に変換先に読み込みます。 データを読み込むには、データ フローに OLE DB 変換先を追加する必要があります。 OLE DB 変換先では、データベース テーブル、ビュー、または SQL コマンドを使用して、OLE DB に準拠するさまざまなデータベースにデータを読み込むことができます。  
  
 この操作では、以前に作成した OLE DB の接続マネージャーを使用できるように、OLE DB 変換先を追加、構成します。  
  
### <a name="to-add-and-configure-the-sample-ole-db-destination"></a>サンプルの OLE DB 変換先を追加および構成するには  
  
1.  **SSIS ツールボックス**で **[その他の変換先]** を展開し、 **[OLE DB 変換先]** を **[データ フロー]** タブのデザイン画面にドラッグします。OLE DB 変換先を **[Lookup Date Key]** 変換のすぐ下に置きます。  
  
2.  **[Lookup Date Key]** 変換をクリックし、緑色の矢印を、新しく追加した **[OLE DB 変換先]** にドラッグします。2 つのコンポーネントが接続されます。  
  
3.  **[入出力の選択]** ダイアログ ボックスの **[出力]** ボックスの一覧で **[参照の一致出力]** をクリックし、 **[OK]** をクリックします。  
  
4.  **[データ フロー]** デザイン画面で、新しく追加した **[OLE DB 変換先]** コンポーネントの **[OLE DB 変換先]** をクリックし、名前を「 **Sample OLE DB Destination**」に変更します。  
  
5.  **[Sample OLE DB Destination]** をダブルクリックします。  
  
6.  **[OLE DB 変換先エディター]** ダイアログ ボックスの **[OLE DB 接続マネージャー]** ボックスで **localhost.AdventureWorksDW2012** が選択されていることを確認します。  
  
7.  **[テーブル名またはビュー名]** ボックスで **[dbo].[FactCurrencyRate]** を選択するか、または直接入力します。  
  
8.  **[新規作成]** ボタンをクリックして新しいテーブルを作成します。  スクリプト内のテーブル名を「 **NewFactCurrencyRate**」に変更します。  **[OK]** をクリックします。  
  
9. **[OK]** をクリックすると、ダイアログが閉じ、 **[テーブル名またはビュー名]** は自動的に「 **NewFactCurrencyRate**」に変更されます。  
  
10. **[マッピング]** をクリックします。  
  
11. **AverageRate**、 **CurrencyKey**、 **EndOfDayRate**、および **DateKey** の各入力列が変換先列に正しくマップされていることを確認します。 同じ名前の列がマップされていれば、マッピングは適切です。  
  
12. **[OK]** をクリックします。  
  
13. **[Sample OLE DB Destination]** 変換先を右クリックし、 **[プロパティ]** をクリックします。  
  
14. [プロパティ] ウィンドウであることを確認、`LocaleID`プロパティに設定されて**英語 (米国)** と`DefaultCodePage`プロパティに設定されて**1252**します。  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [手順 8:レッスン 1 パッケージを理解しやすきます。](lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
## <a name="see-also"></a>参照  
 [[OLE DB 変換先]](data-flow/ole-db-destination.md)  
  
  
