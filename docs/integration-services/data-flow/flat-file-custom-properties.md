---
title: フラット ファイルのカスタム プロパティ | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f2caeab-784c-4b0c-9b3e-6a88d1ccdbf9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 00387fee6a11d3a2416d8440fdb7ae35665c472b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292510"
---
# <a name="flat-file-custom-properties"></a>フラット ファイルのカスタム プロパティ

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **変換元のカスタム プロパティ**  
  
 フラット ファイル ソースには、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、フラット ファイル ソースのカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|[説明]|  
|-------------------|---------------|-----------------|  
|FileNameColumnName|String|ファイル名を格納する出力列の名前。 名前が指定されていない場合、ファイル名を格納する出力列は生成されません。<br /><br /> 注:このプロパティは、**フラット ファイル ソース エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
|RetainNulls|Boolean|データ変換のパイプライン エンジンによってデータが処理される際に、ソース ファイルの NULL 値を NULL 値として保持するかどうかを示す値。 このプロパティの既定値は **False**です。|  
  
 フラット ファイル ソースの出力には、カスタム プロパティがありません。  
  
 次の表は、フラット ファイル ソースの出力列のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|[説明]|  
|-------------------|---------------|-----------------|  
|FastParse|Boolean|列の解析に、DTS が提供するロケール非依存型の高速な解析ルーチンを使用するか、またはロケール依存型の標準的な解析ルーチンを使用するかを示す値。 詳細については、「 [Fast Parse](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) 」および「 [Standard Parse](https://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)」を参照してください。 このプロパティの既定値は **False**です。<br /><br /> 注:このプロパティは、**フラット ファイル ソース エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
  
 詳細については、「 [フラット ファイル ソース](../../integration-services/data-flow/flat-file-source.md)」を参照してください。  
  
 **変換先のカスタム プロパティ**  
  
 フラット ファイル変換先には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、フラット ファイル変換先のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|[説明]|  
|-------------------|---------------|-----------------|  
|[ヘッダー]|String|データが書き込まれる前にファイルに挿入される、テキストのブロック。<br /><br /> このプロパティの値は、プロパティ式を使用して指定することができます。|  
|Overwrite|Boolean|同じ名前の既存の変換先ファイルに対して、上書きまたは追加のどちらを実行するかを指定する値。 このプロパティの既定値は **True**です。|  
  
 フラット ファイル変換先の入力および入力列には、カスタム プロパティはありません。  
  
 詳細については、「 [フラット ファイル変換先](../../integration-services/data-flow/flat-file-destination.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
