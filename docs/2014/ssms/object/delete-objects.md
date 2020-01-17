---
title: '[オブジェクトの削除] | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.deleteobjects.f1
helpviewer_keywords:
- Delete Objects dialog box
ms.assetid: 49541441-179c-40d3-ba0c-01bcae545984
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e8912b0e3cac7ccde8f89c1818fd9737c29ebc0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211248"
---
# <a name="delete-objects"></a>[オブジェクトの削除]
  このダイアログ ボックスを使用すると、データベースまたはデータベース オブジェクトを削除できます。  
  
## <a name="uielement-list"></a>UI 要素の一覧  
 **[削除されるオブジェクト]**  
 削除するオブジェクトの名前、種類、所有者、および状態を、実行中のエラーに関するメッセージと一緒に表示します。  
  
> [!NOTE]  
>  データベース上で **[削除]** を実行することは、 [!INCLUDE[tsql](../../includes/tsql-md.md)]の DROP DATABASE を発行することと同じです。  
  
 **[依存関係の表示]**  
 クリックすると、現在選択されているオブジェクトに依存するオブジェクトと、現在のオブジェクトが依存しているオブジェクトの両方のオブジェクト (上位依存関係と下位依存関係) が表示されます。 **[依存関係の表示]** ダイアログ ボックスに表示される情報は読み取り専用です。  
  
> [!NOTE]  
>  **[依存関係の表示]** ボタンは、すべての種類のデータベース オブジェクトに対して表示されるとは限りません。 **[依存関係の表示]** ボタンが表示されていないときに依存関係を表示するには、オブジェクト エクスプローラーでオブジェクトを右クリックし、 **[依存関係の表示]** をクリックします。  
  
 **[バックアップを削除し、データベースの履歴情報を復元する]**  
 データベースが削除されるときにだけ表示されます。このチェック ボックスを使用すると、サブジェクト データベースのバックアップおよび復元履歴が **msdb** データベースから削除されます。  
  
 **[既存の接続を閉じる]**  
 データベースが削除されるときにだけ表示されます。このチェック ボックスを使用すると、サブジェクト データベースへの接続を終了できます。  
  
  
