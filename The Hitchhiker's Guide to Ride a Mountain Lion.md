![](http://media.tumblr.com/tumblr_m7p8rzVYgu1qcfyao.jpg)

Earlier today, [OS X Mountain Lion][OS X Mountain Lion] has been released for
all users from the Mac App Store. I know that a lot of you have been anticipated
for this release, and very excited that it's finally came out. As I'm in a [Mac
Developer Program][Mac Developer Program], I have decided to ride on this new
cat early, and gave this new OS a try since the Developer Preview 4, up until
the [Golden Master][Golden Master] release. Today, I'd like to share you some
rough edges that I have found using this shiny new operating system.

Word of the Wise: Backup Your System
-----------------------------------------------
Before performing an upgrade, always make sure that you have the latest backup
of your Mac. If you already have your [Time Machine][Time Machine] setup, this
will be easy for you. All you need to do is click on the Time Machine icon on
your menu bar, then click "Back Up Now" to trigger the backup. After it's done,
to make sure that your backup is really going to work if something goes wrong,
Hold the Option (⌥) key and click on the Time Machine icon again, then click on
"Verify Backups" menu. If everything is working perfectly, you should not get
any error message after the verification is done.

If you have been living in an adventurous life, and did not set a Time Machine
backup for your Mac, I would suggest you to use a third party software called
[Carbon Copy Cloner][CCC]. You can use this software to clone and backup your
hard drive to an external drive. It will also give you an option to copy a
recovery partition from your boot drive, and making your external hard drive
bootable. (Still, I would suggest you to setup a Time Machine after you upgrade
to Mountain Lion.)

For myself, I did use both Time Machine and Carbon Copy Cloner to backup my
system, as I had a spare external hard drive and I wanted to be able to fully
boot back to my Lion in case something went wrong. If you have a spare external
hard drive, doing a drive clone would be a good idea as well. It took me only
1/2 hour to clone a 500GB drive to an external USB drive. Having multiple sets
of backup never hurts, for a peace of mind™.

Application Compatibility
-----------------------------
As with other release of the Mac OS X, some of the applications might not be
compatible with OS X Mountain Lion. I would suggest you to search for your
frequently used applications on [RoaringApps][RoaringApps] to see if there's any
compatibility issue up there. If the application that you require for work does
not work in OS X Mountain Lion yet, I'd suggest you to wait for the developers
to release an updated version first before you upgrade your system. 

However, if you're using any application that were written for
[PowerPC][PowerPC] architecture that requires [Rosetta][Rosetta] to run, I'd
have to tell you to kiss those application good bye, as Apple has completely
removed Rosetta support from the operating system.

If you are using any application that uses [X11][X11], such as [Divvy][Divvy],
Apple has dropped support for X11 as well, but you will still be able to install
X11 from external source. Read the post-upgrade section for more detail.

The Upgrade Process
-------------------------
On my 15" 2010 Macbook Pro with SSD, the whole upgrade process took me about 45
minutes to get everything install after I downloaded a 4GB installer from the
Mac App Store. It was very simple and straightforward, as the installer will do
everything for you and reboot back to OS X after it's done. I'd recommend you to
do this on Saturday before you going out to have lunch. At the time you're back,
Mountain Lion will roar and waiting for you.

Post-Upgrade Cleanup
---------------------------
Congratulations! Now you've completed the upgrade process for a normal user.
However, for us developers that need to compile [Ruby][Ruby] using [RVM][RVM] or
[rbenv][rbenv], or install any application using [Homebrew][Homebrew], it would
be only the half way. So, please hold on to your champagne for now.

### Getting Xcode + Command Line Tools Install

You can find the Xcode in the Mac App Store. You'll need at least version 4.4 of
Xcode for it to work with OS X Mountain Lion. It should be available after OS X
Mountain Lion is in the Mac App Store.

After the installation, open up Xcode in your `/Applications` folder. You'll
then go to Xcode -> Preferences menu on the top, then go to Downloads tab. Click
"Install" on the "Command Line Tools." After you're done, quit Xcode and fire up
Terminal.

### Fix Homebrew + install GCC

After the upgrade, Apple will set the ownership of your `/usr/local` folder to
root. You can easily fix this by:

    sudo chown -R `whoami` /usr/local

Next, let's update Homebrew to make sure that we have everything we need:

    brew update

If you need to install any Ruby that's older than 1.9.3, such as 1.9.2, 1.8.7 or
REE, you'll then need to install GCC 4.2. Apple does not ship the Command Line
Tools with `gcc-4.2` compiler anymore (you can try by run `which gcc-4.2`) so
you need to install it via Homebrew. By default, Homebrew doesn't include any
formular that ships with the OS in the main repository, so you'll have to enable
[homebrew-dupes][homebrew-dupes] repository by using `brew tap`

    brew tap homebrew/dupes
    brew install apple-gcc42

Voila! Now you can compile any library that requires non-LLVM GCC.

### Reinstall X11

Now, if you're still using some application that depends on X11, such as
[Wine][Wine] or [gitk][gitk], you'll need to install X11 as well. Apple has
[already removed X11 support][apple remove x11] from their operating system, but
you still can get the X11 package from [XQuartz][XQuartz]. I've been using their
2.7.2 release, and it's working fine for me.

### Growl

If you're using Growl and set the notification location to your top right,
you'll soon notice that your Growl notification actually lays on top of the
Notification Center notifications. The only workarounds I could find now is to
have them put up the notification on the different corner. Low and behold, Growl
developers are [still working][growl notification center] to streamline the
notification and send them to the notification center for you.

ROAR!!!
---------
Finally, your developer machine has been upgraded to OS X Mountain Lion. I hope
you'll enjoy it's [features] as I do. Feel free to let me know if I should add
anything else. Happy coding!

[OS X Mountain Lion]: http://www.apple.com/osx
[Mac Developer Program]: https://developer.apple.com/programs/mac
[Golden Master]: http://en.wikipedia.org/wiki/Golden_master
[Time Machine]: http://www.apple.com/osx/apps/#time-machine
[CCC]: http://www.bombich.com
[RoaringApps]: http://roaringapps.com
[PowerPC]: http://en.wikipedia.org/wiki/PowerPC
[Rosetta]: http://en.wikipedia.org/wiki/Rosetta_(software)
[X11]: http://en.wikipedia.org/wiki/X11.app
[Divvy]: http://mizage.com/divvy
[Ruby]: http://ruby-lang.org
[RVM]: https://rvm.io/
[rbenv]: https://github.com/sstephenson/rbenv
[Homebrew]: http://mxcl.github.com/homebrew
[homebrew-dupes]: https://github.com/Homebrew/homebrew-dupes
[Wine]: http://www.winehq.org
[gitk]: http://www.kernel.org/pub/software/scm/git/docs/gitk.html
[apple remove x11]: http://www.macrumors.com/2012/02/17/apple-removes-x11-in-os-x-mountain-lion-shifts-support-to-open-source-xquartz
[XQuartz]: http://xquartz.macosforge.org/landing
[growl notification center]: http://growl.posterous.com/going-forward-with-growl-and-notification-cen
[features]: http://www.apple.com/osx/whats-new
