---
title: カーソル | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- results [SQL Server], cursors
- Transact-SQL cursors, about cursors
- cursors [SQL Server]
- data access [SQL Server], cursors
- result sets [SQL Server], cursors
- requesting cursors
- cursors [SQL Server], about cursors
ms.assetid: e668b40c-bd4d-4415-850d-20fc4872ee72
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8123179285b94377fff758121f535175705f29af
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62918693"
---
# <a name="cursors"></a>カーソル
  リレーショナル データベースで操作を実行する場合、行の完全なセットが操作の対象になります。 たとえば、SELECT ステートメントでは、WHERE 句で指定した条件を満たすすべての行のセットが返されます。 このステートメントが返す行の完全なセットを結果セットと呼びます。 アプリケーション、特に対話型のオンライン アプリケーションでは、必ずしも、結果セット全体をひとまとめに使用して作業することが効率的であるとは限りません。 そのため、このようなアプリケーションでは、一度に 1 行または少数の行のブロックを使用するためのメカニズムが必要になります。 カーソルはそのメカニズムを提供する結果セットの拡張機能です。  
  
 カーソルでは、次のように結果の処理が拡張されます。  
  
-   結果セット内の特定の行に位置付けることができます。  
  
-   結果セット内の現在位置から 1 行または 1 ブロックの行を取得します。  
  
-   結果セット内の現在位置の行データを修正できます。  
  
-   結果セット内のデータベース データに対して他のユーザーが行った変更をさまざまなレベルで表示できます。  
  
-   スクリプト、ストアド プロシージャ、およびトリガー内の [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントから、結果セット内のデータにアクセスできます。  
  
## <a name="concepts"></a>概念  
 カーソルの実装  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、3 つのカーソルの実装がサポートされています。  
  
 Transact-SQL カーソル  
 DECLARE CURSOR 構文に基づいていて、主に [!INCLUDE[tsql](../includes/tsql-md.md)] スクリプト、ストアド プロシージャ、およびトリガーで使用されます。 [!INCLUDE[tsql](../includes/tsql-md.md)] カーソルはサーバー上で実装され、クライアントからサーバーに送信される [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントによって管理されます。 また、バッチ、ストアド プロシージャ、またはトリガーにも含まれている場合があります。  
  
 アプリケーション プログラミング インターフェイス (API) サーバー カーソル  
 OLE DB および ODBC の API カーソル関数をサポートします。 API サーバー カーソルはサーバー上に実装されます。 クライアント アプリケーションから API カーソル関数が呼び出されるたびに、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client の OLE DB プロバイダーまたは ODBC ドライバーによって、API サーバー カーソルに対するアクションの要求がサーバーに送信されます。  
  
 クライアント カーソル  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client の ODBC ドライバーおよび ADO API を実装する DLL によって、内部的に実装されます。 クライアント カーソルは、結果セットのすべての行をクライアント上でキャッシュすることによって実装されます。 クライアント アプリケーションによって API カーソル関数が呼び出されるたびに、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client の ODBC ドライバーまたは ADO DLL によって、クライアント上にキャッシュされた結果セットの行に対してカーソル操作が実行されます。  
  
 カーソルの種類  
 順方向専用  
 順方向専用カーソルは、スクロールをサポートしていません。カーソル内の最初から最後まで順次に行をフェッチする機能だけをサポートしています。 行はフェッチされるまで、データベースから取得されません。 現在のユーザーが作成または別のユーザーがコミットした INSERT、UPDATE、および DELETE ステートメントが、結果セット内の行に与えた影響は、カーソルから行をフェッチした際に確認できます。  
  
 カーソルは後方にスクロールできないので、データベース内の行のフェッチ後にその行に対して行われた変更内容の大部分は、カーソル内で確認できません。 クラスター化インデックスに含まれる列の更新など、結果セット内の行の位置の判定に使用する値が変更されるような場合は、変更された値がカーソル内で表示されます。  
  
 データベース API カーソル モデルでは、順方向専用カーソルが特殊な種類のカーソルと見なされますが、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では違います。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、順方向専用とスクロールの両方が静的カーソル、キーセット ドリブン カーソル、および動的カーソルに適用できるオプションと見なされます。 [!INCLUDE[tsql](../includes/tsql-md.md)] カーソルは、順方向専用の静的カーソル、キーセット ドリブン カーソル、および動的カーソルをサポートします。 データベース API カーソル モデルでは、静的カーソル、キーセット ドリブン カーソル、および動的カーソルが常にスクロール可能であることを前提としています。 データベース API カーソルの属性またはプロパティを順方向専用に設定すると、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] により、カーソルは順方向専用の動的カーソルとして実装されます。  
  
 スタティック  
 静的カーソルを開くと、そのカーソルの完全な結果セットが **tempdb** に作成されます。 静的カーソルは常に、カーソルを開いた時点の結果セットの状態を表示します。 静的カーソルは変更をほとんど検出しませんが、スクロール中に消費するリソースは比較的少なくなります。  
  
 このカーソルは、結果セットのメンバーシップに影響を与えるデータベース内の変更や、結果セットを構成する行の列内の値に対する変更を反映しません。 静的カーソルを開いた後にデータベースに新しい行が挿入されると、カーソルの SELECT ステートメントの検索条件に一致していても、静的カーソルにそれらの行は表示されません。 結果セットを構成する行が他のユーザーによって更新された場合、その新しいデータ値は静的カーソルに表示されません。 静的カーソルを開いた後にデータベースから削除された行は、静的カーソルに表示されます。 UPDATE、INSERT、または DELETE による操作は、静的カーソルを閉じてから再度開かない限り、静的カーソルに反映されません。これは、その静的カーソルを開いたのと同じ接続を使用して変更を行った場合でも同様です。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の静的カーソルは常に読み取り専用です。  
  
 静的カーソルの結果セットは **tempdb**の作業テーブルに格納されるので、結果セット内の行のサイズを [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] テーブルの最大行サイズよりも大きくすることはできません。  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] では、静的カーソルは非反映型カーソルとも呼ばれます。 一部のデータベース API ではスナップショット カーソルとも呼びます。  
  
 Keyset  
 キーセット ドリブン カーソルの構成要素と行の順序は、カーソルを開いたときに固定されます。 キーセット ドリブン カーソルは、キーセットという一意の識別子 (キー) のセットにより制御されます。 これらのキーは、結果セットの行を一意に識別する列のセットから構築されます。 キーセットは、カーソルを開いた時点で SELECT ステートメントにより限定されたすべての行から取り出したキー値のセットです。 キーセット ドリブン カーソルのキーセットは、カーソルを開いたときに **tempdb** に構築されます。  
  
 動的  
 動的カーソルは静的カーソルと対照的です。 動的カーソルは、スクロールされるときに、結果セット内の行に対して行われたすべての変更を反映します。 結果セット内の行のデータ値、順序、およびメンバーシップは、フェッチを実行するたびに変化する可能性があります。 UPDATE、INSERT、および DELETE ステートメントをどのユーザーが実行しても、その実行結果はすべてカーソルに表示されます。 更新が **SQLSetPos** などの API 関数または [!INCLUDE[tsql](../includes/tsql-md.md)] の WHERE CURRENT OF 句のいずれかを使用してカーソルによって行われた場合、それらの更新結果はすぐに表示されます。 カーソルの外部から行った更新は、コミットされるまで表示されません。ただし、カーソルのトランザクション分離レベルが READ UNCOMMITTED に設定されている場合は、その限りではありません。 動的カーソル プランが空間インデックスを使用することはありません。  
  
