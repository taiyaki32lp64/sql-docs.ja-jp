---
title: "SQLSTATEs |Microsoft ドキュメント"
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
- diagnostic information [ODBC], sqlstates
- SQLSTATE [ODBC]
ms.assetid: f29fff2e-3d09-4a8c-a2f9-2059062cbebf
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0c99959fac35ac1cd312ab3d434f607c3f256dd8
ms.contentlocale: ja-jp
ms.lasthandoff: 09/09/2017

---
# <a name="sqlstates"></a>SQLSTATEs
SQLSTATEs では、警告またはエラーの原因に関する詳細情報を提供します。 このマニュアルで SQLSTATEs は、IM で始まるそれら SQLSTATEs ODBC に固有のですが、ISO/IEF CLI 仕様に含まれる場合に基づいています。  
  
 異なりリターン コードは、このマニュアルで SQLSTATEs ガイドラインについては、ドライバーを取得する必要はありません。 そのため、ドライバーは、エラーまたは警告が検出される適切な SQLSTATE を返す必要があります、中にアプリケーションする必要がありますはカウントされませんでこの常に発生しています。 この状況の理由は、2 つあります。  
  
-   **生み出しました**ドライバーの実装を変更して、あまり; には完了せず、おそらくになりますが、このマニュアルは、多数のエラー、警告、およびそれらのエラーと警告の考えられる原因を示します。 特定のドライバーはすべておそらくは返されませんすべて、SQLSTATEs のこのマニュアルに一覧表示され、このマニュアルに記載いない SQLSTATEs を返す場合があります。  
  
-   **複雑さ**データベース エンジンの一部、特にリレーショナル データベース エンジン — 数千のエラーと警告を返します。 このようなエンジン用のドライバーは、これらすべてのエラーにマップする可能性が低いと労力が SQLSTATEs する警告は、関連のマッピングの inexactness、大きなサイズの結果のコードと結果のコードは、多くの場合、プログラミングを返しますの値が低い実行時に発生する必要がありますしないエラー。 そのため、ドライバーは、多くのエラーをマップする必要があります、警告と必然的になり、これらのエラーとするアプリケーション ロジックに警告をマップすることを確認してある場合があります基づく、SQLSTATE 01004 (データが切り捨てられました) など。  
  
 SQLSTATEs が確実に返されないためほとんどのアプリケーションを表示するだけに、関連付けられている診断メッセージは多くの場合、レポートに特定のエラーまたは警告が発生しましたが、と共に、ユーザーとネイティブ エラー コードにします。 まれに、この機能を低下があるため、アプリケーションはほとんど SQLSTATEs にプログラミング ロジックをまま基本ことはできません。 たとえば、 **SQLExecDirect** SQLSTATE 42000 (構文エラーまたはアクセス違反) を返します。 ハードコーディングまたはアプリケーションでビルドされた SQL ステートメントをこのエラーの原因となったは、これは、プログラミング エラーと、コードを修正する必要があります。 場合は、ユーザーが SQL ステートメントを入力すると、これは、ユーザー エラーおよび問題のユーザーに通知するで考えられるは、アプリケーションが行われました。  
  
 アプリケーションは基にプログラミング ロジック SQLSTATEs、ときにが返される SQLSTATE または返されるさまざまな SQLSTATE、準備する必要があります。 SQLSTATEs は確実に、返される正確には、多数のドライバーの使用経験のみに基づいていることができます。 ただし、一般的なガイドラインでは、ドライバーまたはデータ ソースではなく、ドライバー マネージャーで発生したエラーの SQLSTATEs が確実に返される可能性が高くなります。 たとえば、ほとんどのドライバーは、SQLSTATE HYC00 可能性を返す (省略可能な機能で実装されていません)、少なくドライバー SQLSTATE 42021 を返す可能性があります (既に列が存在する)。  
  
 次の SQLSTATEs は実行時エラーまたは警告を示す、プログラミング ロジックを基になる適切な候補です。 ただし、すべてのドライバーを返すことの保証はありません。  
  
-   01004 (データが切り捨てられました)  
  
-   01S02 (オプションの値が変更されました)  
  
-   HY008 (操作がキャンセルされました)  
  
-   HYC00 (省略可能な機能が実装されていません)  
  
-   HYT00 (タイムアウトになりました)  
  
 SQLSTATE HYC00 (省略可能な機能が実装されていません) は、ドライバーが特定のステートメントまたは接続属性をサポートしているかどうか、アプリケーションを判別する唯一の方法であるため特に重要です。  
  
 SQLSTATEs であり、どのような機能を返すことの完全な一覧を参照してください。[付録 a: ODBC エラー コード](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)です。 各関数を特定の SQLSTATE を返す場合がありますの条件の詳細については、その関数を参照してください。