---
title: データベース (OracleToSQL) からの更新 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 84492f44-c368-4c75-954d-7307a2d2bbc0
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: ba9a56c5fb47be4db081aebb3753db2c3e9ed6ad
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266540"
---
# <a name="refresh-from-database-oracletosql"></a>データベースからの更新 (OracleToSQL)
**データベースからの更新** ダイアログ ボックスを使用して Oracle データベースから更新するには、どのオブジェクトを選択できます。 ダイアログ ボックス内の行は色分け、メタデータの状態に基づいて。  
  
-   ローカルと Oracle データベースにオブジェクトのメタデータを変更した場合は、行は青色です。  
  
-   SSMA ではなく、Oracle データベースでオブジェクトのメタデータを変更した場合は、行が黄色にします。  
  
-   オブジェクトのメタデータがローカルで変更されたが、Oracle データベースではなく、行は緑色です。  
  
-   オブジェクトが、Oracle データベースの新機能の場合は、その行はピンク色です。  
  
オブジェクトの更新設定は既定値を指定することができます、**プロジェクト設定** ダイアログ ボックス。 詳細については、次を参照してください。[プロジェクト設定&#40;同期&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)します。  
  
アクセスする、**データベースからの更新** ダイアログ ボックスで、Oracle メタデータ エクスプ ローラーでオブジェクトを右クリック**データベースからの更新**します。  
  
## <a name="options"></a>および  
**折りたたみ (-)**  
個々 のオブジェクトを非表示にするすべてのオブジェクト グループを折りたたみます。  
  
**展開 (+)**  
個々 のオブジェクトを表示するすべてのオブジェクト グループを展開します。  
  
**等しいオブジェクトを表示/非表示**  
オブジェクトのメタデータが、Oracle データベースと SSMA で同じである場合は、一覧からオブジェクトを非表示にします。  
  
**データベース (矢印) からの更新します。**  
SSMA で選択したオブジェクトのメタデータを更新することを指定するのにには、矢印ボタンを使用します。  
  
**データベースからの更新操作を行います (X ボタン)**  
SSMA で選択したオブジェクトのメタデータを更新しないことを指定するのにには、X ボタンを使用します。  
  
**凡例**  
表示、**凡例** ダイアログ ボックス。 凡例には、行の色とメタデータの状態間のマッピングが含まれています。  
  
保持する、**凡例** ダイアログ ボックスの上に、**データベースからの更新**ダイアログ ボックスで、**上部に表示する**チェック ボックスをオンします。  
  
