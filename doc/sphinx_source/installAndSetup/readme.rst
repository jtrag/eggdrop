Last revised: May 5, 2021

======
README
======

  Please, at least SKIM this document before asking questions. In fact,
  READ IT if you've never successfully set up an Eggdrop bot before.

------
NOTICE
------

    Make SURE that you select your +n (owner) users wisely. They have 100%
    access to your bot and account. ONLY GIVE THIS POWER TO SOMEONE YOU
    TRUST COMPLETELY!

----------------
What is Eggdrop?
----------------

    Eggdrop is the world's most popular Internet Relay Chat (IRC) bot; it is
    freely distributable under the GNU General Public License (GPL). Eggdrop
    is a feature-rich program designed to be easily used and expanded upon by
    both novice and advanced IRC users on a variety of hardware and software
    platforms.

    An IRC bot is a program that sits on an IRC channel and performs automated
    tasks while looking just like a normal user on the channel. Some of these
    functions include protecting the channel from abuse, allowing privileged
    users to gain op or voice status, logging channel events, providing
    information, hosting games, etc.

    One of the features that makes Eggdrop stand out from other bots is module
    and Tcl scripting support. With scripts and modules you can make the bot
    perform almost any task you want. They can do anything: from preventing
    floods to greeting users and banning advertisers from channels.

    You can also link multiple Eggdrop bots together to form a botnet. This
    can allow bots to op each other securely, control floods efficiently and
    even link channels across multiple IRC networks. It also allows the
    Eggdrops share user lists, ban/exempt/invite lists, and ignore
    lists with other bots if userfile sharing is enabled. This allows users
    to have the same access on every bot on your botnet. It also allows the
    bots to distribute tasks such as opping and banning users. See doc/BOTNET
    for information on setting up a botnet.

    Eggdrop is always being improved and adjusted because there are bugs to
    be fixed and features to be added (if the users demand them and they make
    actually sense). In fact, it existed for several years as v0.7 - v0.9
    before finally going 1.0. This version of Eggdrop is part of the 1.9 tree.
    A valiant effort has been made to chase down and destroy bugs.

    This README file contains information about how to get Eggdrop, command
    line options for Eggdrop, what you may need to do when upgrading from
    older versions, a list of frequently asked questions, how to set up a
    crontab, some boring legal stuff, some basics
    about git usage and some channels where you might get help with Eggdrop.

------------------
HOW TO GET EGGDROP
------------------

    Before you can compile Eggdrop, you need to have Tcl installed on your
    system. Most systems should have Tcl on them by now - you can check by
    trying the command "tclsh". If it works, you will be given a "%" prompt
    and you can type "exit" to exit the program. This means Tcl is installed
    on your system. If tclsh doesn't load, then Tcl probably isn't on your
    system, and you will need to install it. The website to download Tcl is
    https://www.tcl.tk/software/tcltk/download.html and most OS distros have
    a binary installation available. If installing via an OS package manager,
    make sure to install the development library as well, usually called
    something similar to 'tcl-dev'.

    Currently, the 1.9 tree of Eggdrop is developed at eggheads.org. You can
    get the latest STABLE version of Eggdrop from the following url:

      `<https://geteggdrop.com/>`_

    You might try `<www.eggheads.org>`_ for help and information.

---------
Git Usage
---------

    Eggdrop development has moved from a CVS-based version control system to
    git. If you are interested in trying out the VERY LATEST updates to 
    Eggdrop, you may be interested in pulling the most recent code from
    there. BE WARNED, the development branch of Eggdrop is not to be
    considered stable and may (haha) have some significant bugs in it. The
    Eggheads Development Team will in NO WAY take any responsibility for 
    whatever might happen to you or your shell if you use the development
    branch of Eggdrop!

    To obtain Eggdrop via the git repository (hosted by GitHub), you can 
    either clone the repository via git or download a development snapshot.

    To clone the repository, simply type::

      git clone https://github.com/eggheads/eggdrop.git 

    Otherwise, you can download the development snapshot as a tar archive 
    from:

      `<https://github.com/eggheads/eggdrop/archive/develop.tar.gz>`_

-------------
Quick Startup
-------------

    Please, see the INSTALL file after you finish reading this file.

