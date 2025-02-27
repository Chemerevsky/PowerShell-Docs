---
description: This article explains how to get started using the PowerShell Gallery and the PowerShellGet cmdlets
ms.date: 10/05/2021
title: Get Started with the PowerShell Gallery
---
# Getting Started with the PowerShell Gallery

The PowerShell Gallery is a package repository containing scripts, modules, and DSC resources you
can download and leverage. You use the cmdlets in the
[PowerShellGet](/powershell/module/powershellget) module to install packages from the PowerShell
Gallery. You don't need to sign in to download items from the PowerShell Gallery.

> [!NOTE]
> It's possible to download a package from the PowerShell Gallery directly, but this isn't a
> recommended approach. For more details, see
> [Manual Package Download](how-to/working-with-packages/manual-download.md).

## Discovering packages from the PowerShell Gallery

You can find packages in the PowerShell Gallery using the **Search** control on the PowerShell
Gallery's [home page](https://www.powershellgallery.com), or by browsing through the Modules and
Scripts from the [Packages page](https://www.powershellgallery.com/packages). You can also find
packages from the PowerShell Gallery by running the `Find-Module`, `Find-DscResource`, and
`Find-Script` cmdlets, depending on the package type, with `-Repository PSGallery`.

You can filter results from the Gallery using the following parameters:

- Name
- AllVersions
- MinimumVersion
- RequiredVersion
- Tag
- Includes
- DscResource
- RoleCapability
- Command
- Filter

If you're only interested in discovering specific DSC resources in the Gallery, you can run the
`Find-DscResource` cmdlet. Find-DscResource returns data on DSC resources contained in the Gallery.
Because DSC resources are always delivered as part of a module, you still need to run
`Install-Module` to install those DSC resources.

## Learning about packages in the PowerShell Gallery

Once you've identified a package that you're interested in, you may want to learn more about it. You
can do this by examining that package's specific page on the Gallery. On that page, you'll be able
to see all the metadata uploaded with the package. This metadata is provided by the package's
author, and is not verified by Microsoft. The Owner of the package is strongly tied to the Gallery
account used to publish the package, and is more trustworthy than the Author field.

If you discover a package that you feel isn't published in good faith, click **Report Abuse** on
that package's page.

If you're running `Find-Module` or `Find-Script`, you can view this data in the returned
PSGetModuleInfo object. For example, running
`Find-Module -Name PSReadLine -Repository PSGallery | Get-Member` returns data on the PSReadLine
module in the Gallery.

## Downloading packages from the PowerShell Gallery

We encourage the following process when downloading packages from the PowerShell Gallery:

### Inspect

To download a package from the Gallery for inspection, run either the `Save-Module` or `Save-Script`
cmdlet, depending on the package type. This lets you save the package locally without installing it,
and inspect the package contents. Remember to delete the saved package manually.

Some of these packages are authored by Microsoft, and others are authored by the PowerShell
community. Microsoft recommends that you review the contents and code of packages on this gallery
before installation.

If you discover a package that you feel isn't published in good faith, click **Report Abuse** on
that package's page.

### Install

To install a package from the Gallery for use, run either the `Install-Module` or `Install-Script`
cmdlet, depending on the package type.

`Install-Module` installs the module to `$env:ProgramFiles\WindowsPowerShell\Modules` by default.
This requires an administrator account. If you add the `-Scope CurrentUser` parameter, the module is
installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .

`Install-Script` installs the script to `$env:ProgramFiles\WindowsPowerShell\Scripts` by default.
This requires an administrator account. If you add the `-Scope CurrentUser` parameter, the script is
installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .

By default, `Install-Module` and `Install-Script` installs the most
current version of a package. To install an older version of the package, add the `-RequiredVersion`
parameter.

### Deploy

To deploy a package from the PowerShell Gallery to Azure Automation, click **Azure Automation**,
then click **Deploy to Azure Automation** on the package details page. You are redirected to the
Azure Management Portal where you sign in using your Azure account credentials. Note that
deploying packages with dependencies deploys all the dependencies to Azure Automation. The 'Deploy
to Azure Automation' button can be disabled by adding the **AzureAutomationNotSupported** tag to
your package metadata.

To learn more about Azure Automation, see the [Azure Automation](/azure/automation) documentation.

## Updating packages from the PowerShell Gallery

To update packages installed from the PowerShell Gallery, run either the `Update-Module` or
`Update-Script` cmdlet. When run without any additional parameters, `Update-Module` attempts to
update all modules installed by running `Install-Module`. To selectively update modules, add the
`-Name` parameter.

Similarly, when run without any additional parameters, `Update-Script` also attempts to update all
scripts installed by running `Install-Script`. To selectively update scripts, add the `-Name`
parameter.

## List packages that you have installed from the PowerShell Gallery

To find out which modules you have installed from the PowerShell Gallery, run the
`Get-InstalledModule` cmdlet. This command lists all the modules you have on your system that were
installed directly from the PowerShell Gallery.

Similarly, to find out which scripts you have installed from the PowerShell Gallery, run the
`Get-InstalledScript` cmdlet. This command lists all the scripts you have on your system that were
installed directly from the PowerShell Gallery.

## Network access to the PowerShell Gallery

These hostnames should be added to the allow lists that control access from your network.

Hosts required for package discovery and download:

- `onegetcdn.azureedge.net` - CDN hostname
- `psg-prod-centralus.azureedge.net` - CDN hostname
- `psg-prod-eastus.azureedge.net` - CDN hostname

> [!NOTE]
> The CDN for the PowerShell gallery is active for one name, `psg-prod-eastus.azureedge.net` or
> `psg-prod-centralus.azureedge.net`, at any given time. The inactive name becomes the valid, active
> name if there is a need to failover the service. Therefore, both names should be included in your
> allow lists.

Hosts required when using the PowerShell Gallery website:

- `devopsgallerystorage.blob.core.windows.net` - storage account hostname
- `*.powershellgallery.com` - website
- `go.microsoft.com` - redirection service

[!INCLUDE [TLS 1.2 Requirement](../../includes/tls-gallery.md)]

## Related links

- [Find-DscResource][Find-DscResource]
- [Find-Module][Find-Module]
- [Find-Script][Find-Script]
- [Get-InstalledModule][Get-InstalledModule]
- [Get-InstalledScript][Get-InstalledScript]
- [Install-Module][Install-Module]
- [Install-Script][Install-Script]
- [Publish-Module][Publish-Module]
- [Publish-Script][Publish-Script]
- [Register-PSRepository][Register-PSRepository]
- [Save-Module][Save-Module]
- [Save-Script][Save-Script]
- [Update-Module][Update-Module]
- [Update-Script][Update-Script]

<!-- link references -->
[Find-DscResource]: /powershell/module/powershellget/Find-DscResource
[Find-Module]: /powershell/module/powershellget/Find-Module
[Find-Script]: /powershell/module/powershellget/Find-Script
[Get-InstalledModule]: /powershell/module/powershellget/Get-InstalledModule
[Get-InstalledScript]: /powershell/module/powershellget/Get-InstalledScript
[Install-Module]: /powershell/module/powershellget/Install-Module
[Install-Script]: /powershell/module/powershellget/Install-Script
[Publish-Module]: /powershell/module/powershellget/Publish-Module
[Publish-Script]: /powershell/module/powershellget/Publish-Script
[Register-PSRepository]: /powershell/module/powershellget/Register-Repository
[Save-Module]: /powershell/module/powershellget/Save-Module
[Save-Script]: /powershell/module/powershellget/Save-Script
[Update-Module]: /powershell/module/powershellget/Update-Module
[Update-Script]: /powershell/module/powershellget/Update-Script
