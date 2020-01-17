---
title: DQS の既定のナレッジ ベースの使用 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d0fa10fa26f46857bd4f6848bd98bdcf1d65253a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484075"
---
# <a name="using-the-dqs-default-knowledge-base"></a>DQS の既定のナレッジ ベースの使用
  このトピックでは、 **(DQS) にインストールされている既定のナレッジ ベース、** DQS データ [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] について説明します。 これは、次のドメインを含む、あらかじめ構築された既定のナレッジ ベースです。  
  
-   **国/地域**:各地域の通常の長い名前 (国/地域が指定した公式名) と短縮名 (一覧やマップなどで一般に使用される名前)、2 文字の省略形、3 文字の省略形、各地域の 3 桁のコードが含まれます。  先頭の値は長い名前に設定されます。  
  
-   **国/地域 (3 文字が先頭)** :各地域の通常の長い名前 (国/地域が指定した公式名) と短縮名 (一覧やマップなどで一般に使用される名前)、2 文字の省略形、3 文字の省略形、各地域の 3 桁のコードが含まれます。  先頭の値は、3 文字の省略形に設定されます。  
  
-   **国/地域 (2 文字が先頭)** :各地域の通常の長い名前 (国/地域が指定した公式名) と短縮名 (一覧やマップなどで一般に使用される名前)、2 文字の省略形、3 文字の省略形、各地域の 3 桁のコードが含まれます。  先頭の値は、2 文字の省略形に設定されます。  
  
-   **米国 - 郡**:米国の郡の一覧が含まれています。  
  
-   **米国 - 姓**:2000 年の国勢調査で 100 例以上登録された姓の一覧です。  
  
-   **米国 - 場所 -** :2010 年の国勢調査から抽出された、50 州、コロンビア特別区、およびプエルトリコの地域の一覧です。  
  
-   **米国 - 州**:米国の各州の通常の長い (公式) の名前と 2 文字の省略形が含まれます。 先頭の値は通常の州名に設定されます。  
  
-   **米国 - 州 (2 文字の省略形)** :米国の各州の通常の長い (公式) の名前と 2 文字の省略形が含まれます。 先頭の値は、州名の 2 文字の省略形に設定されます。  
  
## <a name="using-the-default-knowledge-base"></a>既定のナレッジ ベースの使用  
 既定の DQS ナレッジ ベースである DQS データは、次の方法で使用します。  
  
-   既定のナレッジ ベースを使用してクレンジング データ品質プロジェクトを開始して実行します。先に DQS の新しいナレッジ ベースを作成する必要はありません。  
  
-   既定のナレッジ ベースで、ドメイン管理、ナレッジ検出、または照合ポリシーのアクティビティを実行します。 これを実行するには、 **Data Quality Client Home Screen** の [[ナレッジ ベースを開く]](../../2014/data-quality-services/data-quality-client-home-screen.md)をクリックし、 **[ナレッジ ベースを開く]** 画面の **[DQS Data]** ナレッジ ベースを選択して、 **[アクティビティの選択]** 領域で必要なアクティビティを選択します。 **[次へ]** をクリックします。  
  
-   既定のナレッジ ベースを使用して新しいナレッジ ベースを作成します。 既存のナレッジ ベースからナレッジ ベースを作成する方法については、「 [Create a Knowledge Base](../../2014/data-quality-services/create-a-knowledge-base.md)」を参照してください。  
  
-   「 [Integration Services の DQS クレンジング コンポーネント](https://go.microsoft.com/fwlink/?LinkId=238830) 」および「 [Excel 用マスター データ サービス アドイン](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)」で、それを使用します。  
  
## <a name="see-also"></a>関連項目  
 [DQS のナレッジ ベースとドメイン](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
