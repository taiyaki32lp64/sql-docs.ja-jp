---
title: clr enabled サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- assemblies [CLR integration], verifying can run
- clr enabled option
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 45c72bc5b811fec8e5532d5d03d4552cc2e0d319
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62786684"
---
# <a name="clr-enabled-server-configuration-option"></a>clr enabled サーバー構成オプション
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でユーザー アセンブリを実行できるかどうかを指定するには、clr enabled オプションを使用します。 clr enabled オプションでは、次の値を指定します。  
  
|値|Description|  
|-----------|-----------------|  
|0|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でアセンブリを実行できません。|  
|1|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でアセンブリを実行できます。|  
  
 WOW64 サーバーの場合、この設定に対する変更を有効にするには再起動が必要です。 他の種類のサーバーでは、再起動は不要です。  
  
> [!NOTE]  
>  RECONFIGURE が実行され、clr enabled オプションの実行値が 1 から 0 に変更されると、ユーザー アセンブリが含まれているすべてのアプリケーション ドメインが直ちにアンロードされます。  
  
> [!NOTE]  
>  簡易プーリングでは、共通言語ランタイム (CLR) の実行はサポートされていません。 2 つのオプションのいずれかを無効にします。"clr enabled"または"lightweight pooling します。 CLR に依存していてファイバー モードで正しく動作しない機能には、`hierarchy` データ型、レプリケーション、およびポリシー ベースの管理があります。  
  
## <a name="example"></a>例  
 次の例では、最初に clr enabled オプションの現在の設定を表示し、その後、オプションの値を 1 に設定することで、このオプションを有効にします。 このオプションを無効にするには、値を 0 に設定します。  
  
```  
EXEC sp_configure 'clr enabled';  
EXEC sp_configure 'clr enabled' , '1';  
RECONFIGURE;  
  
```  
  
## <a name="see-also"></a>参照  
 [lightweight pooling サーバー構成オプション](lightweight-pooling-server-configuration-option.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [lightweight pooling サーバー構成オプション](lightweight-pooling-server-configuration-option.md)  
  
  
