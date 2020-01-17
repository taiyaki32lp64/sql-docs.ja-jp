---
title: インライン XDR スキーマの生成 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 2e738002850c372642413c3ffb0b829f899d4060
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943202"
---
# <a name="generate-an-inline-xdr-schema"></a>インライン XDR スキーマの生成
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  FOR XML の **XMLDATA** ディレクティブは、クエリの結果と合わせてインライン XDR スキーマを返します。 ただし、XDR スキーマは、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンで導入された新しいデータ型や拡張のすべてをサポートしているわけではありません。 代わりに、 [XMLSCHEMA ディレクティブ](../../relational-databases/xml/generate-an-inline-xsd-schema.md)を使用してインライン XSD スキーマを要求できます。  
  
> [!IMPORTANT]  
>  FOR XML オプションに対する XMLDATA ディレクティブは非推奨とされます。 RAW モードと AUTO モードの場合は、XSD 世代を使用してください。 EXPLICIT モードでは、XMLDATA ディレクティブに代わる機能はありません。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 また、インライン XDR スキーマのサポートについては、次の点にも注意してください。  
  
-   FOR XML クエリの結果に **xml** 型の列が含まれている場合にインライン XDR スキーマを要求すると、エラーが返されます。 インライン XDR は、xml 型をサポートしていません。  
  
-   **(n)varchar(max)** 型と **(n)varbinary(max)** 型は、それぞれ **(n)varchar(n)** 型と **varbinary(n)** 型にマップされます。  
  
-   互換性モードが 90 以上に設定されている場合、 **timestamp** 型の値は **varbinary(8)** 型のデータと見なされてバイナリ データとして扱われ、次のように結果が返されます。  
  
    -   **binary base64** が指定されている場合は、Base64 エンコード形式が使用されます。  
  
    -   **binary base64** が指定されていない場合、AUTO モードでは URL エンコード形式が使用されます。  
  
  
