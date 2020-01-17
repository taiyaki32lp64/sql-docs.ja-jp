---
title: サブスクリプション ビューを作成してデータをエクスポートする
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- subscription views [Master Data Services], creating
- creating subscription views [Master Data Services]
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 524ff4934adf2317daceff64f70ce4ae0afb7424
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728469"
---
# <a name="create-a-subscription-view-to-export-data-master-data-services"></a>サブスクリプション ビューを作成してデータをエクスポートする (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  サブスクリプション ビューを作成して、マスター データ サービスのデータをサブスクライブ システムにエクスポートします。 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベース内のデータのビューを作成します。  
  
## <a name="prerequisites"></a>Prerequisites  
 この手順を実行するには  
  
-   **[統合管理]** 機能領域にアクセスする権限が必要です。 詳細については、「[機能領域権限 (マスター データ サービス)](../master-data-services/functional-area-permissions-master-data-services.md)」を参照してください。  
  
-   モデル管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-create-and-edit-a-subscription-view"></a>サブスクリプション ビューを作成および編集するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[統合管理]** をクリックします。  
  
2.  メニュー バーの **[ビューの作成]** をクリックします。  
  
3.  **[サブスクリプション ビュー]** ページで、ビューを作成するには **[追加]** 、ビューを編集するには **[編集]** をクリックします。 右側にパネルが表示されます。  
  
4.  **[サブスクリプション ビューの作成]** ペインで、 **[名前]** ボックスにビューの名前を入力します。  
  
     **[サブスクリプション ビューの編集]** ペインで、 **[名前]** ボックスに更新したビューの名前を入力します。  
  
5.  **[モデル]** ボックスの一覧からモデルを選択します。  
  
6.  **[Include soft-deleted members]** (論理削除済みメンバーを含める) を選択して、論理削除済みメンバーをビューに含めます。  
  
7.  **[バージョンのオプション]** で **[バージョン]** または **[バージョン フラグ]** のいずれかを選択し、対応する一覧から選択します。  
  
    > [!TIP]  
    >  サブスクリプション ビューはバージョン フラグに基づいて作成します。 バージョンをロックするとき、サブスクリプション ビューを更新せずに未処理のバージョンにフラグを割り当て直すことができます。  
  
8.  **[データ ソース]** オプションで **[エンティティ]** または **[派生階層]** のいずれかを選択し、対応する一覧から選択します。  
  
9. **[形式]** ボックスの一覧からサブスクリプション ビュー形式を選択します。  
  
10. **[形式]** ボックスの一覧から **[明示的レベル]** または **[派生レベル]** を選択した場合、ビューに含める階層内のレベル数を入力します。  
  
11. **[保存]** をクリックします。  
  
## <a name="view-information"></a>ビュー情報  
 作成されたビューごとに、10 列の行がグリッドに追加されます。 次の表で各列について説明します。  
  
|列|[説明]|  
|------------|-----------------|  
|[状態]|ビューの状態。<br /><br /> **[保存]** をクリックすると、ビューが更新中であることを示す![更新状態の画像のアイコン](../master-data-services/media/mds-statusicon-updating.png "I状態を更新するための con)が表示されます。<br /><br /> ビューの作成時または編集時にエラーが発生した場合は、![エラー状態の画像のアイコン](../master-data-services/media/mds-statusicon-error.png "Iエラー状態のための con)が表示されます。<br /><br /> それ以外の場合、状態は [OK] になり、 ![[OK] 状態の画像のアイコン](../master-data-services/media/mds-statusicon-ok.png "I"OK" 状態の con ")が表示されます。|  
|[オブジェクト名]|サブスクリプション ビュー名。|  
|モデル|モデル名。|  
|Version|バージョン名。|  
|[バージョン]|バージョン フラグ名。|  
|[エンティティ]|派生階層名。|  
|[データ ソース]|エンティティ名。|  
|形式|ビュー内のデータの型を指定します。|  
|Level|ビュー内のレベルの数を指定します。明示的レベルまたは派生レベルのビュー形式にのみ使用されます。|  
|Include delete members (削除済みメンバーを含める)|論理削除済みメンバーをビューに含めるかどうかを示します。|  
  
 ビューをクリックすると、次の情報が表示されます。  
  
-   **作成者**: ビューを作成したユーザーの名前。  
  
-   **作成日時**: ビューが作成された日時。  
  
-   **更新者**: ビューを最後に更新したユーザーの名前。  
  
-   **更新日時**: ビューが最後に更新された日時。  
  
## <a name="see-also"></a>参照  
 [概要: データのエクスポート (マスター データ サービス)](../master-data-services/overview-exporting-data-master-data-services.md)   
 [サブスクリプション ビューを削除する &#40;マスター データ サービス&#41;](../master-data-services/delete-a-subscription-view-master-data-services.md)   
 [バージョン フラグを作成する (マスター データ サービス)](../master-data-services/create-a-version-flag-master-data-services.md)  
  
  
