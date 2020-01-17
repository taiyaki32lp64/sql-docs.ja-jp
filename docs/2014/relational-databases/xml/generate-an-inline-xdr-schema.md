---
title: インライン XDR スキーマの生成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XDR schemas [SQL Server]
- inline XDR schema generation [SQL Server]
- XMLDATA option
- FOR XML clause, inline XDR schema generation
ms.assetid: 2a40d617-9724-4f7d-80a4-a85c702f14d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f93170d78512ba3c79e1dfa4b8e5e9aae83a4862
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205079"
---
# <a name="generate-an-inline-xdr-schema"></a>インライン XDR スキーマの生成
  FOR XML の **XMLDATA** ディレクティブは、クエリの結果と合わせてインライン XDR スキーマを返します。 ただし、XDR スキーマは、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンで導入された新しいデータ型や拡張のすべてをサポートしているわけではありません。 代わりに、 [XMLSCHEMA ディレクティブ](generate-an-inline-xsd-schema.md)を使用してインライン XSD スキーマを要求できます。  
  
> [!IMPORTANT]  
>  FOR XML オプションに対する XMLDATA ディレクティブは非推奨とされます。 RAW モードと AUTO モードの場合は、XSD 世代を使用してください。 EXPLICIT モードでは、XMLDATA ディレクティブに代わる機能はありません。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 また、インライン XDR スキーマのサポートについては、次の点にも注意してください。  
  
-   FOR XML クエリの結果に **xml** 型の列が含まれている場合にインライン XDR スキーマを要求すると、エラーが返されます。 インライン XDR は、xml 型をサポートしていません。  
  
-   **(n)varchar(max)** 型と **(n)varbinary(max)** 型は、それぞれ **(n)varchar(n)** 型と **varbinary(n)** 型にマップされます。  
  
-   互換性モードが 90 以上に設定されている場合、 **timestamp** 型の値は **varbinary(8)** 型のデータと見なされてバイナリ データとして扱われ、次のように結果が返されます。  
  
    -   **binary base64** が指定されている場合は、Base64 エンコード形式が使用されます。  
  
    -   **binary base64** が指定されていない場合、AUTO モードでは URL エンコード形式が使用されます。  
  
  
