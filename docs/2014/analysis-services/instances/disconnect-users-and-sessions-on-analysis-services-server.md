---
title: ユーザーを切断 Analysis Services サーバーとセッション |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ending user activity [Analysis Services]
- connections [Analysis Services]
- sessions [Analysis Services]
ms.assetid: 3b0145a2-f21d-4dd0-a09e-83afeb2ff4a9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7c1a974025e1f23cd5fa0a3b7824431d422bfe35
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080066"
---
# <a name="disconnect-users-and-sessions-on-analysis-services-server"></a>Analysis Services サーバー上のユーザーとセッションの切断
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の管理者は、ワークロード管理の一環としてユーザー操作を終了できます。 ユーザー操作を終了するには、セッションと接続を取り消します。 セッションは、クエリの実行時に自動的に作成される場合 (暗黙的) と、管理者が作成時に名前を付ける場合 (明示的) があります。 接続は、クエリを実行できる開かれたパイプのようなものです。 セッションと接続は両方とも、アクティブなときに終了できます。 たとえば、処理に時間がかかりすぎる場合や、実行中のコマンドが正しく記述されているかどうかについて疑問が生じた場合、管理者はセッションの処理を終了できます。  
  
## <a name="ending-sessions-and-connections"></a>セッションと接続の終了  
 セッションおよび接続の管理には、動的管理ビュー (DMV) および XMLA を使用できます。  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、Analysis Services インスタンスに接続します。  
  
2.  現在実行中のすべてのセッション、接続、およびコマンドのリストを取得するには、次のいずれかの DMV クエリを MDX クエリ ウィンドウに貼り付けます。  
  
     `Select * from $System.Discover_Sessions`  
  
     `Select * from $System.Discover_Connections`  
  
     `Select * from $System.Discover_Commands`  
  
3.  F5 キーを押してクエリを実行します。  
  
     DMV クエリは、セッションと接続の情報を、読み取りやコピーが容易な表形式の結果セットとして返します。  
  
 クエリ ウィンドウを開いた状態にします。 次の手順では、切断するセッションの SPID をコピーするために、このページに戻ります。  
  
 セッションを終了するために、XMLA クエリ ウィンドウをもう 1 つ開きます。  
  
1.  次の構文を MDX クエリ ウィンドウに貼り付けます。ConnectionID、SessionID、または SPID プレースホルダーは、前の手順からコピーした有効な値に置き換えてください。  
  
    ```  
    <Cancel xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
  
       <ConnectionID>111</ConnectionID>  
       <SessionID>222</SessionID>  
       <SPID>333</SPID>  
  
    <CancelAssociated>1</CancelAssociated>  
    </Cancel>  
  
    ```  
  
2.  F5 キーを押してキャンセル コマンドを実行します。  
  
 接続を終了すると、すべてのセッションと SPID が取り消され、ホスト セッションが閉じられます。  
  
 セッションを終了すると、そのセッションの一部として実行されているすべてのコマンド (SPID) が停止します。  
  
 SPID を終了すると、特定のコマンドが取り消されます。  
  
 まれに、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] で接続に関連付けられているすべてのセッションおよび SPID を追跡できない場合 (HTTP シナリオで複数のセッションが開かれている場合など) は、接続を閉じることができません。  
  
 このトピックで参照された XMLA の詳細については、[「Execute メソッド (XMLA)」](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) および [「Cancel 要素 (XMLA)」](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla) を参照してください。  
  
## <a name="see-also"></a>参照  
 [接続およびセッションの管理 (XMLA)](../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [BeginSession 要素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/beginsession-element-xmla)   
 [EndSession 要素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/endsession-element-xmla)   
 [Session 要素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/session-element-xmla)  
  
  