---------
Upgrading
---------

**UPGRADING FROM AN OLDER 1.3/1.4/1.5/1.6/1.8 TO A 1.9 VERSION**

    If you followed the INSTALL file and did a 'make install' (or 'make
    install DEST="path"') after 'make', this will be pretty easy. Just upload
    the new eggdrop-1.9.x.tar.gz file to your home dir on your shell, gunzip
    and untar it, and type 'cd ~/eggdrop-1.9.x'. Next, type './configure',
    'make config' or 'make iconfig', then 'make'. Then, kill the bot ('.die'
    on the partyline) and 'make install' to the same directory your bot
    is currently in. After that, you can just restart your bot. You may wish
    to delete the old Eggdrop executable and modules as well, especially if
    you have limited disk space.

    You should read through the new eggdrop.conf file for all of the new
    options in Eggdrop 1.9.x. You can copy and paste any of these settings
    into you current conf file if you do not want to use the default settings.

------------
Command Line
------------

    Eggdrop has some command line options - not many, because most things
    should be defined through the config file. However, sometimes you may
    want to start up the bot in a different mode and the command line
    options let you do that. Basically, the command line for Eggdrop is::

      % eggdrop [options] [config-file]

    The options available are:

      -t: Don't background, use terminal. This is just like -n, except that
           instead of seeing log entries, your console will simulate a DCC
           chat with the bot.

      -c: Don't background, show channel info. This is just like -n, except
           that instead of seeing log entries, every 10 seconds your screen
           will clear and you will see the current channel status, sort of
           like "top".

      -m: Create userfile. If you don't have a userfile, this will make Eggdrop
          create one and give owner status to the first person that introduces
          himself or herself to it. You'll need to do this when you first set
          up your bot.

      -h: Show help, then quit.

      -v: Show version info, then quit.

    Most people never use any of the options except -m and you usually only
    need to use that once.

--------------------
Setting up a Crontab
--------------------

    Eggdrop has become more stable with time, thanks mostly to people
    reporting bug details and helping find places where it crashes. However,
    there are still a -few- places where things aren't perfect. Few, if any,
    things in life are.

    Also, most systems go down from time to time. These things cause your bot
    to disappear from IRC and you have to restart it.

    Eggdrop comes with a shell script as scripts/botchk that will help keep the
    bot online. It will make the machine check every ten minutes to make sure
    your bot is still running. To use it, you have to add a line to your
    crontab. First, edit 'botchk' and change the directory and command line
    parameters so that it will be able to start up your bot. Then, add this
    line to your crontab::

      0,10,20,30,40,50 * * * * /home/mydir/botchk

    If you don't want to get emails from cron, use this::

      0,10,20,30,40,50 * * * * /home/mydir/botchk >/dev/null 2>&1

    Naturally, you need to change the path to the correct path for botchk. If
    you've never used crontab before, here is a simple way to add that line:

      1. Create a new file called 'mycron' and put the above line into it;

      2. From your shell prompt, type '% crontab mycron'.

    That will create a new crontab entry for you with a line that runs botchk
    every ten minutes. Botchk will then restart the bot when necessary (and
    send you email informing you).

-------------------------------------
Setting up a Crontab using autobotchk
-------------------------------------

    Included with your Eggdrop is an Eggdrop utility called 'autobotchk'.
    Using autobotchk is probably the fastest way of creating your botchk and
    crontabbing it with just a few required steps:

      1.::

           cp scripts/autobotchk ..;

      2.::
     
           ./autobotchk <Eggdrop config file>

    This will hopefully crontab your bot using the default setup. If you want
    a list of autobotchk options, type './autobotchk'. An example with options
    would be::

      ./autobotchk <Eggdrop config file> -noemail -5

    This would setup crontab to run the botchk every 5 minutes and also to
    not send you email saying that it restarted your bot.

------------------
Boring Legal Stuff
------------------

    The Eggdrop bot is Copyright (C) by Robey Pointer. As of January 1997,
    Eggdrop is distributed according to the GNU General Public License. There
    should be a copy of this license in the COPYING file. If not, write to
    the Free Software Foundation, Inc., 51 Franklin Street, Fifth Floor,
    Boston, MA 02110-1301, USA.

    As of Eggdrop 1.3.28, all changes made by the Eggheads Development Team to
    the Eggdrop source code and any related files are Copyright (C) by Eggheads
    Development Team. The source code will still be distributed according to
    the GNU General Public License as Robey Pointer did in the past.

    Releases previous to 1.0m were made using a different licensing scheme.
    You may, at your option, use the GNU General Public License on those
    versions (instead of the license packaged with them) with my blessing.
    For any versions bearing a copyright date of 1997 or later, you have
    no choice - you must use the GNU General Public License.

    The files match.c, net.c and blowfish.c are exempt from the above
    restrictions. match.c is original code by Chris Fuller (email:
    crf@cfox.bchs.uh.edu) and has been placed by him into the public domain.
    net.c is by me, and I (Robey Pointer) also choose to place it in the
    public domain. blowfish.c is by various sources and is in the public
    domain as well. All 3 files contain useful functions that could easily
    be ported to other applications.

    Tcl is by John Ousterhout and is in no way affiliated with Eggdrop. It
    likely has its own set of copyrights and what-nots.

    There is no warranty, implied or whatever. You use this software at your
    own risk, no matter what purpose you put it to.

------------
Mailing List
------------

    There are currently a couple of mailing lists about Eggdrop.
    eggheads@eggheads.org is the one relevant for posts about Eggdrop 1.9 and
    up (suggestions, help, etc).

    To subscribe to the eggheads mailing list, send email to
    eggheads-request@eggheads.org. In the body of the message, put "subscribe
    eggheads". We commonly use this list to announce new releases.You can also
    go to the following url:

      `<http://lists.eggheads.org/mailman/listinfo/eggheads>`_

    DO NOT SEND ROBEY EMAIL ABOUT EGGDROP!

    Robey is no longer developing the Eggdrop code, so don't bother emailing
    him. If you have a serious problem, email the eggheads mailing list and
    it will get to the coders.

    Please, before posting to this list, see what things are like. When you do
    post, read over your post for readability, spelling and grammar mistakes.
    Obviously, we're all human (or are we?) and we all make mistakes (heck,
    look at this document! ;).

    Open discussion and debate is integral to change and progress. Don't flame
    others over mere form (grammar and spelling) or even substantive issues
    for that matter. Please read and follow the mailing list rules.

    The eggheads@eggheads.org mailing list is not dedicated to those all too
    common questions we have all seen on other lists. For example:

      * Why does my bot say this: Please edit your config file.
      * How do I telnet my bot?
      * Where do I get Eggdrop for windows??????

    Technical questions, your thoughts or suggestions on new features being
    added to Eggdrop, things that should be removed or fixed, amazing problems
    that even stump the gurus, etc. are what we want to see here.

    Bug reports should be generated in the issue section of
    `<https://www.github.com/eggheads/eggdrop>`_

    DO NOT SEND HTML EMAILS TO ANY OF THE EGGHEADS.ORG MAILING LISTS. ANYONE
    SENDING HTML EMAILS TO ONE OF THESE LISTS WILL BE REMOVED IMMEDIATELY!

-------------
Documentation
-------------

    We're trying to keep the documentation up to date. If you feel that
    anything is missing here or that anything should be added, etc, please
    create an issue, or better yet a pull request, at 
    `<https://www.github.com/eggheads/eggdrop>`_ Thank you!

--------------
Obtaining Help
--------------

    You can obtain help with Eggdrop in the following IRC channels:

      * Libera Chat - #eggdrop (official channel), #eggheads (development discussion)
      * DALnet - #eggdrop
      * EFnet - #egghelp
      * IRCnet - #eggdrop
      * QuakeNet - #eggdrop.support
      * Undernet - #eggdrop

    If you plan to ask questions in any of the above channels, you should be
    familiar with and follow IRC etiquette:

      * Don't type using CAPITAL letters, colors or bold.
      * Don't use  "!" and "?" excessively.
      * Don't /msg people without their permission.
      * Don't repeat or paste more than 4 lines of text to the channel.
      * Don't ask to ask- just state your question, along with any relevant details and error messages

Copyright (C) 1997 Robey Pointer
Copyright (C) 1999 - 2021 Eggheads Development Team
