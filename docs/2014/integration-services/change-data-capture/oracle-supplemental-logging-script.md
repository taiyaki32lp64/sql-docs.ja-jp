---
title: Oracle の補足ログ スクリプト | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5e6ee618-b89b-46c7-92ad-4fc5ef7b777a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c8f876852ff78e254bdff7ed687d2196d01d9c1d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62835349"
---
# <a name="oracle-supplemental-logging-script"></a>Oracle の補足ログ スクリプト
  このダイアログ ボックスには、Oracle の補足ログ スクリプトが表示されます。  
  
 CDC インスタンスを使用に備えて準備すると、CDC デザイナーにより、キャプチャするテーブル用の補足ログを設定する Oracle SQL スクリプトが作成されます。 補足ログ スクリプトは Oracle に対し、特定のテーブルが更新された場合、トランザクション ログに書き込む変更レコードに、変更された列だけでなく、対象のすべての列のデータを含める必要があることを伝えます。  
  
 組織の Oracle DBA ポリシーによっては、補足ログ スクリプトを実行するために、Oracle DBA による確認と承認が必要な場合があります。  
  
## <a name="options"></a>および  
 スクリプトの実行方法について使用可能なオプションを次に示します。  
  
 **[スクリプトの実行]**  
 CDC インスタンスに定義されているテーブルで補足ログ スクリプトを実行します。 このスクリプトを実行するには、キャプチャするすべてのテーブルに対する ALTER TABLE 権限と、DBA_LOG_GROUPS ビューに対する SELECT 権限が Oracle ユーザーに必要です。 さらに、必要な権限と共に使用する Oracle データベースの資格情報が Oracle ユーザーに必要です。 プログラムに Oracle 資格情報を要求させ、スクリプトを実行させることができます。  
  
 **[名前を付けて保存]**  
 スクリプトをテキスト ファイルに保存します。 このオプションは、Oracle データベース管理者 (DBA) が補足ログ スクリプトを調べて実行する必要がある場合に使用されます。ユーザーはスクリプトをテキスト ファイルに保存し、そのテキスト ファイルを後で Oracle DBA に電子メールまたはその他の方法で送信して実行してもらうことができます (SQL*Plus Oracle ユーティリティまたは Oracle データベースでスクリプトを実行するためのその他のツールを使用)。  
  
 **コピー**  
 スクリプトをクリップボードにコピーします。 Oracle 管理者 (DBA) が補足ログ スクリプトを調べて実行する必要がある場合は、必要な場所にスクリプトを貼り付けることができます。  
  
## <a name="see-also"></a>関連項目  
 [How to Manage a CDC Instance](manage-a-cdc-instance.md)   
 [CDC インスタンスの管理](manage-a-cdc-instance.md)  
  
  
