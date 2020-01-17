---
title: DQS の既定のナレッジ ベースの使用
ms.custom: ''
ms.date: 07/31/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b36af13b-9fcc-4168-bb92-214d600b1c93
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 2696a911edeefecc1dc34efeb77351acbaafc0d8
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257743"
---
# <a name="using-the-dqs-default-knowledge-base"></a>DQS の既定のナレッジ ベースの使用

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  このトピックでは、 **(DQS) にインストールされている既定のナレッジ ベース、** DQS データ [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] について説明します。 これは、次のドメインを含む、あらかじめ構築された既定のナレッジ ベースです。  
  
-   **国/地域**: 場所ごとに、通常の長い名前 (国/地域によって指定された公式名) と短い名前 (リスト、マップなどで使用される共通名)、2文字の省略形、3文字の省略形、および3桁のコードが含まれています。  先頭の値は長い名前に設定されます。  
  
-   **国/地域 (3 文字の先頭)**: 通常の長い名前 (国/地域によって指定された公式名) と短い名前 (リスト、マップなどで使用される共通名)、2文字の省略形、3文字の省略形、および各場所の3桁のコードが含まれています。  先頭の値は、3 文字の省略形に設定されます。  
  
-   **国/地域 (2 文字の先頭)**: 地域ごとに、通常の長い名前 (国/地域によって指定された公式名) と短い名前 (リストやマップなどで使用される共通名)、2文字の省略形、3文字の省略形、および3桁のコードが含まれています。  先頭の値は、2 文字の省略形に設定されます。  
  
-   **米国-郡**: 米国の郡の一覧が含まれています。  
  
-   **米国-Last Name**: 国勢調査2000で100回以上発生した姓 (姓) の一覧が含まれています。  
  
-   **米国-場所**: 国勢調査2010から抽出された50州、コロンビアの地区、およびプエルトリコの場所の一覧が含まれています。  
  
-   **米国-州**: 米国の各州の通常の長い (公式) 名と2文字の省略形が含まれています。 先頭の値は通常の州名に設定されます。  
  
-   **米国-州 (2 文字の見出し)**: 米国の各州の通常の長い (公式) 名と2文字の省略形が含まれています。 先頭の値は、州名の 2 文字の省略形に設定されます。  
  
## <a name="using-the-default-knowledge-base"></a>既定のナレッジ ベースの使用  
 既定の DQS ナレッジ ベースである DQS データは、次の方法で使用します。  
  
-   既定のナレッジ ベースを使用してクレンジング データ品質プロジェクトを開始して実行します。先に DQS の新しいナレッジ ベースを作成する必要はありません。  
  
-   既定のナレッジ ベースで、ドメイン管理、ナレッジ検出、または照合ポリシーのアクティビティを実行します。 これを実行するには、 **Data Quality Client Home Screen** の [[ナレッジ ベースを開く]](../data-quality-services/data-quality-client-home-screen.md)をクリックし、 **[ナレッジ ベースを開く]** 画面の **[DQS Data]** ナレッジ ベースを選択して、 **[アクティビティの選択]** 領域で必要なアクティビティを選択します。 
  **[次へ]** をクリックします。  
  
-   既定のナレッジ ベースを使用して新しいナレッジ ベースを作成します。 既存のナレッジ ベースからナレッジ ベースを作成する方法については、「 [Create a Knowledge Base](../data-quality-services/create-a-knowledge-base.md)」を参照してください。  
  
-   「 [Integration Services の DQS クレンジング コンポーネント](https://go.microsoft.com/fwlink/?LinkId=238830) 」および「 [Excel 用マスター データ サービス アドイン](../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)」で、それを使用します。  
  
## <a name="see-also"></a>参照  
 [DQS のナレッジベースとドメイン](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
