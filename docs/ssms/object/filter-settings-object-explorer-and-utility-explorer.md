---
title: '[フィルターの設定] (オブジェクト エクスプローラーおよびユーティリティ エクスプローラー) | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.common.filtersettings.f1
- sql13.ag.job.filtersettings.f1
ms.assetid: 4aab04bc-e1ab-4d4b-ab74-b287fc805bc2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e3a5cfecc4bf111e16da6451b56637abe9214c65
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264107"
---
# <a name="filter-settings-object-explorer-and-utility-explorer"></a>[フィルターの設定] \(オブジェクト エクスプローラーおよびユーティリティ エクスプローラー)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
このダイアログ ボックスを使用すると、フィルターを指定できます。 フィルターを使用すると、特定の条件を満たす項目だけを表示するようにオブジェクト エクスプローラーとユーティリティ エクスプローラーを構成できます。 たとえば、フィルターを使用して、"Maintenance" という単語を含む名前のジョブだけを表示できます。 **[フィルターの設定]** ダイアログ ボックスのヘッダーにはサーバーの名前が含まれ、場合によってはデータベースの名前が含まれます。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
**プロパティ**  
フィルター処理の対象となるプロパティを表示します。  
  
**[演算子]**  
フィルターの値をプロパティに適用する方法を選択します。 次のオプションがあります。  
  
-   **[等しい]**  
  
    このフィルターは、プロパティとこの値が厳密に一致する項目を表示します。  
  
-   **[値を含む]**  
  
    このフィルターは、プロパティにこの値が含まれている項目を表示します。 プロパティには他のテキストが含まれていてもかまいません。  
  
-   **[次を含まない]**  
  
    このフィルターは、プロパティにこの値が含まれていない項目を表示します。  
  
-   **より小さい**  
  
    日付に使用できるこのフィルターは、指定された値よりも古い日付を持つ項目を表示します。  
  
-   **[次の値以下]**  
  
    日付に使用できるこのフィルターは、指定された値の日付またはそれよりも古い日付を持つ項目を表示します。  
  
-   **より大きい**  
  
    日付に使用できるこのフィルターは、指定された値よりも新しい日付を持つ項目を表示します。  
  
-   **[次の値以上]**  
  
    日付に使用できるこのフィルターは、指定された値の日付またはそれよりも新しい日付を持つ項目を表示します。  
  
-   **[次の値の間]**  
  
    日付に使用できるこのフィルターは、指定された 2 つの日付で示される範囲内の日付を持つ項目を表示します。 **[次の値の間]** を選択し、Tab キーを押すと、2 番目の日付を入力するための行が追加されます。  
  
-   **[次の値の範囲外]**  
  
    日付に使用できるこのフィルターは、指定された 2 つの日付で示される範囲よりも前または後の日付を持つ項目を表示します。 **[次の値の範囲外]** を選択し、Tab キーを押して **[オペレーター]** 列の外に移動すると、2 番目の日付を入力するための行が追加されます。  
  
**[値]**  
プロパティと比較する値を入力します。 日付の場合は、矢印をクリックして日付を選択するためのカレンダーを表示します。  
  
**[フィルターのクリア]**  
現在のすべてのフィルター設定を削除します。  
  
## <a name="see-also"></a>参照  
[SQL Server Management Studio の使用 [SQL Server]](../../ssms/use-sql-server-management-studio.md)  
[SQL Server ユーティリティの概要](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
