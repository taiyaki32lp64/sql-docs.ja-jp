---
title: 手順 5:フラット ファイルの変換元を追加し、構成する | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e95b86d2d29bb3883f6fd76db29f17e5936d1b53
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283689"
---
# <a name="lesson-1-5-add-and-configure-the-flat-file-source"></a>レッスン 1-5:フラット ファイルの変換元を追加し、構成する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


ここでは、フラット ファイル ソースをパッケージに追加し、構成します。 フラット ファイル ソースとは、フラット ファイル接続マネージャーにより定義されるメタデータを使用するデータ フロー コンポーネントです。 このメタデータは、変換処理によってフラット ファイルから取得されるデータの形式や構造を指定します。 フラット ファイル ソースは、フラット ファイル接続マネージャーの形式定義を利用し、1 つのフラット ファイルからデータを抽出します。  
  
この実習では、以前に作成した **Sample Flat File Source Data** 接続マネージャーを使用するように、フラット ファイル ソースを構成します。  
  
## <a name="add-a-flat-file-source-component"></a>フラット ファイル ソース コンポーネントを追加する  
  
1.  **[データ フロー]** デザイナーを開くには、 **[Extract Sample Currency Data]** データ フローをダブルクリックするか、 **[データ フロー]** タブを選択します。  
  
2.  **[SSIS ツールボックス]** で **[その他の変換元]** を展開し、 **[フラット ファイル ソース]** を **[データ フロー]** タブのデザイン画面にドラッグします。  
  
3.  **[データ フロー]** デザイン画面で、新しく追加した **[フラット ファイル ソース]** を右クリックし、 **[名前の変更]** を選択し、名前を「**Extract Sample Currency Data**」に変更します。  
  
4.  このフラット ファイル ソースをダブルクリックし、 **[フラット ファイル ソース エディター]** ダイアログを開きます。  
  
5.  **[フラット ファイル接続マネージャー]** フィールドで **[Sample Flat File Source Data]** を選択します。  
  
6.  **[列]** を選択し、列名が正しいことを確認します。  
  
7.  **[OK]** を選択します。  
  
8.  [フラット ファイル ソース] を右クリックし、 **[プロパティ]** を選択します。  
  
9. **[プロパティ]** ウィンドウで、 **[LocaleID]** プロパティが **[英語 (米国)]** に設定されていることを確認します。  
  
## <a name="go-to-next-task"></a>次の実習に進む
[手順 6:参照変換を追加し、構成する](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>参照  
[フラット ファイル変換元](../integration-services/data-flow/flat-file-source.md)  
[フラット ファイル接続マネージャー](../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  
  
