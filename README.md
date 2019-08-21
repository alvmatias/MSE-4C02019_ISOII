# MSE-4C02019_ISOII

#### Pasos para armar una distribucion con Yocto Project:

> Instalar los siguientes paquetes con el comando:
sudo apt install bc build-essential chrpath cpio diffstat gawk git python texinfo wget

> Bajar yocto, posicionarse en la rama de la version  19.0.0 y aplicar el parche de no incluir meta-yocto-bsp(presente en este repositorio):
git clone git://git.yoctoproject.org/poky.git
cd $HOME/yocto/poky
git checkout -b sumo-19.0.0 sumo-19.0.0
git am $HOME/yocto/0001-bblayers-do-not-include-meta-yocto-bsp.patch

> Descargar la layer de TI y aplicar los parches correspondientes(presentes en este repositorio):
cd $HOME/yocto/
git clone git://git.yoctoproject.org/meta-ti.git
cd $HOME/yocto/meta-ti
git checkout -b sumo ti2018.02
git am $HOME/yocto/0001-Simplify-linux-ti-staging-recipe.patch
git am $HOME/yocto/0002-do-not-use-base_read_file.patch
git am $HOME/yocto/0003-recipes-bsp-u-boot-fix-non-booting-U-Boot.patch
git am $HOME/yocto/0004-fix-bitbake-warnings.patch

> Exportar todas las variables de entorno necesarias y setear el build environment:
cd $HOME/yocto
source poky/oe-init-build-env

> Modificar bblayers.conf y local.conf con los archivos de este repositorio

> Compilar:
bitbake core-image-minimal

> Chequear los archivos de salida de la compilacion en $BUILDDIR/tmp/deploy/images/
beaglebone.

#### Pasos para crear una layer y una recipe de un Hello World

> Crear una layer meta-custom:
bitbake-layers create-layer meta-custom

> Modificar los archivos layer.conf y example.bb(recipe de Hello World) con los presentes en el repositorio
