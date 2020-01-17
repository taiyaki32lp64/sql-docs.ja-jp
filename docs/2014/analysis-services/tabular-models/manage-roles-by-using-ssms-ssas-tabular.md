---
title: SSMS (SSAS テーブル) を使用してロールの管理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 652faac0-1cfc-438b-8119-2f4b090a2381
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 098d9b589396ebd6a9c622f921efd97d0b000929
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067035"
---
# <a name="manage-roles-by-using-ssms-ssas-tabular"></a>SSMS を使用したロールの管理 (SSAS テーブル)
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用して、配置したテーブル モデルのロールの作成、編集、および管理を行うことができます。  
  
 このトピックのタスク:  
  
-   [新しいロールを作成するには](#bkmk_new_role)  
  
-   [ロールをコピーするには](#bkmk_copy_role)  
  
-   [ロールを編集するには](#bkmk_edit_role)  
  
-   [ロールを削除するには](#bkmk_deletet_role)  
  
> [!CAUTION]  
>  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] のロール マネージャーを使用して定義済みロールを含むテーブル モデル プロジェクトを再配置すると、配置済みテーブル モデルに定義されたロールが上書きされます。  
  
> [!CAUTION]  
>  モデル プロジェクトが [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で開いているときに、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] を使用してテーブル モデル ワークスペース データベースを管理すると、Model.bim ファイルが破損することがあります。 テーブル モデル ワークスペース データベースのロールを作成および管理するときは、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]のロール マネージャーを使用してください。  
  
###  <a name="bkmk_new_role"></a> 新しいロールを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、新しいロールを作成するテーブル モデル データベースを展開し、 **[ロール]** を右クリックしてから **[新しいロール]** をクリックします。  
  
2.  **[ロールの作成]** ダイアログ ボックスの [ページの選択] ウィンドウで **[全般]** をクリックします。  
  
3.  全般設定のウィンドウの **[名前]** フィールドにロールの名前を入力します。  
  
     既定では、既定ロールの名前に番号が付き、新しいロールを作成するたびにその番号が増加します。 Finance Managers や Human Resources Specialists など、メンバーの種類を明確に特定する名前を付けることをお勧めします。  
  
4.  **[このロールにデータベースの権限を設定します]** で、次の権限オプションのいずれかを選択します。  
  
    |権限|説明|  
    |----------------|-----------------|  
    |**[フル コントロール (管理者)]**|メンバーは、モデル スキーマを変更したり、すべてのデータを表示したりできます。|  
    |**[データベースの処理]**|メンバーは、処理およびすべて処理の各操作を実行できます。 モデル スキーマを変更することはできませんし、データを表示することもできません。|  
    |**読み取り**|メンバーは、データを表示できますが (行フィルターに従って)、モデル スキーマを変更することはできません。|  
  
5.  **[ロールの作成]** ダイアログ ボックスの [ページの選択] ウィンドウで **[メンバーシップ]** をクリックします。  
  
6.  メンバーシップ設定ウィンドウで **[追加]** をクリックし、 **[ユーザーまたはグループの選択]** ダイアログ ボックスで、メンバーとして追加する Windows ユーザーまたはグループを選択します。  
  
7.  作成しているロールに読み取り権限がある場合、DAX 数式を使用してテーブルに行フィルターを追加できます。 行フィルターを追加する、**ロールのプロパティ - \<rolename >**  ダイアログ ボックスで**ページの選択**、 をクリックして**行フィルター**します。  
  
8.  行フィルター ウィンドウで、テーブルを選択し、をクリックして、 **DAX フィルター**フィールド、し、 **DAX フィルター - \<tablename >** フィールドに、DAX 式を入力します。  
  
    > [!NOTE]  
    >  DAX フィルター - \<tablename > フィールドが、オートコンプリート クエリ エディターまたは関数挿入機能していません。 DAX 数式を作成するときにオートコンプリート機能を使用するには、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]の DAX 数式エディターを使用する必要があります。  
  
9. **[OK]** をクリックして、ロールを保存します。  
  
###  <a name="bkmk_copy_role"></a> ロールをコピーするには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、コピーするロールを含むテーブル モデル データベースを展開し、 **[ロール]** を展開してから、ロールを右クリックして **[複製]** をクリックします。  
  
###  <a name="bkmk_edit_role"></a> ロールを編集するには  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、編集するロールを含むテーブル モデル データベースを展開し、 **[ロール]** を展開してから、ロールを右クリックして **[プロパティ]** をクリックします。  
  
     **ロールのプロパティ** \<rolename > ダイアログ ボックスで、アクセス許可を変更、追加またはメンバーの削除、および行フィルターの追加/編集します。  
  
###  <a name="bkmk_deletet_role"></a> ロールを削除するには  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、削除するロールを含むテーブル モデル データベースを展開し、 **[ロール]** を展開してから、ロールを右クリックして **[削除]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [ロール (SSAS テーブル)](roles-ssas-tabular.md)  
  
  
