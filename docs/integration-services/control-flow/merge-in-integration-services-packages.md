---
title: MERGE in Integration Services Packages | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- MERGE statement [SQL Server]
ms.assetid: 7e44a5c2-e6d6-4fe2-a079-4f95ccdb147b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f152f3c0115ad2af67a1b258ff19aa0142b277d9
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294050"
---
# <a name="merge-in-integration-services-packages"></a>MERGE in Integration Services Packages

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  現在のリリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]では、SQL 実行タスクの SQL ステートメントに MERGE ステートメントを含めることができます。 この MERGE ステートメントを使用すると、1 つのステートメントで複数の INSERT、UPDATE、および DELETE 操作を実行できます。  
  
 パッケージで MERGE ステートメントを使用するには、次の手順を実行します。  
  
-   一時テーブルまたはステージング テーブルへのソース データの読み込み、変換、保存を実行するデータ フロー タスクを作成します。  
  
-   MERGE ステートメントを含む SQL 実行タスクを作成します。  
  
-   データ フロー タスクを SQL 実行タスクに接続し、ステージング テーブルのデータを MERGE ステートメントへの入力として使用します。  
  
    > [!NOTE]  
    >  このシナリオでは、一般に、MERGE ステートメントにステージング テーブルが必要ですが、MERGE ステートメントのパフォーマンスは、通常、参照変換で実行される 1 行ずつの参照のパフォーマンスを上回ります。 また、MERGE は、大きなサイズの参照テーブルが参照変換でその参照テーブルをキャッシュするために使用できるメモリをテストする場合にも役立ちます。  
  
 MERGE ステートメントの使用をサポートする変換先コンポーネントのサンプルについては、CodePlex コミュニティのサンプル ( [MERGE Destination](https://go.microsoft.com/fwlink/?LinkId=141215)) を参照してください。  
  
## <a name="using-merge"></a>MERGE を使用する  
 通常、MERGE ステートメントは、挿入、更新、および削除を含む変更をあるテーブルから別のテーブルに適用する場合に使用します。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]より前のバージョンでこの処理を行うには、参照変換と複数の OLE DB コマンド変換の両方が必要でした。 参照変換で、1 行ずつ参照を実行して各行が新しいか変更されたかを判断し、 次に、OLE DB コマンド変換で、必要な INSERT、UPDATE および DELETE の操作を実行しました。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]以降、1 つの MERGE ステートメントを、参照変換と対応する OLE DB コマンド変換に代わって使用できます。  
  
### <a name="merge-with-incremental-loads"></a>増分読み込みを伴う MERGE  
 Change Data Capture 機能は [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] の新機能で、これを使用すると、データ ウェアハウスへの増分読み込みを簡単に実行できます。 パラメーター化された OLE DB コマンド変換を使用して挿入と更新を実行する代わりに、MERGE ステートメントを使用して両方の操作を組み合わせることができます。  
  
 詳細については、「 [変換先に変更を適用する](../../integration-services/change-data-capture/apply-the-changes-to-the-destination.md)」を参照してください。  
  
#### <a name="merge-in-other-scenarios"></a>他のシナリオでの MERGE  
 次のシナリオでは、MERGE ステートメントを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの内部でも外部でも使用できます。 ただし、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは、多くの場合、このデータを複数の異種ソースから読み込み、データを結合および消去する際に必要になることがあります。 したがって、メンテナンスを都合に合わせて簡単に行えるように、パッケージ内では MERGE ステートメントを使用することを検討してください。  
  
##### <a name="track-buying-habits"></a>購買習慣の追跡  
 データ ウェアハウスの FactBuyingHabits テーブルでは、各顧客が特定の製品を最後に購入した日付を追跡しています。 このテーブルは、ProductID、CustomerID、および PurchaseDate の各列で構成されています。 トランザクション データベースは、毎週、その週に行われた購入を記録する PurchaseRecords テーブルを生成します。 1 つの MERGE ステートメントを使用して PurchaseRecords テーブルの情報を FactBuyingHabits テーブルにマージすることが目的です。 製品と顧客の組み合わせが存在しない場合は、MERGE ステートメントによって新しい行が挿入されます。 製品と顧客の組み合わせが存在する場合は、MERGE ステートメントによって最新の購入日が更新されます。  
  
###### <a name="track-price-history"></a>価格履歴の追跡  
 DimBook テーブルは、書店の在庫にある書籍の一覧を表し、各書籍の価格履歴を示しています。 このテーブルには次の各列が含まれています: ISBN、ProductID、Price、Shelf、IsCurrent。 また、このテーブルでは、書籍の価格が変更されるたびに 1 行追加されます。 こうした行の 1 つに、現在の価格が含まれています。 現在の価格が含まれている行を示すために、その行の IsCurrent 列の値は 1 に設定されます。  
  
 データベースは、毎週、その週の価格変更と、その週に追加された新しい書籍を記録する WeeklyChanges テーブルを生成します。 1 つの MERGE ステートメントを使用して、WeeklyChanges テーブルの変更を DimBook テーブルに適用できます。 MERGE ステートメントにより、新しく追加された書籍用に新しい行が挿入され、価格が変更された既存の書籍の行では IsCurrent 列が 0 に更新されます。 また、価格が変更された書籍用に新しい行が挿入され、その行では IsCurrent 列の値が 1 に設定されます。  
  
### <a name="merge-a-table-with-new-data-against-the-old-table"></a>新しいデータを含むテーブルと古いテーブルのマージ  
 データベースは、"オープン スキーマ"、つまり、各プロパティの名前と値の組み合わせが格納されているテーブルを使用して、オブジェクトのプロパティをモデル化します。 Properties テーブルには次の 3 つの列があります: EntityID、PropertyID、Value。 NewProperties テーブルは、Properties テーブルと同期する必要のある、新しいバージョンのテーブルです。 この 2 つのテーブルを同期するには、1 つの MERGE ステートメントを使用して次の操作を実行します。  
  
-   Properties テーブルから、NewProperties テーブルに存在しないプロパティを削除します。  
  
-   Properties テーブルに存在するプロパティの値を、NewProperties テーブルにある新しい値で更新します。  
  
-   NewProperties テーブルに存在して Properties テーブルにはないプロパティについては、新しいプロパティを挿入します。  
  
 この方法は、レプリケーション シナリオのようなシナリオで役立ちます。この場合は、2 つのサーバー上の 2 つのテーブル内のデータを同期しておくことが目的です。  
  
### <a name="track-inventory"></a>在庫の追跡  
 Inventory データベースには、ProductID 列と StockOnHand 列を含む ProductsInventory テーブルがあります。 ProductID、CustomerID、および Quantity の各列を含む Shipments テーブルでは、顧客に対する製品の出荷を追跡しています。 ProductInventory テーブルは、Shipments テーブルの情報に基づいて毎日更新する必要があります。 1 つの MERGE ステートメントによって、出荷が行われると ProductInventory テーブルの在庫が減少します。 製品の在庫が 0 まで減少した場合は、その MERGE ステートメントによって、ProductInventory テーブルからその製品の行も削除されます。  
  
  
