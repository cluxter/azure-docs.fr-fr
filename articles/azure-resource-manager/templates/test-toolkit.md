---
title: Kit de ressources de test de modèle ARM
description: Décrit la procédure d’exécution du kit de ressources de test de modèle ARM sur votre modèle. Le kit de ressources vous permet de voir si vous avez implémenté les pratiques recommandées.
ms.topic: conceptual
ms.date: 06/19/2020
ms.author: tomfitz
author: tfitzmac
ms.openlocfilehash: 7b88096dfdd1c7fb3e2671a369132e75a8885b8d
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85255772"
---
# <a name="use-arm-template-test-toolkit"></a>Utiliser un kit de ressources de test de modèle ARM

Le [kit de ressources de test de modèle ARM](https://aka.ms/arm-ttk) vérifie si votre modèle utilise les pratiques recommandées. Lorsque votre modèle n’est pas conforme aux pratiques recommandées, il retourne une liste d’avertissements avec les modifications suggérées. Avec le kit de ressources de test, vous pouvez apprendre à éviter les problèmes courants liés au développement de modèles.

Le kit de ressources de test fournit un [ensemble de tests par défaut](test-cases.md). Ces tests sont des recommandations, mais pas des exigences. Vous pouvez choisir les tests qui sont pertinents pour vos objectifs et personnaliser les tests à exécuter.

Cet article explique les procédures d’exécution du kit de ressources de test, et d’ajout ou de suppression des tests. Pour obtenir une description des tests par défaut, consultez [les cas de test du kit de ressources](test-cases.md).

Le kit de ressources est un ensemble de scripts PowerShell qui peuvent être exécutés à partir d’une commande dans PowerShell ou CLI.

## <a name="download-test-toolkit"></a>Télécharger le kit de ressources de test

Pour utiliser le kit de ressources de test, vous pouvez répliquer et cloner le [référentiel](https://aka.ms/arm-ttk) contenant les scripts ou [télécharger le fichier. zip le plus récent](https://aka.ms/arm-ttk-latest).

Selon la stratégie d’exécution de l’ordinateur sur lequel vous exécutez le script, vous pouvez obtenir une erreur d’exécution des scripts à partir d’Internet. Vous devez modifier la [stratégie d’exécution](/powershell/module/microsoft.powershell.core/about/about_execution_policies) ou [débloquer les fichiers de script](/powershell/module/microsoft.powershell.utility/unblock-file).

## <a name="run-on-powershell"></a>Exécuter dans PowerShell

Avant d’exécuter les tests, importez le module.

```powershell
Import-Module .\arm-ttk.psd1 # from the same directory as .\arm-ttk.psd1
```

Pour exécuter les tests dans **PowerShell**, utilisez la commande suivante :

```powershell
Test-AzTemplate -TemplatePath $TemplateFolder
```

## <a name="run-on-linux"></a>Exécuter sur Linux

Avant d’exécuter les tests, installez [PowerShell Core](/powershell/scripting/install/installing-powershell-core-on-linux).

Pour exécuter les tests sur **Linux** dans Bash, utilisez la commande suivante :

```bash
Test-AzTemplate.sh -TemplatePath $TemplateFolder
```

Vous pouvez également exécuter le test sur pwsh.exe.

## <a name="run-on-macos"></a>Exécuter sur macOS

Avant d’exécuter les tests, installez [PowerShell Core](/powershell/scripting/install/installing-powershell-core-on-macos). 

Installez `coreutils` :

```bash
brew install coreutils
```

Pour exécuter les tests sur **macOS**, utilisez la commande suivante :

```bash
Test-AzTemplate.sh -TemplatePath $TemplateFolder
```

## <a name="result-format"></a>Format de résultat

Les tests réussis s’affichent en **vert** et sont précédés de **[+]** .

Les tests qui échouent s’affichent en **rouge** et sont précédés de **[-]** .

:::image type="content" source="./media/template-test-toolkit/view-results.png" alt-text="afficher les résultats des tests":::

Résultats de texte :

```powershell
[+] adminUsername Should Not Be A Literal (24 ms)
[+] apiVersions Should Be Recent (18 ms)
[+] artifacts parameter (16 ms)
[+] DeploymentTemplate Schema Is Correct (17 ms)
[+] IDs Should Be Derived From ResourceIDs (15 ms)
[-] Location Should Not Be Hardcoded (41 ms)
     azuredeploy.json must use the location parameter, not resourceGroup().location (except when used as a default value in the main template)
```

## <a name="test-parameters"></a>Paramètres de test

Lorsque vous fournissez le paramètre **-TemplatePath**, le kit de ressources recherche dans ce dossier un modèle nommé azuredeploy.json ou maintemplate.json. Il teste d’abord ce modèle, puis teste tous les autres modèles du dossier et de ses sous-dossiers. Les autres modèles sont testés en tant que modèles liés. Si votre chemin d’accès comprend un fichier nommé [CreateUiDefinition.json](../managed-applications/create-uidefinition-overview.md), il exécute les tests qui sont pertinents pour la définition de l’interface utilisateur.

```powershell
Test-AzTemplate -TemplatePath $TemplateFolder
```

Pour tester un fichier dans ce dossier, ajoutez le paramètre **-File**. Toutefois, le dossier doit toujours avoir un modèle principal nommé azuredeploy.json ou maintemplate.json.

```powershell
Test-AzTemplate -TemplatePath $TemplateFolder -File cdn.json
```

Par défaut, tous les tests sont exécutés. Pour spécifier les tests individuels à exécuter, utilisez le paramètre **-Test**. Indiquez le nom du test. Pour les noms, consultez [Cas de test pour le kit de ressources](test-cases.md).

```powershell
Test-AzTemplate -TemplatePath $TemplateFolder -Test "Resources Should Have Location"
```

## <a name="customize-tests"></a>Personnaliser les tests

Pour les modèles ARM, le kit d’outils exécute tous les tests du dossier **\arm-ttk\testcases\deploymentTemplate**. Si vous souhaitez supprimer définitivement un test, supprimez ce fichier du dossier.

Pour les fichiers [CreateUiDefinition](../managed-applications/create-uidefinition-overview.md), il exécute tous les tests du dossier **\arm-ttk\testcases\CreateUiDefinition**.

Pour ajouter votre propre test, créez un fichier respectant la convention d’affectation de noms : **Nom-de-votre-test-personnalisé.test.ps1**.

Le test peut obtenir le modèle sous la forme d’un paramètre d’objet ou d’un paramètre de chaîne. En règle générale, vous utilisez l’un ou l’autre, mais vous pouvez utiliser les deux.

Utilisez le paramètre d’objet lorsque vous devez obtenir une section du modèle et itérer au sein de ses propriétés. Un test qui utilise le paramètre d’objet a le format suivant :

```powershell
param(
    [Parameter(Mandatory=$true,Position=0)]
    [PSObject]
    $TemplateObject
)

# Implement test logic that evaluates parts of the template.
# Output error with: Write-Error -Message
```

L’objet de modèle présente les propriétés suivantes :

* $schema
* contentVersion
* parameters
* variables
* les ressources
* outputs

Par exemple, vous pouvez obtenir la collection de paramètres avec `$TemplateObject.parameters`.

Utilisez le paramètre de chaîne lorsque vous devez effectuer une opération de chaîne sur l’ensemble du modèle. Un test qui utilise le paramètre de chaîne a le format suivant :

```powershell
param(
    [Parameter(Mandatory)]
    [string]
    $TemplateText
)

# Implement test logic that performs string operations.
# Output error with: Write-Error -Message
```

Par exemple, vous pouvez exécuter une expression régulière du paramètre de chaîne pour voir si une syntaxe spécifique est utilisée.

Pour en savoir plus sur l’implémentation du test, examinez les autres tests de ce dossier.

## <a name="integrate-with-azure-pipelines"></a>Intégrer à Azure Pipelines

Vous pouvez ajouter le kit de ressources de test à votre pipeline Azure. Avec un pipeline, vous pouvez exécuter le test chaque fois que le modèle est mis à jour ou l’exécuter dans le cadre de votre processus de déploiement.

Le moyen le plus simple d’ajouter le kit de ressources de test à votre pipeline consiste à utiliser des extensions tierces. Les deux extensions suivantes sont disponibles  :

* [Run ARM TTK Tests](https://marketplace.visualstudio.com/items?itemName=Sam-Cogan.ARMTTKExtension) (Exécuter les tests ARM TTK)
* [ARM Template Tester](https://marketplace.visualstudio.com/items?itemName=maikvandergaag.maikvandergaag-arm-ttk) (Testeur de modèle ARM)

Vous pouvez également implémenter vos propres tâches. L’exemple suivant illustre la procédure de téléchargement du kit de ressources de test.

```json
{
    "environment": {},
    "enabled": true,
    "continueOnError": false,
    "alwaysRun": false,
    "displayName": "Download TTK",
    "timeoutInMinutes": 0,
    "condition": "succeeded()",
    "task": {
        "id": "e213ff0f-5d5c-4791-802d-52ea3e7be1f1",
        "versionSpec": "2.*",
        "definitionType": "task"
    },
    "inputs": {
        "targetType": "inline",
        "filePath": "",
        "arguments": "",
        "script": "New-Item '$(ttk.folder)' -ItemType Directory\nInvoke-WebRequest -uri '$(ttk.uri)' -OutFile \"$(ttk.folder)/$(ttk.asset.filename)\" -Verbose\nGet-ChildItem '$(ttk.folder)' -Recurse\n\nWrite-Host \"Expanding files...\"\nExpand-Archive -Path '$(ttk.folder)/*.zip' -DestinationPath '$(ttk.folder)' -Verbose\n\nWrite-Host \"Expanded files found:\"\nGet-ChildItem '$(ttk.folder)' -Recurse",
        "errorActionPreference": "stop",
        "failOnStderr": "false",
        "ignoreLASTEXITCODE": "false",
        "pwsh": "true",
        "workingDirectory": ""
    }
}
```

L’exemple suivant illustre la procédure d’exécution des tests.

```json
{
    "environment": {},
    "enabled": true,
    "continueOnError": true,
    "alwaysRun": false,
    "displayName": "Run Best Practices Tests",
    "timeoutInMinutes": 0,
    "condition": "succeeded()",
    "task": {
        "id": "e213ff0f-5d5c-4791-802d-52ea3e7be1f1",
        "versionSpec": "2.*",
        "definitionType": "task"
    },
    "inputs": {
        "targetType": "inline",
        "filePath": "",
        "arguments": "",
        "script": "Import-Module $(ttk.folder)/arm-ttk/arm-ttk.psd1 -Verbose\n$testOutput = @(Test-AzTemplate -TemplatePath \"$(sample.folder)\")\n$testOutput\n\nif ($testOutput | ? {$_.Errors }) {\n   exit 1 \n} else {\n    Write-Host \"##vso[task.setvariable variable=result.best.practice]$true\"\n    exit 0\n} \n",
        "errorActionPreference": "continue",
        "failOnStderr": "true",
        "ignoreLASTEXITCODE": "false",
        "pwsh": "true",
        "workingDirectory": ""
    }
}
```

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur les tests par défaut, consultez [Cas de test pour le kit de ressources](test-cases.md).
