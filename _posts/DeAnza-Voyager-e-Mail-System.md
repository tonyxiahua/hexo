---
title: DeAnza Voyager e-Mail System
date: 2016-11-16 02:53:27
tags:
---
这里有一些本校的linux系统的操作还有基本功能的介绍，由于本资料都是没有整理过的，还请大家各取所需。

Session 1:

2.$ mesg y

4.$ talk ibobm
[Connection established]
I offered to 'talk' first, but i needed your response.

5.Used ctrl^c for a polite exit
[1]+  Stopped                 talk ibobm

6.$ write ibobm
write: ibobm is logged in more than once; writing to pts/52

Message from ibobm@voyager.deanza.edu on pts/52 at 18:34 ...
can you see this?
yes i can
Are you still there?
yes i am
just recovered a file

7.Yes, because if there is anything typed afterwards. If the session is not closed, then one cannot enter commands or expressions.
<!-- more -->
Session 2:

2.$ mkdir Ch7S2OutGoMail

3.$ mkdir Ch7S2InComMail

4.$ mail rigodom tee Ch7S2OutGoMail/OutMail1
Subject: Hello Rigo
This is an attempt to mail myself and also save this file in a directory.

5.&3

6.&s Ch7S2InComMail/InMail1

7.&x

8.$ echo $MAIL
/var/spool/mail/rigodom

9.$ more /var/spool/mail/rigodom
From MAILER-DAEMON Mon Nov  7 19:20:59 2011
Date: 07 Nov 2011 19:20:59 -0800
From: Mail System Internal Data <MAILER-DAEMON@voyager.deanza.edu>
Subject: DON'T DELETE THIS MESSAGE -- FOLDER INTERNAL DATA
Message-ID: <1320722459@voyager.deanza.edu>
X-IMAP: 1320722190 0000000001
Status: RO

This text is part of the internal format of your mail folder, and is not
a real message.  It is created automatically by the mail system software.
If deleted, important folder data will be lost, and it will be re-created
with the data reset to initial values.

From rigodom@voyager.deanza.edu  Wed Nov 16 15:15:17 2011
Return-Path: <rigodom@voyager.deanza.edu>
Received: from voyager.deanza.edu (localhost.localdomain [127.0.0.1])
        by voyager.deanza.edu (8.13.8/8.13.8) with ESMTP id pAGNFHgE026385;
        Wed, 16 Nov 2011 15:15:17 -0800
Received: (from rigodom@localhost)
        by voyager.deanza.edu (8.13.8/8.13.8/Submit) id pAGNFHHu026384;
        Wed, 16 Nov 2011 15:15:17 -0800
Date: Wed, 16 Nov 2011 15:15:17 -0800
From: Dominguez Rigoberto  <rigodom@voyager.deanza.edu>
Message-Id: <201111162315.pAGNFHHu026384@voyager.deanza.edu>
To: Ch7S2OutGoMail/OutMail1@voyager.deanza.edu, rigodom@voyager.deanza.edu,
        tee@voyager.deanza.edu
Subject: Hello Rigo
Status: O

10.$ mail
No mail for rigodom

14.$ find mbox
mbox

15.$ more mbox
   Yes i can see the email i sent to myself.

16.$ lpr Ch7S2OutGoMail/OutMail1 Ch7S2InComMail/InMail1 mbox /var/spool/mail/rigodom

Session 3:

2.$ ssh rigodom@voyager

3. Internet access.
    email address     : yourloginname@voyager.deanza.edu
    ssh address       : voyager.deanza.edu
    sftp address      : voyager.deanza.edu

4.$ pwd
4.$ pwd
/home/student/rigodom

5.$ mkdir MadeFromRemote

6.$ vi MadeFromRemote/RemoteFile

7.$ logout
Connection to voyager.deanza.edu closed.

8.$ pwd
/home/student/rigodom

9.$ more MadeFromRemote/RemoteFile
THIS IS A TEST TO SEE IF SSH WORKED!!!

10. yes. everything's the same. There is no need for this because we are already
    in a secure shell. So it's unneccesary.
Session 4:

2.$ cat > LocalFile

3.$ sftp rigodom@voyager
Connecting to voyager...

4.sftp> put LocalFile rigodom@voyager
Uploading LocalFile to /home/student/rigodom/rigodom@voyager
LocalFile                                          100%    5     0.0KB/s   00:00

5.sftp> get LocalFile rigodom@voyager RemoteFileCopy
Fetching /home/student/rigodom/LocalFile to rigodom@voyager
/home/student/rigodom/LocalFile                    100%    5     0.0KB/s   00:00

6.sftp> rm MadeFromRemote/RemoteFile
Removing /home/student/rigodom/MadeFromRemote/RemoteFile

7.sftp> quit

8.$ pwd
/home/student/rigodom

9.$ more MadeFromRemote/RemoteFile
MadeFromRemote/RemoteFile: No such file or directory
$ more MadeFromRemote/RemoteFileCopy
MadeFromRemote/RemoteFileCopy: No such file or directory

They don't exist. This because it DID delete the file when the command was place, but
any file created in this Unsecure Shell, was not saved.


