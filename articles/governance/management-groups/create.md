---
title: Créer des groupes d’administration pour organiser les ressources Azure
description: Découvrez comment créer des groupes d’administration Azure pour gérer plusieurs ressources.
author: rthorn17
manager: rithorn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/10/2018
ms.author: rithorn
ms.openlocfilehash: 6a45ffa13ead40b72fd1a0a3c2696a6e6829a4d5
ms.sourcegitcommit: 5c00e98c0d825f7005cb0f07d62052aff0bc0ca8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/24/2018
ms.locfileid: "49956406"
---
# <a name="create-management-groups-for-resource-organization-and-management"></a>Créer des groupes d’administration pour la gestion et l’organisation des ressources

Les groupes d’administration sont des conteneurs qui vous aident à gérer l’accès, la stratégie et la conformité dans plusieurs abonnements. Créez ces conteneurs pour construire une hiérarchie efficace utilisable avec [Azure Policy](../policy/overview.md) et les [contrôles d’accès en fonction du rôle Azure](../../role-based-access-control/overview.md). Pour plus d’informations sur les groupes d’administration, consultez [Organiser vos ressources avec des groupes d’administration Azure](overview.md).

La création du premier groupe d’administration dans l’annuaire peut nécessiter jusqu’à 15 minutes. En effet, des processus s’exécutent la première fois pour configurer le service des groupes d’administration dans Azure pour votre annuaire. Vous recevez une notification quand le processus est terminé.

## <a name="create-a-management-group"></a>Créer un groupe d’administration

Vous pouvez créer un groupe d’administration en utilisant le portail, PowerShell ou Azure CLI. Actuellement, vous ne pouvez pas utiliser les modèles Resource Manager pour créer des groupes d’administration.

### <a name="create-in-portal"></a>Créer dans le portail

1. Connectez-vous au [portail Azure](http://portal.azure.com).

1. Sélectionnez **Tous les services** > **Groupes d’administration**.

1. Dans la page principale, sélectionnez **Nouveau groupe d’administration**.

   ![Groupe principal](./media/main.png)

1. Renseignez le champ ID du groupe d’administration.

   - L’**ID du groupe d’administration** est l’identificateur unique de l’annuaire utilisé pour envoyer des commandes sur ce groupe d’administration. Cet identificateur n’est pas modifiable après sa création car il est utilisé dans tout le système Azure pour identifier ce groupe.
   - Le champ du nom d’affichage correspond au nom qui s’affiche dans le portail Azure. Un nom d’affichage distinct est un champ facultatif lors de la création du groupe d’administration. Il peut être modifié à tout moment.  

   ![Créer](./media/create_context_menu.png)  

1. Sélectionnez **Enregistrer**.

### <a name="create-in-powershell"></a>Créer dans PowerShell

Dans PowerShell, utilisez l’applet de commande New-AzureRmManagementGroup :

```azurepowershell-interactive
New-AzureRmManagementGroup -GroupName 'Contoso'
```

**GroupName** est un identificateur unique créé. Cet ID est utilisé par d’autres commandes pour faire référence à ce groupe et il ne peut pas être modifié ultérieurement.

Si vous voulez afficher un autre nom pour le groupe d’administration dans le portail Azure, ajoutez le paramètre **DisplayName** avec la chaîne. Par exemple, pour créer un groupe d’administration dont l’identificateur GroupName est Contoso et le nom d’affichage « Contoso Group », utilisez l’applet de commande suivante :

```azurepowershell-interactive
New-AzureRmManagementGroup -GroupName 'Contoso' -DisplayName 'Contoso Group' -ParentId 'ContosoTenant'
```

Utilisez le paramètre **ParentId** pour que ce groupe d’administration soit créé sous un autre groupe d’administration.

### <a name="create-in-azure-cli"></a>Créer dans Azure CLI

Dans Azure CLI, utilisez la commande az account management-group create.

```azurecli-interactive
az account management-group create --name 'Contoso'
```

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur les groupes d’administration, consultez :

- [Organiser vos ressources avec des groupes d’administration Azure](overview.md)
- [Guide pratique pour modifier, supprimer ou gérer vos groupes d’administration](manage.md)
- [Installer le module Azure PowerShell](https://www.powershellgallery.com/packages/AzureRM.ManagementGroups)
- [Passer en revue les spécifications de l’API REST](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/managementgroups/resource-manager/Microsoft.Management/preview)
- [Installer l’extension Azure CLI](/cli/azure/extension?view=azure-cli-latest#az-extension-list-available)
