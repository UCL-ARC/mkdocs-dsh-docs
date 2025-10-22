
# Where do my results go?

After submitting your job, you can use the command `qstat` to view the status of all the jobs you have submitted. Once you can no longer see your job on the list, this means your job has completed. There are various ways of monitoring the output of your job.

## Output and error files

When writing your job script you can either tell it to start in the directory you submit it from (`-cwd`), or from a particular directory (`-wd <dir>`), or from your home directory (the default). When your job runs, it will create files in this directory for the job's output and errors:

| File Name | Contents |
|:----------|:---------|
| `myscript.sh` | Your job script. |
| `myscript.sh.o12345` | Output from the job. (`stdout`) |
| `myscript.sh.e12345`  | Errors, warnings, and other messages from the job that aren't mixed into the output. (`stderr`) |
| `myscript.sh.po12345` | Output from the setup script run before a job. ("prolog") |
| `myscript.sh.pe12345` | Output from the clean-up script run after a job. ("epilog") |

Normally there should be nothing in the `.po` and `.pe` files, and that's fine. If you change the name of the job in the queue, using the `-N` option, your output and error files will use that as the filename stem instead.

Most programs will also produce *separate* output files, in a way that is particular to that program. Often these will be in the same directory, but that depends on the program and how you ran it.




