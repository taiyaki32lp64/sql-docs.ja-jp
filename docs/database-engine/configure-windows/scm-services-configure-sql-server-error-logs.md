---
title: SQL Server エラー ログの構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.configurelogs.configureerrorlogs.f1
ms.assetid: 03f0d463-9b0b-4af9-a853-da936d75e5af
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8e746861ef30305a901c388f7574a4a27e2edab4
ms.sourcegitcommit: 02b7fa5fa5029068004c0f7cb1abe311855c2254
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2019
ms.locfileid: "74127478"
---
# <a name="scm-services---configure-sql-server-error-logs"></a>SCM サービス - SQL Server エラー ログを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログを再利用する方法を表示したり、変更したりする方法について説明します。  

## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>[SQL Server エラー ログの構成] ダイアログ ボックスを開くには  

1. オブジェクト エクスプローラーで、使用している SQL Server のインスタンスを展開し、 **[管理]** を展開します。次に、 **[SQL Server ログ]** を右クリックし、 **[構成]** をクリックします。

2. **[SQL Server エラー ログの構成]** ダイアログ ボックスで、次のオプションから選択します。

    A. ログ ファイルの数

      **[再利用する前に、エラー ログ ファイルの数を制限する]**

      再利用されるまでに作成されるエラー ログの数を制限する場合にオンにします。 新しいエラー ログは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを起動するたびに作成されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、このチェック ボックスをオンにし、エラー ログ ファイルの最大数に別の数を指定しない限り、6 つ前までのログのバックアップが保持されます。  
  
      **[エラー ログ ファイルの最大数]**

      再利用されるまでに作成されるアーカイブ済みエラー ログ ファイルの最大数を指定します。 既定値は 6 です。現在のファイルは含まれません。 この値により、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が再利用するまで保有している以前のバックアップ ログの数が決定されます。

    B. ログ ファイルのサイズ

      **エラー ログ ファイルの最大サイズ (KB 単位)**

      各ファイルのサイズは KB 単位で設定できます。 0 のままにしておくと、ログのサイズは無制限になります。
