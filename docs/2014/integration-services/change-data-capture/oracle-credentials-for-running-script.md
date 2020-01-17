---
title: スクリプトを実行するための Oracle 資格情報 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4a301cb0-2f5b-41ba-81bf-46b41d07f137
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 12de97bf147ccb61cde5f82e2fa31782404071e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771113"
---
# <a name="oracle-credentials-for-running-script"></a>Oracle Credentials for Running Script
  Oracle CDC デザイナー コンソールから Oracle の補足ログ スクリプトを実行するために、スクリプトを実行する Oracle ユーザーの資格情報の入力が求められます。 このスクリプトを実行するには、キャプチャするすべてのテーブルに対する ALTER TABLE 権限と、DBA_LOG_GROUPS ビューに対する SELECT 権限が Oracle ユーザーに必要です。  
  
## <a name="task-list"></a>タスク一覧  
 このダイアログ ボックスでは次の情報を入力します。  
  
 **[認証]**  
  
 次のいずれかを選択します。  
  
-   **[Windows 認証]**:現在の Windows ドメイン資格情報を使用する場合に選択します。 このオプションは、Oracle データベースが Windows 認証と連動するように構成されている場合にのみ使用できます。  
  
-   **[Oracle 認証]**:このオプションを選択する場合、接続先の Source Oracle データベースのユーザーの **[ユーザー名]** と **[パスワード]** を入力する必要があります。  
  
## <a name="see-also"></a>参照  
 [CDC インスタンスを管理する方法](manage-a-cdc-instance.md)   
 [補足ログ スクリプトの確認および生成](review-and-generate-supplemental-logging-scripts.md)  
  
  
