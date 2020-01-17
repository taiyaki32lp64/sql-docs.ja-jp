---
title: filestream access level サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], access level
- filestream access level
ms.assetid: b88f6ff2-795e-4730-bfb8-dbc6a958f2ad
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8335f821e2bd4026c17b0054e047125a0afd0177
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68011704"
---
# <a name="filestream-access-level-server-configuration-option"></a>filestream access level サーバー構成オプション
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  この [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスに対する FILESTREAM のアクセス レベルを変更するには、filestream_access_level オプションを使用します。  
  
> [!NOTE]  
>  このオプションを有効にする前に、FILESTREAM の Windows 管理者設定を有効にする必要があります。 これらの設定は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール時に有効にできます。また、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して有効にすることもできます。  
  
|[値]|定義|  
|-----------|----------------|  
|0|このインスタンスに対する FILESTREAM サポートを無効にします。|  
|1|[!INCLUDE[tsql](../../includes/tsql-md.md)] アクセスに対して FILESTREAM を有効にします。|  
|2|[!INCLUDE[tsql](../../includes/tsql-md.md)] アクセスおよび Win32 ストリーム アクセスに対して FILESTREAM を有効にします。|  
  
## <a name="see-also"></a>参照  
 [データベース エンジンの構成 - Filestream](https://msdn.microsoft.com/library/641a10a1-ae52-4d26-8f1c-a032a4aeff02)   
 [FILESTREAM の有効化と構成](../../relational-databases/blob/enable-and-configure-filestream.md)  
  
  
