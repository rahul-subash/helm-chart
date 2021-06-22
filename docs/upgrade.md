# Upgrading Bold BI to 4.1.36

This section explains how to upgrade Bold BI to 4.1.36 version in your Kubernetes cluster. You can refer to the features and enhancements from this [Release Notes](https://www.boldbi.com/release-history/enterprise/).


## Backup the existing data
Before upgrading the Bold BI to latest version, make sure to take the backup of the following items.

* Files and folders from the shared location, which you have mounted to the deployments by persistent volume claims (pvclaim_*.yaml).

* Database backup - Take a backup of Database, to restore incase if the upgrade was not successful or if applications are not working properly after the upgrade.


## Proceeding with upgrade
Bold BI updates the database schema of your current version to the latest version. The upgrade process will retain all the resources and settings from the previous deployment.

You can download the upgrade script from this [link](https://raw.githubusercontent.com/boldbi/boldbi-kubernetes/v4.1.36/deploy/upgrade.sh).

Run the following command to execute the shell script to upgrade Bold BI.

```sh
./upgrade.sh --version="4.1.36" --namespace="default"
```

<table>
    <tr>
      <td>
       version
      </td>
      <td>
      Image tag of the current version, which you are going to upgrade.
      </td>
    </tr>
    <tr>
      <td>
       namespace (optional)
      </td>
      <td>
       namespace in which your existing Bold BI application was running. </br>
       Default value: <i>default</i>
      </td>
    </tr>
</table>
