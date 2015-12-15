GYP can Generate Your Projects.
===================================

This fork of the upstream GIT repo at Google has 3 additional features:

1. The xcode generator recognizes the full set of build variables
that correspond to the set of destination names for the copy phase,
as appears in the Xcode UI. Do
 ```
 git diff upstream_master xcode_changes
 ```
 to see the list. The original version only understands
 the variable `$(BUILD_PRODUCTS_DIR)` which corresponds to
 'Products Directory'.

    All GYP xcode tests that pass on upstream_master pass with these
    changes. (There are 5 tests that fail in both cases.)

2. The msvs generator supports the Emscripten vs-tool plug-in.
That is, it recognizes the properties vs-tool offers to
control the Emscripten compiler and linker. These properties
can be included in an `msvs_settings` dictionary. Note this feature
has only been tested with Visual Studio 2010.

    All GYP msvs tests are expected to still pass. That will be tested soon.
    
3. Various changes to the `make` generator to better support generating
projects to build Android native applications. These include additions
to the `make_global_settings` dictionary such as being able to create
 _simply expanded variables_ and to specify a TARGET_ABI. The latter
 becomes a component of `builddir` in the generated make files. They
 also in include changes to the handling of path relativization in
 various cases.
 
    These changes are a work in progress and are known to break several
    of the GYP `make` generator tests.

The first of these has been submitted to Google but they want
tests, that I have not had time to write, before merging. The
same lack of tests prevents submission of the second and third.

To install, clone the repo to your machine and run the following
commands in a shell:
```bash
cd <your_gyp_clone>; sudo ./setup.py install
```
On Windows, use either a Git Bash or Cygwin Bash shell and omit the
`sudo`. Alternatively enter the following commands at a Windows Command
Prompt (`cmd.exe`):
```cmd
cd <your_gyp_clone>
python setup.py install
```

Documents are available at [gyp.gsrc.io](https://gyp.gsrc.io), or you can check out ```md-pages``` branch to read those documents offline.
