mac-java-launcher
=================

Launcher for bundled java applications on Mac OS

Mac OS launcher for bundled java applications requires jdk 1.6 to be installed.
And even if application itself requires only jdk 1.7 you will still need to
install jdk 1.6 - just to satisfy application launcher. You can see this
issue, for example, with IntelliJ IDEA 12 and IntelliJ IDEA 13 after changing
"JVMVersion" in Info.plist to "1.7\*"

**mac-java-launcher** replaces launcher shiped with the application and requires
no jdk by itself (it will replace launcher only for single application
specified in command line argument). After that, only jdk version required by
application must be installed.

Usage is simple:
```bash
$ cd mac-java-launcher.git
$ ./use --apply "/Applications/IntelliJ IDEA 12 CE.app"
```

This command will:

1.  Backup original _Info.plist_ to _Info.plist.original_

2.  Copy _launcher_ to _Bundle.app/Contents/MacOS/mac-java-launcher_

3.  Remove "Java" section from _Info.plist_

4.  Set "CFBundleExecutable" in _Info.plist_ to _mac-java-launcher_

**mac-java-launcher** uses "Java" section from _Info.plist.original_ when
launching application. If you want, for example, change "JVMVersion" from
"1.6\*" to "1.7\*" you can do it in _Info.plist.original_.

Also, it is easy to restore original launcher:
```bash
$ cd mac-java-launcher.git
$ ./use --undo "/Applications/IntelliJ IDEA 12 CE.app"
```
