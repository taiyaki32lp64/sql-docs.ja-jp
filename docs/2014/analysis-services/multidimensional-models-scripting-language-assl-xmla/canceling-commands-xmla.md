---
title: コマンドのキャンセル (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- connections [XML for Analysis]
- associated connections [XML for Analysis]
- XML for Analysis, canceling
- associated sessions [XML for Analysis]
- canceling connections
- canceling commands
- canceling sessions
- SPID
- XMLA, canceling
- server process IDs [XML for Analysis]
- sessions [XML for Analysis]
ms.assetid: b59f8197-c33d-4e65-9022-848ccba540f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 80bddac8f800c1b9394c1ed605007ab0f2137b88
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62727466"
---
# <a name="canceling-commands-xmla"></a>コマンドのキャンセル (XMLA)
  コマンドを発行したユーザーの管理アクセス許可に応じて、[キャンセル](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)Analysis (XMLA) は、コマンドをキャンセルして、セッション、セッション、接続、サーバー プロセス、または、関連付けられているセッションでの XML でコマンドまたは接続します。  
  
## <a name="canceling-commands"></a>コマンドのキャンセル  
 プロパティを指定せずに `Cancel` コマンドを送信することにより、ユーザーは現在の明示的なセッションのコンテキスト内で現在実行中のコマンドをキャンセルできます。  
  
> [!NOTE]  
>  暗黙のセッション内で実行中のコマンドは、ユーザー操作によって取り消すことはできません。  
  
### <a name="canceling-batch-commands"></a>バッチ コマンドのキャンセル  
 ユーザーが `Batch` コマンドを取り消した場合、`Batch` コマンド内に残っている未実行のコマンドはすべて取り消されます。 `Batch` コマンドがトランザクション型であれば、`Cancel` コマンドの実行前に実行されたすべてのコマンドはロールバックされます。  
  
## <a name="canceling-sessions"></a>セッションのキャンセル  
 明示的なセッションのセッション識別子を指定することによって、 [SessionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)のプロパティ、`Cancel`コマンドをデータベース管理者またはサーバー管理者は、現在実行中のコマンドを含む、セッションをキャンセルできます. データベース管理者は、自分が管理権限を持つデータベースに対するセッションだけをキャンセルできます。  
  
 データベース管理者は、DISCOVER_SESSIONS スキーマ行セットを取得することにより、指定されたデータベースに対するアクティブ セッションを取得することができます。 データベース管理者が、XMLA を使用するには、DISCOVER_SESSIONS スキーマ行セットを取得するには、`Discover`メソッド内の SESSION_CURRENT_DATABASE 制限列の適切なデータベース識別子を指定し、 [の制限](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictions-element-xmla)のプロパティ、`Discover`メソッド。  
  
## <a name="canceling-connections"></a>接続のキャンセル  
 接続識別子を指定することで、 [ConnectionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/connectionid-element-xmla)のプロパティ、`Cancel`コマンド、サーバー管理者がすべての実行中のすべてのコマンドを含む、特定の接続に関連付けられているセッションをキャンセルし、接続をキャンセルします。  
  
> [!NOTE]  
>  場合、インスタンスの[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]見つけてインスタンスが接続を取り消すことはできません、データ ポンプでは、HTTP 接続を提供しながら複数のセッションが開いたらなど、接続に関連付けられているセッションを取り消すことはできません。 `Cancel` コマンドの実行中にこのような状況が生じた場合には、エラーが発生します。  
  
 サーバー管理者は XMLA の `Discover` メソッドを使用して DISCOVER_CONNECTIONS スキーマ行セットを取得することにより、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスのアクティブな接続を取得できます。  
  
## <a name="canceling-server-processes"></a>サーバー プロセスのキャンセル  
 サーバー プロセス識別子 (SPID) を指定することによって、 [SPID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)のプロパティ、`Cancel`コマンド、サーバー管理者は、特定の SPID に関連付けられているコマンドを取り消すことができます。  
  
## <a name="canceling-associated-sessions-and-connections"></a>関連するセッションおよび接続のキャンセル  
 設定することができます、 [CancelAssociated](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cancelassociated-element-xmla)プロパティを接続、セッション、および接続、セッション、またはで指定された SPID に関連付けられているコマンドをキャンセルする場合は true、`Cancel`コマンド。  
  
## <a name="see-also"></a>参照  
 [Discover メソッド&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)   
 [Analysis Services での XMLA による開発](developing-with-xmla-in-analysis-services.md)  
  
  
