---
title: サポートされていない関数を削除する OPENXML の XPath 式の更新 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- OPENXML queries
ms.assetid: b459abaf-8787-4b65-9231-ae30e5469fd0
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec0edb2e72143fd41709355a3e9cc338544289a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091690"
---
# <a name="update-openxml-xpath-expressions-to-remove-unsupported-functions"></a>OPENXML XPath 式の更新によりサポートされていない関数が削除される
  アップグレード アドバイザーによって、XPath 機能の使用が検出されました。 OPENXML の XPath 機能が変更されているので、アップグレードした後でその影響を受ける可能性があります。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>説明  
 現在では、MSXML 3.0 が、OPENXML クエリ内で使用される XPath 式を処理するための基本エンジンとなっています。 MSXML 3.0 には、より精密な XPath 1.0 エンジンがあります。これにより、以下の関数のサポートが削除されています。  
  
-   format-number()  
  
-   formatNumber()  
  
-   current()  
  
-   element-available()  
  
-   function-available()  
  
-   system-property()  
  
## <a name="corrective-action"></a>修正措置  
 format-number() と formatNumber() の場合、[!INCLUDE[tsql](../../includes/tsql-md.md)] を使用できます。 前述したその他のサポートされていない関数については、直接的な対応策はありません。  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 アップグレード アドバイザー&#91;新規&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
