---
---
---
**Links**: [[104 Linux Index]]

---
## Good old packages
- `.deb` → used by debian and its derivatives like ubuntu.
- `.rpm` → red hat, fedora, opensuse and their derivatives.
- These contain the **binary version of the app**. There is *no source code*. 
- It is just *precompiled version of the application*. 
- It is compiled depending on the architecture of your system like arm, x86 etc.
- These come with a descriptor file inside the package which lets the system know which *libraries it needs* since these packages only package the application. *These repositories are then fetched at install*.
- Some problems with these packages are that the *developer needs to package the application for various distributions*.

> [!important] Snap, AppImage, and Flatpak, all *distro independent*

### Flatpak:

It is also the binary version of the application i.e. they are also precompiled. But they ship with their own subset of libraries which means you don't need to rely on system's libraries to run.

Some disadvantages are that they take more disc space. Also since they come with their own libraries it is the developer's job to patch them on a regular basis otherwise there can be security issues.

You can go to go to flathub for downloading flatpaks.

### Snaps:

These are also binaries with all the libraries included. It is not really open. The snaps are available at snapcraft which is owned by canonical and they decide what goes in the store. They are bigger than flatpaks. They are mostly available on ubuntu and some ubuntu based distributions.

-   Different parts of a snap
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4fc1006d-1da8-4d5e-b615-eb4b8e121fdd/Untitled.png)
    

### Appimages:

They ship the whole application in one package. They ship the binaries, the run time and other things. This means you just need to download the file and click on it to start it. No need to install anything.

---

An app is no longer maintained but users still want to install it on modern systems. In that case, I think it makes sense to "preserve" the app as something completely self-contained & guaranteed to run like an AppImage, so the developer never has to touch it again but users who want it can keep using it forever.

Flatpaks, appimages and snaps are also known as universal packaging systems.