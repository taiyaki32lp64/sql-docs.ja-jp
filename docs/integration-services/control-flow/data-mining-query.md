---
title: データ マイニング クエリ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquery.f1
ms.assetid: 948e358a-6245-429f-82c7-4cedc5e048fd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6ab9374312051ab22aa90c48bfed40713fe4e318
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298317"
---
# <a name="data-mining-query"></a>データ マイニング クエリ

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  デザイン ペインには、データ マイニング予測クエリ ビルダーがあり、これを利用してデータ マイニング予測クエリを作成できます。 予測クエリは、入力テーブルまたはシングルトン予測クエリに基づいてデザインできます。 クエリを実行して結果を表示するには、結果ビューに切り替えます。 クエリ ビューには、予測クエリ ビルダーによって作成されたデータ マイニング拡張機能 (DMX) のクエリが表示されます。  
  
## <a name="options"></a>オプション  
 ビュー切り替えボタン  
 デザイン ペインとクエリ ペインを切り替える場合は、アイコンをクリックします。 既定では、デザイン ペインが開きます。  
  
 デザイン ペインに切り替えるには、![デザイン アイコン](../../integration-services/control-flow/media/ssis-designicon.gif "デザイン アイコン") アイコンをクリックします。  
  
 クエリ ペインに切り替えるには、![SQL アイコン](../../integration-services/control-flow/media/ssis-queryicon.gif "SQL アイコン") アイコンをクリックします。  
  
 **[マイニング モデル]**  
 予測の基準として選択されているマイニング モデルを表示します。  
  
 **[モデルの選択]**  
 **[マイニング モデルの選択]** ダイアログ ボックスを開きます。  
  
 **[入力列]**  
 予測を生成するために選択されている入力列を表示します。  
  
 **ソース**  
 列に使用するフィールドを持つソースをドロップダウン リストから選択します。 **[マイニング モデル]** テーブルで選択したマイニング モデル、 **[入力テーブルの選択]** テーブルで選択した入力テーブル、予測関数、またはカスタム式を使用できます。  
  
 マイニング モデルを含むテーブルや入力列から列をセルにドラッグできます。  
  
 **フィールド**  
 ソース テーブルから派生した列の一覧から列を選択します。 **[ソース]** で **[予測関数]** を選択した場合、このセルは、選択されたマイニング モデルで利用できる予測関数のドロップダウン リストを含みます。  
  
 **別名**  
 サーバーから返された列の名前です。  
  
 **[表示]**  
 列を返す場合、または WHERE 句内でのみ列を使用する場合に選択します。  
  
 **[グループ]**  
 式をグループ化するために **[ルールの適用条件]** 列と組み合わせて使用します。 たとえば、(expr1 OR expr2) AND expr3 のように指定します。  
  
 **[ルールの適用条件]**  
 論理クエリを作成するために使用します。 たとえば、(expr1 OR expr2) AND expr3 のように指定します。  
  
 **[条件と引数]**  
 列に適用する条件またはユーザー式を指定します。 マイニング モデルを含むテーブルや入力列から列をセルにドラッグできます。  
  
## <a name="see-also"></a>参照  
 [データ マイニング クエリ ツール](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../../dmx/data-mining-extensions-dmx-statements.md)  
  
  
