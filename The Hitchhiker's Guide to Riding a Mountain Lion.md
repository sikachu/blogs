![](http://media.tumblr.com/tumblr_m7p8rzVYgu1qcfyao.jpg)

Earlier today, [OS X Mountain Lion][OS X Mountain Lion] was released for all
users in the Mac App Store. As a member of the [Mac Developer Program][Mac
Developer Program], I decided to tame this wild cat early on, jumping on the
beta tester bandwagon since the Developer Preview 4. Here are some of the
things you should consider as you make the switch to this shiny new operating
system.

The Upgrade Process
-------------------------
After I downloaded the 4GB installer from the Mac App Store, the whole upgrade
process took me about 45 minutes on my 15" 2010 Macbook Pro with an SSD drive.
It was a simple and straightforward process as the installer takes care of
everything.

Once the installer is done, we need to do some additional work to get up to
speed once again and be able to compile [Ruby][Ruby] (using [RVM][RVM] or
[rbenv][rbenv]) or install packages using [Homebrew][Homebrew]. Hold on to your
champagne for now.

### Getting Xcode + Command Line Tools Installed

You can get Xcode from the Mac App Store. You'll need at least version 4.4 of
Xcode for it to work with OS X Mountain Lion. After the installation, open up
Xcode in your `/Applications` folder. You'd want to go to Xcode -> Preferences
-> Downloads tab then install the "Command Line Tools." After you're done, quit
Xcode and fire up Terminal.

### Fix Homebrew + install GCC

After the upgrade, Apple will set the ownership of your `/usr/local` folder to
root. You can easily fix this by running this command in Terminal:

    sudo chown -R `whoami` /usr/local

Next, you need to update Homebrew:

    brew update

If you need to install any Ruby that's older than 1.9.3, such as 1.9.2, 1.8.7
or REE, you'll need to install GCC 4.2. Apple does not ship the Command Line
Tools with `gcc-4.2` compiler anymore (you can check by running `which
gcc-4.2`), so you need to install it via Homebrew. By default, Homebrew doesn't
include any formula that ships with the OS in the main repository, so you'll
have to enable [homebrew-dupes][homebrew-dupes] repository by using `brew tap`

    brew tap homebrew/dupes
    brew install apple-gcc42

Voila! Now you can compile any library that requires non-LLVM GCC.

### Reinstall X11

Now, if you're still using some application that depend on X11, such as
[Divvy][Divvy] or [gitk][gitk], you'll need to install X11 as well. Apple has
[already removed X11 support][apple remove x11] from their operating system,
but you can still get the X11 package from [XQuartz][XQuartz]. I've been using
their 2.7.2 release, and it's working fine for me.

Word to the Wise: Backup Your System
-----------------------------------------------
Before performing any major upgrade, always make sure that you have the latest
backup of your Mac. If you already have [Time Machine][Time Machine] set up,
all you need to do is click its icon on the menu bar, then choose "Back Up Now"
to start backing up your system. Once done, make sure your backup is working by
holding the Option (⌥) key while the Time Machine menubar drop down is visible,
then clicking the new "Verify Backups" menu item. Ensure you don't have any
error messages at the end of the verification process.

If you have been leading a carefree life and did not bother setting up Time
Machine, I would suggest using [Carbon Copy Cloner][CCC]—a third party
application—to clone your internal hard drive to an external one. CCC will not
only make the backup bootable, but will also take care of cloning the hidden
recovery partition in your boot drive, may you choose this option in the
settings. When all's said and done, I would still recommend setting up Time
Machine once you upgrade to Mountain Lion.

If you have a spare external hard drive, consider keeping a bootable
installation of Lion—even after the upgrade—in case something goes wrong. It
took me only half an hour to clone a 500GB drive to an external USB drive.

ROAR!!!
---------
Finally, your developer machine has been upgraded to OS X Mountain Lion. I hope
you'll enjoy the [new features][features] as much I do. Happy coding!

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
