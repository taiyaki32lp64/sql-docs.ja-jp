---
title: インライン ワークロードを使用した XML 入力ファイルのサンプル (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: 7c04fe1d-6669-44a1-8b73-36d469e9b002
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b1b53076a7528d0e9eaff1244c206dee4127150e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63063138"
---
# <a name="xml-input-file-sample-with-inline-workload-dta"></a>インライン ワークロードを使用した XML 入力ファイルのサンプル (DTA)
  この XML 入力ファイルのサンプルでは、ワークロードを **EventString** 要素を使用して指定しています。このサンプルをコピーして、お使いの XML エディターやテキスト エディターに貼り付けてください。 個別のワークロード ファイルを使用する代わりに、 **EventString** 要素を使用して XML 入力ファイル内の [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト ワークロードを指定することができます。 このサンプルを編集ツールにコピーした後に、 **Server**、 **Database**、 **Schema**、 **Table**、 **Workload**、 **EventString**、および **TuningOptions** 要素で指定する値を、特定のチューニング セッションの値に置き換えてください。 これらの要素で使用できるすべての属性および子要素の詳細については、「[XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)」を参照してください。 以下のサンプルでは、使用できる属性や子要素の一部だけを使用しています。  
  
## <a name="code"></a>コード  
 [!code-xml[InputFileSamples#InlineWorkloadInputFile](../../snippets/xml/SQL14/dta_xml/inputfilesamples/xml/dta_xml_input_file_samples.xml#inlineworkloadinputfile)]  
  
## <a name="comments"></a>コメント  
 `USE database_name` ステートメントは、 **EventString** 要素に含まれるインライン ワークロードで指定できます。  
  
## <a name="see-also"></a>参照  
 [データベース エンジン チューニング アドバイザーの起動および使用](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [データベース エンジン チューニング アドバイザーからの出力の表示および操作](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
