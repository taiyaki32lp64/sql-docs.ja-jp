---
title: filestream access level サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 90b4ec97a3ab31c93e92219b96724b75d7f86425
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62782257"
---
# <a name="filestream-access-level-server-configuration-option"></a>filestream access level サーバー構成オプション
  この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスに対する FILESTREAM のアクセス レベルを変更するには、filestream_access_level オプションを使用します。  
  
> [!NOTE]  
>  このオプションを有効にする前に、FILESTREAM の Windows 管理者設定を有効にする必要があります。 これらの設定は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール時に有効にできます。また、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して有効にすることもできます。  
  
|値|定義|  
|-----------|----------------|  
|0|このインスタンスに対する FILESTREAM サポートを無効にします。|  
|1|[!INCLUDE[tsql](../../includes/tsql-md.md)] アクセスに対して FILESTREAM を有効にします。|  
|2|[!INCLUDE[tsql](../../includes/tsql-md.md)] アクセスおよび Win32 ストリーム アクセスに対して FILESTREAM を有効にします。|  
  
## <a name="see-also"></a>参照  
 [データベース エンジンの構成 - Filestream](../../sql-server/install/database-engine-configuration-filestream.md)   
 [FILESTREAM の有効化と構成](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  
