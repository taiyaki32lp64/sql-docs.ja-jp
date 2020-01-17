---
title: トレース データへのアクセスを向上させる | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], space
- SQL Server Profiler, space
- space [SQL Server], SQL Server Profiler
ms.assetid: c260c000-fd53-4831-993f-df6894f3228b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 540a0bd9430a182ef3eda43fd816b4a495dc36b5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62714619"
---
# <a name="improve-access-to-trace-data"></a>トレース データへのアクセスを向上させる
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] は、トレース データのアクセスを向上させるために、 **temp** ディレクトリの領域を使用します。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] には、最低で 10 MB の空き領域が必要です。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]の使用中に空き容量が 10 MB より少なくなると、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] のすべての機能が停止します。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] によって **temp** ディレクトリの領域が使用されると、 **temp** ディレクトリのサイズがすぐに大きくなってしまう場合があります。 ファイル サイズ増大の問題を防ぐために、TEMP 環境変数の値を変更して、 **temp** ディレクトリをシステム ドライブでないドライブに配置することができます。  
  
 以下の手順は、ほとんどの Microsoft Windows オペレーティング システムで TEMP 環境変数の値を変更する方法を説明しています。 環境変数の設定の詳細については、お使いの Windows オペレーティング システムのドキュメントを参照してください。  
  
### <a name="to-change-the-temp-environment-variable-in-windows-operating-systems"></a>Windows オペレーティング システムで TEMP 環境変数を変更するには  
  
1.  **[スタート]** メニューの **[コントロール パネル]** をクリックし、 **[システム]** をクリックします。  
  
2.  **[システムのプロパティ]** ダイアログ ボックスで、 **[詳細設定]** タブをクリックし、 **[環境変数]** をクリックします。  
  
3.  **[システム環境変数]** ボックスの一覧をスクロールして、 **TEMP** 変数の行をクリックし、 **[編集]** をクリックします。  
  
4.  **[システム変数の編集]** ダイアログ ボックスで、 **temp** ディレクトリを配置するドライブとディレクトリのパスと名前を入力します。  
  
5.  **[OK]** をクリックして変更を保存します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler の起動](../../tools/sql-server-profiler/start-sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
