---
title: アップデートグラムのガイドラインと制限事項 (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9eb717968b191bb7d80f5d68542178bf32734b00
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241297"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>XML アップデートグラムのガイドラインと制限 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML アップデートグラムを使用する場合は、次の点に注意してください。  
  
-   1組だけを持つ挿入操作のためのアップデートグラムを使用している場合は、>と** \<>** ブロックの後** \<に**、 ** \<>前**のブロックを省略できます。 逆に、削除操作の場合は、 ** \<after>** ブロックを省略できます。  
  
-   ** \<以前**に複数のアップデートグラムを使用していて、 ** \<同期>** タグで** \<>** ブロックを>している場合は、 ** \<>** ブロックの**前と\<>** のブロックの後の両方で、>と** \<>のペアの** ** \<前に**形成するように指定する必要があります。  
  
-   アップデートグラムの更新は、XML スキーマで提供される XML ビューに適用されます。 したがって、既定のマッピングが正しく行われるようにするには、アップデートグラムでスキーマ ファイル名を指定するか、ファイル名を指定しない場合は、要素名と属性名がデータベースのテーブル名と列名に一致している必要があります。  
  
-   SQLXML 4.0 を使用する場合、アップデートグラムのすべての列値は、子要素の XML ビューを構成するために提供される XDR スキーマまたは XSD スキーマで明示的にマップする必要があります。 この動作は、以前のバージョンの SQLXML とは異なります。これは、 **sql: relationship**注釈で外部キーの一部として暗黙的に指定されている場合に、スキーマでマップされていない列の値を許可します。 この変更は、子要素への主キー値の割り当てには影響しません。SQLXML 4.0 では、子要素に対して明示的に値が指定されていない場合でも、値が割り当てられます。  
  
-   アップデートグラムを使用してバイナリ列 ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **image**データ型など) のデータを変更する[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]場合は、データ型 (たとえば、 **sql: datatype = "image"**) と XML データ型 (たとえば、 **dt: type = "binhex"** や**dt: type = "binbase64**) を指定する必要があるマッピングスキーマを指定する必要があります。 アップデートグラムでバイナリ列のデータを指定する必要があります。マッピングスキーマで指定されている**sql: url エンコード**の注釈は、アップデートグラムによって無視されます。  
  
-   XSD スキーマを記述する場合、 **sql: relation**注釈または**sql: field**注釈に指定する値に、空白文字 (たとえば、"order details" テーブル名) などの特殊文字が含まれている場合は、この値を角かっこで囲む必要があります (たとえば、"[order details]")。  
  
-   アップデートグラムの使用で、チェーン リレーションシップはサポートされません。 たとえば、テーブル A とテーブル C が、テーブル B を使用するチェーン リレーションシップで関連付けられている場合は、アップデートグラムの実行時に次のエラーが発生します。  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     スキーマとアップデートグラムの両方が正しく、有効な形式であっても、チェーン リレーションシップが存在すると、このエラーが発生します。  
  
-   アップデートグラムでは、**イメージ**の種類のデータを更新中にパラメーターとして渡すことは許可されていません。  
  
-   **Text/ntext**および image のようなバイナリラージオブジェクト (BLOB) 型は、 ** \<** updategrams を使用する場合、の before>ブロックでは使用しないでください。これには、同時実行制御で使用するためのものが含まれます。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で、BLOB 型の比較の制限によって問題が発生する可能性があります。 たとえば、 **text**データ型の列を比較するには、WHERE 句で LIKE キーワードを使用します。ただし、データのサイズが8K を超える BLOB 型の場合、比較は失敗します。  
  
-   **Ntext**データ内の特殊文字は、BLOB 型の比較の制限により、SQLXML 4.0 で問題が発生する可能性があります。 たとえば、 ** \<>以前**のでは、 **ntext**型の列の同時実行制御チェックで使用されたときに "[Serializable]" を使用しているときに "[Serializable]" を使用すると、次の SQLOLEDB エラーの説明で失敗します。  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>参照  
 [SQLXML 4.0&#41;&#40;アップデートグラムのセキュリティに関する考慮事項](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
