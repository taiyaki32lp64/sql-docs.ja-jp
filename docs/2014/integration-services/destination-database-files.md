---
title: 転送先データベース ファイル |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.destdbfiles.f1
ms.assetid: f6f90417-86fb-4b8c-a790-0b215c344ef6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2cfee31b4167625b4f868d7312abd752a215652c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059546"
---
# <a name="destination-database-files"></a>[転送先データベース ファイル]
  **[転送先データベース ファイル]** ダイアログ ボックスを使用すると、転送先サーバーのデータベース ファイルの名前と場所を表示または変更したり、データベース転送タスクのネットワーク ファイルの場所を指定したりできます。 このタスクの詳細については、「 [データベース転送タスク](control-flow/transfer-database-task.md)」を参照してください。  
  
 このダイアログ ボックスで転送元サーバーのデータベース ファイルの名前と場所を自動的に入力するには、最初に **[データベース転送タスク エディター]** ダイアログ ボックスの **[データベース]** ページで、 **[SourceConnection]** 、 **[SourceDatabaseName]** 、および **[SourceDatabaseFiles]** を指定します。  
  
## <a name="options"></a>および  
 **[転送先ファイル]**  
 転送先サーバーの転送されたデータベース ファイルの名前です。  
  
 ファイル名を入力するか、ファイル名をクリックして編集します。  
  
 **[同期先フォルダー]**  
 データベース ファイルの転送先となる転送先サーバーのフォルダーです。  
  
 フォルダー パスを入力するか、フォルダー パスをクリックして編集するか、参照ボタンをクリックしてデータベース ファイルを転送する転送先サーバーのフォルダーを指定します。  
  
 **[ネットワーク ファイル共有]**  
 データベース ファイルの転送先となる転送先サーバーのネットワーク共有フォルダーです。 **[ネットワーク ファイル共有]** は、データベースをオフライン モードで転送する場合に使用します。 **[データベース転送タスク エディター]** ダイアログ ボックスの **[データベース]** ページの **[Method]** に、 **[DatabaseOffline]** を指定します。  
  
 ネットワーク ファイル共有の場所を入力するか、参照ボタンをクリックしてネットワーク ファイル共有の場所を見つけます。  
  
 オフライン モードでデータベースを転送すると、データベース ファイルは **[転送先フォルダー]** で指定した場所に転送される前に、 **[ネットワーク ファイル共有]** で指定した場所にコピーされます。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [[データベース転送タスク エディター] &#40;[全般] ページ&#41;](general-page-of-integration-services-designers-options.md)   
 [[データベース転送タスク エディター] &#40;[データベース] ページ&#41;](../../2014/integration-services/transfer-database-task-editor-databases-page.md)  
  
  
