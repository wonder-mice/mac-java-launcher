mac-java-launcher
=================

Launcher for bundled java applications on Mac OS

Usage is simple:

```bash
$ git clone https://github.com/wonder-mice/mac-java-launcher.git mac-java-launcher.git
$ cd mac-java-launcher.git
$ ./use --apply "/Applications/IntelliJ IDEA 12 CE.app" --java-version "1.6+" 
```

This command will:

1.  Backup original `Info.plist` to `Info.plist.original`

2.  Copy `launcher` script to `AppBundle.app/Contents/MacOS/mac-java-launcher`

3.  Remove "Java" (or "JVMOptions")  section from `Info.plist`

4.  Set "CFBundleExecutable" in `Info.plist` to `mac-java-launcher`

5.  Set "JVMVersion" in `Info.plist.original` to `1.6+`

Also, it is easy to restore original launcher:

```bash
$ ./use --undo "/Applications/IntelliJ IDEA 12 CE.app" --java-version "1.6*"
```

This command will revert previous one. "--java-version" is optional in both cases,
however "--undo" doesn't revert java version change by itself.

Changing Only the JDK Version
=============================

Many newer `.app` bundles do not require the `launcher` script to work, such as
`IntelliJ IDEA 13.x`. However, these applications may still require an earlier
version of Java to be installed (e.g., JDK 1.6).

In such cases, the `Info.plist` needs to have its `JVMVersion` updated. IntelliJ
IDEA 13.x has a value of `1.6*`, which _requires_ a release of JDK 1.6 to be
installed. However, changing it to `1.6+` allows it to work with JDK 1.6 and
newer.

```bash
$ ./use --java-version "1.6+" "/Applications/IntelliJ IDEA 13.app"
```

This command will:

1. Change the `JVMVersion` to `1.6+` from the default `1.6*` and allow IntelliJ
IDEA 13 to work JDK 1.6, JDK 1.7, or JDK 1.8.

About
=====

Mac OS launcher for bundled java applications requires JDK 1.6 to be installed.
And even if application itself requires only JDK 1.7 you will still need to
install JDK 1.6 -- just to satisfy the application launcher. You can see this
issue, for example, with `IntelliJ IDEA` or `yEd` after changing
"JVMVersion" in Info.plist to `1.6+` (not the case for newer releases of IDEA).

If you would like to require a specific JDK release, such as JDK 1.7, then you
can change the value to `1.7*`. If you would like to allow for any release
_after_ a specific release, such as JDK 1.7, then you can specify the value with
a `+`--like `1.7+`--to allow any JDK to be used _starting_ with that relase and
up (e.g., JDK 1.8 would also work).

`mac-java-launcher` replaces the default launcher shipped with the application
and `mac-java-launcher` requires no JDK by itself (it will replace launcher only
for single application specified in command line argument). After that, only the
JDK version actually required by application must be installed.

`mac-java-launcher` uses the "Java" section from `Info.plist.original` when
launching application. If you want, for example, change "JVMVersion" from
`1.6*` to `1.6+` you can do it in `Info.plist.original`. Also, that can be
done with "--java-version" option.