## <a name="requesting-a-cursor"></a>カーソルの要求  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、カーソルの要求方法として、次の 2 つの方法がサポートされます。  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)]  
  
     [!INCLUDE[tsql](../includes/tsql-md.md)] 言語では、ISO カーソル構文以降にモデル化されたカーソルを使用するための構文がサポートされます。  
  
-   データベース API (アプリケーション プログラミング インターフェイス) のカーソル機能  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、次のデータベース API のカーソル機能がサポートされます。  
  
    -   ADO ([!INCLUDE[msCoName](../includes/msconame-md.md)] ActiveX データ オブジェクト)  
  
    -   OLE DB (OLE DB)  
  
    -   ODBC (Open Database Connectivity)  
  
 アプリケーションでは、カーソルを要求するこれら 2 つの方法を混在して使用しないでください。 また、API を使用してカーソル動作を指定するアプリケーションでは、 [!INCLUDE[tsql](../includes/tsql-md.md)] の DECLARE CURSOR ステートメントを実行して [!INCLUDE[tsql](../includes/tsql-md.md)] カーソルを要求しないでください。 アプリケーションで DECLARE CURSOR ステートメントを実行できるのは、API カーソル属性をすべて既定値に戻した場合だけです。  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] カーソルも API カーソルも要求されない場合、既定では、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] によって既定の結果セットと呼ばれる完全な結果セットがアプリケーションに返されます。  
  
## <a name="cursor-process"></a>カーソル処理  
 [!INCLUDE[tsql](../includes/tsql-md.md)] カーソルと API カーソルでは構文が異なりますが、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のどのカーソルでも、以下の一般的な処理を行います。  
  
1.  カーソルを [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの結果セットに関連付け、カーソル内の行を更新可能にするかどうかなど、そのカーソルの特性を定義します。  
  
2.  カーソルを設定する [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントを実行します。  
  
3.  参照するカーソル内の行を取得します。 カーソルから 1 行または 1 ブロックの行を取得する操作をフェッチと言います。 フェッチを連続して実行し、順方向または逆方向に行を取得することをスクロールと呼びます。  
  
4.  必要に応じて、カーソル内の現在位置の行に対して、更新または削除の変更操作を行います。  
  
5.  カーソルを閉じます。  
  
## <a name="related-content"></a>関連コンテンツ  
 [Cursor Behaviors](native-client-odbc-cursors/cursor-behaviors.md) [How Cursors Are Implemented](native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
## <a name="see-also"></a>参照  
 [DECLARE CURSOR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-cursor-transact-sql)   
 [カーソル &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/cursors-transact-sql)   
 [カーソル関数 &#40;Transact-SQL&#41;](/sql/t-sql/functions/cursor-functions-transact-sql)   
 [カーソル ストアド プロシージャ &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/cursor-stored-procedures-transact-sql)  
  
  
