---
title: "トレース定義の既定値 (SQL Server Profiler) を設定 |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- traces [SQL Server], defaults
ms.assetid: ab9fc570-797d-411e-814f-1c46d2d5feae
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4ef7efda96c725e38ebb3f5d63f93c33816e790a
ms.contentlocale: ja-jp
ms.lasthandoff: 08/02/2017

---
# <a name="set-trace-definition-defaults-sql-server-profiler"></a>トレース定義の既定値の設定 (SQL Server Profiler)
  トレース定義の既定値は、プロバイダーまたはサーバーごとに使用される既定のトレース テンプレートです。 既定のトレース テンプレートは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]に設定できます。  
  
### <a name="to-set-trace-definition-defaults"></a>トレース定義の既定値を設定するには  
  
1.  **[ファイル]** メニューの **[テンプレート]**をクリックし、 **[テンプレートの編集] をクリックします。**  
  
2.  **[トレース テンプレートのプロパティ]** ダイアログ ボックスの **[全般]**タブで、 **[サーバーの種類の選択]**ボックスの一覧からサーバーの種類を選択します。  
  
3.  **[テンプレート名の選択]**ボックスの一覧で、トレース定義の既定値として使用するテンプレートの名前を選択します。  
  
4.  **[選択したサーバーの種類に対する既定のテンプレートとして使用する]**チェック ボックスをオンにします。  
  
5.  必要な場合は、 **[イベントの選択]**タブをクリックして、テンプレートを編集します。  
  
6.  **[保存]**をクリックします。  
  
## <a name="see-also"></a>参照  
 [SQL Server プロファイラーのテンプレート](../../tools/sql-server-profiler/sql-server-profiler-templates.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  