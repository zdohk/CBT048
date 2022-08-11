~~~~~~~~~~~~~~~~

//***FILE 048 is a pds which contains the LISTVOL and LISTSPC       *   FILE 048
//*           TSO commands, and it contains the LOCINDEX            *   FILE 048
//*           subroutine, which they both need.  Both commands      *   FILE 048
//*           have been "modernized" somewhat (see below for        *   FILE 048
//*           details as to how).                                   *   FILE 048
//*                                                                 *   FILE 048
//*           HELP data for both commands is also contained in      *   FILE 048
//*           this file.  These programs used to exist in separate  *   FILE 048
//*           files on the tape (since 1976 or so), and now these   *   FILE 048
//*           files have been combined into one file.               *   FILE 048
//*                                                                 *   FILE 048
//*      email:  sbgolob@cbttape.org                                *   FILE 048
//*                                                                 *   FILE 048
//*       Modifications:                     (S.Golob 2006/Jan 04)  *   FILE 048
//*                                                                 *   FILE 048
//*       1.  IBM standard macro YREGS was inserted in the code     *   FILE 048
//*           of both programs instead of the EQUATE macro, for     *   FILE 048
//*           easier assembly.  Sample assembly JCL added.          *   FILE 048
//*                                                                 *   FILE 048
//*       2.  The GETMAIN in LOCINDEX was doubled.  I don't know    *   FILE 048
//*           if this is SUPPOSED to work, but it did.  More        *   FILE 048
//*           datasets can now be displayed.  (Now perhaps 800.)    *   FILE 048
//*                                                                 *   FILE 048
//*       3.  All TPUTs were converted to PUTLINE using Howard      *   FILE 048
//*           Dean and Jim Elsworth's method of doing the PUTLINE   *   FILE 048
//*           setup in an external module called EPUTL and calling  *   FILE 048
//*           EPUTL with a macro called APUT that has the same      *   FILE 048
//*           coding rules as a single line TPUT.                   *   FILE 048
//*                                                                 *   FILE 048
//*       4.  To take advantage of the PUTLINE outputs, two REXX    *   FILE 048
//*           execs called TSOE and TSOB from Mark Zelden were      *   FILE 048
//*           included to trap the SYSOUT output.  TSOE will ISPF   *   FILE 048
//*           Edit the trapped output, and TSOB will ISPF Browse    *   FILE 048
//*           it.  TSOV (made by me) will ISPF View it.             *   FILE 048
//*                                                                 *   FILE 048
//*       Output Samples:                                           *   FILE 048
//*                                                                 *   FILE 048
//*       (Note that DSAT from File 296 gives combined outputs      *   FILE 048
//*        from these two, using one command.  In DSAT, the         *   FILE 048
//*        space and volume serial information is combined in       *   FILE 048
//*        one command.  However, the DSAT width is greater than    *   FILE 048
//*        80 characters wide in output.  DSAT also includes DCB    *   FILE 048
//*        attributes of the datasets.)                             *   FILE 048
//*                                                                 *   FILE 048
//*   From LISTVOL:       LISTVOL LEV(IBMUSER)                      *   FILE 048
//*                                                                 *   FILE 048
//*       VOLUME  DATASET NAME                                      *   FILE 048
//*         VPMVSH  IBMUSER.B.ASM                                   *   FILE 048
//*         DATA05  IBMUSER.BDM.I130.LOAD                           *   FILE 048
//*         DATA05  IBMUSER.BDM.I130.OBJ                            *   FILE 048
//*         DATA05  IBMUSER.BDM.I138.CNTL                           *   FILE 048
//*         WORK05  IBMUSER.BDM.I138.LOAD                           *   FILE 048
//*         WORK04  IBMUSER.BDM.I138.OBJ                            *   FILE 048
//*         DATA05  IBMUSER.BDM.SYSPRINT                            *   FILE 048
//*         DATA05  IBMUSER.BDM.SYSPRINT.IEWL                       *   FILE 048
//*         WORKA4  IBMUSER.BRODCAST                                *   FILE 048
//*         WORK07  IBMUSER.CBT487.FILE185.TEST                     *   FILE 048
//*         WORKE3  IBMUSER.CCKD.ASM                                *   FILE 048
//*         WORK08  IBMUSER.CCKD.ASM.XMI                            *   FILE 048
//*         WORKE3  IBMUSER.CCKD.BZLIB.C                            *   FILE 048
//*         WORKE3  IBMUSER.CCKD.BZLIB.H                            *   FILE 048
//*                                                                 *   FILE 048
//*   From LISTSPC:       LISTSPC LEV(IBMUSER)                      *   FILE 048
//*                                                                 *   FILE 048
//*       DSORG ALLOC UNUSED EXTENTS DSNAME                         *   FILE 048
//*         PO  10943    790     1   IBMUSER.B.ASM                  *   FILE 048
//*         PS     15     15     1   IBMUSER.BDM.I130.LOAD          *   FILE 048
//*         PS     15     15     1   IBMUSER.BDM.I130.OBJ           *   FILE 048
//*         PS     15     15     1   IBMUSER.BDM.I138.CNTL          *   FILE 048
//*         PO     15     13     1   IBMUSER.BDM.I138.LOAD          *   FILE 048
//*         PS     15     14     1   IBMUSER.BDM.I138.OBJ           *   FILE 048
//*         PS     15     15     1   IBMUSER.BDM.SYSPRINT           *   FILE 048
//*         PS     15     15     1   IBMUSER.BDM.SYSPRINT.IEWL      *   FILE 048
//*         PS      1      1     1   IBMUSER.BRODCAST               *   FILE 048
//*         PO     59     14     1   IBMUSER.CBT487.FILE185.TEST    *   FILE 048
//*         PO     65      1    14   IBMUSER.CCKD.ASM               *   FILE 048
//*         PS     18     10     1   IBMUSER.CCKD.ASM.XMI           *   FILE 048
//*         PO      7      3     1   IBMUSER.CCKD.BZLIB.C           *   FILE 048
//*         PO      2      1     1   IBMUSER.CCKD.BZLIB.H           *   FILE 048
//*                                                                 *   FILE 048
~~~~~~~~~~~~~~~~

