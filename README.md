mac-java-launcher
=================

Launcher for bundled java application on Mac OS

Mac OS launcher for bundled java applications requires jdk 1.6 to be installed.
And even if application itself requires only jdk 1.7 you will still need to
install jdk 1.6 - just to satisfy application launcher. You can see this
issue, for example, with IntelliJ IDEA 12 and IntelliJ IDEA 13.

mac-java-launcher replaces launcher shiped with the application and requires
no jdk by itself (it will replace launcher only for single application
specified in command line argument).

Usage is simple:
```bash
$ cd mac-java-launcher.git
$ ./use --apply "/Applications/IntelliJ IDEA 12 CE.app"
```
This command will:
# Backup original Info.plist to Info.plist.original
# Copy launcher to Bundle.app/Contents/MacOS/mac-java-launcher
# Remove "Java" section from Info.plist
# Set "CFBundleExecutable" in Info.plist to mac-java-launcher 
