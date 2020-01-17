---
title: 補足ログ スクリプトの生成および実行 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- supLog
ms.assetid: 6e940d93-12c6-4cda-9333-5489b245f0e4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ebf080b38e618a807ff9b3b48711ee89f0e56028
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298746"
---
# <a name="generate-and-run-the-supplemental-logging-script"></a>補足ログ スクリプトの生成および実行

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  補足ログを設定する Oracle ソース データベースでスクリプトを実行するには、[変更をキャプチャするためのテーブルの設定] ページを使用します。  
  
 **補足ログ スクリプトを実行するには**  
  
 **[スクリプトの実行]** をクリックして、CDC インスタンスに定義されているテーブルで補足ログ スクリプトを実行します。 このスクリプトは、キャプチャされるテーブルに UPDATE 操作のログを記録するときに、必要なすべての列をトランザクション ログに書き込むように Oracle データベースに対して指示します。 通常、このスクリプトは Oracle システム管理者によって検査されて実行されます。  
  
 SQL*Plus を使用してスクリプトを手動で実行することもできます。  
  
 **スクリプトを手動で実行するには**  
  
 **[コピー]** をクリックしてスクリプトをクリップボードに貼り付けます。 SQL*Plus を開き、Oracle ソース データベースのディレクトリに移動します。 SQL\*Plus にスクリプトを貼り付けて実行します。  
  
 補足ログ スクリプトをテキスト ファイルで保存するには、 **[名前を付けて保存]** をクリックし、ファイルを保存する場所を参照します。 ファイルに名前を付け、 **[保存]** をクリックしてファイルを保存します。  
  
 **[次へ]** をクリックして「 [Generate Mirror Tables and CDC Capture Instances](../../integration-services/change-data-capture/generate-mirror-tables-and-cdc-capture-instances.md)」に進みます。  
  
## <a name="see-also"></a>参照  
 [SQL Server 変更データベース インスタンスを作成する方法](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [補足ログ スクリプトの確認および生成](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md)  
  
  
