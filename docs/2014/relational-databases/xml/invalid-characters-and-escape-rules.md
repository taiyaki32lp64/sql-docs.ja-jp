---
title: 無効な文字とエスケープの規則 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, invalid characters
- FOR XML clause, escape rules
ms.assetid: f2e9b997-f400-4963-b225-59d46c6b93e8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aafacefa7a5bab5f8bc828f48384a79e17a13b11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63241197"
---
# <a name="invalid-characters-and-escape-rules"></a>無効な文字とエスケープの規則
  このトピックでは、無効な XML 文字が FOR XML 句でどのように処理されるのかを説明し、XML 名では無効になる文字のエスケープの規則を示します。  
  
## <a name="for-xml-and-invalid-characters"></a>For XML と無効な文字  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、無効な XML 文字が TYPE ディレクティブの指定されていない FOR XML クエリの結果として返される場合、これらの文字をエンティティに変換します。  
  
 XML 1.0 準拠のパーサーは、これらの文字がエンティティであるかどうかにかかわらず解析エラーを返しますが、エンティティで表現すると XML 1.1 への準拠度が高くなります。 エンティティによる表現は、XML 標準の今後のバージョンでも推奨されると考えられます。 また、コード内で無効な文字を検出しやすくなるため、デバッグが容易になります。  
  
 XML ツールを使用している場合は、データ ストリーム中で無効な文字が見つかった場合は、どのような場合でも XML パーサーは失敗するので、対処する必要はありません。 XML 以外のツールを使用している場合は、エンティティとして表現すべき文字を検索するようにプログラミング ロジックを変更する必要が生じる可能性があります。  
  
 FOR XML クエリ内の以下の空白文字が情報のやり取りの間に失われないようにするため、異なるエンティティに変換されます。  
  
-   要素のコンテンツおよび属性内: **hex(0D)** (キャリッジ リターン)  
  
-   属性のコンテンツ内: **hex(09)** (タブ)、 **hex(0A)** (ライン フィード)  
  
 これらの文字は出力に保持され、パーサーはこれらの文字を正規化しません。  
  
## <a name="escape-rules"></a>エスケープの規則  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前にスペースなどの XML では無効になる文字が含まれている場合、この名前は、無効な文字がエスケープ数値エンティティ エンコードに変換された XML 名に変換されます。  
  
 英字以外で XML 名に使用できる文字は、コロン (:) と下線 (_) の 2 つだけです。 コロンは既に名前空間用に予約されているので、エスケープ文字としてはアンダースコアが使われます。 エンコードに使用されるエスケープの規則は、次のとおりです。  
  
-   有効な XML 名の文字ではない UCS-2 文字は、XML 1.0 の仕様に従って、_xHHHH\_としてエスケープされます。 この HHHH は、その文字の 4 桁の 16 進数 UCS-2 コードを最上位ビットから順に表しています。 たとえば、テーブル名 **Order Details** は、Order_x0020_Details のようにエンコードされます。  
  
-   UCS-2 領域に適合しない文字 (U+00010000 ～ U+0010FFFF の範囲の UCS-4 追加分) は、_xHHHHHHHH\_のようにエンコードされます。 SQL Server 2000 以前の下位互換性モードで実行されている場合、この HHHHHHHH は、その文字の 8 桁の 16 進数 UCS-4 エンコードを表します。 それ以外の場合は、ISO 標準に合わせ、文字は _xHHHHHH\_の形式でエンコードされます。  
  
-   アンダースコア文字は、その後に文字 x が続いていない場合はエスケープする必要はありません。 たとえば、テーブル名 **Order_Details** はエンコードされません。  
  
-   識別子内のコロン (:) 文字はエスケープされません。このため、FOR XML クエリで名前空間の要素と属性名を生成できます。 たとえば、次のクエリでは名前にコロンが含まれる名前空間属性が生成されます。  
  
    ```  
    SELECT 'namespace-urn' as 'xmlns:namespace',   
     1 as 'namespace:a'   
    FOR XML RAW  
    ```  
  
     クエリの結果は以下のとおりです。  
  
    ```  
    <row xmlns:namespace="namespace-urn" namespace:a="1"/>  
    ```  
  
     XML 名前空間を追加する場合は、WITH XMLNAMESPACES を使用することをお勧めします。  
  
## <a name="see-also"></a>参照  
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
