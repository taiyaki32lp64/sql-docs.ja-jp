---
title: Excel から MDS (MDS アドインを Excel 用) へのデータの発行 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 89fce454-a816-4b33-a26a-d1b9741d269b
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ffb122b96182b1079c95adf13d26c9a4949f6ddf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65478804"
---
# <a name="publish-data-from-excel-to-mds-mds-add-in-for-excel"></a>Excel から MDS へのデータのパブリッシュ (Excel 用 MDS アドイン)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]で、Excel での作業が終わったときに、変更を保存して他のユーザーがアクセスできるようにするには、MDS リポジトリにデータをパブリッシュします。  
  
> [!NOTE]
>  -   変更をパブリッシュすると、MDS によって管理されるセルのコメントは削除されます。  
> -   MDS によって管理されるセルでは、数式がサポートされていません。 MDS によって管理されるセル内の数式はテキスト値として処理されます。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。  
  
-   アクティブなワークシートに MDS によって管理されるデータが含まれており、そのデータに対して変更または追加を行っている必要があります。  
  
-   メンバーを追加する場合、エンティティのコードが自動的に生成されているときは、**コード**値を指定する必要はありません。 詳細については、「[コードの自動作成 (マスター データ サービス)](../automatic-code-creation-master-data-services.md)」を参照してください。  
  
### <a name="to-publish-data-to-the-mds-repository"></a>MDS リポジトリにデータをパブリッシュするには  
  
1.  **[パブリッシュと検証]** グループの **[パブリッシュ]** をクリックします。  
  
2.  任意。 **[パブリッシュと注釈設定]** ダイアログ ボックスが表示された場合は、すべての更新で同じ注釈 (コメント) を共有するか、各変更の注釈を個別に設定するかを選択します。  
  
3.  任意。 **[今後、このダイアログ ボックスを表示しない]** チェック ボックスをオンにします。 後で、このダイアログ ボックスが常に表示されるようにするには、 **[設定]** をクリックして **[パブリッシュ時に [パブリッシュと注釈設定] ダイアログ ボックスを表示する]** チェック ボックスをオンにします。  
  
4.  **[パブリッシュ]** をクリックします。  
  
> [!NOTE]  
>  新しいメンバー (行) をワークシートに追加する場合、MDS リポジトリに正常にパブリッシュできないときは、ワークシートのすべての属性に対する **更新** 権限がない可能性があります。 **[校閲]** タブの **[変更]** グループの **[シート保護の解除]** をクリックし、再度パブリッシュしてください。  
  
## <a name="next-steps"></a>次の手順  
 [ビジネス ルールの適用 (Excel 用 MDS アドイン)](apply-business-rules-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>参照  
 [データのパブリッシュ&#40;MDS アドインの Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)   
 [データの検証 (Excel 用 MDS アドイン)](validating-data-mds-add-in-for-excel.md)  
  
  
