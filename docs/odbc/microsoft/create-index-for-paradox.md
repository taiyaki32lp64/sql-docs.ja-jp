---
title: Paradox の CREATE INDEX |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- Paradox driver [ODBC], create index
ms.assetid: 6472bd69-b931-4bc2-a9bf-f1873ed4cdfe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 331613676b748453a56da1e41fe85f04a7715038
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081938"
---
# <a name="create-index-for-paradox"></a>Paradox の CREATE INDEX
ODBC Paradox ドライバーの CREATE INDEX ステートメントの構文です。  
  
 **CREATE** **[UNIQUE]** **INDEX** *index-name*  
  
 **ON** *テーブル名*  
  
 **(** *列識別子* **[ASC]**  
  
 [ **、** *列識別子* **[ASC]** ... **)**  
  
 ODBC Paradox ドライバーはサポートしていません、 **DESC** CREATE INDEX ステートメントの ODBC SQL 文法のキーワード。 *テーブル名*引数は、テーブルの完全なパスを指定できます。  
  
 場合、キーワード**UNIQUE**指定すると、ODBC Paradox ドライバーは一意のインデックスを作成します。 最初の一意のインデックスは、プライマリ インデックスとして作成されます。 Paradox プライマリ キーという名前のファイルは、この*テーブル名*します。ピクセルです。 プライマリ インデックスは、次の制限が適用されます。  
  
-   すべての行がテーブルに追加される前に、プライマリ インデックスを作成する必要があります。  
  
-   プライマリ インデックスは、テーブル内の最初の"n"列に基づいて定義する必要があります。  
  
-   1 つだけのプライマリ インデックスは、テーブルごとに許可されます。  
  
-   プライマリ インデックスがテーブルに定義されていない場合、Paradox ドライバーによって、テーブルを更新できません。 (空のテーブル、テーブルの一意のインデックスが定義されていない場合でも更新できる場合は true はないことに注意してください)。  
  
-   *インデックス名*プライマリ インデックスの引数は Paradox によって必要に応じて、テーブルの基本名と同じである必要があります。  
  
 場合、キーワード**UNIQUE**は省略すると、ODBC Paradox ドライバーは一意でないインデックスが作成されます。 という名前の 2 つの Paradox セカンダリ インデックスのファイルから成る*テーブル名*します。X*nn*と*テーブル名*します。Y*nn*ここで、 *nn*は、テーブル内の列の数です。 非一意のインデックスは、次の制限が適用されます。  
  
-   テーブルの非一意のインデックスを作成することができます、前に、プライマリ インデックスはそのテーブルの存在する必要があります。  
  
-   Paradox 3。*x*、*インデックス名*(一意または一意ではない)、プライマリ インデックス以外の任意のインデックスの引数には、列名と同じである必要があります。 Paradox 4。*x* 5 *。x*、このようなインデックスの名前はできますが、列名と同じである、する必要はありません。  
  
-   一意でないインデックスの 1 列だけを指定できます。  
  
 テーブルにインデックスを定義した後、列を追加できません。 CREATE TABLE ステートメントの引数リストの最初の列は、インデックスを作成する場合は、引数リストの 2 番目の列を含めることができません。  
  
 たとえば、販売注文番号を使用して、SO_LINES テーブルの一意のインデックスと数値列を行するには、ステートメントを使用します。  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 SO_LINES テーブルの一意でないインデックスと一部の数値列を使用するには、ステートメントを使用します。  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 2 つの CREATE INDEX ステートメントが実行されると、最初のステートメントでは、プライマリ インデックス テーブルと同じ名前で作成常にし、2 番目のステートメントでは、一意でないインデックス列と同じ名前で作成常に注意してください。 場合でも、2 つ目の CREATE INDEX ステートメントで、インデックスが UNIQUE をラベル付けと CREATE INDEX ステートメントごとに異なる名前を入力した場合でもにより、これらのインデックスにこの方法を名前なります。  
  
> [!NOTE]  
>  Borland データベース エンジン, のみ読み取りを実装することがなく Paradox ドライバーを使用して追加すると、ステートメントが許可されています。
