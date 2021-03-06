# Ghidraal

A Ghidra extension for scripting with GraalVM languages, including Javascript, Python3, R, and Ruby.

## setup

GraalVM is a drop in replacement for OpenJDK with some extra powers.

**Ghidraal will only work when Ghidra is run within a GraalVM!!!**


1. download GraalVM (20.1+) and set up set `JAVA_HOME`, `PATH`, etc.  You can
   copy and source [env.sh](/env.sh) for a hopefully painless install, e.g.
    ```
    mkdir ~/graalvm
    cp env.sh ~/graalvm
    cd ~/graalvm
    . env.sh
    ```

2. build or download
    - to build, you'll need gradle 5.  Create a symlink to your Ghidra
      installation and run gradle.  The extension will be generated in `dist`,
      e.g.
        ```bash
        # in the directory containing your checkout of this repo 
        ln -s ~/ghidra_9.1.2_PUBLIC ghidra
        . ~/graalvm/env.sh # must build with Graal available
        gradle
        ls dist/
        ```
    - or download a [release](/../../releases)

3. copy the zip file to Ghidra's extension directory, e.g.
    ```bash
    cp ghidra_9.1.2_PUBLIC_20200428_Ghidraal.zip ~/ghidra_9.1.2_PUBLIC/Extensions/Ghidra/
    ```
4. Run ghidra with GraalVM and install the extension
    ```bash
    . ~/graalvm/env.sh
    ~/ghidra_9.1.2_PUBLIC/ghidraRun
    ```
    From the main window, select `File->Install Extensions...`, check `Ghidraal` and restart Ghidra.

5. Open a program, select `File->Configure...` under `Experiment`, select
   `Configure`, and check `GhidraalPlugin`.  Restart Ghidra to register new
   language providers.

## usage

There are some extremely basic scripts for each supported language in the
[ghidra_scripts](/ghidra_scripts) directory.  When the extension is installed,
they should become visible in the Script Manager.

An interactive console for each language is available under the code browser "Window"
menu option.

Note: Ghidraal hijacks the `.py` extension by unloading the Jython script
provider!  Disable `GhidraalPlugin` to reenable Jython.

Note: Ghidra's built in Python scripts are Python 2, so won't work with Ghidraal's Python 3.  Some
can be ported automatically with `2to3`.



# changelog

- ghidraal-0.0.2
    - added interactive consoles
    - made basic.py like the other basic scripts
- ghidraal-0.0.1
    - initial
