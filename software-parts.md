# The 4 Universal Parts of Any Software

from [The Linux Documentation Project](http://www.tldp.org/HOWTO/HighQuality-Apps-HOWTO/software.html) (with little modification)


### 1. The Software on its own - the body

The executables, libraries, static-data files, examples, manuals etc. Regular users must have read-only access to these files. They are changed only when the system administrator makes an upgrade on the Software.

### 2. Configuration Files - the soul

The files that define how the Software will run, how to use the Content, security, performance etc.

Depending on your Software, specific privileged users may change these files to make the Software behave as they want.

It is important to provide documentation about the Configuration Files.

### 3. Content

The tables of a database system, the documents for a text editor, the images and HTML pages of a web-server etc.

This is what receives all the user attention. This is what the user delegated to be managed by your Product. If it gets damaged, the user may throw away your Product and use the competitor’s.

### 4. Logs, Dumps etc.

This is the last class of file, but many times they are the most problem generator for a system administrator because their volume can surpass even the Content size. Due to this fact, it is important to think about a methodology or facility for this issue while in design phase.
