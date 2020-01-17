---
title: コメント (MDX 構文) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1ffcb57a48c7d6e265daa786912cfd37f0b43754
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001529"
---
# <a name="comments-mdx-syntax"></a>コメント (MDX 構文)


  コメントは、実行中でないプログラム コード内のテキスト文字列。 (コメントは "注釈" とも呼ばれます)。 ドキュメントのコードのコメントを使用してまたは多次元式 (MDX) ステートメントおよびスクリプトの診断中の部分を一時的に無効にできます。 コードを説明するコメントを使用すると、簡単に後でプログラム コードの保守します。 また、プログラム名、作成者名、およびコードの主要な変更日を記録するためにコメントを使用する場合も少なくありません。 複雑な計算を記述したり、プログラミング方法を説明するコメントを使用することもできます。  
  
 MDX のコメントでは、次のガイドラインに従います。  
  
-   すべての文字の英数字と記号がコメント内で使用できます。  コメント内のすべての文字は無視されます。  
  
-   ステートメント内またはスクリプト内のコメント長には制限がありません。 1 行または複数行のコメントを作成できます。  
  
 MDX は、次の 3 つの種類のコメント文字をサポートしています。  
  
 // (二重スラッシュ)  
 このコメント文字は、単独で実行するコードと同じ行または行に使用できます。 すべての行の末尾に二重スラッシュからは、コメントの一部です。 複数行にコメントを記述する場合は、二重スラッシュは、それぞれのコメント行の先頭に表示する必要があります。 詳細については、次を参照してください。 [&#40;コメント&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md)します。  
  
 -- (二重ハイフン)  
 このコメント文字は、単独で実行するコードと同じ行または行に使用できます。 すべての行の末尾に二重ハイフンの後ろからは、コメントの一部です。 複数行にわたってコメントを記述する場合、それぞれのコメント行の先頭に二重ハイフンを入力する必要があります。 詳細については、次を参照してください。 [--&#40;コメント&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)します。  
  
 /* ...\*/(スラッシュとアスタリスク文字のペア)  
 このコメント文字では、実行コードと同じ行にコメントを記述できるほか、コメント専用の行にすることもできます。さらに、実行可能コード内でもこのコメント文字を使用できます。 コメント開始記号からのすべてのもの (/\*) にコメント終了記号 (\*/)、コメントの一部と見なされます。 複数行コメント、コメント文字のペアの (/\*)、コメント、および閉じるコメント文字のペアを開始する必要があります (\*/)、コメントを終了する必要があります。 コメント行ではそれ以外のコメント文字を使用できません。 詳細については、次を参照してください[/*...\*/ (Comment)](../mdx/comment-mdx.md).  
  
## <a name="example"></a>例  
 次のクエリでは、3 種類すべてのコメントの例を示します。  
  
 `//An example of a comment using the double-forward slash`  
  
 `--An example of a comment using the double-hypen`  
  
 `/*An example of a`  
  
 `multi-line`  
  
 `comment*/`  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>関連項目  
 [MDX 構文の要素&#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
