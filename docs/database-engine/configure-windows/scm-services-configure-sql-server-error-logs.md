---
title: "SQL Server エラー ログの構成 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.configurelogs.configureerrorlogs.f1
ms.assetid: 03f0d463-9b0b-4af9-a853-da936d75e5af
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d6815aac3852922ae49a4953abc501a2cf958a4c
ms.contentlocale: ja-jp
ms.lasthandoff: 08/02/2017

---
# <a name="scm-services---configure-sql-server-error-logs"></a>SCM サービス - SQL Server エラー ログを構成する
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログを再利用する方法を表示したり、変更したりする方法について説明します。  
  
## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>[SQL Server エラー ログの構成] ダイアログ ボックスを開くには  
  
1.  オブジェクト エクスプローラーで、使用している SQL Server のインスタンスを展開し、 **[管理]**を展開します。次に、 **[SQL Server ログ]**を右クリックし、 **[構成]**をクリックします。  
  
2.  **[SQL Server エラー ログの構成]** ダイアログ ボックスで、次のオプションから選択します。  
  
     **[再利用する前に、エラー ログ ファイルの数を制限する]**  
     再利用されるまでに作成されるエラー ログの数を制限する場合にオンにします。 新しいエラー ログは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを起動するたびに作成されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、このチェック ボックスをオンにし、エラー ログ ファイルの最大数に別の数を指定しない限り、6 つ前までのログのバックアップが保持されます。  
  
     **[エラー ログ ファイルの最大数]**  
     再利用されるまでに作成されるエラー ログ ファイルの最大数を指定します。 既定値は 6 で、これは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が再利用するまで保有している以前のバックアップ ログの数と同じです。  
  
  