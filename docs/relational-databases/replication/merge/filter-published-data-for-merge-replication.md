---
title: マージ レプリケーション用にパブリッシュされたデータのフィルター選択 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], filtering published data
- replication [SQL Server], filtering published data
ms.assetid: 46c5023d-7a3b-4455-becc-e159fcb5d6c4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1e0d157b6a4f7f08d068dc8da75c42f4ad924044
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033261"
---
# <a name="filter-published-data-for-merge-replication"></a>マージ レプリケーション用にパブリッシュされたデータのフィルター選択
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  他の種類のレプリケーションで定義できる静的行フィルターと列フィルター以外に、マージ レプリケーションでは、パラメーター化された行フィルターと結合フィルターが用意されています。 静的行フィルターと列フィルターの詳細については、「[パブリッシュされたデータのフィルター選択](../../../relational-databases/replication/publish/filter-published-data.md)」を参照してください。  
  
 マージ レプリケーションは、モバイル ユーザーをサポートする多くのアプリケーションで使用されています。これらのアプリケーションには通常、多数のサブスクリプションが含まれ、各サブスクリプションが一意のデータセットを受信します。 パラメーター化されたフィルターと結合フィルターを組み合わせることにより、管理者は 1 つのパブリケーション (多くても数個のパブリケーション) を設定するだけでさまざまなデータセットをユーザーに提供でき、複数のパブリケーションを作成することにより発生する管理オーバーヘッドを減らすことができます。  
  
-   パラメーター化されたフィルターを使用すると、複数のパブリケーションを作成しなくても、パーティションの異なるデータをそれぞれ対応するサブスクライバーに送信できます。 たとえば、テーブルをフィルターして、指定された営業担当者のデータをその担当者に対してのみレプリケートすることができます。 パラメーター化されたフィルターには、パフォーマンスを最適化し、データとアプリケーションの要件に最も適した結果が得られるようにフィルターを調整するための、さまざまなオプションがあります。 詳しくは、「 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」をご覧ください。  
  
-   結合フィルターは、通常、関連するテーブルに対するフィルターを拡張するために、パラメーター化されたフィルターと組み合わせて使用します (静的フィルターと組み合わせて使用することもできます)。 たとえば、営業担当者は、通常、顧客テーブルや注文テーブルなどの他のテーブルにデータを持っています。 このデータをフィルター選択することにより、営業担当者は、担当の顧客とその顧客の注文についてのデータのみを受信することができます。 詳細については、「 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)」を参照してください。  
  
 フィルターには、レプリケーションで行の識別に使用される **rowguidcol** を含めることはできません。 既定では、これはマージ レプリケーションのセットアップ時に追加される列であり、 **rowguid**という名前が付けられます。  
  
## <a name="see-also"></a>参照  
 [データとデータベース オブジェクトのパブリッシュ](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
