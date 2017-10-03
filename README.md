# Flatpak distribution of OpenRCT2
## Setup the build environment
Install Flatpak on your system.
See the [Flatpak homepage](http://flatpak.org/getting.html).
Then you can add the repository at gnome.org which provides different Platforms(run-times) and SDKs:
```
flatpak --user remote-add --from gnome https://sdk.gnome.org/gnome.flatpakrepo
flatpak --user install gnome org.freedesktop.Platform//1.6 org.freedesktop.Sdk//1.6
```

## Run the build
``flatpak-builder`` automates the build using the manifest file ``org.openrct2.OpenRCT2.json``.
The Freedesktop runtime provides all dependencies except ``jansson`` and ``libzip``.
These will be bundled with the Flatpak.
The builder downloads and compiles these two libraries before building OpenRCT2.
```
mkdir fp_build
flatpak-builder --force-clean --repo=my_local_repo fp_build org.openrct2.OpenRCT2.json
```
After the build has completed, the application will be added to the new repository ``my_local_repo``.

## Install the package
Add the repository and install the package:
```
flatpak --user remote-add my_local_repo my_local_repo --no-gpg-verify --if-not-exists
flatpak --user install my_local_repo org.openrct2.OpenRCT2
```
You must update your package after each build to get the new version:
```
flatpak --user update org.openrct2.OpenRCT2
```

## Run the application
You will find a standard desktop entry in your menu. To use the command line do:
```
flatpak run org.openrct2.OpenRCT2
```
