---
title: Avant de déployer App Service sur Azure Stack | Microsoft Docs
description: Étapes à effectuer avant de déployer App Service sur Azure Stack
services: azure-stack
documentationcenter: ''
author: apwestgarth
manager: stefsch
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2018
ms.author: anwestg
ms.openlocfilehash: 4f669d44582c47cc6c7c090627f957288fee0f1a
ms.sourcegitcommit: b62f138cc477d2bd7e658488aff8e9a5dd24d577
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51615872"
---
# <a name="before-you-get-started-with-app-service-on-azure-stack"></a>Avant de commencer avec App Service sur Azure Stack

*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*

Avant de déployer Azure App Service sur Azure Stack, vous devez effectuer les étapes de prérequis décrites dans cet article.

> [!IMPORTANT]
> Appliquez la mise à jour 1809 à votre système intégré Azure Stack ou déployez le dernier Kit de développement Azure Stack (ASDK) avant de déployer Azure App Service 1.4.

## <a name="download-the-installer-and-helper-scripts"></a>Téléchargez le programme d’installation et les scripts d’assistance

1. Téléchargez les [scripts d’assistance au déploiement App Service sur Azure Stack](https://aka.ms/appsvconmashelpers).
2. Téléchargez le [programme d’installation d’App Service sur Azure Stack](https://aka.ms/appsvconmasinstaller).
3. Extrayez les fichiers à partir du fichier zip des scripts d’assistance. Les fichiers et dossiers suivants sont extraits :

   - Common.ps1
   - Create-AADIdentityApp.ps1
   - Create-ADFSIdentityApp.ps1
   - Create-AppServiceCerts.ps1
   - Get-AzureStackRootCert.ps1
   - Remove-AppService.ps1
   - Dossier Modules
     - GraphAPI.psm1

## <a name="syndicate-the-custom-script-extension-from-the-marketplace"></a>Syndiquez l’extension de script personnalisé à partir d’Azure Marketplace

Azure App Service sur Azure Stack nécessite la version 1.9.0 de l’extension de script personnalisé.  Vous devez [syndiquer l’extension à partir d’Azure Marketplace](https://docs.microsoft.com/azure/azure-stack/azure-stack-download-azure-marketplace-item) avant de commencer le déploiement ou la mise à niveau d’Azure App Service sur Azure Stack

## <a name="high-availability"></a>Haute disponibilité

La mise à jour 1802 d’Azure Stack prend en charge les domaines d’erreur. Les nouveaux déploiements d’Azure App Service sur Azure Stack sont distribués sur différents domaines d’erreur et assurent une tolérance de panne.

Pour les déploiements existants d’Azure App Service sur Azure Stack, qui ont été effectués avant la mise à jour 1802, consultez l’article [Rééquilibrer un fournisseur de ressources App Service sur les domaines d’erreur](azure-stack-app-service-fault-domain-update.md).

En outre, déployez le serveur de fichiers requis et les instances de SQL Server dans une configuration hautement disponible.

## <a name="get-certificates"></a>Obtenir des certificats

### <a name="azure-resource-manager-root-certificate-for-azure-stack"></a>Certificat racine Azure Resource Manager pour Azure Stack

Ouvrez une session PowerShell avec élévation de privilèges sur un ordinateur qui peut atteindre le point de terminaison privilégié sur le système intégré Azure Stack ou l’hôte du Kit de développement Azure Stack.

Exécutez le script *Get-AzureStackRootCert.ps1* à partir du dossier où vous avez extrait les scripts d’assistance. Le script crée un certificat racine dans le même dossier que le script dont App Service a besoin pour créer des certificats.

Lorsque vous exécutez la commande PowerShell suivante, vous devez fournir le point de terminaison privilégié et les informations d’identification du compte AzureStack\CloudAdmin.

```PowerShell
    Get-AzureStackRootCert.ps1
```

#### <a name="get-azurestackrootcertps1-script-parameters"></a>Paramètres du script Get-AzureStackRootCert.ps1

| Paramètre | Obligatoire ou facultatif | Valeur par défaut | Description |
| --- | --- | --- | --- |
| PrivilegedEndpoint | Obligatoire | AzS-ERCS01 | Point de terminaison privilégié |
| CloudAdminCredential | Obligatoire | AzureStack\CloudAdmin | Informations d’identification du compte de domaine pour les administrateurs cloud d’Azure Stack |

### <a name="certificates-required-for-asdk-deployment-of-azure-app-service"></a>Certificats requis pour le déploiement ASDK d’Azure App Service

Le script *Create-AppServiceCerts.ps1* fonctionne avec l’autorité de certification Azure Stack pour créer les quatre certificats dont App Service a besoin.

| Nom de fichier | Utilisation |
| --- | --- |
| _.appservice.local.azurestack.external.pfx | Certificat SSL par défaut d’App Service |
| api.appservice.local.azurestack.external.pfx | Certificat SSL de l’API App Service |
| ftp.appservice.local.azurestack.external.pfx | Certificat SSL d’App Service Publisher |
| sso.appservice.local.azurestack.external.pfx | Certificat d’application d’identité App Service |

Pour créer les certificats, suivez les étapes ci-dessous :

1. Connectez-vous à l’hôte du Kit de développement Azure Stack en utilisant le compte AzureStack\AzureStackAdmin.
2. Ouvrez une session PowerShell avec élévation de privilèges.
3. Exécutez le script *Create-AppServiceCerts.ps1* à partir du dossier où vous avez extrait les scripts d’assistance. Ce script crée quatre certificats dans le même dossier que le script dont App Service a besoin pour créer des certificats.
4. Entrez un mot de passe pour sécuriser les fichiers .pfx et prenez-en note. Vous devez l’entrer dans le programme d’installation App Service sur Azure Stack.

#### <a name="create-appservicecertsps1-script-parameters"></a>Paramètres du script Create-AppServiceCerts.ps1

| Paramètre | Obligatoire ou facultatif | Valeur par défaut | Description |
| --- | --- | --- | --- |
| pfxPassword | Obligatoire | Null | Mot de passe pour aider à protéger la clé privée du certificat |
| DomainName | Obligatoire | local.azurestack.external | Suffixe de la région et du domaine Azure Stack |

### <a name="certificates-required-for-azure-stack-production-deployment-of-azure-app-service"></a>Certificats requis pour un déploiement de production Azure Stack d’Azure App Service

Pour exécuter le fournisseur de ressources en production, vous devez fournir les certificats suivants :

- Certificat de domaine par défaut
- Certificat d’API
- Certificat de publication
- Certificat d’identité

#### <a name="default-domain-certificate"></a>Certificat de domaine par défaut

Le certificat de domaine par défaut est placé sur le rôle de serveur frontal. Les applications utilisateur pour une demande de domaine par défaut ou de caractères génériques à Azure App Service utilisent ce certificat. Le certificat est également utilisé pour les opérations de contrôle de code source (Kudu).

Le certificat doit être un certificat générique à trois sujets au format .pfx. Cette exigence permet à un seul certificat de couvrir à la fois au domaine par défaut et au point de terminaison SCM pour les opérations de contrôle de code source.

| Format | Exemples |
| --- | --- |
| \*.appservice.\<region\>.\<DomainName\>.\<extension\> | \*.appservice.redmond.azurestack.external |
| \*.scm.appservice.<region>.<DomainName>.<extension> | \*.scm.appservice.redmond.azurestack.external |
| \*.sso.appservice.<region>.<DomainName>.<extension> | \*.sso.appservice.redmond.azurestack.external |

#### <a name="api-certificate"></a>Certificat d’API

Le certificat de l’API est placé sur le rôle de gestion. Le fournisseur de ressources l’utilise pour aider à sécuriser les appels d’API. Le certificat de publication doit contenir un objet qui correspond à l’entrée DNS de l’API.

| Format | Exemples |
| --- | --- |
| api.appservice.\<région\>.\<nom_domaine\>.\<extension\> | api.appservice.redmond.azurestack.external |

#### <a name="publishing-certificate"></a>Certificat de publication

Le certificat du rôle de serveur de publication sécurise le trafic FTPS des propriétaires d’applications lorsqu’ils chargent du contenu. Le certificat de publication doit contenir un objet qui correspond à l’entrée DNS FTPS.

| Format | Exemples |
| --- | --- |
| ftp.appservice.\<region\>.\<DomainName\>.\<extension\> | ftp.appservice.redmond.azurestack.external |

#### <a name="identity-certificate"></a>Certificat d’identité

Le certificat de l’application de l’identité permet :

- l’intégration entre le répertoire Azure Active Directory (Azure AD) ou les services de fédération Active Directory (AD FS), Azure Stack et App Service pour prendre en charge l’intégration avec le fournisseur de ressources de calcul.
- Des scénarios d’authentification unique pour les outils de développement avancés dans Azure App Service sur Azure Stack.

Le certificat d’identité doit contenir un objet qui correspond au format suivant.

| Format | Exemples |
| --- | --- |
| sso.appservice.\<region\>.\<DomainName\>.\<extension\> | sso.appservice.redmond.azurestack.external |

## <a name="virtual-network"></a>Réseau virtuel

> [!NOTE]
> La pré-création d’un réseau virtuel personnalisé est optionnelle car le service Azure App Service sur Azure Stack peut créer le réseau virtuel requis mais devra ensuite communiquer avec SQL et File Server via des adresses IP publiques.

Azure App Service sur Azure Stack permet de déployer le fournisseur de ressources sur un réseau virtuel existant ou de créer un réseau virtuel dans le cadre du déploiement. Le fait d’utiliser un réseau virtuel existant permet d’utiliser des adresses IP internes pour se connecter au serveur de fichiers et au serveur SQL Server requis par Azure App Service sur Azure Stack. Vous devrez configurer le réseau virtuel avec la plage d’adresses et les sous-réseaux suivants avant d’installer Azure App Service sur Azure Stack :

Virtual Network - /16

Sous-réseaux

- ControllersSubnet /24
- ManagementServersSubnet /24
- FrontEndsSubnet /24
- PublishersSubnet /24
- WorkersSubnet /21

## <a name="prepare-the-file-server"></a>Préparer le serveur de fichiers

Azure App Service requiert l’utilisation d’un serveur de fichiers. Pour les déploiements de production, le serveur de fichiers doit être configuré en haute disponibilité et capable de gérer les défaillances.

### <a name="quickstart-template-for-file-server-for-deployments-of-azure-app-service-on-asdk"></a>Modèle de démarrage rapide pour le File Server destiné aux déploiements d’Azure App Service sur ASDK.

Pour les déploiements du Kit de développement Azure Stack uniquement, vous pouvez utiliser cet [exemple de modèle de déploiement Azure Resource Manager](https://aka.ms/appsvconmasdkfstemplate) pour déployer un serveur de fichiers configuré avec un seul nœud. Le serveur de fichiers à nœud unique sera dans un groupe de travail.

### <a name="quickstart-template-for-highly-available-file-server-and-sql-server"></a>Modèle de démarrage rapide pour une instance de File Server et SQL Server à haute disponibilité

Un [modèle de démarrage rapide d’architecture de référence](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/appservice-fileserver-sqlserver-ha) est désormais disponible. Il permet de déployer une instance de File Server et de SQL Server qui prend en charge l’infrastructure Active Directory dans un réseau virtuel configuré pour la prise en charge d’un déploiement à haute disponibilité d’Azure App Service sur Azure Stack.  

### <a name="steps-to-deploy-a-custom-file-server"></a>Étapes pour déployer une instance personnalisée de File Server

>[!IMPORTANT]
> Si vous choisissez de déployer App Service dans un réseau virtuel existant, le serveur de fichiers devra être déployé dans un sous-réseau distinct d’App Service.

#### <a name="provision-groups-and-accounts-in-active-directory"></a>Approvisionner des groupes et des comptes dans Active Directory

1. Créez les groupes de sécurité globaux Active Directory suivants :

   - FileShareOwners
   - FileShareUsers

2. Créez les comptes Active Directory suivants en tant que comptes du service :

   - FileShareOwner
   - FileShareUser

   En ce qui concerne les meilleures pratiques en termes de sécurité, les utilisateurs de ces comptes (et pour tous les rôles web) doivent être uniques et détenir des noms d’utilisateur et des mots de passe sécurisés. Définissez les mots de passe avec les conditions suivantes :

   - Activez **Le mot de passe n’expire jamais**.
   - Activez **L’utilisateur ne peut pas changer de mot de passe**.
   - Désactivez **L’utilisateur doit changer de mot de passe à la prochaine ouverture de session**.

3. Ajoutez les comptes aux appartenances aux groupes comme suit :

   - Ajoutez **FileShareOwner** au groupe **FileShareOwners**.
   - Ajoutez **FileShareUser** au groupe **FileShareUsers**.

#### <a name="provision-groups-and-accounts-in-a-workgroup"></a>Approvisionner des groupes et des comptes dans un groupe de travail

>[!NOTE]
> Quand vous configurez un serveur de fichiers, exécutez toutes les commandes suivantes à partir d’une **invite de commandes en mode Administrateur**. <br>***N’utilisez pas PowerShell.***

Lorsque vous utilisez le modèle Azure Resource Manager, les utilisateurs sont déjà créés.

1. Exécutez les commandes suivantes pour créer les comptes FileShareOwner et FileShareUser. Remplacez `<password>` par vos propres valeurs.

   ``` DOS
   net user FileShareOwner <password> /add /expires:never /passwordchg:no
   net user FileShareUser <password> /add /expires:never /passwordchg:no
   ```

2. Définissez les mots de passe pour les comptes de sorte qu’ils n’expirent jamais en exécutant les commandes WMIC suivantes :

   ``` DOS
   WMIC USERACCOUNT WHERE "Name='FileShareOwner'" SET PasswordExpires=FALSE
   WMIC USERACCOUNT WHERE "Name='FileShareUser'" SET PasswordExpires=FALSE
   ```

3. Créez les groupes locaux FileShareUsers et FileShareOwners et ajoutez-y les comptes lors de la première étape :

   ``` DOS
   net localgroup FileShareUsers /add
   net localgroup FileShareUsers FileShareUser /add
   net localgroup FileShareOwners /add
   net localgroup FileShareOwners FileShareOwner /add
   ```

#### <a name="provision-the-content-share"></a>Approvisionner le partage de contenu

Le partage de contenu contient le contenu du site web du locataire. La procédure d’approvisionnement de partage de contenu sur un seul serveur de fichiers est identique pour les environnements Active Directory et de groupe de travail. Mais elle est différente pour un cluster de basculement dans Active Directory.

#### <a name="provision-the-content-share-on-a-single-file-server-active-directory-or-workgroup"></a>Approvisionnez le partage de contenu sur un seul serveur de fichiers (Active Directory ou Groupe de travail)

Exécutez les commandes suivantes dans une invite de commandes avec élévation de privilèges sur un serveur de fichiers unique. Remplacez la valeur pour `C:\WebSites` par les chemins d’accès correspondants dans votre environnement.

```DOS
set WEBSITES_SHARE=WebSites
set WEBSITES_FOLDER=C:\WebSites
md %WEBSITES_FOLDER%
net share %WEBSITES_SHARE% /delete
net share %WEBSITES_SHARE%=%WEBSITES_FOLDER% /grant:Everyone,full
```

### <a name="configure-access-control-to-the-shares"></a>Configurer le contrôle d’accès aux partages

Exécutez les commandes suivantes dans une invite de commandes avec élévation de privilèges sur le serveur de fichiers ou sur le nœud de cluster de basculement, qui est le propriétaire actuel de la ressource de cluster. Remplacez les valeurs en italiques par les valeurs spécifiques de votre environnement.

#### <a name="active-directory"></a>Active Directory

```DOS
set DOMAIN=<DOMAIN>
set WEBSITES_FOLDER=C:\WebSites
icacls %WEBSITES_FOLDER% /reset
icacls %WEBSITES_FOLDER% /grant Administrators:(OI)(CI)(F)
icacls %WEBSITES_FOLDER% /grant %DOMAIN%\FileShareOwners:(OI)(CI)(M)
icacls %WEBSITES_FOLDER% /inheritance:r
icacls %WEBSITES_FOLDER% /grant %DOMAIN%\FileShareUsers:(CI)(S,X,RA)
icacls %WEBSITES_FOLDER% /grant *S-1-1-0:(OI)(CI)(IO)(RA,REA,RD)
```

#### <a name="workgroup"></a>Groupe de travail

```DOS
set WEBSITES_FOLDER=C:\WebSites
icacls %WEBSITES_FOLDER% /reset
icacls %WEBSITES_FOLDER% /grant Administrators:(OI)(CI)(F)
icacls %WEBSITES_FOLDER% /grant FileShareOwners:(OI)(CI)(M)
icacls %WEBSITES_FOLDER% /inheritance:r
icacls %WEBSITES_FOLDER% /grant FileShareUsers:(CI)(S,X,RA)
icacls %WEBSITES_FOLDER% /grant *S-1-1-0:(OI)(CI)(IO)(RA,REA,RD)
```

## <a name="prepare-the-sql-server-instance"></a>Préparer l’instance SQL Server

Pour qu’Azure App Service sur Azure Stack héberge et contrôle les bases de données, vous devez préparer une instance SQL Server pour stocker les bases de données d’App Service.

Pour les déploiements du Kit de développement Azure Stack, vous pouvez utiliser SQL Server Express 2014 SP2 ou une version ultérieure.

Pour des raisons de production et de haute disponibilité, vous devez utiliser une version complète de SQL Server 2014 SP2 ou une version ultérieure, activer l’authentification en mode mixte et déployer une [configuration hautement disponible](https://docs.microsoft.com/sql/sql-server/failover-clusters/high-availability-solutions-sql-server).

L’instance SQL Server pour Azure App Service sur Azure Stack doit être accessible depuis tous les rôles App Service. SQL Server peut être déployé au sein d’un abonnement de fournisseur par défaut dans Azure Stack. Vous pouvez aussi vous servir d’une infrastructure existante au sein de votre organisation (tant qu’il existe une connectivité avec Azure Stack). Si vous utilisez une image de Place de marché Azure, pensez à configurer le pare-feu en conséquence.

>[!NOTE]
> Un certain nombre d’images de machines virtuelles IaaS SQL sont disponibles via la fonctionnalité Gestion de la Place de Marché. Assurez-vous de toujours télécharger la dernière version de l’extension Iaas SQL avant de déployer une machine virtuelle à l’aide d’un élément de la Place de marché. Les images SQL sont les mêmes que les machines virtuelles SQL sont disponibles dans Azure. Pour les machines virtuelles SQL créées à partir de ces images, l’extension IaaS et les améliorations apportées au portail correspondantes fournissent des fonctionnalités de mise à jour corrective et de sauvegarde automatique.
>
Pour tous les rôles SQL Server, vous pouvez utiliser une instance par défaut ou une instance nommée. Si vous utilisez une instance nommée, assurez-vous de démarrer manuellement le service SQL Server Browser et d’ouvrir le port 1434.

>[!IMPORTANT]
> Si vous choisissez de déployer App Service dans un réseau virtuel existant, le serveur SQL Server devra être déployé dans un sous-réseau distinct d’App Service et du serveur de fichiers.
>

## <a name="create-an-azure-active-directory-application"></a>Créer une application Azure Active Directory

Configurer un principal du service Azure AD pour prendre en charge les opérations suivantes :

- Intégration d’un groupe de machines virtuelles identiques sur les niveaux de travail.
- Authentification unique pour le portail Azure Functions et les outils de développement avancés.

Ces étapes s’appliquent uniquement aux environnements Azure Stack sécurisés avec Azure AD.

Les administrateurs doivent configurer l’authentification unique pour :

- Activer les outils de développement avancés dans App Service (Kudu).
- Activer l’utilisation de l’expérience du portail Azure Functions.

Procédez comme suit :

1. Ouvrez une instance PowerShell en tant que azurestack\Azurestackadmin.
2. Accédez à l’emplacement où les scripts ont été téléchargés et extraits dans [l’étape des prérequis](https://docs.microsoft.com/azure/azure-stack/azure-stack-app-service-before-you-get-started#download-the-azure-app-service-on-azure-stack-installer-and-helper-scripts).
3. [Installez PowerShell pour Azure Stack](azure-stack-powershell-install.md).
4. Exécutez le script **Create-AADIdentityApp.ps1**. Lorsque vous y êtes invité, entrez l’ID de locataire Azure AD que vous utilisez pour votre déploiement Azure Stack. Par exemple, entrez **myazurestack.onmicrosoft.com**.
5. Dans la fenêtre **Informations d’identification**, entrez votre compte administrateur et votre mot de passe pour le service Azure AD. Sélectionnez **OK**.
6. Entrez le chemin d’accès au fichier du certificat et le mot de passe du certificat pour le [certificat créé précédemment](https://docs.microsoft.com/azure/azure-stack/azure-stack-app-service-before-you-get-started#certificates-required-for-azure-app-service-on-azure-stack). Le certificat par défaut créé pour cette étape est **sso.appservice.local.azurestack.external.pfx**.
7. Le script crée une nouvelle application dans l’instance de locataire Azure AD. Notez l’ID d’application qui est retourné dans la sortie PowerShell. Vous avez besoin de ces informations lors de l’installation.
8. Ouvrez une nouvelle fenêtre de navigateur et connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur du service Azure Active Directory.
9. Ouvrez le fournisseur de ressources Azure AD.
10. Sélectionner **Inscriptions des applications**.
11. Recherchez l’ID d’application retourné à l’étape 7. Une application App Service est répertoriée.
12. Sélectionnez **Application** dans la liste.
13. Sélectionnez **Paramètres**.
14. Sélectionnez **Autorisations requises** > **Accorder des autorisations** > **Oui**.

```PowerShell
    Create-AADIdentityApp.ps1
```

| Paramètre | Obligatoire ou facultatif | Valeur par défaut | Description |
| --- | --- | --- | --- |
| DirectoryTenantName | Obligatoire | Null | ID de locataire Azure AD. Fournir le GUID ou une chaîne. Par exemple : myazureaaddirectory.onmicrosoft.com. |
| AdminArmEndpoint | Obligatoire | Null | Point de terminaison Azure Resource Manager d’administrateur. Par exemple : adminmanagement.local.azurestack.external. |
| TenantARMEndpoint | Obligatoire | Null | Point de terminaison Azure Resource Manager de locataire. Par exemple : management.local.azurestack.external. |
| AzureStackAdminCredential | Obligatoire | Null | Informations d’identification de l’administrateur du service Azure AD. |
| CertificateFilePath | Obligatoire | Null | **Chemin complet** du fichier de certificat d’application d’identité généré précédemment. |
| CertificatePassword | Obligatoire | Null | Mot de passe pour aider à protéger la clé privée du certificat. |
| Environnement | Facultatif | AzureCloud | Le nom de l’environnement de Cloud pris en charge dans lequel le service Graph Azure Active Directory cible est disponible.  Valeurs autorisées : 'AzureCloud', 'AzureChinaCloud', 'AzureUSGovernment', 'AzureGermanCloud'.|

## <a name="create-an-active-directory-federation-services-application"></a>Créer une application de services de fédération Active Directory (AD FS)

Pour les environnements Azure Stack sécurisés par AD FS, vous devez configurer un principal du service AD FS pour prendre en charge les opérations suivantes :

- Intégration d’un groupe de machines virtuelles identiques sur les niveaux de travail.
- Authentification unique pour le portail Azure Functions et les outils de développement avancés.

Les administrateurs doivent configurer l’authentification unique pour :

- Configurer un principal du service pour l’intégration d’un groupe de machines virtuelles identiques sur les niveaux Worker.
- Activer les outils de développement avancés dans App Service (Kudu).
- Activer l’utilisation de l’expérience du portail Azure Functions.

Procédez comme suit :

1. Ouvrez une instance PowerShell en tant que azurestack\Azurestackadmin.
2. Accédez à l’emplacement où les scripts ont été téléchargés et extraits dans [l’étape des prérequis](https://docs.microsoft.com/azure/azure-stack/azure-stack-app-service-before-you-get-started#download-the-azure-app-service-on-azure-stack-installer-and-helper-scripts).
3. [Installez PowerShell pour Azure Stack](azure-stack-powershell-install.md).
4. Exécutez le script **Create-ADFSIdentityApp.ps1**.
5. Dans la fenêtre **Informations d’identification**, entrez votre compte administrateur et votre mot de passe pour le cloud AD FS. Sélectionnez **OK**.
6. Entrez le chemin d’accès au fichier du certificat et le mot de passe du certificat pour le [certificat créé précédemment](https://docs.microsoft.com/azure/azure-stack/azure-stack-app-service-before-you-get-started#certificates-required-for-azure-app-service-on-azure-stack). Le certificat par défaut créé pour cette étape est **sso.appservice.local.azurestack.external.pfx**.

```PowerShell
    Create-ADFSIdentityApp.ps1
```

| Paramètre | Obligatoire ou facultatif | Valeur par défaut | Description |
| --- | --- | --- | --- |
| AdminArmEndpoint | Obligatoire | Null | Point de terminaison Azure Resource Manager d’administrateur. Par exemple : adminmanagement.local.azurestack.external. |
| PrivilegedEndpoint | Obligatoire | Null | Point de terminaison privilégié. Par exemple : AzS-ERCS01. |
| CloudAdminCredential | Obligatoire | Null | Informations d’identification du compte de domaine pour les administrateurs cloud d’Azure Stack. Par exemple : Azurestack\CloudAdmin. |
| CertificateFilePath | Obligatoire | Null | **Chemin complet** du fichier PFX du certificat d’application d’identité. |
| CertificatePassword | Obligatoire | Null | Mot de passe pour aider à protéger la clé privée du certificat. |

## <a name="next-steps"></a>Étapes suivantes

[Installer le fournisseur de ressources App Service](azure-stack-app-service-deploy.md)
