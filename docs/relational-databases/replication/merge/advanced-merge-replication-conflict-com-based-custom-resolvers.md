---
title: COM ベースのカスタム競合回避モジュール | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- COM-based resolvers [SQL Server replication]
- custom resolvers [SQL Server replication]
ms.assetid: 94195797-ad7a-4962-a8e3-b259cd13aa38
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 96716d694a44003105190e287cfc7a4662924663
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033421"
---
# <a name="advanced-merge-replication-conflict---com-based-custom-resolvers"></a>マージ レプリケーションの競合の詳細 - COM ベースのカスタム競合回避モジュール
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  カスタム競合回避モジュールを使用すると、既定の解決メカニズムより高い柔軟性が得られ、レプリケートされたデータを使用するアプリケーションに必要なビジネス ロジックを実装できます。 COM ベースのカスタム競合回避モジュールは、 **ICustomResolver** COM インターフェイス、メソッドとプロパティ、および競合解決専用に設計されたその他のインターフェイスとデータ型定義を実装するダイナミック リンク ライブラリ (DLL) です。  
  
> [!NOTE]  
>  可能であれば、COM ベースのカスタム競合回避モジュールではなくビジネス ロジック ハンドラーを使用することをお勧めします。 ビジネス ロジック ハンドラーの詳細については、「[Execute Business Logic During Merge Synchronization](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)」 (マージ同期中のビジネス ロジックの実行) を参照してください。  
  
 カスタム COM 競合回避モジュールを作成する場合は、replrec.dll に含まれているタイプ ライブラリを使用できます。このライブラリは、既定では [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM にインストールされます。  
  
 カスタム COM 競合解決モジュールを記述する前に、以下のことを決定する必要があります。  
  
-   更新、挿入、削除など、解決する必要がある行の変更の種類、およびマージ変更のアップロード、ダウンロード、またはその両方で競合回避モジュールを呼び出すかどうか。 1 種類の変更、すべての変更、または各変更の組み合わせを指定できます。 既定のマージ競合回避モジュールでは、カスタム競合回避モジュールで対応しなかった競合が処理されます。  
  
-   競合の解決時に列レベルの追跡を使用するかどうか。 列レベルの追跡が有効になっている場合、競合が発生した列のデータに対してのみ競合のフラグが付けられ、それ以外の場合、データはマージされます。 しかし、競合の解決方法は行レベルの追跡の場合と同じです。競合で優先されるデータによって行全体が上書きされます。ただし、データは、パブリッシャー、サブスクライバー、またはそれ以外で変更された値が混合されている場合があります。 詳細については、「 [マージ レプリケーションの競合の検出および解決](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)」を参照してください。  
  
 COM ベースのカスタム競合回避モジュールを実装するには、「 [マージ アーティクルのカスタム競合回避モジュールの実装](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)」を参照してください。  
  
 カスタム競合回避モジュールは、パブリケーション全体ではなくアーティクルに対して指定されます。 複数のアーティクルで同じ競合回避モジュールを使用できますが、カスタム競合回避モジュールのロジックは特定のテーブル専用であるのが一般的です。 競合回避モジュールを作成した後に、アーティクルで使用されているテーブルが変更されると (競合解決に使用している列の名前が変更された場合など)、カスタム競合回避モジュールを変更して再コンパイルすることが必要な場合があります。  
  
 カスタム競合回避モジュールを指定するには、「 [マージ アーティクル競合回避モジュールの指定](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [マージ レプリケーションの競合検出および解決の詳細](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Microsoft COM ベースの競合回避モジュール](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)  
  
  
