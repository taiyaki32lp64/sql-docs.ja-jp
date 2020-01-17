---
ms.openlocfilehash: 497a564a10a3d35b33f47222fce8f89fe36bd15e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73530924"
---
サーバー設定のインスタンス レベルでの構成、またはデータベースの可用性グループへの手動での追加などの一部の操作は、SQL Server インスタンスへの接続が必要です。 可用性グループに属するデータベース内での `sp_configure`、`RESTORE DATABASE`、または DDL コマンドのような操作は、SQL Server インスタンスへの接続が必要です。 既定では、ビッグ データ クラスターには、インスタンスへの接続を有効にするエンドポイントが含まれません。 このエンドポイントは、手動で公開する必要があります。

手順については、[プライマリ レプリカのデータベースへの接続](../big-data-cluster/deployment-high-availability.md#instance-connect)に関するページを参照してください。