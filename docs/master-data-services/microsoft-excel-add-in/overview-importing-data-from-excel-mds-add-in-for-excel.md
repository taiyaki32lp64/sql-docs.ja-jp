---
title: 概要:(MDS アドインを Excel の) Excel からデータをインポートする |Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ea84a9aa-aeec-411b-ab8d-bc1b14f864a3
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1da9e1876995f81fd2b40b9ef1bb4b509b4c848d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68074485"
---
# <a name="overview-importing-data-from-excel-mds-add-in-for-excel"></a>概要:Excel からのデータのインポート (Excel 用 MDS アドイン)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]で、他のユーザーとデータを共有するには、データを MDS リポジトリにパブリッシュします。 パブリッシュされたデータはすぐに、他のアドイン ユーザーがダウンロードできるようになります。  
  
 データを発行すると、追加または更新したすべてのデータが MDS リポジトリに発行されます。 削除したデータは発行されません。データの削除は個別に行う必要があります。 詳細については、「 [行の削除 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/delete-a-row-mds-add-in-for-excel.md)」を参照してください。  
  
> [!NOTE]  
>  パブリッシュは、新しいエンティティの作成には使用できません。 エンティティの作成の詳細については、「[エンティティを作成する (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)」を参照してください。  
  
## <a name="when-multiple-users-publish-at-the-same-time"></a>複数のユーザーが同時にパブリッシュした場合  
 複数のユーザーが同じデータの更新をパブリッシュする場合があります。 各ユーザーがパブリッシュすると、更新がデータベースに保存されます。 つまり、最後に更新されたデータを操作していなかったユーザーが、パブリッシュ時に値を変更する可能性があります。  
  
 実行した更新だけがデータベースにパブリッシュされます。 ワークシート内の古いデータはパブリッシュされません。  
  
## <a name="transactions-and-annotations"></a>トランザクションと注釈  
 パブリッシュされた各変更は、トランザクションとして保存されます。 必要に応じて、変更を行った理由を説明する注釈 (コメント) をトランザクションに追加できます。  
  
-   削除に注釈を付けることはできませんが、削除は管理者が取り消すことができるトランザクションとして保存されます。  
  
-   メンバーの **コード** 値を変更した場合、そのメンバーの以前のトランザクションはすべて使用できなくなります。 **コード** 値を元の値に戻すことで、以前のトランザクションにアクセスできます。  
  
-   他のユーザーがメンバーに対して行ったトランザクションを表示することができます。 また、特定の属性に対する権限を失った場合でも、メンバーに対して行ったすべてのトランザクションを表示できます。 権限が拒否と設定されている属性を含むトランザクションは表示できません。  
  
 メンバーに対して行われたすべてのトランザクションを表示することができます。 詳細については、「 [メンバーのすべての注釈またはトランザクションの表示 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)」を参照してください。  
  
> [!IMPORTANT]  
>  500 文字を超える注釈を入力すると、その注釈は自動的に切り捨てられます。  
  
## <a name="business-rule-and-other-validation"></a>ビジネス ルールとその他の検証  
 データを発行すると、MDS リポジトリへの追加前に、データが正確であることを確保する検証が実行されます。 データが指定した条件を満たしていない場合は、リポジトリにパブリッシュされません。 詳細については、「[データの検証 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|アクティブなワークシートのデータをパブリッシュして MDS リポジトリに戻します。|[Excel からマスター データ サービスにデータをインポートする (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|MDS リポジトリとワークシートから行を同時に削除します。|[行の削除 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/delete-a-row-mds-add-in-for-excel.md)|  
|データの更新履歴を確認するときに、データ行 (メンバー) の注釈 (コメント) およびトランザクションを表示します。|[メンバーのすべての注釈またはトランザクションの表示 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|パブリッシュする前にデータを比較するときに、2 つのワークシートのデータを結合します。|[データの結合 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/combine-data-mds-add-in-for-excel.md)|  

  
## <a name="related-content"></a>関連コンテンツ  
  
-   [データの更新 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md)  
  
-   [Microsoft Excel 用マスター データ サービス アドイン](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)  
  
  
