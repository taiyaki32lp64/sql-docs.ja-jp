---
title: 設定し、バージョン情報の取得 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- historical information [SQL Server]
- source controls [SQL Server Management Studio], version information
- retrieving version information
- current file version information
- version control services [SQL Server], retrieving version information
- version control services [SQL Server], setting version information
- status information [SQL Server], source control files
- historical information [SQL Server], source control files
ms.assetid: c3f253c4-4e3d-48e8-8d90-bd6ee899faf7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 68113c6de003aea94924f6e220373664212becf1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62843483"
---
# <a name="set-and-retrieve-version-information"></a>バージョン情報の設定と取得
  バージョン情報には、ソース管理の対象であるファイルの履歴と現在のステータスが記録されています。 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe では、ソース管理の対象であるすべてのファイルについて包括的な履歴が保持されるため、1 つ以上のファイルの変化を論理的に追跡できます。 この情報を使用して、ファイルのあらゆるバージョンのローカル コピーを取得したり、任意の 2 つのファイル バージョンを比較したりすることができます。  
  
 ファイル履歴には、次の情報が含まれています。  
  
-   バージョン番号。この番号により、同じファイルの他のバージョンとの間で順序を識別します。  
  
-   実行されたアクション。 追跡される操作には、ファイルの作成、チェックイン、削除が含まれます。  
  
-   ファイルを対象とするアクションを実行したユーザーの名前。  
  
-   操作が実行された日付と時刻。  
  
 Visual SourceSafe では、現在読み込まれているソリューションの現在のステータス情報も保持されます。 この情報によって、ファイルの現在のステータスを示すスナップショットが作成されます。このスナップショットには、以下の項目が含まれます。  
  
-   ファイルをチェックアウトしたユーザーの ID  
  
-   選択したファイルの最新のバージョン番号  
  
-   バージョンの作成日  
  
-   バージョンに関するユーザー コメント  
  
-   ファイルを共有するプロジェクトへのパス  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [ファイル履歴の表示](../../2014/database-engine/view-file-history.md)  
  
-   [プロジェクト履歴の表示](../../2014/database-engine/view-project-history.md)  
  
-   [ファイルの状態の表示](../../2014/database-engine/view-file-status.md)  
  
-   [ファイルの取得](../../2014/database-engine/retrieve-files.md)  
  
-   [特定のバージョンを最新バージョンとして指定する](../../2014/database-engine/specify-a-version-as-the-latest-version.md)  
  
-   [ファイルの比較](../../2014/database-engine/compare-files.md)  
  
-   [ファイルの共有](../../2014/database-engine/share-files.md)  
  
-   [履歴レポートおよびステータス レポートの作成](../../2014/database-engine/create-history-and-status-reports.md)  
  
## <a name="see-also"></a>関連項目  
 [ソース管理の基礎](../../2014/database-engine/source-control-basics.md)  
  
  
