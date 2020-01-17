---
title: 注釈付き XDR スキーマの XSD への変換 (SQLXML)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XDR schemas, converting schemas
- annotated XSD schemas, converting schemas
- XDR to XSD Converter tool [SQLXML]
- XDR schemas [SQLXML], converting
- converting annotated schemas
- mapping schema [SQLXML], conversions
- XSD schemas [SQLXML], converting schemas
ms.assetid: 151c94a8-66d3-4c46-a5ff-a22df456940a
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 10c85b4c4f2e08518703a67256bd169afb2d0455
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247074"
---
# <a name="converting-annotated-xdr-schemas-to-equivalent-xsd-schemas-sqlxml-40"></a>注釈付き XDR スキーマから同等の XSD スキーマへの変換 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML スキーマ定義 (XSD) 言語は、XML-Data Reduced (XDR) スキーマ定義言語に代わるものです。 
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 では XSD サポートが導入され、新しい注釈付きスキーマの作成には XSD を使用することになりました。 SQLXML 4.0 には XDR から XSD への変換ツールが用意されており、既存の注釈付き XDR スキーマを同等の XSD スキーマに簡単に変換できます。  
  
> [!IMPORTANT]  
>  このツールは、SQLXML 4.0 で、注釈付き XDR スキーマを XSD スキーマに変換する場合にのみ使用してください。 これは XDR を XSD に変換する汎用ツールではありません。 変換された XSD スキーマを別の環境で使用した場合、元の XDR スキーマと同じように動作しない可能性があります。  
  
 入力 XDR ファイルで XML 宣言内にエンコードが指定されている場合、このエンコードが、生成される XSD 出力ファイルのエンコードになります。  
  
 変換ツール (Cvtschema.exe) は Program Files\SQLXML 4.0\bin フォルダーにインストールされており、コマンド プロンプトから実行します。  
  
 一般的な構文は次のとおりです。  
  
```  
cvtschema XDRFileName, [-y], [-w] [-?]  
```  
  
 各値の説明:  
  
 XDRFileName  
 XSD に変換する XDR ファイルの名前を指定します。 このツールでは入力 XDR ファイルが読み取られ、現在の作業ディレクトリに XSD 出力ファイルが作成されます。 入力ファイルに拡張子 .xdr または .xml が付けられている場合、出力 XSD ファイルは同じ名前で拡張子が .xsd に変更されます。 入力ファイル名の拡張子が .xml または xdr 以外の場合 (または拡張機能がない場合)、出力ファイルは同じ名前で作成され、.xsd 拡張子が入力ファイル名に付加されます。 たとえば、入力 XDR ファイル名が SampleFile.abc の場合、出力される XSD ファイルは SampleFile.abc.xsd になります。  
  
 -y  
 (省略可) 既存の XSD ファイルを、変換ツールで生成される XSD ファイルで上書きします。 このフラグを指定しない場合は、既存の XSD ファイルを上書きするかどうかを確認するメッセージが表示され、このときに出力ファイル名を変更できます。  
  
 -w  
 (省略可) ツールによる変換処理で発生する、致命的でない警告を返します。 既定では、致命的なエラーだけが表示されます。  
  
 -?  
 説明と共に、 **cvtschema**で指定できるオプションの一覧を返します。  
  
## <a name="see-also"></a>参照  
 [XSD データ型から XPath データ型へのマッピング &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)   
 [&#40;SQLXML 4.0&#41;の XSD 注釈](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
  
  
