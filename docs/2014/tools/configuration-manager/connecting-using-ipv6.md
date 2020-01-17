---
title: IPv6 を使用して接続する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Internet Protocol
- IPv4
- IPv6
ms.assetid: 2669098c-f5f1-43da-aec6-e91003ac89f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: db26351430c6b7e0737273b2107bea242c455a2a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63253780"
---
# <a name="connecting-using-ipv6"></a>IPv6 を使用した接続
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client では、インターネット プロトコル バージョン 4 (IPv4) とインターネット プロトコル バージョン 6 (IPv6) の両方が完全にサポートされます。 Windows で IPv6 が構成されている場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のコンポーネントは IPv6 の存在を自動的に認識します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で特別な構成は必要ありません。  
  
 サポートには次のものが含まれていますが、これらだけではありません。  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] と他のサーバー コンポーネントは、同時に IPv4 および IPv6 の両方のアドレスでリッスンできます。 IPv4 と IPv6 の両方が存在する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、IPv4 アドレスまたは IPv6 アドレスのどちらかだけでリッスンするように [!INCLUDE[ssDE](../../includes/ssde-md.md)] を構成できます。  
  
-   IPv4 および IPv6 の両方をサポートするコンピューターで実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスに対して、IPv4 アドレスにクエリが実行された場合、IPv4 アドレスとそのリストにある最初の IPv4 TCP ポートを使用して応答が行われます。 IPv6 アドレスにクエリが実行された場合は、IPv6 アドレスとそのリストにある最初の IPv6 TCP ポートを使用して応答が行われます。 一貫性を保つために、IPv4 リスナーと IPv6 リスナーが同じポートでリッスンするように構成することをお勧めします。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーなどのツールでは、IP アドレスに IPv4 と IPv6 の両方の形式を使用できます。 ほとんどの場合、\<*computer_name*>\\<*instance_name*> がサーバーのホスト名か完全修飾ドメイン名 (FQDN) を使用して指定されているときは、接続文字列を変更する必要はありません。 サーバー コンピューターで IPv4 と IPv6 の両方が構成されている場合、そのホスト名または FQDN は複数の IP アドレス (少なくとも、1 つの IPv4 アドレスと複数の IPv6 アドレス) に解決されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client は、これらの IP アドレスを TCP/IP から受信した順序で使用して接続の確立を試み、最初に成功した接続を使用します。 順序は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client が予測できないため、ランダムな順序になります。 IPv4 アドレスと IPv6 アドレスの両方が存在する場合、最初に IPv4 アドレスで試行されます。 このロジックは、ODBC、OLE DB、または ADO.NET のユーザーに対して透過的です。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssDE](../../includes/ssde-md.md)] が IPv4 でリッスンしていない場合、IPv6 アドレスで試行するには、試行された IPv4 接続がタイムアウトするまでの間、待機する必要があります。 これを回避するには、直接 IPv6 の IP アドレスで接続するか、IPv6 アドレスを使用してクライアントの別名を構成してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server 構成マネージャー](../../relational-databases/sql-server-configuration-manager.md)  
  
  
