# aegisub-flatpak

**Aegisub** is a free, cross-platform open source tool for creating and modifying subtitles.

![aegisub-flatpak screenshot](aegisub-flatpak.png)

[Homepage](http://www.aegisub.org)

This repo is about the flatpak package.

## Instructions

### Requirements

* [flatpak](https://github.com/flatpak/flatpak)
* [flatpak-builder](https://github.com/flatpak/flatpak-builder)

For EL7:

```
# yum install 'flatpak' 'flatpak-builder'
```

You may also wish to install the `xdg-desktop-portal*` packages:

```
# yum install 'xdg-desktop-portal*'
```

See also:

* [flatpak setup](https://flatpak.org/setup)

### Adding repository

```
$ flatpak remote-add --if-not-exists "flathub" "https://dl.flathub.org/repo/flathub.flatpakrepo"
```

See also:

* [flathub setup](http://docs.flatpak.org/en/latest/using-flatpak.html#add-a-remote)

### Prepare

```
$ flatpak install "flathub" "org.gnome.Sdk//3.34"
```

```
$ flatpak install "flathub" "org.gnome.Platform//3.34"
```

Clone this repository, then checkout the right branch.

```
$ git submodule init
```

```
$ git submodule update
```

### Build

```
$ flatpak-builder "build" "org.aegisub.Aegisub.yaml" --force-clean --install-deps-from="flathub"
```

### Test

```
$ flatpak-builder --run "build" "org.aegisub.Aegisub.yaml" "sh"
```

### Test run

```
$ flatpak-builder --run "build" "org.aegisub.Aegisub.yaml" "aegisub"
```

### Create repo

```
$ flatpak-builder --repo="repo" --force-clean "build" "org.aegisub.Aegisub.yaml"
```

### Install

```
$ flatpak --user remote-add --no-gpg-verify "aegisub" "repo"
```

```
$ flatpak --user install "aegisub" "org.aegisub.Aegisub"
```

### Run

```
$ flatpak run "org.aegisub.Aegisub"
```

### Uninstall

```
$ flatpak --user uninstall "org.aegisub.Aegisub"
```

```
$ flatpak --user remote-delete "aegisub"
```

### Build single-file bundle

```
$ flatpak build-bundle "repo" "aegisub.flatpak" "org.aegisub.Aegisub" --runtime-repo="https://flathub.org/repo/flathub.flatpakrepo"
```

### Install single-file bundle

If you have already [installed](#install) the package, you have to [uninstall](#uninstall) it before continuing.

```
$ flatpak --user install "aegisub.flatpak"
```

See also:
* [Building your first Flatpak](http://docs.flatpak.org/en/latest/first-build.html)
* [Single-file bundles](http://docs.flatpak.org/en/latest/single-file-bundles.html#single-file-bundles)

## FAQ

### Why not a RPM package?

I already provided [COPR repo](https://copr.fedorainfracloud.org/coprs/scx/aegisub) with (S)RPM packages for EL.

### Are you the author of Aegisub?

No, I only created the flatpak package for it.

See also:

* [GitHub repo](https://github.com/Aegisub/Aegisub)

