---
title: '[フィルター] ダイアログ ボックス (Excel 用 MDS アドイン) | Microsoft Docs'
ms.custom: microsoft-excel-add-in
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b987b141-5abf-4161-a073-4cfc3e7f5aae
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 57b24ed1096078529e4e46a094737c8b37bf7020
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68092265"
---
# <a name="filter-dialog-box-mds-add-in-for-excel"></a>[フィルター] ダイアログ ボックス (Excel 用 MDS アドイン)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]では、 **[フィルター]** ダイアログ ボックスを使用して、MDS によって管理されるデータを Excel に読み込む前に絞り込むことができます。  
  
 このダイアログ ボックスには、3 つのセクションが含まれています。**列**、**行**、および**概要**します。  
  
## <a name="columns"></a>[列]  
 Excel で表示する属性 (列) を決定するには、 **[列]** セクションを使用します。  
  
|コントロール名|説明|  
|------------------|-----------------|  
|属性の型|属性の型は、使用するメンバーの種類を示します。 ほとんどの場合は **[リーフ]** です。 詳細については、「[メンバー (マスター データ サービス)](../../master-data-services/members-master-data-services.md)」を参照してください。|  
|明示的階層|属性の型として **[統合]** を選択した場合に、統合メンバーが属する階層を選択します。 詳細については、「[明示的階層 (マスター データ サービス)](../../master-data-services/explicit-hierarchies-master-data-services.md)」を参照してください。|  
|属性グループ|属性グループは、属性のサブセットをグループ化する方法です。 使用可能な属性のサブセットを表示する場合は、属性グループを選択します。 属性の詳細については、「[属性 (マスター データ サービス)](../../master-data-services/attribute-groups-master-data-services.md)」を参照してください。|  
|[すべて選択]|一覧に表示されているすべての属性を選択します。|  
|[すべてクリア]|一覧に表示されている選択済みの属性をクリアします。<br /><br /> **[名前]** および **[コード]** をクリアすることはできません。|  
|↑/↓|選択した属性を一覧内で上下に移動します。 この順序 (上から下) は、ワークシート内で列が表示される順序 (左から右) に対応します。|  
  
## <a name="rows"></a>[行]  
 Excel で表示するメンバー (行) を決定するには、 **[行]** セクションを使用します。 この操作は、表示される行をフィルター選択する条件を定義することによって行います。  
  
|コントロール名|説明|  
|------------------|-----------------|  
|属性|フィルター処理の基準にする属性が表示されます。 属性が表示されない場合は、属性が追加されていません。<br /><br /> 注:ワークシートに表示する予定がない属性によってフィルター処理することができます。|  
|演算子|選択した属性の型に対応する演算子が表示されます。 詳細については、「[フィルター演算子 (マスター データ サービス)](../../master-data-services/filter-operators-master-data-services.md)」を参照してください。|  
|[抽出条件]|フィルター処理に使用する条件。|  
|概要の更新|大きなデータセットを操作する場合に、クリックすると、読み込まれるデータの量に関する詳細を含む **[概要]** セクションが更新されます。|  
|追加|**[列]** セクションで属性をクリックし、 **[追加]** をクリックすると、属性がフィルターの一覧に追加されます。|  
|[すべて削除]|一覧からすべてのフィルターを削除します。|  
|削除|一覧から選択したフィルターを削除します。|  
  
## <a name="summary"></a>[概要]  
 データを読み込む前に、読み込まれるデータの量に関する詳細を表示するには、 **[概要]** セクションを使用します。  
  
|コントロール名|説明|  
|------------------|-----------------|  
|モデル|モデルの名前。|  
|バージョン|バージョンの名前。|  
|Entity|エンティティの名前。|  
|行|Excel に読み込まれる行数。 **[行]** セクションで適用したフィルターに基づきます。|  
|[列]|Excel に読み込まれる列数。 **[列]** セクションで選択した属性に基づきます。|  
  
## <a name="see-also"></a>関連項目  
 [エクスポート前のデータのフィルター処理 (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)   
 [概要:Excel へのデータのエクスポート &#40;Excel 用 MDS アドイン&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  
