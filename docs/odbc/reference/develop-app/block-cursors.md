---
title: ブロック カーソル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 1a92b5d8-7c6e-4ce5-8c99-600a387026aa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e0ea6ff655140c979f400f67a59cd7259bac9e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118818"
---
# <a name="block-cursors"></a>ブロック カーソル
多くのアプリケーションでは、かなりのネットワーク経由でデータを取り込む時間を費やしています。 この時間の一部では、実際には、ネットワーク経由でデータを取り込むに費やされ、行のデータを要求する、ドライバーによって行われた呼び出しなどの一部がネットワークのオーバーヘッドに費やされました。 アプリケーションが効率的に使用した場合、後者の時間を短縮できます。*ブロック、* または*fat、* *カーソル、* を一度に 1 つ以上の行を返すことができます。  
  
 アプリケーションを常には、ブロック カーソルを使用するオプションがあります。 一度に 1 つだけの行をフェッチできる、データ ソースのドライバーでブロック カーソルをシミュレートする必要があります。 これは、複数の単一行のフェッチを実行することによって実行できます。 これはありませんが、パフォーマンスが大幅に向上する可能性があります、アプリケーションの営業案件を開きます。 このようなアプリケーションでは、Dbms ブロック カーソルをネイティブに実装すると、ドライバーがこれらの Dbms に関連付けられている公開、パフォーマンスが向上が、発生します。  
  
 ブロック カーソルを 1 回のフェッチで返される行が呼び出される、*行セット*します。 結果セットの行セットを混同しないように重要です。 アプリケーション バッファーに行セットを保持したまま、結果セットは、データ ソースで保持されます。 結果セットを固定すると、行セットがない - 位置を変更し、内容を毎回新しい一連の行がフェッチされます。 ブロック カーソルとして考えることができますが、行セットを指す、単一行には、現在の行には、従来の SQL 順方向専用カーソル ポイントなどのカーソルが、同様*現在行*します。  
  
 複数の行がフェッチされたときに 1 つの行で動作する操作を実行するには、アプリケーションする必要がありますまずを示しますが、現在の行の行。 呼び出して、現在の行が必要な**SQLGetData**と更新プログラムを配置および delete ステートメント。 最初に、ブロック カーソルでは、行セットが戻るときに現在の行が行セットの最初の行にします。 現在の行では、アプリケーション呼び出しを変更する**SQLSetPos**または**SQLBulkOperations** (ブックマークによる更新) します。 次の図は、結果セット、行セット、現在の行、行セットのカーソル、およびブロック カーソルとの関係を示します。 詳細については、次を参照してください。[ブロック カーソルを使用して](../../../odbc/reference/develop-app/using-block-cursors.md)は、このセクションでは、後半と[配置の更新と削除ステートメント](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)と[SQLSetPos によるデータの更新](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)します。  
  
 ![次に、前に、最初と最後の行セットのフェッチ](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 カーソルは、ブロック カーソルであるかどうかは、スクロール可能かどうかを依存しません。 たとえば、レポート アプリケーションでの作業のほとんどを取得して、行の印刷に費やされます。 このため、順方向専用を最速操作、カーソルがブロックされます。 順方向専用カーソルを使用して、スクロール可能なカーソルとネットワーク トラフィックを削減するブロック カーソルの費用を回避するためにします。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ブロック カーソルで使用するためのバインディング列](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [ブロック カーソルの使用](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [行の状態の配列](../../../odbc/reference/develop-app/row-status-array.md)
