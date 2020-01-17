---
title: 拡張ストアド プロシージャのプログラミング |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- gateway applications [SQL Server]
- extended stored procedures [SQL Server], about extended stored procedures
- Open Data Services [SQL Server]
- ODS [SQL Server]
ms.assetid: 561305cd-c803-48af-9eec-2c19f4d311ce
author: rothja
ms.author: jroth
ms.openlocfilehash: 541f24693598d20925dd37d4970c6d9916945793
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032015"
---
# <a name="database-engine-extended-stored-procedures---programming"></a>データベース エンジン拡張ストアド プロシージャ - プログラミング
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]代わりに CLR Integration をご使用ください。  
  
 以前は、SQL Server 以外のデータベース環境とのゲートウェイなど、サーバー アプリケーションの記述には Open Data Services が使用されていましたが、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オープン データ サービス API の廃止になった部分をサポートしません。 当初の Open Data Services API のうち、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で現在でもサポートされているのは拡張ストアド プロシージャ関数の部分のみです。このため、Open Data Services API は拡張ストアド プロシージャ API という名前に変わりました。  
  
 拡張ストアド プロシージャ API アプリケーションへのニーズは、現在では分散クエリや CLR 統合などの強力な新しいテクノロジにほとんど移行しています。  
  
> [!NOTE]  
>  既存のゲートウェイ アプリケーションがある場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に付属している opends60.dll を使用してアプリケーションを実行することはできません。 ゲートウェイ アプリケーションはサポート対象外になりました。  
  
## <a name="extended-stored-procedures-vs-clr-integration"></a>拡張ストアド プロシージャとします。CLR 統合  
 以前のリリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、[!INCLUDE[tsql](../../includes/tsql-md.md)] で表現することが非常に困難であるか記述が不可能なサーバー側ロジックをデータベース アプリケーション開発者が記述するための唯一の方法として、XP (拡張ストアド プロシージャ) が用意されていました。 CLR 統合は、このような拡張ストアド プロシージャの記述に代わる、より堅牢な手段を提供します。 さらに、CLR 統合を使用すると、ストアド プロシージャの形式で記述していたロジックが、テーブル値関数でさらに的確に表現できる場合が多くあります。これにより、関数が生成する結果を SELECT ステートメントの FROM 句に埋め込んでクエリできるようになります。  
  
## <a name="see-also"></a>関連項目  
 [共通言語ランタイム&#40;CLR&#41;統合の概要](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)   
 [CLR テーブル値関数](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)  
  
  
