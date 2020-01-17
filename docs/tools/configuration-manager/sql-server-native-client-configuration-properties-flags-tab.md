---
title: '[SQL Server Native Client の構成のプロパティ] ダイアログ ボックス ([フラグ] タブ) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 59af121d-c8b9-4faa-91a1-b664f2c9b441
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e185c6bd783ef656871ae75e34be3b6a5216964a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68024002"
---
# <a name="sql-server-native-client-configuration-properties-flags-tab"></a>[SQL Server Native Client の構成のプロパティ] ダイアログ ボックス ([フラグ] タブ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ライブラリ ファイルで提供されているプロトコルを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サーバーと通信します。 このページでは、クライアント コンピューターで SSL (Secure Sockets Layer) を使用した暗号化接続を要求するための構成を行います。 暗号化接続を確立できない場合は、接続が失敗します。  
  
 ログイン プロセスは常に暗号化されます。 以下のオプションは暗号化されているデータにのみ適用されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が通信を暗号化する方法の詳細、およびサーバー証明書のルート機関を信頼するようにクライアントを構成する方法については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続の暗号化」と「[!INCLUDE[ssDE](../../includes/ssde-md.md)] への暗号化接続を有効にする方法 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャー)」をご覧ください。  
  
## <a name="options"></a>オプション  
 **[Force protocol encryption]**  
 常に、SSL を使用して接続する必要があります。  
  
 **[Trust Server Certificate]**  
 **[いいえ]** に設定されている場合、クライアント プロセスはサーバー証明書の検証を試みます。 クライアントとサーバーはそれぞれ、公的な証明機関から発行された証明書を持っている必要があります。 クライアント コンピューターに証明書がない場合や、証明書の検証が失敗した場合は、接続が終了します。  
  
 **[はい]** に設定されている場合、クライアントは、サーバー証明書を検証せずに、自己署名証明書の使用を許可します。  
  
 **[Trust Server Certificate]** は、 **[Force protocol encryption]** が **[はい]** に設定されている場合のみ使用できます。  
  
  
