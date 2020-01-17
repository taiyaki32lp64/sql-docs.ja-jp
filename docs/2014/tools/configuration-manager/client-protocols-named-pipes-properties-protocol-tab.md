---
title: クライアント プロトコル - [名前付きパイプのプロパティ] ダイアログ ボックス ([プロトコル] タブ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server], connecting to
- Named Pipes [SQL Server], default pipe
- client protocols [SQL Server]
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3fe7bb05afc8e0814ddb3d872a810759aae2a678
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63253544"
---
# <a name="client-protocols---named-pipes-properties-protocol-tab"></a>クライアント プロトコル - [名前付きパイプのプロパティ] ダイアログ ボックス ([プロトコル] タブ)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーでは、 **[名前付きパイプのプロパティ]** ダイアログ ボックスの **[プロトコル]** タブを使用して、既定のパイプに関する説明の表示や変更を行います。 別のパイプに接続するには、そのパイプを **[既定のパイプ]** ボックスに入力してください。 接続文字列の詳細については、「 [名前付きパイプを使用した有効な接続文字列の作成](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[既定のパイプ]**  
 名前付きパイプ Net-Library が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の対象インスタンスに接続するために使用する既定のパイプを指定します。 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は `\\.\pipe\sql\query`  
  
 既定のパイプに接続するには、 `sql\query`  
  
 **有効**  
 指定できる値は **[はい]** か **[いいえ]** のいずれかです。  
  
## <a name="see-also"></a>参照  
 [ネットワーク プロトコルの選択](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
