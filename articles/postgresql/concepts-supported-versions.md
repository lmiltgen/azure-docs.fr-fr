---
title: Versions prises en charge dans Azure Database pour PostgreSQL
description: Décrit les versions prises en charge des bases de données Azure pour PostgreSQL.
services: postgresql
author: rachel-msft
ms.author: raagyema
manager: kfile
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 11/12/2018
ms.openlocfilehash: 04e47e15206e22e7965121c6c277e4032ea04ddf
ms.sourcegitcommit: 1f9e1c563245f2a6dcc40ff398d20510dd88fd92
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51621052"
---
# <a name="supported-postgresql-database-versions"></a>Versions prises en charge de la base de données PostgreSQL
Microsoft entend prendre en charge les versions n-2 du moteur PostgreSQL dans le service Azure Database pour PostgreSQL : Autrement dit, la version principale actuellement publiée (n) et les deux principales versions antérieures (-2).

La base de données Azure pour PostgreSQL prend actuellement en charge les versions suivantes :

## <a name="postgresql-version-105"></a>PostgreSQL Version 10.5
Consultez la [documentation PostgreSQL](https://www.postgresql.org/docs/10/static/release-10-5.html) pour en savoir plus sur les améliorations et les correctifs de cette version mineure.

## <a name="postgresql-version-9610"></a>PostgreSQL Version 9.6.10
Consultez la [documentation PostgreSQL](https://www.postgresql.org/docs/9.6/static/release-9-6-10.html) pour en savoir plus sur les améliorations et les correctifs de cette version mineure.

## <a name="postgresql-version-9514"></a>PostgreSQL Version 9.5.14
Consultez la [documentation PostgreSQL](https://www.postgresql.org/docs/9.5/static/release-9-5-14.html) pour en savoir plus sur les améliorations et les correctifs de cette version mineure.

## <a name="managing-updates-and-upgrades"></a>Gestion des mises à jour et des mises à niveau
Azure Database pour PostgreSQL gère automatiquement les correctifs pour les versions mineures. Actuellement, la mise à niveau de version principale n’est pas prise en charge. Par exemple, la mise à niveau de PostgreSQL 9.5 à PostgreSQL 9.6 n’est pas prise en charge. Si vous souhaitez mettre à niveau vers la version principale suivante, effectuez une [sauvegarde et une restauration](./howto-migrate-using-dump-and-restore.md) vers un serveur créé avec la nouvelle version du moteur.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la prise en charge des différentes extensions PostgreSQL, consultez [Extensions PostgreSQL](concepts-extensions.md).
