---
title: "シリアル化可能性 |Microsoft ドキュメント"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction isolation [ODBC]
- transactions [ODBC], serialization
- serialization [ODBC]
- transactions [ODBC], isolation
ms.assetid: 142e4ac0-2977-4a2b-96ae-c9e5bd2c448a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 81d23b5bc94f2982becca5e76ab28269d6c233c1
ms.contentlocale: ja-jp
ms.lasthandoff: 09/09/2017

---
# <a name="serializability"></a>シリアル化可能性
トランザクションが理想的には、する必要があります*シリアル化可能な*します。 トランザクションが同時に実行されるトランザクションの結果が同じで、結果を逐次的に実行する場合は、シリアル化できると考えられます: つまり、1 つずつです。 トランザクションが最初に実行、のみ結果反映されていないトランザクションを混在させることは重要はありません。  
  
 たとえば、トランザクション A が 2 でのデータ値を乗算し、トランザクション B がデータ値に 1 を加算します。 たとえば次の 2 つのデータ値があること。 0 から 10。 これらのトランザクションが実行される場合、他の後に 1 つ、新しい値はされ、1 と 21 トランザクション A が最初に、実行された場合または 2 22 トランザクション B が最初に実行される場合。 2 つのトランザクションの実行順序は値ごとに異なる場合。 トランザクション A が最初の値の先頭を実行し、トランザクション B が最初に実行する 2 番目の値の場合、新しい値は 1 および 22 です。 この順序が元に戻す場合、新しい値は 2 および 21 です。 このトランザクションはシリアル化可能な 1、21、および 2 22 が可能な唯一の結果。 このトランザクションはいない場合は 1、22 または 2、21 シリアル化可能な考えられる結果です。  
  
 なぜシリアル化可能性ことをお勧めしますか。 つまり、その 1 つのトランザクションが表示されることが重要である理由は、次のトランザクションを開始する前に終了するか。 次の問題を検討してください。 セールスマンは、注文を入力する、同時に、クラークの請求額を送信していますがします。 セールスマン会社 X から注文を入力します。 コミットしません。セールスマンはもやはり、担当者に会社 X からです。クラークは、開いているすべての注文の一覧を要求し、会社 X の順序を検出し、請求書を送信します。 これで、会社 X の担当者、セールスマン変更した場合に、トランザクションをコミットする前に、その順序を変更することにしました。 会社 X は、正しくない、課金内容を取得します。  
  
 セールスマンのおよびクラークのトランザクション シリアル化可能な場合は、この問題が発生したことはありませんが。 正しい課金内容をクラークは送信がいる場合、クラークのトランザクションを開始する前にセールスマンのトランザクションが完了または後者セールスマンのトランザクションが開始する前に、クラークのトランザクションが完了したら、クラークは送信していない部品表会社 X にまったくです。