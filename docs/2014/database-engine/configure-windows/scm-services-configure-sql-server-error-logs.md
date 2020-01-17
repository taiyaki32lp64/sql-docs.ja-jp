---
title: SQL Server エラー ログの構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.configurelogs.configureerrorlogs.f1
ms.assetid: 03f0d463-9b0b-4af9-a853-da936d75e5af
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 60d38caf365d6db54ea0abe688a3fc2979fdab82
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62809685"
---
# <a name="configure-sql-server-error-logs"></a>SQL Server エラー ログの構成
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログを再利用する方法を表示したり、変更したりする方法について説明します。  
  
## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>[SQL Server エラー ログの構成] ダイアログ ボックスを開くには  
  
1.  オブジェクト エクスプローラーで、使用している SQL Server のインスタンスを展開し、 **[管理]** を展開します。次に、 **[SQL Server ログ]** を右クリックし、 **[構成]** をクリックします。  
  
2.  **[SQL Server エラー ログの構成]** ダイアログ ボックスで、次のオプションから選択します。  
  
     **[再利用する前に、エラー ログ ファイルの数を制限する]**  
     再利用されるまでに作成されるエラー ログの数を制限する場合にオンにします。 新しいエラー ログは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを起動するたびに作成されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、このチェック ボックスをオンにし、エラー ログ ファイルの最大数に別の数を指定しない限り、6 つ前までのログのバックアップが保持されます。  
  
     **[エラー ログ ファイルの最大数]**  
     再利用されるまでに作成されるエラー ログ ファイルの最大数を指定します。 既定値は 6 で、これは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が再利用するまで保有している以前のバックアップ ログの数と同じです。  
  
  
