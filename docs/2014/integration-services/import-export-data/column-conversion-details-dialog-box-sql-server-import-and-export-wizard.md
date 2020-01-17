---
title: '[列変換の詳細] ダイアログ ボックス (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.issuedetails.f1
ms.assetid: e2d00a39-dfbd-4821-a4d8-a5bd1164ed4d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9ac9035865a472b4f6c019124f6b3fd337e27f77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62893171"
---
# <a name="column-conversion-details-dialog-box-sql-server-import-and-export-wizard"></a>[列変換の詳細] ダイアログ ボックス (SQL Server インポートおよびエクスポート ウィザード)
  使用して、**列変換の詳細** ダイアログ ボックスで、個々 の列に関する詳細な変換情報を確認します。 この変換情報には、変換元および変換先での列のデータ型や、ウィザードが実行する変換が含まれます。 このページには、必要なデータ型変換を判断するためにウィザードで使用されるデータ型マッピング ファイルも一覧表示されます。 これらのデータ型マッピング ファイルは、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] によってセットアップ時にインストールされます。  
  
 **列変換の詳細 ダイアログ ボックスを開く**  
  
1.  **データ型の問題の確認**のページ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インポートおよびエクスポート ウィザードで、**テーブル**一覧で、テーブルを選択します。  
  
2.  **データ型マッピング**一覧で、変換の詳細を表示する列を含む行をダブルクリックします。  
  
 詳細について、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インポートおよびエクスポート ウィザードを参照してください[SQL Server インポートおよびエクスポート ウィザード](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)します。 ウィザードを正常に実行するために必要なアクセス許可と、ウィザードを起動するオプションについて説明しますを参照してください。 [、SQL Server インポートおよびエクスポート ウィザードを実行](start-the-sql-server-import-and-export-wizard.md)します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードの目的は、変換元から変換先にデータをコピーすることです。 また、このウィザードでは、変換先データベースと変換先テーブルも作成できます。 ただし、複数のデータベースやテーブルまたは他の種類のデータベース オブジェクトをコピーする必要がある場合は、データベース コピー ウィザードを使用してください。 詳細については、「 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)」を参照してください。  
  
  
