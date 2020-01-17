---
title: (MDS アドインを Excel の) データのパブリッシュ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ea84a9aa-aeec-411b-ab8d-bc1b14f864a3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: dd5046c9a307f498ffb585c99cba8044c7b18b3f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479034"
---
# <a name="publishing-data-mds-add-in-for-excel"></a>データのパブリッシュ (Excel 用 MDS アドイン)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]で、他のユーザーとデータを共有するには、データを MDS リポジトリにパブリッシュします。 パブリッシュされたデータはすぐに、他のアドイン ユーザーがダウンロードできるようになります。  
  
 データを発行すると、追加または更新したすべてのデータが MDS リポジトリに発行されます。 削除したデータは発行されません。データの削除は個別に行う必要があります。 詳細については、「 [行の削除 (Excel 用 MDS アドイン)](delete-a-row-mds-add-in-for-excel.md)」を参照してください。  
  
> [!NOTE]  
>  パブリッシュは、新しいエンティティの作成には使用できません。 エンティティの作成の詳細については、「[エンティティを作成する (Excel 用 MDS アドイン)](create-an-entity-mds-add-in-for-excel.md)」を参照してください。  
  
## <a name="when-multiple-users-publish-at-the-same-time"></a>複数のユーザーが同時にパブリッシュした場合  
 複数のユーザーが同じデータの更新をパブリッシュする場合があります。 各ユーザーがパブリッシュすると、更新がデータベースに保存されます。 つまり、最後に更新されたデータを操作していなかったユーザーが、パブリッシュ時に値を変更する可能性があります。  
  
 実行した更新だけがデータベースにパブリッシュされます。 ワークシート内の古いデータはパブリッシュされません。  
  
## <a name="transactions-and-annotations"></a>トランザクションと注釈  
 パブリッシュされた各変更は、トランザクションとして保存されます。 必要に応じて、変更を行った理由を説明する注釈 (コメント) をトランザクションに追加できます。  
  
-   削除に注釈を付けることはできませんが、削除は管理者が取り消すことができるトランザクションとして保存されます。  
  
-   変更した場合、**コード**値は、メンバーは記録されず、トランザクションとして、メンバーの以前のすべてのトランザクションは使用できません。  
  
-   他のユーザーがメンバーに対して行ったトランザクションを表示することができます。 また、特定の属性に対する権限を失った場合でも、メンバーに対して行ったすべてのトランザクションを表示できます。  
  
 メンバーに対して行われたすべてのトランザクションを表示することができます。 詳細については、「[メンバーのすべての注釈またはトランザクションの表示 (Excel 用 MDS アドイン)](view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)」を参照してください。  
  
> [!IMPORTANT]  
>  500 文字を超える注釈を入力すると、その注釈は自動的に切り捨てられます。  
  
## <a name="business-rule-and-other-validation"></a>ビジネス ルールとその他の検証  
 データを発行すると、MDS リポジトリへの追加前に、データが正確であることを確保する検証が実行されます。 データが指定した条件を満たしていない場合は、リポジトリにパブリッシュされません。 詳細については、「[データの検証 (Excel 用 MDS アドイン)](validating-data-mds-add-in-for-excel.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|アクティブなワークシートのデータをパブリッシュして MDS リポジトリに戻します。|[Excel からデータを MDS にパブリッシュ&#40;MDS アドインの Excel&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|MDS リポジトリとワークシートから行を同時に削除します。|[行の削除 (Excel 用 MDS アドイン)](delete-a-row-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [データの更新 (Excel 用 MDS アドイン)](refreshing-data-mds-add-in-for-excel.md)  
  
-   [Microsoft Excel 用マスター データ サービス アドイン](master-data-services-add-in-for-microsoft-excel.md)  
  
  
