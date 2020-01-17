---
title: XML アップデート グラム (SQLXML 4.0) のガイドラインと制限 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 953fc5b7c203faa8fa6a9820993a3d0fd7a7de40
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014828"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>XML アップデートグラムのガイドラインと制限 (SQLXML 4.0)
  XML アップデートグラムを使用する場合は、次の点に注意してください。  
  
-   1 つのペアのみを使用して、挿入操作のアップデート グラムを使用している場合 **\<する前に >** と **\<後 >** 、ブロック、 **\<する前に>** ブロックを省略できます。 逆に、削除操作が発生した場合、 **\<後 >** ブロックを省略できます。  
  
-   複数のアップデート グラムを使用している場合 **\<する前に >** と **\<後 >** 内のブロック、 **\<同期 >** 両方のタグ **\<する前に >** ブロックと **\<後 >** フォームにブロックを指定する必要があります **\<する前に >** と **\<後 >** ペア。  
  
-   アップデートグラムの更新は、XML スキーマで提供される XML ビューに適用されます。 したがって、既定のマッピングが正しく行われるようにするには、アップデートグラムでスキーマ ファイル名を指定するか、ファイル名を指定しない場合は、要素名と属性名がデータベースのテーブル名と列名に一致している必要があります。  
  
-   SQLXML 4.0 を使用する場合、アップデートグラムのすべての列値は、子要素の XML ビューを構成するために提供される XDR スキーマまたは XSD スキーマで明示的にマップする必要があります。 この動作は以前のバージョンの SQLXML とは異なります。以前のバージョンでは、`sql:relationship` 注釈で列の値が外部キーの一部として暗黙的に指定されていれば、スキーマでマップされない列値も許可されていました。 この変更は、子要素への主キー値の割り当てには影響しません。SQLXML 4.0 では、子要素に対して明示的に値が指定されていない場合でも、値が割り当てられます。  
  
-   バイナリ列のデータを変更するアップデート グラムを使用している場合 (など、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `image`データ型)、マッピング スキーマで指定する必要があります、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型 (たとえば、 `sql:datatype="image"`) と、XML データ型 (たとえば、 `dt:type="binhex"`または`dt:type="binbase64`) 指定する必要があります。 バイナリ列のデータは、アップデートグラム内に指定する必要があります。マッピング スキーマで指定される `sql:url-encode` 注釈は、アップデートグラムでは無視されます。  
  
-   XSD スキーマを記述するときに、`sql:relation` 注釈または `sql:field` 注釈に指定する値に特殊文字が含まれる場合、たとえば、スペースを含むテーブル名 "Order Details" を指定する場合などは、値を "[Order Details]" のように角かっこで囲む必要があります。  
  
-   アップデートグラムの使用で、チェーン リレーションシップはサポートされません。 たとえば、テーブル A とテーブル C が、テーブル B を使用するチェーン リレーションシップで関連付けられている場合は、アップデートグラムの実行時に次のエラーが発生します。  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     スキーマとアップデートグラムの両方が正しく、有効な形式であっても、チェーン リレーションシップが存在すると、このエラーが発生します。  
  
-   アップデートグラムでは、更新中に `image` 型データをパラメーターとして引き渡すことはできません。  
  
-   バイナリ ラージ オブジェクト (BLOB) のような種類`text/ntext`でイメージを使用する必要があります、 **\<する前に >** ので、同時実行制御で使用するためには、これは、アップデート グラムを使用する場合ブロックします。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で、BLOB 型の比較の制限によって問題が発生する可能性があります。 たとえば、`text` データ型の列を比較するには WHERE 句で LIKE キーワードを使用しますが、データ サイズが 8 KB を超える BLOB 型の場合、この比較は失敗します。  
  
-   `ntext` データで特殊文字を使用すると、BLOB 型の比較の制限によって、SQLXML 4.0 で問題が発生する可能性があります。 "[Serializable]"の使用など、 **\<する前に >** 同時実行制御の列のチェックで使用する場合は、アップデート グラムのブロック`ntext`型は、次の SQLOLEDB エラー説明の失敗します。  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>関連項目  
 [アップデート グラムのセキュリティに関する考慮事項&#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
