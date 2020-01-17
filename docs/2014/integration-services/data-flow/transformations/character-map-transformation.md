---
title: 文字マップ変換 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.charactertrans.f1
helpviewer_keywords:
- mutually exclusive mapping [Integration Services]
- mapping data [Integration Services]
- string functions
- Character Map transformation [Integration Services]
ms.assetid: e0f50eb6-b893-400f-bb8c-fb3072cc2620
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d00f864d5e7209bc0865bfbb52bd1231a2c12a9c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770422"
---
# <a name="character-map-transformation"></a>文字マップ変換
  文字マップ変換は、小文字から大文字への変換関数などの文字列関数を、文字データに適用します。 この変換は、文字列データ型の列データにのみ実行されます。  
  
 文字マップ変換では、列データを適切に変換したり、変換出力に列を追加して、変換後のデータを新しい列に挿入したりできます。 また、さまざまなマップ操作のセットを同じ入力列に適用し、その結果を別の列に格納できます。 たとえば、同じ列を大文字と小文字に変換し、その結果を 2 つの異なる列に格納できます。  
  
 状況によっては、マップによってデータが切り捨てられる場合があります。 たとえば、1 バイト文字をマルチバイトで表記される文字にマップした場合、切り捨てが発生することがあります。 文字マップ変換には 1 つのエラー出力が含まれます。このエラー出力を使用すると、切り捨てられたデータを別の出力に送ることができます。 詳しくは、「 [データのエラー処理](../error-handling-in-data.md)」をご覧ください。  
  
 この変換は、1 つの入力、1 つの出力、および 1 つのエラー出力をとります。  
  
## <a name="mapping-operations"></a>マップ操作  
 次の表では、文字マップ変換がサポートするマップ操作について説明します。  
  
|操作|説明|  
|---------------|-----------------|  
|バイトの反転|バイト順を反転します。|  
|全角|半角文字を全角文字にマップします。|  
|半角|全角文字を半角文字にマップします。|  
|ひらがな|カタカナをひらがなにマップします。|  
|カタカナ|ひらがなをカタカナにマップします。|  
|言語の文字種|システム規則ではなく言語の文字種を適用します。 言語の文字種は、Win32 API が提供する、チュルク語や他のロケールの Unicode 単純文字種のマップに関する機能を基準とします。|  
|小文字|文字を小文字に変換します。|  
|簡体中国語|繁体中国語文字を簡体中国語文字にマップします。|  
|繁体字中国語|簡体中国語文字を繁体中国語文字にマップします。|  
|大文字|文字を大文字に変換します。|  
  
## <a name="mutually-exclusive-mapping-operations"></a>相互に排他的なマップ操作  
 変換では、複数の操作を実行できます。 ただし、一部のマップ操作は相互に排他的です。 次の表に、同じ行に対して複数の操作を行う場合に適用される制限の一覧を示します。 操作 A 列と操作 B 列の操作は、相互に排他的です。  
  
|操作 A|操作 B|  
|-----------------|-----------------|  
|小文字|大文字|  
|ひらがな|カタカナ|  
|半角|全角|  
|繁体字中国語|簡体中国語|  
|小文字|ひらがな、カタカナ、半角、全角|  
|大文字|ひらがな、カタカナ、半角、全角|  
  
## <a name="configuration-of-the-character-map-transformation"></a>文字マップ変換の構成  
 文字マップ変換は、次の方法で構成できます。  
  
-   変換する列を指定します。  
  
-   各列に適用する操作を指定します。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[文字マップ変換エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、「 [文字マップ変換エディター](../../character-map-transformation-editor.md)」をご覧ください。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [共通プロパティ](../../common-properties.md)  
  
-   [変換のカスタム プロパティ](transformation-custom-properties.md)  
  
 プロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [データ フロー コンポーネントのプロパティを設定する](../set-the-properties-of-a-data-flow-component.md)  
  
-   [マージ変換およびマージ結合変換用にデータを並べ替える](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
  
