mac-java-launcher
=================

Launcher for bundled java applications on Mac OS

Usage is simple:
```bash
$ git clone https://github.com/wonder-mice/mac-java-launcher.git mac-java-launcher.git
$ cd mac-java-launcher.git
$ ./use --apply "/Applications/IntelliJ IDEA 12 CE.app" --java-version "1.7*" 
```

This command will:

1.  Backup original _Info.plist_ to _Info.plist.original_

2.  Copy _launcher_ script to _Bundle.app/Contents/MacOS/mac-java-launcher_

3.  Remove "Java" (or "JVMOptions")  section from _Info.plist_

4.  Set "CFBundleExecutable" in _Info.plist_ to _mac-java-launcher_

5.  Set "JVMVersion" in _Info.plist.original_ to "1.7*"

Also, it is easy to restore original launcher:
```bash
$ ./use --undo "/Applications/IntelliJ IDEA 12 CE.app" --java-version "1.6*"
```

This command will revert previous one. "--java-version" is optional in both cases,
however "--undo" doesn't revert java version change by itself.

About
=====

Mac OS launcher for bundled java applications requires jdk 1.6 to be installed.
And even if application itself requires only jdk 1.7 you will still need to
install jdk 1.6 - just to satisfy application launcher. You can see this
issue, for example, with IntelliJ IDEA or yEd after changing
"JVMVersion" in Info.plist to "1.7\*" (not the case for newer releases of IDEA).

**mac-java-launcher** replaces launcher shiped with the application and requires
no jdk by itself (it will replace launcher only for single application
specified in command line argument). After that, only jdk version required by
application must be installed.

**mac-java-launcher** uses "Java" section from _Info.plist.original_ when
launching application. If you want, for example, change "JVMVersion" from
"1.6\*" to "1.7\*" you can do it in _Info.plist.original_. Also, that can be
done with "--java-version" option.
