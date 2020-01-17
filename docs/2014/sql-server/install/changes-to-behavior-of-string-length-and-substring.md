---
title: String-length と substring の動作への変更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2119b7ba-2e52-44bf-ac57-82c2d46a48ff
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18643dfc11d2b1b1d875a19c478f9ec8cbdd5be6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66428846"
---
# <a name="changes-to-behavior-of-string-length-and-substring"></a>string-length および substring の動作の変更
  [String-length 関数&#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length)と[substring 関数&#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring)関数が含まれている XML データベースで使用すると、異なる結果を返す可能性がありますサロゲート文字。  
  
## <a name="description"></a>説明  
 データベースの設定されていると互換性がある場合[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]の動作、 [string-length 関数&#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-string-length)と[substring 関数&#40;XQuery&#41; ](/sql/xquery/functions-on-string-values-substring)Unicode 補助文字を扱うときの関数の変更。 U+FFFF より大きいコード ポイントで定義された各 Unicode 補助文字は、これらの関数では 1 文字としてカウントされます。前のバージョンでは 2 文字としてカウントされていました。  
  
 サロゲート文字の詳細については、次を参照してください。[サロゲートおよび補助文字](https://go.microsoft.com/fwlink/?LinkId=178317)します。  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 アップグレード アドバイザー&#91;新規&#93;](https://docs.microsoft.com/sql/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
