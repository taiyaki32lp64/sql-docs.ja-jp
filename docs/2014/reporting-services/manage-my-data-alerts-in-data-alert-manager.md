---
title: データ警告マネージャーでのデータ警告の管理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- managing, alerts
- managing, data alerts
ms.assetid: e0e4ffdf-bd4c-4ebd-872b-07486cbb47c2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 07c75779d05d22e09e7823b5d0b3bffc2ca7acc8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108306"
---
# <a name="manage-my-data-alerts-in-data-alert-manager"></a>データ警告マネージャーでのデータ警告の管理
  SharePoint ユーザーは、自分が作成したデータ警告と、それらの警告に関する情報を一覧表示できます。 また、警告を削除したり、データ警告デザイナーで警告定義を開いて編集したり、それらの警告を実行することもできます。 次の図に、データ警告マネージャーでユーザーが使用できる機能を示します。  
  
 ![SharePoint ユーザー向けの警告マネージャー機能](media/rs-alertmanageriw.gif "SharePoint ユーザー向けの警告マネージャー機能")  
  
### <a name="to-view-a-list-of-your-alerts"></a>警告の一覧を表示するには  
  
1.  データ警告の作成対象のレポートが保存されている SharePoint ライブラリに移動します。  
  
2.  レポートの展開ドロップダウン メニューのアイコンをクリックし、 **[データ警告の管理]** をクリックします。 ドロップダウン メニューを次の図に示します。  
  
     ![レポート コンテキスト メニューから警告マネージャーを開く](media/rs-openalertmanager.gif "レポート コンテキスト メニューから警告マネージャーを開く")  
  
     データ警告マネージャーが開きます。 既定では、ライブラリで選択したレポートに対する警告が一覧表示されます。  
  
3.  **[レポート用の警告の表示]** の一覧の横にある下矢印をクリックして、警告を表示するレポートを選択するか、 **[すべて表示]** をクリックして警告をすべて表示します。  
  
    > [!NOTE]  
    >  選択したレポートに警告が存在しない場合、SharePoint ライブラリに戻って警告があるレポートを検索および選択する必要はありません。 代わりに、 **[すべて表示]** をクリックしてすべての警告を一覧表示します。  
  
     警告名、レポート名、警告の作成者としての自分の名前、送信された警告の数、最後に警告定義が変更された日時、および警告の状態が表に一覧表示されます。 警告の生成や送信ができない場合は、エラーに関する情報が状態列に含まれているので、これを利用して問題のトラブルシューティングを行います。  
  
### <a name="to-edit-an-alert-definition"></a>警告定義を編集するには  
  
-   警告定義を編集するデータ警告を右クリックし、 **[編集]** をクリックします。  
  
     データ警告デザイナーに警告定義が表示されます。 詳しくは、「 [警告デザイナーでのデータ警告の編集](edit-a-data-alert-in-alert-designer.md) 」および「 [データ警告デザイナー](../../2014/reporting-services/data-alert-designer.md)」をご覧ください。  
  
    > [!NOTE]  
    >  データ警告定義は、作成したユーザーのみが編集できます。  
  
    > [!NOTE]  
    >  レポートが変更され、レポートから生成されたデータ フィードが変更されている場合、警告の定義が無効になっている可能性があります。 この状況が生じるのは、警告のルールで参照される列がレポートから削除された場合、列のデータ型が変更された場合、列が別のデータ フィードに含まれている場合、またはレポートが削除または移動された場合です。 無効な警告定義は開くことはできますが、基になるレポート データ フィードの現行バージョンに基づいて有効になるまでは再保存できません。 レポートからデータ フィードが生成される方法の詳細については、「[複数のレポートからのデータ フィードの生成 &#40;レポート ビルダーおよび SSRS&#41;](report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)」を参照してください。  
  
### <a name="to-delete-an-alert-definition"></a>警告の定義を削除するには  
  
-   削除するデータ警告を右クリックして、 **[削除]** をクリックします。  
  
     警告を削除すると、それ以降、警告メッセージは送信されません。  
  
### <a name="to-run-an-alert"></a>警告を実行するには  
  
-   実行するデータ警告を右クリックして、 **[実行]** をクリックします。  
  
     警告インスタンスが作成され、データ警告メッセージが直ちに送信されます。これは、データ警告デザイナーで指定したスケジュール オプションの内容にかかわらず実行されます。 たとえば、結果が変更された場合にのみ、週単位で送信されるよう構成された警告も同様です。  
  
## <a name="see-also"></a>関連項目  
 [警告管理者用のデータ警告マネージャー](../../2014/reporting-services/data-alert-manager-for-alerting-administrators.md)   
 [Reporting Services Data Alerts](../ssms/agent/alerts.md)  
  
  
