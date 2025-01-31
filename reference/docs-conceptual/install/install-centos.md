---
description: Information about installing PowerShell on CentOS
ms.date: 09/22/2021
title: Installing PowerShell on CentOS
---
# Installing PowerShell on CentOS

All packages are available on our GitHub [releases][releases] page. After the package is installed,
run `pwsh` from a terminal. Run `pwsh-preview` if you installed a preview release.

> [!NOTE]
> PowerShell 7.2 is an in-place upgrade that removes previous versions of PowerShell.
>
> If you need to run PowerShell 7.2 side-by-side with a previous version, reinstall the previous
> version using the [binary archive](install-other-linux.md#binary-archives) method.

CentOS 7 uses Yum as a package manager and CentOS 8 uses DNF.

[!INCLUDE [CentOS support](../../includes/centos-support.md)]

## Installation via Package Repository (preferred)

PowerShell for CentOS is published to official Microsoft repositories for easy installation and
updates. The URL to the package depends on the version of CentOS you are using

- CentOS 8 - `https://packages.microsoft.com/config/rhel/8/prod.repo`
- CentOS 7 - `https://packages.microsoft.com/config/rhel/7/prod.repo`

Change the URL in the following shell commands to match the version you need.

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/8/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

As superuser, register the Microsoft repository once. After registration, you can update PowerShell
with `sudo yum update powershell`.

### Installation via direct download

PowerShell 7.2 is distributed as a universal RPM package. Previous versions of PowerShell had
separate package for each OS. Download the RPM package you need onto your CentOS machine.

- PowerShell 7.2-preview.10 - `https://github.com/PowerShell/PowerShell/releases/download/v7.2.0-preview.10/powershell-preview-7.2.0_preview.10-1.rh.x86_64.rpm`
- PowerShell 7.1.4
  - CentOS 7 - `https://github.com/PowerShell/PowerShell/releases/download/v7.1.4/powershell-7.1.4-1.rhel.7.x86_64.rpm`
  - CentOS 8 - `https://github.com/PowerShell/PowerShell/releases/download/v7.1.4/powershell-7.1.4-1.centos.8.x86_64.rpm`
- PowerShell 7.0.7
  - CentOS 7 - `https://github.com/PowerShell/PowerShell/releases/download/v7.1.4/powershell-7.0.7-1.rhel.7.x86_64.rpm`
  - CentOS 8 - `https://github.com/PowerShell/PowerShell/releases/download/v7.1.4/powershell-7.0.7-1.centos.8.x86_64.rpm`

Change the URL in the following shell commands to match the version you need.

On CentOS 7:

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v7.2.0-preview.10/powershell-preview-7.2.0_preview.10-1.rh.x86_64.rpm
```

On CentOS 8:

```sh
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v7.2.0-preview.10/powershell-preview-7.2.0_preview.10-1.rh.x86_64.rpm
```

## Uninstall PowerShell from CentOS

```sh
sudo yum remove powershell
```

## PowerShell paths

- `$PSHOME` is `/opt/microsoft/powershell/7/`
- User profiles are read from `~/.config/powershell/profile.ps1`
- Default profiles are read from `$PSHOME/profile.ps1`
- User modules are read from `~/.local/share/powershell/Modules`
- Shared modules are read from `/usr/local/share/powershell/Modules`
- Default modules are read from `$PSHOME/Modules`
- PSReadLine history is recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

The profiles respect PowerShell's per-host configuration, so the default host-specific profiles
exists at `Microsoft.PowerShell_profile.ps1` in the same locations.

PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.

## Installation support

Microsoft supports the installation methods in this document. There may be other methods of
installation available from other third-party sources. While those tools and methods may work,
Microsoft cannot support those methods.

<!-- link references -->
[releases]: https://aka.ms/PowerShell-Release?tag=stable
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
[lifecycle]: ../PowerShell-Support-Lifecycle.md
[eol-centos]: https://www.centos.org/centos-linux-eol/
