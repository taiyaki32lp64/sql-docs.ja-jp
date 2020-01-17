---
title: SQL Server エラー ログ (可用性グループ)
description: Always On 可用性グループによって報告されるエラー ログ イベントの説明です。
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 39d0c98d-75af-4dd1-b908-30d31af56f2a
author: rothja
ms.author: jroth
ms.openlocfilehash: 81d31225838ec029a020af2df25753b26acd2fb1
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75251252"
---
# <a name="sql-server-error-log-always-on-availability-groups"></a>SQL Server エラー ログ (Always On 可用性グループ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server エラー ログでは、次のような Always On 可用性グループに影響するイベントを報告します。  
  
-   Windows Server フェールオーバー クラスタリング (WSFC) クラスターとの通信    
-   可用性レプリカの状態遷移    
-   可用性データベースの状態遷移    
-   プライマリ レプリカとセカンダリ レプリカの間での可用性データベースの接続状態    
-   可用性グループのエンドポイントの状態    
-   可用性グループのリスナーの状態    
-   SQL Server リソース DLL (WSFC クラスターで実行されている) と SQL Server インスタンスの間のリース ステータス (詳細については、「[How It Works: SQL Server Always On lease timeout](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-alwayson-lease-timeout.aspx)」 (動作方法: SQL Server Always On のリース タイムアウト) を参照してください)。    
-   可用性グループのエラー イベント  

次の現象は、SQL Server エラー ログで確認する必要があります。  

-   可用性データベースにアクセスできない    
-   可用性グループの予期しないフェールオーバー    
-   予期しない解決状態の可用性グループ    
-   不確定な状態の可用性グループ  
  
詳細については、「[SQL Server エラー ログの表示 &#40;SQL Server Management Studio&#41;](~/relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)」を参照してください。  
  
  
