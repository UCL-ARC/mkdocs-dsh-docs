---
title: Troubleshooting
categories:
 - User Guide
layout: docs
---

# Troubleshooting

This page lists some common problems encountered by users, with methods to investigate or solve them.

### Why is my job in Eqw status?

If your job goes straight into Eqw state, there was an error in your
jobscript that meant your job couldn't be started. The standard `qstat`
job information command will give you a truncated version of the error:

```
qstat -j <job_ID>
```

The most common reason jobs go into this error state is that 
a file or directory your job is trying to use doesn't exist.
Creating it after the job is in the `Eqw` state won't make the job
run: it'll still have to be deleted and re-submitted.


### "/bin/bash: invalid option" error

This is a sign that your jobscript is a DOS-formatted text file and not
a Unix one - the line break characters are different. Type `dos2unix
<yourscriptname>` in your terminal to convert it.

Sometimes the offending characters will be visible in the error. You can
see here it's trying to parse `^M` as an option.


### Which MKL library files should I use to build my application?

Depending on which whether you wish to use BLAS/LAPACK/ScaLAPACK/etc...
there is a specific set of libraries that you need to pass to your
compilation command line. Fortunately, Intel have released a tool that
allows you to determine which libraries to link and in which order for a
number of compilers and operating systems:

<http://software.intel.com/en-us/articles/intel-mkl-link-line-advisor/>

### What can I do to minimise the time I need to wait for my job(s) to run?

1.  Minimise the amount of wall clock time you request.
2.  Use job arrays instead of submitting large numbers of jobs (see our
    [job script examples](../Example_Jobscripts.md)).
3.  Plan your work so that you can do other things while your jobs are
    being scheduled.


