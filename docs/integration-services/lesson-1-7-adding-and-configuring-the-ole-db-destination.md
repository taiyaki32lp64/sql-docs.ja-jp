---
title: 手順 7:OLE DB 変換先を追加し、構成する | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 442c841d-d528-4bf0-8724-7156f909ee50
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7c4a51bfb9da9abe3e50c85896f32269e3fee5ff
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296096"
---
# <a name="lesson-1-7-add-and-configure-the-ole-db-destination"></a>レッスン 1-7:OLE DB 変換先を追加し、構成する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



前回までの実習で、フラット ファイル ソースからデータを抽出し、変換先との互換性のある形式にデータを変換できるパッケージを作成しました。 次は、変換したデータを変換先に読み込みます。 データを読み込むには、データ フローに OLE DB 変換先を追加します。 OLE DB 変換先では、データベース テーブル、ビュー、または SQL コマンドを使用して、OLE DB に準拠するさまざまなデータベースにデータを読み込むことができます。  
  
この実習では、以前に作成した OLE DB の接続マネージャーを使用できるように、OLE DB 変換先を追加、構成します。  
  
## <a name="add-and-configure-the-sample-ole-db-destination"></a>サンプルの OLE DB 変換先を追加および構成する  
  
1.  **SSIS ツールボックス**で **[その他の変換先]** を展開し、 **[OLE DB 変換先]** を **[データ フロー]** タブのデザイン画面にドラッグします。**OLE DB 変換先**を **[Lookup Date Key]** 変換のすぐ下に置きます。  
  
2.  **[Lookup Date Key]** 変換を選択し、青色の矢印を新しい **[OLE DB 変換先]** にドラッグし、2 つのコンポーネントを接続します。  
  
3.  **[入出力の選択]** ダイアログの **[出力]** ボックスの一覧で **[参照の一致出力]** を選択し、 **[OK]** を選択します。  
  
4.  **[データ フロー]** デザイン画面で、新しい **[OLE DB 変換先]** コンポーネントの名前 **[OLE DB 変換先]** を選択し、その名前を「**Sample OLE DB Destination**」に変更します。  
  
5.  **[Sample OLE DB Destination]** をダブルクリックします。  
  
6.  **[OLE DB 変換先エディター]** ダイアログの **[OLE DB 接続マネージャー]** ボックスで確実に **localhost.AdventureWorksDW2012** が選択されているようにします。  
  
7.  **[テーブル名またはビュー名]** ボックスで **[dbo].[FactCurrencyRate]** を入力するか、選択します。  
  
8.  **[新規作成]** ボタンを選択して新しいテーブルを作成します。  スクリプトのテーブル名を **Sample OLE DB Destination** から **NewFactCurrencyRate** に変更します。  **[OK]** を選択します。  
  
9. **[OK]** を選択すると、ダイアログが閉じ、 **[テーブル名またはビュー名]** が自動的に「**NewFactCurrencyRate**」に変更されます。  
  
10. **[マッピング]** を選択します。  
  
11. **AverageRate**、 **CurrencyKey**、 **EndOfDayRate**、および **DateKey** の各入力列が変換先列に正しくマップされていることを確認します。 同じ名前の列がマップされていれば、マッピングは適切です。  
  
12. **[OK]** を選択します。  
  
13. **[Sample OLE DB Destination]** 変換先を右クリックし、 **[プロパティ]** を選択します。  
  
14. **[プロパティ]** ウィンドウで、**LocaleID** プロパティが **[英語 (米国)]** に、 **[DefaultCodePage]** プロパティが **[1252]** に設定されていることを確認します。  
  
## <a name="go-to-next-task"></a>次の実習に進む
[手順 8:レッスン 1 パッケージに注釈を付け、書式を設定する](../integration-services/lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
## <a name="see-also"></a>参照  
[OLE DB 変換先](../integration-services/data-flow/ole-db-destination.md)  
  
  
  
