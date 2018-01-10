# Seattle Defensive Security System
Created a security layer reference monitor which keeps a backup copy of a file in case it is written incorrectly. This is a common technique for things like firmware images where a system may not be able to recover if the file is written incorrectly. In this system, every correct file must start with the character 'S' and end with the character 'E'. If any other characters (including lowercase 's', 'e', etc.) are the first or last characters, then the file is considered invalid.

However, the user has permission to write information into the file. The application should not be blocked from performing any writeat() operation, because when it chooses it may later write 'S' at the start and 'E' at the end. Note that checking if the file starts with 'S' and ends with 'E' is only performed when close is called.

Now, you may store two copies of A/B files on disk, one that is the valid backup (which is used for reading) and the other that is written to. When an app calls ABopenfile(), this indicates that the A/B files, which you should name filename.a and filename.b, should be opened.
When the app calls readat(), all reads must be performed on the valid file. Similarly, when the app calls writeat(), all writes must be performed on the invalid file. If the app uses ABopenfile() to create a file that does not exist (by setting create=True when calling ABopenfile()), the reference monitor will create a new file 'SE' in filename.a and an empty file called filename.b. When close() is called on the file, if a file is not valid, it is discarded. if both files are valid, the older one is discarded.

Note that the behavior of other file system calls should remain unchanged. This means listfiles(), removefile(), and calls to files accessed with openfile() instead of ABopenfile() remain unchanged by this reference monitor.

To run the reference monitor, type the following commands in the terminal window with attack program:
'python repy.py restrictions.default encasementlib.r2py [security_layer].r2py [attack_program].r2py'

## NOTE
1. Never raise unexpected errors or produce any output. Your program must produce no output when run normally.

For further documentation refer: https://github.com/SeattleTestbed/docs/blob/master/EducationalAssignments/ABStoragePartOne.md
