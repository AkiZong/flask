# P4 Triggers


### The p4 triggers command has a very simple syntax:
~~~
p4 triggers [ -i | -o ]
~~~

- With no flags, the user's editor is invoked to specify the trigger definitions.
- The -i flag reads the trigger table from standard input.
- The -o flag displays all the trigger definitions stored in the trigger table.

### Execution environment
- any p4 commands invoked from within the script will run within a different environment (P4USER, P4CLIENT, and so on) than that of the calling user
~~~
export P4USER=george
export P4PASSWD=abracadabra
cd /home/pforce/database

p4 admin checkpoint
ls -l checkpoint.* journal*
~~~
- For path names that contain spaces, use the short path name.
~~~
For example, C:\Program Files\Perforce\p4.exe is most likely located in C:\PROGRA~1\Perforce\p4.exe.
~~~

### Multiple submit triggers of different types that fire on the same path fire in the following order
- change-submit (fired on changelist submission, before file transmission)
- change-content triggers (after changelist submission and file transmission)
  - Change-content triggers can access file contents by using the p4 diff2, p4 files, p4 fstat, and p4 print commands with the @=change revision specifier
- change-commit triggers (on any automatic changelist renumbering by the server)

### form triggers of different types are fired in the following order
- form-out (form generation)
- form-in (changed form is transmitted to the server)
- form-save (validated form is ready for storage in the Perforce database)
- form-delete (validated form is already stored in the Perforce database)

