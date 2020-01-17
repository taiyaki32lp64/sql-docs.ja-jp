---
title: インデックス操作用のトランザクション ログのディスク領域 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index disk space [SQL Server]
- space [SQL Server], indexes
- transaction logs [SQL Server], disk space
- disk space [SQL Server], transaction logs
- space [SQL Server], transaction logs
ms.assetid: 4f8a4922-4507-4072-be67-c690528d5c3b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4af90d16e4e81b5d2ee1dc73de78826073d1cbff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909460"
---
# <a name="transaction-log-disk-space-for-index-operations"></a>インデックス操作用のトランザクション ログのディスク領域
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  大規模なインデックス操作では、大量のデータが読み込まれるためにトランザクション ログがすぐにいっぱいになることがあります。 インデックス操作を確実にロールバックできるようにするには、インデックス操作が完了するまでトランザクション ログを切り捨てることができません。ただし、インデックス操作中にログをバックアップすることはできます。 このため、トランザクション ログには、インデックス操作中のインデックス操作によるトランザクションと同時実行ユーザーによるトランザクションの両方を格納できるだけの十分な空き領域が必要です。 これは、インデックス操作がオフラインでもオンラインでも同じです。 オフライン インデックス操作中は基になるテーブルにアクセスできないので、ユーザー トランザクションはそれほど多くなく、ログの増大もそれほど速くない可能性があります。 オンライン インデックス操作では同時実行ユーザーによる操作を防ぐことができないので、大規模なオンライン インデックス操作で同時実行ユーザーによる膨大なトランザクションが発生すると、ログの切り捨てオプションが使用されずに、トランザクション ログが増大し続けることがあります。  
  
## <a name="recommendations"></a>推奨事項  
 大規模なインデックス操作を実行する場合は、次の推奨事項を考慮してください。  
  
1.  大規模なインデックス操作をオンラインで実行する前に、トランザクション ログを必ずバックアップし切り捨てを行います。また、予定しているインデックス トランザクションとユーザー トランザクションを格納できるだけの十分な領域をログのために用意しておきます。  
  
2.  インデックス操作の場合は、SORT_IN_TEMPDB オプションを ON に設定することを検討します。 この設定により、インデックス トランザクションが同時実行のユーザー トランザクションから分離されます。 インデックス トランザクションは、 **tempdb** データベースのトランザクション ログに格納され、同時実行ユーザー トランザクションはユーザー データベースのトランザクション ログに格納されます。 これにより、ユーザー データベースのトランザクション ログをインデックス操作中に必要に応じて切り捨てられるようになります。 さらに、 **tempdb** データベースのログとユーザー データベース ログを別のディスク上に格納すれば、2 つのログで同じディスク領域を奪い合うことはありません。  
  
    > [!NOTE]  
    >  **tempdb** データベースとトランザクション ログに、インデックス操作を処理できるだけの十分なディスク領域があることを確認してください。 インデックス操作が完了するまで、 **tempdb** データベースのトランザクション ログを切り捨てることはできません。  
  
3.  インデックス操作の最小ログ記録を行うことができるデータベース復旧モデルを使用します。 これにより、ログのサイズを削減し、ログでログ領域がいっぱいになるのを防ぐことができます。  
  
4.  明示的なトランザクションではオンライン インデックス操作を実行しないでください。 ログの切り捨ては、明示的なトランザクションが終了するまで行われません。  
  
## <a name="related-content"></a>関連コンテンツ  
 [インデックス DDL 操作に必要なディスク領域](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [インデックスのディスク領域の例](../../relational-databases/indexes/index-disk-space-example.md)  
  
  
