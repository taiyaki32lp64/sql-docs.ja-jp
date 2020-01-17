---
title: 名前付きパイプのプロパティ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- pipes [SQL Server]
- listening [SQL Server], pipes
- pipes [SQL Server], listening on pipes
- Named Pipes [SQL Server], listening on pipes
ms.assetid: a5fd5b8e-f889-485b-89e3-d4010ec4c6ec
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5d8b542e709ed7104d851652e75be41ae4d6afec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62911477"
---
# <a name="named-pipes-properties"></a>[名前付きパイプのプロパティ] ダイアログ ボックス
  **[名前付きパイプのプロパティ]** ダイアログ ボックスの **[プロトコル]** ページでは、名前付きパイプ プロトコルを使用している場合に [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がリッスンする名前付きパイプの表示や変更を行います。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動する必要があるのは、プロトコルを有効または無効にする場合、または名前付きパイプを変更する場合です。  
  
## <a name="options"></a>および  
 **有効**  
 可能な値は、 **[はい]** と **[いいえ]** です。  
  
 **[パイプ名]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がリッスンする名前付きパイプを指定します。 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が既定のインスタンスの場合は `\\.\pipe\sql\query` と、名前付きインスタンスの場合は `\\.\pipe\MSSQL$<instancename>\sql\query` でリッスンします。 このフィールドには最大 2,047 文字まで入力できます。  
  
## <a name="creating-an-alternate-named-pipe"></a>代替名前付きパイプの作成  
 名前付きパイプを変更するには、新しいパイプ名を **[パイプ名]** ボックスに入力し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を再起動します。 **sql\query** は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が使用する名前付きパイプとしてよく知られているため、パイプを変更することによって、悪意のあるプログラムによる攻撃の危険性を減らすことができます。  
  
### <a name="example"></a>例  
 **\\\\unit\app** パイプでリッスンするには、 **.\pipe\unit\app** と入力します。  
  
 **\\\\acct** パイプでリッスンするには、 **.\pipe\acct** と入力します。  
  
## <a name="see-also"></a>参照  
 [サーバー ネットワーク プロトコルの有効化または無効化](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [ネットワーク プロトコルの選択](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [名前付きパイプを使用した有効な接続文字列の作成](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md)  
  
  
