---
title: どのような&#39;CLR 統合の新 |Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: clr
ms.topic: conceptual
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
ms.openlocfilehash: 8d37d476808f80cf132037542d17cb3de61eeccc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134874"
---
# <a name="clr-integration---what39s-new"></a>CLR 統合 - 何&#39;s New
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] の CLR 統合で新しくなった点は次のとおりです。  
  
-   CLR のバージョン 4 では、破損状態の例外を CLR データベース オブジェクトはキャッチしません。 これらの例外は、CLR 統合ホスト層でキャッチされるようになりました。 コード属性を設定して、CLR データベース コンポーネントによってこれらの例外がキャッチもできます ([\<legacyCorruptedStateExceptionsPolicy > 要素](https://go.microsoft.com/fwlink/?LinkId=204954))。 ただし、破損状態の例外が発生した場合の結果には信頼性がないため、この設定はお勧めできません。  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] には厳しいセキュリティ要件があるため、CLR データベース コンポーネントには、今後も CLR バージョン 2.0 で定義されたコード アクセス セキュリティ モデルが使用されます。  
  
-   CLR バージョン 4 の形式エラーで、 **System.TimeSpan**値が生成されます、 **System.FormatExceptions**します。 形式エラーは、CLR の version 4 より前、 **System.TimeSpan**値は無視されました。 CLR の version 4 より前の動作に依存するデータベース アプリケーションは、データベースの互換性レベルで実行する必要があります (**ALTER DATABASE 互換性レベル**) を 100 以下。 詳細については、次を参照してください。 [< TimeSpan_LegacyFormatMode > 要素](https://go.microsoft.com/fwlink/?LinkId=205109)します。  
  
-   CLR のバージョン 4 は、Unicode 5.1 をサポートします。 アクセントや記号を含んだ並べ替えの処理が改善されます。 従来の並べ替え動作に依存したアプリケーションでは、互換性の問題が生じる場合があります。 従来のデータベースの互換性レベルの並べ替え動作を有効にする (**ALTER DATABASE 互換性レベル**) を 100 以下に設定する必要があります。 この点をサポートするために、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] では、.NET Framework 4 ディレクトリ (C:\Windows\Microsoft.NET\Framework\v4.0.30319) に sort00001000.dll がインストールされます。 詳細については、次を参照してください。 [ \<CompatSortNLSVersion > 要素](https://go.microsoft.com/fwlink/?LinkId=205110)します。  
  
-   次の列が追加されている[sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md): **total_processor_time_ms**、 **total_allocated_memory_kb**、および**survived_memory_kb**します。  
  
  
