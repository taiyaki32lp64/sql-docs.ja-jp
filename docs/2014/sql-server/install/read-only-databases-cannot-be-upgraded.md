---
title: 読み取り専用データベースをアップグレードすることはできません |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- database cannot be upgraded
ms.assetid: 27964211-ea30-4390-b791-dcf225fb9ae7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 414b26cf860ab32bb11beaa1ccbef3316c68f557
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093369"
---
# <a name="read-only-databases-cannot-be-upgraded"></a>読み取り専用データベースをアップグレードできない
  アップグレード アドバイザーによって、この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにある一部のデータベースをアップグレードできないことが判定されました。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>説明  
 読み取り専用データベースが検出されました。 データベースをアップグレードするには、セットアップ時にそのデータベースへの書き込みが可能である必要があります。  
  
## <a name="corrective-action"></a>修正措置  
 使用して、データベースを使用していない、ときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Manager、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]、または ALTER DATABASE ステートメントを読み取り/書き込みデータベースを変更します。 次のステートメントを使用すると、データベースが読み取り/書き込み可能に変更されます。  
  
```  
USE master;  
GO  
ALTER DATABASE <database name>  
SET READ_WRITE;  
GO  
```  
  
 ALTER DATABASE ステートメントの詳細については、[!INCLUDE[tsql](../../includes/tsql-md.md)] オンライン ブックのトピック「ALTER DATABASE ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 アップグレード アドバイザー&#91;新規&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
