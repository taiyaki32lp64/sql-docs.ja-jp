---
title: 書き戻し ダイアログ ボックス (Analysis Services - 多次元データ) を有効にする に無効にする |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitiondesigner.writebackenabledisable.f1
ms.assetid: 2d254393-3f0d-4b70-8b98-87159f9f3639
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 498d1af6f96791b9ee3912c09a3667e139f30ff0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081285"
---
# <a name="enable-disable-writeback-dialog-box-analysis-services---multidimensional-data"></a>書き戻し ダイアログ ボックス (Analysis Services - 多次元データ) を有効にする に無効にします。
  **[書き戻しの有効化]/[書き戻しの無効化]** ダイアログ ボックスを使用すると、キューブ内のメジャー グループの書き戻しを有効または無効にできます。 メジャー グループの書き戻しを有効にすると、書き戻しパーティションが定義され、そのメジャー グループの書き戻しテーブルが作成されます。 メジャー グループの書き戻しを無効にすると、書き戻しパーティションが削除されます。ただし、予期しないデータの消失を避けるために、書き戻しテーブルは削除されません。 **[書き戻しの有効化]/[書き戻しの無効化]** ダイアログ ボックスを表示するには、次の操作を行います。  
  
-   キューブ デザイナーの **[パーティション]** タブの **[メジャー グループ]** ペインの **[書き戻しの設定]** をクリックします。  
  
-   キューブ デザイナーの **[パーティション]** タブの **[メジャー グループ]** ペインの **[パーティション]** グリッドでパーティションを右クリックし、ショートカット メニューの **[書き戻しの設定]** をクリックします。  
  
## <a name="options"></a>および  
 **[テーブル名]**  
 選択したパーティションに対して作成する書き戻しテーブルの名前を入力します。 書き戻しテーブルには、クライアント アプリケーションからのメジャー グループへの変更が格納されます。  
  
> [!NOTE]  
>  書き戻しが有効でない場合、このオプションは無効になります。  
  
 **データ ソース**  
 書き戻しテーブルを格納するデータ ソースを選択します。  
  
> [!NOTE]  
>  書き戻しが有効でない場合、このオプションは無効になります。  
  
 **[新規作成]**  
 クリックすると、 **[接続マネージャー]** ダイアログ ボックスが表示されます。このダイアログ ボックスで、書き戻しテーブルを格納する新しいデータ ソースを定義します。  
  
> [!NOTE]  
>  書き戻しが有効でない場合、このオプションは無効になります。  
  
  
