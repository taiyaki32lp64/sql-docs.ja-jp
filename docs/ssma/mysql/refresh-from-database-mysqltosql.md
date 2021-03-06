---
title: データベース (MySQLToSQL) からの更新 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 59a6db8f-2db6-4071-9005-928a7231de92
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 690d12a2f5f397256760c1c0cf5e2ee954d90843
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2018
ms.locfileid: "47746440"
---
# <a name="refresh-from-database-mysqltosql"></a>データベースからの更新 (MySQLToSQL)
**データベースからの更新** ダイアログ ボックスを使用して MySQL データベースから更新するには、どのオブジェクトを選択できます。 ダイアログ ボックス内の行は色分け、メタデータの状態に基づいて。  
  
-   ローカルと MySQL データベースにオブジェクトのメタデータを変更した場合は、行は青色です。  
  
-   SSMA ではなく、MySQL データベースにオブジェクトのメタデータを変更した場合は、行が黄色にします。  
  
-   オブジェクトのメタデータがローカルで変更されたが、MySQL データベースではなく、行は緑色です。  
  
-   オブジェクトが新しい MySQL データベースの場合、その行はピンク色です。  
  
オブジェクトの更新設定は既定値を指定することができます、**プロジェクト設定** ダイアログ ボックス。 詳細については、次を参照してください[プロジェクト設定&#40;同期&#41; &#40;MySQLToSQL。&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)  
  
アクセスする、**データベースからの更新**MySQL メタデータ エクスプ ローラーでオブジェクトを右クリックしてダイアログ ボックスで、**データベースからの更新**します。  
  
## <a name="options"></a>および  
  
|||  
|-|-|  
|**項目**|**定義**|  
|**折りたたみ (-)**|個々 のオブジェクトを非表示にするすべてのオブジェクト グループを折りたたみます。|  
|**展開 (+)**|個々 のオブジェクトを表示するすべてのオブジェクト グループを展開します。|  
|**等しいオブジェクトを表示/非表示**|オブジェクトのメタデータが、MySQL データベースと SSMA で同じである場合は、一覧からオブジェクトを非表示にします。|  
|**データベース (矢印) からの更新します。**|SSMA で選択したオブジェクトのメタデータを更新することを指定するのにには、矢印ボタンを使用します。|  
|**データベースからの更新操作を行います (X ボタン)**|SSMA で選択したオブジェクトのメタデータを更新しないことを指定するのにには、X ボタンを使用します。|  
|**凡例**|表示、**凡例** ダイアログ ボックス。 凡例には、行の色とメタデータの状態間のマッピングが含まれています。<br /><br />保持する、**凡例** ダイアログ ボックスの上に、**データベースからの更新**ダイアログ ボックスで、**上部に表示する**チェック ボックスをオンします。|  
  
