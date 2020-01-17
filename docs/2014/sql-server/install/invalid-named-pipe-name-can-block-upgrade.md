---
title: 無効な名前付きパイプ名によってアップグレードがブロック |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- invalid named pipes [SQL Server]
- named pipes
ms.assetid: 58c2199c-4fdf-4d43-ac1c-842703344b75
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dddd5da66f09226579a6366baa1a16a6ab00d6bf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094190"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>無効な名前付きパイプ名によってアップグレードがブロックされる
  アップグレードは、名前付きパイプのプロトコルの構成が正しくない場合は失敗します。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>説明  
 アップグレード中に、セットアップ プログラムの起動、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]インスタンス共有メモリ サポートと、ローカル接続のみを受け入れる名前付きパイプします。 文字列で始まる必要がありますが、サーバーで指定したパイプ名が空白でない場合は、"\\\\. \pipe\\"を有効にします。 パイプ名が有効でない場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)]が起動せず、セットアップは失敗します。  
  
## <a name="corrective-action"></a>修正措置  
 使用して、  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ネットワーク ユーティリティ**有効なパイプ名を指定し、セットアップを実行します。  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 アップグレード アドバイザー&#91;新規&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
