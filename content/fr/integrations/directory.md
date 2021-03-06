---
assets:
  dashboards: {}
  monitors: {}
  service_checks: assets/service_checks.json
categories:
  - os & system
creates_events: false
ddtype: check
dependencies:
  - 'https://github.com/DataDog/integrations-core/blob/master/directory/README.md'
display_name: Directory
git_integration_title: directory
guid: 0c38c4ef-5266-4667-9fb1-de8f2b73708a
integration_id: system
integration_title: Directory
is_public: true
kind: integration
maintainer: help@datadoghq.com
manifest_version: 1.0.0
metric_prefix: system.
metric_to_check: system.disk.directory.file.bytes
name: directory
public_title: Intégration Datadog/Directory
short_description: L'intégration Directory transmet des métriques sur des fichiers pour un répertoire donné.
support: core
supported_os:
  - linux
  - mac_os
  - windows
---
## Présentation

Capturez des métriques à partir des répertoires et des fichiers de votre choix. L'Agent recueille les éléments suivants :

  * Le nombre de fichiers
  * La taille des fichiers
  * La date de dernière modification
  * La date de création

## Implémentation

### Installation

Le check Directory est inclus avec le paquet de l'[Agent Datadog][1] : vous n'avez donc rien d'autre à installer sur votre serveur.

### Configuration

1. Modifiez le fichier `directory.d/conf.yaml` dans le dossier `conf.d/` à la racine du [répertoire de configuration de votre Agent][2] pour commencer à recueillir vos données de performance Directory. Consultez le [fichier d'exemple directory.d/conf.yaml][3] pour découvrir toutes les options de configuration disponibles.

    ```yaml
      init_config:

      instances:
        - directory: "/path/to/directory" # the only required option
          name: "my_monitored_dir"        # What the Agent will tag this directory's metrics with. Defaults to "directory"
          pattern: "*.log"                # defaults to "*" (all files)
          recursive: True                 # default False
          countonly: False                # set to True to only collect the number of files matching 'pattern'. Useful for very large directories.
          ignore_missing: False           # set to True to not raise exceptions on missing or inaccessible directories
    ```

    Vérifiez que l'utilisateur qui exécute le processus de l'Agent (généralement, `datadog-agent`) dispose d'un accès en lecture aux répertoires, sous-répertoires et fichiers que vous configurez.

    **Remarque** : sur Windows, lorsque vous ajoutez votre répertoire, utilisez deux barres obliques (`C:\\chemin\\vers\\répertoire`) au lieu d'une seule (`C:\chemin\vers\répertoire`) pour exécuter le check, ceci afin d'éviter que le check Directory échoue et que la traceback se termine par l'erreur `found unknown escape character in "<chaîne>"` signalant un problème de caractère d'échappement inconnu.

2. [Redémarrez l'Agent][4].

#### Collecte de métriques
Le check Directory peut potentiellement générer des [métriques custom][5], ce qui peut avoir une incidence sur votre [facture][6].

### Validation

[Lancez la sous-commande status de l'Agent][7] et cherchez `directory` dans la section Checks.

## Données collectées
### Métriques
{{< get-metrics-from-git "directory" >}}


### Événements
Le check Directory n'inclut aucun événement.

### Checks de service
Le check Directory n'inclut aucun check de service.

## Dépannage
Besoin d'aide ? Contactez [l'assistance Datadog][9].

[1]: https://app.datadoghq.com/account/settings#agent
[2]: https://docs.datadoghq.com/fr/agent/guide/agent-configuration-files/#agent-configuration-directory
[3]: https://github.com/DataDog/integrations-core/blob/master/directory/datadog_checks/directory/data/conf.yaml.example
[4]: https://docs.datadoghq.com/fr/agent/guide/agent-commands/#start-stop-and-restart-the-agent
[5]: https://docs.datadoghq.com/fr/developers/metrics/custom_metrics
[6]: https://docs.datadoghq.com/fr/account_management/billing/custom_metrics
[7]: https://docs.datadoghq.com/fr/agent/guide/agent-commands/#agent-status-and-information
[8]: https://github.com/DataDog/integrations-core/blob/master/directory/metadata.csv
[9]: https://docs.datadoghq.com/fr/help