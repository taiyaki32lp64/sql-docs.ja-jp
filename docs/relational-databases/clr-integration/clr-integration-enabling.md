---
title: CLR 統合の有効化 |Microsoft Docs
ms.custom: ''
ms.date: 09/17/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- clr enabled option
- common language runtime [SQL Server], enabling
ms.assetid: eb3e9c64-7486-42e7-baf6-c956fb311a2c
author: rothja
ms.author: jroth
ms.openlocfilehash: 07066dc7ffbd48273ace55e0c9867661b2cbfe59
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71680852"
---
# <a name="clr-integration---enabling"></a>CLR 統合 - 有効化
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  CLR (共通言語ランタイム) 統合機能は既定では無効になっているので、CLR 統合を使用して実装されるオブジェクトを使用するには、この機能を有効にする必要があります。 CLR 統合を有効にするには、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の**sp_configure**ストアドプロシージャの**clr enabled**オプションを使用します。  
  
```sql  
EXEC sp_configure 'clr enabled', 1;  
RECONFIGURE;  
GO  
```  
  
 Clr の統合を無効にするには、 **clr enabled**オプションを0に設定します。 CLR 統合を無効にすると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] すべてのユーザー定義 CLR ルーチンの実行が停止し、すべてのアプリケーションドメインがアンロードされます。 **Hierarchyid**データ型、`FORMAT` 関数、レプリケーション、ポリシーベースの管理など、CLR に依存する機能は、この設定の影響を受けず、引き続き機能します。
  
> [!NOTE]  
>  CLR 統合を有効にするには、 **sysadmin**固定サーバーロールおよび**serveradmin**固定サーバーロールのメンバーによって暗黙的に保持される ALTER SETTINGS サーバーレベル権限が必要です。  
  
> [!NOTE]  
>  コンピューターを構成しているメモリ サイズとプロセッサ数が非常に大きい場合、SQL Server の CLR 統合機能をサーバーの起動時に読み込めないことがあります。 この問題に対処するには、 **-gmemory_to_reserve**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスのスタートアップオプションを使用してサーバーを起動し、十分な大きさのメモリ値を指定します。 詳細については、「 [データベース エンジン サービスのスタートアップ オプション](../../database-engine/configure-windows/database-engine-service-startup-options.md)」を参照してください。  
  
> [!NOTE]  
>  簡易プーリングでは、共通言語ランタイム (CLR) の実行はサポートされていません。 CLR 統合を有効にする前に、簡易プーリングを無効にする必要があります。 詳細については、「 [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [clr enabled サーバー構成オプション](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [サーバー レベルのロール](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
