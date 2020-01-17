---
title: 注釈付き XDR スキーマから同等の XSD スキーマ (SQLXML 4.0) を変換する |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 7c09f9eff920c11f37f0fd173f6cd612aca6df6e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014536"
---
# <a name="converting-annotated-xdr-schemas-to-equivalent-xsd-schemas-sqlxml-40"></a>注釈付き XDR スキーマから同等の XSD スキーマへの変換 (SQLXML 4.0)
  XML スキーマ定義 (XSD) 言語は、XML-Data Reduced (XDR) スキーマ定義言語に代わるものです。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 では XSD サポートが導入され、新しい注釈付きスキーマの作成には XSD を使用することになりました。 SQLXML 4.0 には XDR から XSD への変換ツールが用意されており、既存の注釈付き XDR スキーマを同等の XSD スキーマに簡単に変換できます。  
  
> [!IMPORTANT]  
>  このツールは、SQLXML 4.0 で、注釈付き XDR スキーマを XSD スキーマに変換する場合にのみ使用してください。 これは XDR を XSD に変換する汎用ツールではありません。 変換された XSD スキーマを別の環境で使用した場合、元の XDR スキーマと同じように動作しない可能性があります。  
  
 入力 XDR ファイルで XML 宣言内にエンコードが指定されている場合、このエンコードが、生成される XSD 出力ファイルのエンコードになります。  
  
 変換ツール (Cvtschema.exe) は Program Files\SQLXML 4.0\bin フォルダーにインストールされており、コマンド プロンプトから実行します。  
  
 一般的な構文は次のとおりです。  
  
```  
cvtschema XDRFileName, [-y], [-w] [-?]  
```  
  
 各要素の説明は次のとおりです。  
  
 XDRFileName  
 XSD に変換する XDR ファイルの名前を指定します。 このツールでは入力 XDR ファイルが読み取られ、現在の作業ディレクトリに XSD 出力ファイルが作成されます。 入力ファイルに拡張子 .xdr または .xml が付けられている場合、出力 XSD ファイルは同じ名前で拡張子が .xsd に変更されます。 入力ファイルの拡張子が .xml または .xdr 以外の場合、または拡張子がない場合、出力ファイルは同じ名前で作成され、拡張子 .xsd が追加されます。 たとえば、入力 XDR ファイル名が SampleFile.abc の場合、出力される XSD ファイルは SampleFile.abc.xsd になります。  
  
 -y  
 (省略可) 既存の XSD ファイルを、変換ツールで生成される XSD ファイルで上書きします。 このフラグを指定しない場合は、既存の XSD ファイルを上書きするかどうかを確認するメッセージが表示され、このときに出力ファイル名を変更できます。  
  
 -w  
 (省略可) ツールによる変換処理で発生する、致命的でない警告を返します。 既定では、致命的なエラーだけが表示されます。  
  
 -?  
 `cvtschema` で指定できるオプションの一覧とその説明を返します。  
  
## <a name="see-also"></a>参照  
 [XSD データ型を XPath データ型にマッピング&#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-xpath-queries/xpath-data-types-sqlxml-4-0.md)   
 [XSD 注釈&#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
  
  
