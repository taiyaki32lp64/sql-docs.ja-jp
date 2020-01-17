---
title: 大きな定数が互換性モード 90 以上に大きな値の型として型指定された |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- binary constants
- CHARINDEX function
- constants
- character string constants
- PATINDEX function
ms.assetid: 6e309fa0-5fb9-45a1-9739-f13fae525bfe
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c7aded5577e28d94f42e108e46bb8a9c3cd6020
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094091"
---
# <a name="large-constants-are-typed-as-large-value-types-in-90-or-later-compatibility-modes"></a>90 以上の互換性モードでは大きな定数が大きな値の型として指定される
  アップグレード アドバイザーは、大きな定数の存在を検出しました。 サイズが 8,000 バイトを超える文字列定数とバイナリ定数は、[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ではラージ オブジェクト データ型として扱われます。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンでは、大きなサイズの文字定数、Unicode 定数、およびバイナリ定数が大きな値の型として指定されます。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>説明  
 CHARINDEX や PATINDEX などの文字列関数が 8,000 バイトを超える文字列定数またはバイナリ定数と共に使用されると、[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] はエラー番号 8116 を返し、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンはエラー番号 8152 を返します。  
  
 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] では、文字列関数を `text`、`ntext`、および `image` データ型と共に使用した場合に、文字列関数がエラー 8116 を返します。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンでは、大きな定数はそれぞれが `varchar(max)`、`nvarchar(max)`、および `varbinary(max)` データ型として扱われます。 これらのデータ型は文字列関数と互換性があります。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンでは、CHARINDEX や PATINDEX などの文字列関数は、検出される文字シーケンスを含む文字列が 8,000 バイト未満であると想定しています。 このため、CHARINDEX や PATINDEX に対してエラー 8152 が発生します。  
  
## <a name="see-also"></a>関連項目  
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 アップグレード アドバイザー&#91;新規&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
