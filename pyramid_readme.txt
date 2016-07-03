1.follow SailfishOS hadk-1.1.2: setup sdk, etc., stop on page 15, when 'repo init'm read it but don't run commands
2.repo init -u git://github.com/mer-hybris/android.git -b hybris-12.0
3.use the pyramid.xml inplace $ANDROID_ROOT/.repo/local_manifests/$DEVICE.xml:
4.repo sync --fetch-submodules
if experience any problems, refere to hadk 5.5 Common Pitfalls

source build/envsetup.sh
export USE_CCACHE=1
breakfast $DEVICE
make -j4 hybris-hal

if you experience fstab warnings breaking make process, the command
find -name *.fstab -exec 'rm or mv somewhere' {} \;
should fix them.
I did rm device/htc/pyramid/recovery/root/etc/twrp.fstab
and later deleted one more fstab.

6.proceed with chapter 6. SETTING UP SCRATCHBOX2 TARGET.
7.skip to 7.2.1 Building the droid-hal-device packages,
as all repositories already were created and added to pyramid.xml in local_manifests.
8.continue with hadk.

I had a errors while building the image, so if nothing helps, try this:
HA_REPO1="repo --name=common  \
--baseurl=$MOBS_URI/nemo:/devel:/hw:/common/sailfish_latest_@ARCH@/"
sed -i -e "/^$HA_REPO.*$/a$HA_REPO1" tmp/Jolla-@RELEASE@-$DEVICE-@ARCH@.ks 
then mic create, as in hadk, and build.
