---
title: ファイルの取得 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- version control services [SQL Server], file retrieval
- file retrieval [SQL Server]
- retrieving files
ms.assetid: 37b74426-e262-43b2-a81f-79b1fd1a36ec
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 548fac7dbc7d1f2750a130da9847be406361d8bf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62843668"
---
# <a name="retrieve-files"></a>ファイルの取得
  ソース管理の対象プロジェクトを開いた後、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を使用して、ソース管理の格納場所からプロジェクトがあるローカル ディレクトリに、プロジェクト ファイルのローカル コピーを取得できます。  
  
 統合ソース管理を使用してファイルを取得するには、以下の方法があります。  
  
-   **最新バージョン (再帰) を取得**コマンド  
  
     選択したファイルの最新のチェックイン バージョンが取得されます。 ソリューションまたはプロジェクトを選択した場合は、ソリューションとプロジェクトのすべてのファイルの最新バージョンが取得されます。  
  
-   **取得**コマンド  
  
     表示、**取得** ダイアログ ボックスで、選択したファイルの最新バージョンを取得するか、選択したソリューションまたはプロジェクト内のファイルのサブセットを取得するを使用することができます。  
  
### <a name="to-retrieve-the-latest-version-of-all-the-files-in-a-project"></a>プロジェクト内のすべてのファイルの最新バージョンを取得するには  
  
1.  ソリューション エクスプローラーで、プロジェクトを選択します。  
  
2.  **ファイル**メニューで、**ソース管理**、 をクリックし、**最新バージョンの取得 (再帰)** します。  
  
 プロジェクト内のファイルの最新のバージョンが、ローカル ディスクのプロジェクトが存在する場所に取得されます。  
  
#### <a name="to-retrieve-only-certain-files-in-a-project"></a>プロジェクト内の特定のファイルだけを取得するには  
  
1.  ソリューション エクスプローラーで、取得する項目を選択します。  
  
2.  **ファイル**メニューで、**ソース管理**、 をクリックし、**取得**。  
  
3.  **取得**ダイアログ ボックスで、をクリックして **[ok]** します。 または、ソリューション エクスプローラーでソリューションまたはプロジェクトを選択した場合は、取得しない項目の横にあるチェック ボックスをオフにします。  
  
## <a name="see-also"></a>参照  
 [ダイアログ ボックスが表示&#40;ソース管理&#41;](../../2014/database-engine/get-dialog-box-source-control.md)   
 [設定し、バージョン情報の取得](../../2014/database-engine/set-and-retrieve-version-information.md)   
 [プロジェクト履歴の表示](../../2014/database-engine/view-project-history.md)   
 [ファイルの状態の表示](../../2014/database-engine/view-file-status.md)  
  
  
