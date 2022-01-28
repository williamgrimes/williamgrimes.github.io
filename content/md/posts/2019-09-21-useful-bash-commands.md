{:title "The Bourne Again Shell"
 :layout :post
 :toc true
 :tags  ["bash" "notes"]}

A shell or command-line interpreter (CLI) provides an interface for a user to input commands in Unix-like operating systems. The shell can be used as an interactive command prompt and also written as a scripting programming language. Typically users interact with the shell using a text window called a terminal emulator, that is a computer program that emulates a video terminal. The shell maybe executing directly on the local hardware or remotely connecting to a server via Secure Shell (SSH). All Unix shells provide filename wildcarding, piping, here documents, command substitution, variables and control structures for condition-testing and iteration [[^1]].

The Bourne Again SHell (bash) is the Unix-shell and command language for the GNU operating system written by Brian Fox and first released in 1989. It serves as a replacement to its predecessor the Bourne Shell (sh), and has a superset of its features. The bash shell incorporates features from the Bourne shell (sh) the KornShell (ksh) and the C shell (csh). For example the expansion of the tilde `~` character to the value held in the `$HOME` environment variable comes from the C shell. Bash has gone on to become the most popular shell among users of Linux and the default on many distributions [[^2]].

In addition to the KornShell and C shell there are many alternative shells available such as the Z shell (zsh) and the Friendly Interactive Shell (fish). Even though more modern shells are available with it's large user base and long service bash remains a mature and stable choice, despite this vulnerabilities have been found in Bash.

# Shellshock
---
The shellshock software bug is an example of a vulnerability found in Bash and first disclosed on 24 September 2014 by Stéphane Chazelas [[^3]]. Shellshock is a security bug that was introduced on 5 August 1989, and released in Bash version 1.03 on 1 September 1989 causing Bash to execute commands from environment variables unintentionally. Using this vulnerability attackers can remotely issue commands on a server. Many machines were vulnerable since many internet and network services such as web servers use environment variables to communicate with the server's operating system.

A patch was worked on with the maintainers of Bash and a fix issued for the bug with identifier CVE-2014-6271 [[^4]]. However within hours of disclosure attackers already started exploiting Shellshock, creating botnets of compromised computers to perform distributed denial-of-service attacks and vulnerability scanning.

The bug exploits a problem sanitising environment variables before being executed, this allows attackers to send commands to a remote server through HTTP requests and get them executed by the web server operating system.

Although the majority of machines will have been patched by now, any organisation without proper patch management running a version of bash older than 4.3 may still be vulnerable. You can check if your system is vulnerable by issuing the following command in Bash:

``` shell
env x='() { :;}; echo vulnerable' bash -c "echo this is a test"
```

This bug exploits a flaw in Bash's "function export" feature, whereby one Bash process can share command scripts with other Bash processes that it executes. These data are shared between processes by encoding the scripts in a table of environment variables. Every new Bash process scans the table for encoded scripts, creating a command for each environment variable and executes that command. This can be used for example over HTTP to create an environment variable on a remote machine that is a function export, this can contain additional unsanitised malicious code that gets executed on the remote machine by other bash processes.

# Bash Commands
---
Given here are some frequently used commands and different examples of how they may be used with a brief explanation, these are a subset taken from the helpful tldr package [[^5]].

## alias
> Creates aliases -- words that are replaced by a command string.<br>
> Aliases expire with the current shell session unless defined in the shell's configuration file, e.g. `~/.bashrc`.<br>
> More information: <https://tldp.org/LDP/abs/html/aliases.html>.

 - `alias`&nbsp;&ndash; list all aliases
 - `alias {{word}}="{{command}}"`&nbsp;&ndash; create a generic alias
 - `alias {{word}}`&nbsp;&ndash; view the command associated to a given alias.
 - `unalias {{word}}`&nbsp;&ndash; remove an aliased command.
 - `alias {{rm}}="{{rm --interactive}}"`&nbsp;&ndash; turn `rm` into an interactive command.
 - `alias {{la}}="{{ls --all}}"`&nbsp;&ndash; create `la` as a shortcut for `ls --all`.

## awk
> A versatile programming language for working on files.<br>
> More information: <https://github.com/onetrueawk/awk>.
 - `awk '{print $5}' {{filename}}`&nbsp;&ndash; print the fifth column (a.k.a. field) in a space-separated file.
 - `awk '/{{foo}}/ {print $2}' {{filename}}`&nbsp;&ndash; print the second column of the lines containing "foo" in a space-separated file.
 - `awk -F ',' '{print $NF}' {{filename}}`&nbsp;&ndash; print the last column of each line in a file, using a comma (instead of space) as a field separator.
 - `awk '{s+=$1} END {print s}' {{filename}}`&nbsp;&ndash; sum the values in the first column of a file and print the total.
 - `awk 'NR%3==1' {{filename}}`&nbsp;&ndash; print every third line starting from the first line.
 - `awk '{if ($1 == "foo") print "Exact match foo"; else if ($1 ~ "bar") print "Partial match bar"; else print "Baz"}' {{filename}}`&nbsp;&ndash; print different values based on conditions.
 - `awk '($10 == value)'`&nbsp;&ndash; print all lines where the 10th column value equals the specified value .
 - `awk '($10 >= min_value && $10 <= max_value)'`&nbsp;&ndash; print all the lines which the 10th column value is between a min and a max .

## bash
> Bourne-Again SHell, an `sh`-compatible command-line interpreter.<br>
> See also `histexpand` for history expansion.<br>
> More information: <https://gnu.org/software/bash/>.
 - `bash`&nbsp;&ndash; start an interactive shell session.
 - `bash -c "{{command}}"`&nbsp;&ndash; execute a command and then exit.
 - `bash {{path/to/script.sh}}`&nbsp;&ndash; execute a script.
 - `bash -x {{path/to/script.sh}}`&nbsp;&ndash; execute a script, printing each command before executing it.
 - `bash -e {{path/to/script.sh}}`&nbsp;&ndash; execute commands from a script, stopping at the first error.
 - `bash -s`&nbsp;&ndash; read and execute commands from stdin.
 - `bash --version`&nbsp;&ndash; print the Bash version (`$BASH_VERSION` contains the version without license information).

## cat
> Print and concatenate files.<br>
> More information: <https://www.gnu.org/software/coreutils/cat>.
 - `cat {{file}}`&nbsp;&ndash; print the contents of a file to the standard output.
 - `cat {{file1}} {{file2}} > {{target_file}}`&nbsp;&ndash; concatenate several files into the target file.
 - `cat {{file1}} {{file2}} >> {{target_file}}`&nbsp;&ndash; append several files into the target file.
 - `cat -n {{file}}`&nbsp;&ndash; number all output lines.
 - `cat -v -t -e {{file}}`&nbsp;&ndash; display non-printable and whitespace characters (with `M-` prefix if non-ASCII).

## chmod
> Change the access permissions of a file or directory.<br>
> More information: <https://www.gnu.org/software/coreutils/chmod>.
 - `chmod u+x {{file}}`&nbsp;&ndash; give the [u]ser who owns a file the right to e[x]ecute it.
 - `chmod u+rw {{file_or_directory}}`&nbsp;&ndash; give the [u]ser rights to [r]ead and [w]rite to a file/directory.
 - `chmod g-x {{file}}`&nbsp;&ndash; remove e[x]ecutable rights from the [g]roup.
 - `chmod a+rx {{file}}`&nbsp;&ndash; give [a]ll users rights to [r]ead and e[x]ecute.
 - `chmod o=g {{file}}`&nbsp;&ndash; give [o]thers (not in the file owner's group) the same rights as the [g]roup.
 - `chmod o= {{file}}`&nbsp;&ndash; remove all rights from [o]thers.
 - `chmod -R g+w,o+w {{directory}}`&nbsp;&ndash; change permissions recursively giving [g]roup and [o]thers the ability to [w]rite.
 - `chmod -R a+rX {{directory}}`&nbsp;&ndash; recursively give [a]ll users [r]ead permissions to files and e[X]ecute permissions to sub-directories within a directory.

## chown
> Change user and group ownership of files and directories.<br>
> More information: <https://www.gnu.org/software/coreutils/chown>.
 - `chown {{user}} {{path/to/file_or_directory}}`&nbsp;&ndash; change the owner user of a file/directory.
 - `chown {{user}}:{{group}} {{path/to/file_or_directory}}`&nbsp;&ndash; change the owner user and group of a file/directory.
 - `chown -R {{user}} {{path/to/directory}}`&nbsp;&ndash; recursively change the owner of a directory and its contents.
 - `chown -h {{user}} {{path/to/symlink}}`&nbsp;&ndash; change the owner of a symbolic link.
 - `chown --reference={{path/to/reference_file}} {{path/to/file_or_directory}}`&nbsp;&ndash; change the owner of a file/directory to match a reference file.

## chsh
> Change the user's login shell.<br>
> More information: <https://manned.org/chsh>.
 - `chsh`&nbsp;&ndash; change the current user's login shell interactively.
 - `chsh --shell {{/bin/zsh}} {{username}}`&nbsp;&ndash; change the login shell for a given user to Zsh.
 - `chsh --list-shells`&nbsp;&ndash; list available shells.

## cp
> Copy files and directories.<br>
> More information: <https://www.gnu.org/software/coreutils/cp>.
 - `cp {{path/to/source_file.ext}} {{path/to/target_file.ext}}`&nbsp;&ndash; copy a file to another location.
 - `cp {{path/to/source_file.ext}} {{path/to/target_parent_directory}}`&nbsp;&ndash; copy a file into another directory, keeping the filename.
 - `cp -R {{path/to/source_directory}} {{path/to/target_directory}}`&nbsp;&ndash; recursively copy a directory's contents to another location (if the destination exists, the directory is copied inside it).
 - `cp -vR {{path/to/source_directory}} {{path/to/target_directory}}`&nbsp;&ndash; copy a directory recursively, in verbose mode (shows files as they are copied).
 - `cp -i {{*.txt}} {{path/to/target_directory}}`&nbsp;&ndash; copy text files to another location, in interactive mode (prompts user before overwriting).
 - `cp -L {{link}} {{path/to/target_directory}}`&nbsp;&ndash; follow symbolic links before copying.

## crontab
> Schedule cron jobs to run on a time interval for the current user.<br>
> Job definition format: "(min) (hour) (day_of_month) (month) (day_of_week) command_to_execute".<br>
> More information: <https://manned.org/crontab>.
 - `crontab -e`&nbsp;&ndash; edit the crontab file for the current user.
 - `sudo crontab -e -u {{user}}`&nbsp;&ndash; edit the crontab file for a specific user.
 - `crontab {{path/to/file}}`&nbsp;&ndash; replace the current crontab with the contents of the given file.
 - `crontab -l`&nbsp;&ndash; view a list of existing cron jobs for current user.
 - `crontab -r`&nbsp;&ndash; remove all cron jobs for the current user.
 - `0 10 * * * {{command_to_execute}}`&nbsp;&ndash; sample job which runs at 10:00 every day (* means any value).
 - `* * 3 Apr * {{command_to_execute}}`&nbsp;&ndash; sample job which runs every minute on the 3rd of April.
 - `30 2 * * Fri {{/absolute/path/to/script.sh}}`&nbsp;&ndash; sample job which runs a certain script at 02:30 every Friday.

## curl
> Transfers data from or to a server.<br>
> Supports most protocols, including HTTP, FTP, and POP3.<br>
> More information: <https://curl.se>.
 - `curl {{http://example.com}} --output {{filename}}`&nbsp;&ndash; download the contents of a URL to a file.
 - `curl --remote-name {{http://example.com/filename}}`&nbsp;&ndash; download a file, saving the output under the filename indicated by the URL.
 - `curl --fail --remote-name --location --continue-at - {{http://example.com/filename}}`&nbsp;&ndash; download a file, following location redirects, and automatically continuing (resuming) a previous file transfer and return an error on server error.
 - `curl --data {{'name=bob'}} {{http://example.com/form}}`&nbsp;&ndash; send form-encoded data (POST request of type `application/x-www-form-urlencoded`). Use `--data @file_name` or `--data @'-'` to read from STDIN.
 - `curl --header {{'X-My-Header: 123'}} --request {{PUT}} {{http://example.com}}`&nbsp;&ndash; send a request with an extra header, using a custom HTTP method.
 - `curl --data {{'{"name":"bob"}'}} --header {{'Content-Type: application/json'}} {{http://example.com/users/1234}}`&nbsp;&ndash; send data in JSON format, specifying the appropriate content-type header.
 - `curl --user myusername:mypassword {{http://example.com}}`&nbsp;&ndash; pass a username and password for server authentication.
 - `curl --cert {{client.pem}} --key {{key.pem}} --insecure {{https://example.com}}`&nbsp;&ndash; pass client certificate and key for a resource, skipping certificate validation.

## cut
> Cut out fields from stdin or files.<br>
> More information: <https://www.gnu.org/software/coreutils/cut>.
 - `cut -c {{1-16}}`&nbsp;&ndash; cut out the first sixteen characters of each line of stdin.
 - `cut -c {{1-16}} {{file}}`&nbsp;&ndash; cut out the first sixteen characters of each line of the given files.
 - `cut -c {{3-}}`&nbsp;&ndash; cut out everything from the 3rd character to the end of each line.
 - `cut -d'{{:}}' -f{{5}}`&nbsp;&ndash; cut out the fifth field of each line, using a colon as a field delimiter (default delimiter is tab).
 - `cut -d'{{;}}' -f{{2,10}}`&nbsp;&ndash; cut out the 2nd and 10th fields of each line, using a semicolon as a delimiter.
 - `cut -d'{{ }}' -f{{3-}}`&nbsp;&ndash; cut out the fields 3 through to the end of each line, using a space as a delimiter.

## date
> Set or display the system date.<br>
> More information: <https://www.gnu.org/software/coreutils/date>.
 - `date +"%c"`&nbsp;&ndash; display the current date using the default locale's format.
 - `date -u +"%Y-%m-%dT%H:%M:%SZ"`&nbsp;&ndash; display the current date in UTC and ISO 8601 format.
 - `date +%s`&nbsp;&ndash; display the current date as a Unix timestamp (seconds since the Unix epoch).
 - `date -d @1473305798`&nbsp;&ndash; display a specific date (represented as a Unix timestamp) using the default format.
 - `date -d "{{2018-09-01 00:00}}" +%s --utc`&nbsp;&ndash; convert a specific date to the Unix timestamp format.
 - `date --rfc-3339=s`&nbsp;&ndash; display the current date using the RFC-3339 format (`YYYY-MM-DD hh:mm:ss TZ`).
 - `date {{093023592021.59}}`&nbsp;&ndash; set the current date using the format `MMDDhhmmYYYY.ss` (`YYYY` and `.ss` are optional).

## diff
> Compare files and directories.<br>
> More information: <https://man7.org/linux/man-pages/man1/diff.1.html>.
 - `diff {{old_file}} {{new_file}}`&nbsp;&ndash; compare files (lists changes to turn `old_file` into `new_file`).
 - `diff --ignore-all-space {{old_file}} {{new_file}}`&nbsp;&ndash; compare files, ignoring white spaces.
 - `diff --side-by-side {{old_file}} {{new_file}}`&nbsp;&ndash; compare files, showing the differences side by side.
 - `diff --unified {{old_file}} {{new_file}}`&nbsp;&ndash; compare files, showing the differences in unified format (as used by `git diff`).
 - `diff --recursive {{old_directory}} {{new_directory}}`&nbsp;&ndash; compare directories recursively (shows names for differing files/directories as well as changes made to files).
 - `diff --recursive --brief {{old_directory}} {{new_directory}}`&nbsp;&ndash; compare directories, only showing the names of files that differ.
 - `diff --text --unified --new-file {{old_file}} {{new_file}} > {{diff.patch}}`&nbsp;&ndash; create a patch file for Git from the differences of two text files, treating nonexistent files as empty.

## echo
> Print given arguments.<br>
> More information: <https://www.gnu.org/software/coreutils/echo>.
 - `echo "{{Hello World}}"`&nbsp;&ndash; print a text message. Note: quotes are optional.
 - `echo "{{My path is $PATH}}"`&nbsp;&ndash; print a message with environment variables.
 - `echo -n "{{Hello World}}"`&nbsp;&ndash; print a message without the trailing newline.
 - `echo "{{Hello World}}" >> {{file.txt}}`&nbsp;&ndash; append a message to the file.
 - `echo -e "{{Column 1\tColumn 2}}"`&nbsp;&ndash; enable interpretation of backslash escapes (special characters).

## env
> Show the environment or run a program in a modified environment.<br>
> More information: <https://www.gnu.org/software/coreutils/env>.
 - `env`&nbsp;&ndash; show the environment.
 - `env {{program}}`&nbsp;&ndash; run a program. Often used in scripts after the shebang (##!) for looking up the path to the program.
 - `env -i {{program}}`&nbsp;&ndash; clear the environment and run a program.
 - `env -u {{variable}} {{program}}`&nbsp;&ndash; remove variable from the environment and run a program.
 - `env {{variable}}={{value}} {{program}}`&nbsp;&ndash; set a variable and run a program.
 - `env {{variable1}}={{value}} {{variable2}}={{value}} {{variable3}}={{value}} {{program}}`&nbsp;&ndash; set multiple variables and run a program.

## eval
> Execute arguments as a single command in the current shell and return its result.<br>
> More information: <https://manned.org/eval>.
 - `eval "{{echo foo}}"`&nbsp;&ndash; call `echo` with the "foo" argument.
 - `eval "{{foo=bar}}"`&nbsp;&ndash; set a variable in the current shell.

## file
> Determine file type.<br>
> More information: <https://manned.org/file>.
 - `file {{filename}}`&nbsp;&ndash; give a description of the type of the specified file. Works fine for files with no file extension.
 - `file -z {{foo.zip}}`&nbsp;&ndash; look inside a zipped file and determine the file type(s) inside.
 - `file -s {{filename}}`&nbsp;&ndash; allow file to work with special or device files.
 - `file -k {{filename}}`&nbsp;&ndash; don't stop at first file type match; keep going until the end of the file.
 - `file -i {{filename}}`&nbsp;&ndash; determine the mime encoding type of a file.

## find
> Find files or directories under the given directory tree, recursively.<br>
> More information: <https://manned.org/find>.
 - `find {{root_path}} -name '{{*.ext}}'`&nbsp;&ndash; find files by extension.
 - `find {{root_path}} -path '{{**/path/**/*.ext}}' -or -name '{{*pattern*}}'`&nbsp;&ndash; find files matching multiple path/name patterns.
 - `find {{root_path}} -type d -iname '{{*lib*}}'`&nbsp;&ndash; find directories matching a given name, in case-insensitive mode.
 - `find {{root_path}} -name '{{*.py}}' -not -path '{{*/site-packages/*}}'`&nbsp;&ndash; find files matching a given pattern, excluding specific paths.
 - `find {{root_path}} -size {{+500k}} -size {{-10M}}`&nbsp;&ndash; find files matching a given size range.
 - `find {{root_path}} -name '{{*.ext}}' -exec {{wc -l {} }}\;`&nbsp;&ndash; run a command for each file (use `{}` within the command to access the filename).
 - `find {{root_path}} -daystart -mtime -{{7}} -delete`&nbsp;&ndash; find files modified in the last 7 days and delete them.
 - `find {{root_path}} -type {{f}} -empty -delete`&nbsp;&ndash; find empty (0 byte) files and delete them.

## grep
> Find patterns in files using regular expressions.<br>
> More information: <https://www.gnu.org/software/grep/manual/grep.html>.
 - `grep "{{search_pattern}}" {{path/to/file}}`&nbsp;&ndash; search for a pattern within a file.
 - `grep --fixed-strings "{{exact_string}}" {{path/to/file}}`&nbsp;&ndash; search for an exact string (disables regular expressions).
 - `grep --recursive --line-number --binary-files={{without-match}} "{{search_pattern}}" {{path/to/directory}}`&nbsp;&ndash; search for a pattern in all files recursively in a directory, showing line numbers of matches, ignoring binary files.
 - `grep --extended-regexp --ignore-case "{{search_pattern}}" {{path/to/file}}`&nbsp;&ndash; use extended regular expressions (supports `?`, `+`, `{}`, `()` and `|`), in case-insensitive mode.
 - `grep --{{context|before-context|after-context}}={{3}} "{{search_pattern}}" {{path/to/file}}`&nbsp;&ndash; print 3 lines of context around, before, or after each match.
 - `grep --with-filename --line-number "{{search_pattern}}" {{path/to/file}}`&nbsp;&ndash; print file name and line number for each match.
 - `grep --only-matching "{{search_pattern}}" {{path/to/file}}`&nbsp;&ndash; search for lines matching a pattern, printing only the matched text.
 - `cat {{path/to/file}} | grep --invert-match "{{search_pattern}}"`&nbsp;&ndash; search stdin for lines that do not match a pattern.

## gunzip
> Extract file(s) from a gzip (.gz) archive.<br>
> More information: <https://manned.org/gunzip>.
 - `gunzip {{archive.tar.gz}}`&nbsp;&ndash; extract a file from an archive, replacing the original file if it exists.
 - `gunzip --stdout {{archive.tar.gz}} > {{archive.tar}}`&nbsp;&ndash; extract a file to a target destination.
 - `gunzip --keep {{archive.tar.gz}}`&nbsp;&ndash; extract a file and keep the archive file.
 - `gunzip --list {{file.txt.gz}}`&nbsp;&ndash; list the contents of a compressed file.

## head
> Output the first part of files.<br>
> More information: <https://www.gnu.org/software/coreutils/head>.
 - `head --lines {{count}} {{path/to/file}}`&nbsp;&ndash; output the first few lines of a file.
 - `head --bytes {{count}} {{path/to/file}}`&nbsp;&ndash; output the first few bytes of a file.
 - `head --lines -{{count}} {{path/to/file}}`&nbsp;&ndash; output everything but the last few lines of a file.
 - `head --bytes -{{count}} {{path/to/file}}`&nbsp;&ndash; output everything but the last few bytes of a file.

## history
> Command-line history.<br>
> More information: <https://www.gnu.org/software/bash/manual/html_node/Bash-History-Builtins.html>.
 - `history`&nbsp;&ndash; display the commands history list with line numbers.
 - `history {{20}}`&nbsp;&ndash; display the last 20 commands (in `zsh` it displays all commands starting from the 20th).
 - `history -c`&nbsp;&ndash; clear the commands history list (only for current `bash` shell).
 - `history -w`&nbsp;&ndash; overwrite history file with history of current `bash` shell (often combined with `history -c` to purge history).
 - `history -d {{offset}}`&nbsp;&ndash; delete the history entry at the specified offset.

## ifconfig
> Network Interface Configurator.<br>
> More information: <https://net-tools.sourceforge.io/man/ifconfig.8.html>.
 - `ifconfig eth0`&nbsp;&ndash; view network settings of an Ethernet adapter.
 - `ifconfig -a`&nbsp;&ndash; display details of all interfaces, including disabled interfaces.
 - `ifconfig eth0 down`&nbsp;&ndash; disable eth0 interface.
 - `ifconfig eth0 up`&nbsp;&ndash; enable eth0 interface.
 - `ifconfig eth0 {{ip_address}}`&nbsp;&ndash; assign IP address to eth0 interface.

## last
> View the last logged in users.<br>
> More information: <https://manned.org/last>.
 - `last`&nbsp;&ndash; view last logins, their duration and other information as read from `/var/log/wtmp`.
 - `last -n {{login_count}}`&nbsp;&ndash; specify how many of the last logins to show.
 - `last -F -a`&nbsp;&ndash; print the full date and time for entries and then display the hostname column last to prevent truncation.
 - `last {{username}} -i`&nbsp;&ndash; view all logins by a specific user and show the IP address instead of the hostname.
 - `last reboot`&nbsp;&ndash; view all recorded reboots (i.e., the last logins of the pseudo user "reboot").
 - `last shutdown`&nbsp;&ndash; view all recorded shutdowns (i.e., the last logins of the pseudo user "shutdown").

## ln
> Creates links to files and directories.<br>
> More information: <https://www.gnu.org/software/coreutils/ln>.
 - `ln -s {{/path/to/file_or_directory}} {{path/to/symlink}}`&nbsp;&ndash; create a symbolic link to a file or directory.
 - `ln -sf {{/path/to/new_file}} {{path/to/symlink}}`&nbsp;&ndash; overwrite an existing symbolic link to point to a different file.
 - `ln {{/path/to/file}} {{path/to/hardlink}}`&nbsp;&ndash; create a hard link to a file.

## ls
> List directory contents.<br>
> More information: <https://www.gnu.org/software/coreutils/ls>.
 - `ls -1`&nbsp;&ndash; list files one per line.
 - `ls -a`&nbsp;&ndash; list all files, including hidden files.
 - `ls -F`&nbsp;&ndash; list all files, with trailing `/` added to directory names.
 - `ls -la`&nbsp;&ndash; long format list (permissions, ownership, size, and modification date) of all files.
 - `ls -lh`&nbsp;&ndash; long format list with size displayed using human-readable units (KiB, MiB, GiB).
 - `ls -lS`&nbsp;&ndash; long format list sorted by size (descending).
 - `ls -ltr`&nbsp;&ndash; long format list of all files, sorted by modification date (oldest first).
 - `ls -d */`&nbsp;&ndash; only list directories.

## lsof
> Lists open files and the corresponding processes.<br>
> Note: Root privileges (or sudo) is required to list files opened by others.<br>
> More information: <https://manned.org/lsof>.
 - `lsof {{path/to/file}}`&nbsp;&ndash; find the processes that have a given file open.
 - `lsof -i :{{port}}`&nbsp;&ndash; find the process that opened a local internet port.
 - `lsof -t {{path/to/file}}`&nbsp;&ndash; only output the process ID (PID).
 - `lsof -u {{username}}`&nbsp;&ndash; list files opened by the given user.
 - `lsof -c {{process_or_command_name}}`&nbsp;&ndash; list files opened by the given command or process.
 - `lsof -p {{PID}}`&nbsp;&ndash; list files opened by a specific process, given its PID.
 - `lsof +D {{path/to/directory}}`&nbsp;&ndash; list open files in a directory.
 - `lsof -i6TCP:{{port}} -sTCP:LISTEN -n -P`&nbsp;&ndash; find the process that is listening on a local IPv6 TCP port and don't convert network or port numbers.

## man
> Format and display manual pages.<br>
> More information: <https://www.man7.org/linux/man-pages/man1/man.1.html>.
 - `man {{command}}`&nbsp;&ndash; display the man page for a command.
 - `man {{7}} {{command}}`&nbsp;&ndash; display the man page for a command from section 7.
 - `man --path`&nbsp;&ndash; display the path searched for manpages.
 - `man -w {{command}}`&nbsp;&ndash; display the location of a manpage rather than the manpage itself.
 - `man {{command}} --locale={{locale}}`&nbsp;&ndash; display the man page using a specific locale.
 - `man -k "{{search_string}}"`&nbsp;&ndash; search for manpages containing a search string.

## mkdir
> Creates a directory.<br>
> More information: <https://www.gnu.org/software/coreutils/mkdir>.
 - `mkdir {{directory}}`&nbsp;&ndash; create a directory in current directory or given path.
 - `mkdir {{directory_1 directory_2 ...}}`&nbsp;&ndash; create multiple directories in the current directory.
 - `mkdir -p {{path/to/directory}}`&nbsp;&ndash; create directories recursively (useful for creating nested dirs).

## more
> Open a file for interactive reading, allowing scrolling and search.<br>
> More information: <https://manned.org/more>.
 - `more {{path/to/file}}`&nbsp;&ndash; open a file.
 - `more +{{line_number}} {{path/to/file}}`&nbsp;&ndash; open a file displaying from a specific line.
 - `more --help`&nbsp;&ndash; display help.
 - `<Space>`&nbsp;&ndash; go to the next page.
 - `/{{something}}`&nbsp;&ndash; search for a string (press `n` to go to the next match).
 - `q`&nbsp;&ndash; exit.
 - `h`&nbsp;&ndash; display help about interactive commands.

## mv
> Move or rename files and directories.<br>
> More information: <https://www.gnu.org/software/coreutils/mv>.
 - `mv {{source}} {{target}}`&nbsp;&ndash; move a file to an arbitrary location.
 - `mv {{source1}} {{source2}} {{source3}} {{target_directory}}`&nbsp;&ndash; move files into another directory, keeping the filenames.
 - `mv -f {{source}} {{target}}`&nbsp;&ndash; do not prompt for confirmation before overwriting existing files.
 - `mv -i {{source}} {{target}}`&nbsp;&ndash; prompt for confirmation before overwriting existing files, regardless of file permissions.
 - `mv -n {{source}} {{target}}`&nbsp;&ndash; do not overwrite existing files at the target.
 - `mv -v {{source}} {{target}}`&nbsp;&ndash; move files in verbose mode, showing files after they are moved.

## ps
> Information about running processes.<br>
> More information: <https://manned.org/ps>.
 - `ps aux`&nbsp;&ndash; list all running processes.
 - `ps auxww`&nbsp;&ndash; list all running processes including the full command string.
 - `ps aux | grep {{string}}`&nbsp;&ndash; search for a process that matches a string.
 - `ps --user $(id -u) -F`&nbsp;&ndash; list all processes of the current user in extra full format.
 - `ps --user $(id -u) f`&nbsp;&ndash; list all processes of the current user as a tree.
 - `ps -o ppid= -p {{pid}}`&nbsp;&ndash; get the parent PID of a process.
 - `ps --sort size`&nbsp;&ndash; sort processes by memory consumption.

## sed
> Edit text in a scriptable manner.<br>
> More information: <https://man.archlinux.org/man/sed.1>.
 - `sed 's/{{regular_expression}}/{{replace}}/' {{filename}}`&nbsp;&ndash; replace the first occurrence of a regular expression in each line of a file, and print the result.
 - `sed -r 's/{{regular_expression}}/{{replace}}/g' {{filename}}`&nbsp;&ndash; replace all occurrences of an extended regular expression in a file, and print the result.
 - `sed -i 's/{{find}}/{{replace}}/g' {{filename}}`&nbsp;&ndash; replace all occurrences of a string in a file, overwriting the file (i.e. in-place).
 - `sed '/{{line_pattern}}/s/{{find}}/{{replace}}/' {{filename}}`&nbsp;&ndash; replace only on lines matching the line pattern.
 - `sed '/{{line_pattern}}/d' {{filename}}`&nbsp;&ndash; delete lines matching the line pattern.
 - `sed 11q {{filename}}`&nbsp;&ndash; print the first 11 lines of a file.
 - `sed -e 's/{{find}}/{{replace}}/' -e 's/{{find}}/{{replace}}/' {{filename}}`&nbsp;&ndash; apply multiple find-replace expressions to a file.
 - `sed 's##{{find}}#{{replace}}#' {{filename}}`&nbsp;&ndash; replace separator `/` by any other character not used in the find or replace patterns, e.g. `##`.


## sleep
> Delay for a specified amount of time.<br>
> More information: <https://www.gnu.org/software/coreutils/sleep>.
 - `sleep {{seconds}}`&nbsp;&ndash; delay in seconds.
 - `sleep {{minutes}}m`&nbsp;&ndash; delay in minutes.
 - `sleep {{hours}}h`&nbsp;&ndash; delay in hours.

## sort
> Sort lines of text files.<br>
> More information: <https://www.gnu.org/software/coreutils/sort>.

 - `sort {{path/to/file}}`&nbsp;&ndash; sort a file in ascending order.
 - `sort --reverse {{path/to/file}}`&nbsp;&ndash; sort a file in descending order.
 - `sort --ignore-case {{path/to/file}}`&nbsp;&ndash; sort a file in case-insensitive way.
 - `sort --numeric-sort {{path/to/file}}`&nbsp;&ndash; sort a file using numeric rather than alphabetic order.
 - `sort --field-separator={{:}} --key={{3n}} {{/etc/passwd}}`&nbsp;&ndash; sort `/etc/passwd` by the 3rd field of each line numerically, using ":" as a field separator.
 - `sort --unique {{path/to/file}}`&nbsp;&ndash; sort a file preserving only unique lines.
 - `sort --output={{path/to/file}} {{path/to/file}}`&nbsp;&ndash; sort a file, printing the output to the specified output file (can be used to sort a file in-place).
 - `sort --general-numeric-sort {{path/to/file}}`&nbsp;&ndash; sort numbers with exponents.

## ssh
> Secure Shell is a protocol used to securely log onto remote systems.<br>
> It can be used for logging or executing commands on a remote server.<br>
> More information: <https://man.openbsd.org/ssh>.

 - `ssh {{username}}@{{remote_host}}`&nbsp;&ndash; connect to a remote server.
 - `ssh -i {{path/to/key_file}} {{username}}@{{remote_host}}`&nbsp;&ndash; connect to a remote server with a specific identity (private key).
 - `ssh {{username}}@{{remote_host}} -p {{2222}}`&nbsp;&ndash; connect to a remote server using a specific port.
 - `ssh {{username}}@{{remote_host}} -t {{command}} {{command_arguments}}`&nbsp;&ndash; run a command on a remote server with a [t]ty allocation allowing interaction with the remote command.
 - `ssh -D {{1080}} {{username}}@{{remote_host}}`&nbsp;&ndash; SSH tunneling: Dynamic port forwarding (SOCKS proxy on `localhost:1080`).
 - `ssh -L {{9999}}:{{example.org}}:{{80}} -N -T {{username}}@{{remote_host}}`&nbsp;&ndash; sSH tunneling: Forward a specific port (`localhost:9999` to `example.org:80`) along with disabling pseudo-[T]ty allocation and executio[N] of remote commands.
 - `ssh -J {{username}}@{{jump_host}} {{username}}@{{remote_host}}`&nbsp;&ndash; sSH jumping: Connect through a jumphost to a remote server (Multiple jump hops may be specified separated by comma characters).
 - `ssh -A {{username}}@{{remote_host}}`&nbsp;&ndash; agent forwarding: Forward the authentication information to the remote machine (see `man ssh_config` for available options).

## stat
> Display file and filesystem information.<br>
> More information: <https://www.gnu.org/software/coreutils/manual/html_node/stat-invocation.html>.
 - `stat {{file}}`&nbsp;&ndash; show file properties such as size, permissions, creation and access dates among others.
 - `stat -t {{file}}`&nbsp;&ndash; same as above but in a more concise way.
 - `stat -f {{file}}`&nbsp;&ndash; show filesystem information.
 - `stat -c "%a %n" {{file}}`&nbsp;&ndash; show only octal file permissions.
 - `stat -c "%U %G" {{file}}`&nbsp;&ndash; show owner and group of the file.
 - `stat -c "%s %n" {{file}}`&nbsp;&ndash; show the size of the file in bytes.

## tail
> Display the last part of a file.<br>
> See also: `head`.<br>
> More information: <https://www.gnu.org/software/coreutils/tail>.
 - `tail --lines {{count}} {{path/to/file}}`&nbsp;&ndash; show last 'count' lines in file.
 - `tail --lines +{{count}} {{path/to/file}}`&nbsp;&ndash; print a file from a specific line number.
 - `tail --bytes {{count}} {{path/to/file}}`&nbsp;&ndash; print a specific count of bytes from the end of a given file.
 - `tail --follow {{path/to/file}}`&nbsp;&ndash; print the last lines of a given file and keep reading file until `Ctrl + C`.
 - `tail --retry --follow {{path/to/file}}`&nbsp;&ndash; keep reading file until `Ctrl + C`, even if the file is inaccessible.
 - `tail --lines {{count}} --sleep-interval {{seconds}} --follow {{path/to/file}}`&nbsp;&ndash; show last 'num' lines in 'file' and refresh every 'n' seconds.

## tee
> Read from standard input and write to standard output and files (or commands).<br>
> More information: <https://www.gnu.org/software/coreutils/tee>.
 - `echo "example" | tee {{path/to/file}}`&nbsp;&ndash; copy standard input to each file, and also to standard output.
 - `echo "example" | tee -a {{path/to/file}}`&nbsp;&ndash; append to the given files, do not overwrite.
 - `echo "example" | tee {{/dev/tty}} | {{xargs printf "[%s]"}}`&nbsp;&ndash; print standard input to the terminal, and also pipe it into another program for further processing.
 - `echo "example" | tee >(xargs mkdir) >(wc -c)`&nbsp;&ndash; create a directory called "example", count the number of characters in "example" and write "example" to the terminal.

## touch
> Change a file access and modification times (atime, mtime).<br>
> More information: <https://www.gnu.org/software/coreutils/touch>.
 - `touch {{path/to/file}}`&nbsp;&ndash; create a new empty file(s) or change the times for existing file(s) to current time.
 - `touch -t {{YYYYMMDDHHMM.SS}} {{path/to/file}}`&nbsp;&ndash; set the times on a file to a specific date and time.
 - `touch -d "{{-1 hour}}" {{path/to/file}}`&nbsp;&ndash; set the time on a file to one hour in the past.
 - `touch -r {{path/to/file1}} {{path/to/file2}}`&nbsp;&ndash; use the times from a file to set the times on a second file.
 - `touch {{path/to/file{1,2,3}.txt}}`&nbsp;&ndash; create multiple files.

## tr
> Translate characters: run replacements based on single characters and character sets.<br>
> More information: <https://www.gnu.org/software/coreutils/tr>.
 - `tr {{find_character}} {{replace_character}} < {{filename}}`&nbsp;&ndash; replace all occurrences of a character in a file, and print the result.
 - `echo {{text}} | tr {{find_character}} {{replace_character}}`&nbsp;&ndash; replace all occurrences of a character from another command's output.
 - `tr '{{abcd}}' '{{jkmn}}' < {{filename}}`&nbsp;&ndash; map each character of the first set to the corresponding character of the second set.
 - `tr -d '{{input_characters}}' < {{filename}}`&nbsp;&ndash; delete all occurrences of the specified set of characters from the input.
 - `tr -s '{{input_characters}}' < {{filename}}`&nbsp;&ndash; compress a series of identical characters to a single character.
 - `tr "[:lower:]" "[:upper:]" < {{filename}}`&nbsp;&ndash; translate the contents of a file to upper-case.
 - `tr -cd "[:print:]" < {{filename}}`&nbsp;&ndash; strip out non-printable characters from a file.

## uniq
> Output the unique lines from the given input or file.<br>
> Since it does not detect repeated lines unless they are adjacent, we need to sort them first.<br>
> More information: <https://www.gnu.org/software/coreutils/uniq>.
 - `sort {{file}} | uniq`&nbsp;&ndash; display each line once.
 - `sort {{file}} | uniq -u`&nbsp;&ndash; display only unique lines.
 - `sort {{file}} | uniq -d`&nbsp;&ndash; display only duplicate lines.
 - `sort {{file}} | uniq -c`&nbsp;&ndash; display number of occurrences of each line along with that line.
 - `sort {{file}} | uniq -c | sort -nr`&nbsp;&ndash; display number of occurrences of each line, sorted by the most frequent.

## watch
> Execute a program periodically, showing output fullscreen.<br>
> More information: <https://manned.org/watch>.
 - `watch {{command}}`&nbsp;&ndash; repeatedly run a command and show the result.
 - `watch -n {{60}} {{command}}`&nbsp;&ndash; re-run a command every 60 seconds.
 - `watch -d {{ls -l}}`&nbsp;&ndash; monitor the contents of a directory, highlighting differences as they appear.

## wc
> Count lines, words, and bytes.<br>
> More information: <https://www.gnu.org/software/coreutils/wc>.
 - `wc --lines {{path/to/file}}`&nbsp;&ndash; count all lines in a file.
 - `wc --words {{path/to/file}}`&nbsp;&ndash; count all words in a file.
 - `wc --bytes {{path/to/file}}`&nbsp;&ndash; count all bytes in a file.
 - `wc --chars {{path/to/file}}`&nbsp;&ndash; count all characters in a file (taking multi-byte characters into account).
 - `{{find .}} | wc`&nbsp;&ndash; count all lines, words and bytes from `stdin`.
 - `wc --max-line-length {{path/to/file}}`&nbsp;&ndash; count the length of the longest line in number of characters.

## whereis
> Locate the binary, source, and manual page files for a command.<br>
> More information: <https://manned.org/whereis>.
 - `whereis {{ssh}}`&nbsp;&ndash; locate binary, source and man pages for ssh.
 - `whereis -bm {{ls}}`&nbsp;&ndash; locate binary and man pages for ls.
 - `whereis -s {{gcc}} -m {{git}}`&nbsp;&ndash; locate source of gcc and man pages for Git.
 - `whereis -b -B {{/usr/bin/}} -f {{gcc}}`&nbsp;&ndash; locate binaries for gcc in `/usr/bin/` only.
 - `whereis -u *`&nbsp;&ndash; locate unusual binaries (those that have more or less than one binary on the system).
 - `whereis -u -m *`&nbsp;&ndash; locate binaries that have unusual manual entries (binaries that have more or less than one manual installed).

## whoami
> Print the username associated with the current effective user ID.<br>
> More information: <https://www.gnu.org/software/coreutils/whoami>.
 - `whoami`&nbsp;&ndash; display currently logged username.
 - `sudo whoami`&nbsp;&ndash; display the username after a change in the user ID.

# Pipelines
---
Bash also allows users to take advantage of Unix pipelines with the pipe `|` symbol. These are a mechanism for inter-process communication using message passing. Essentially pipelines allow bash commands to be chained together in a pipeline by passing the output of one command as the input of another. The output text of each process (stdout) is passed directly as input (stdin) to the next one. The second process is started as the first process is still executing, and they are executed concurrently. Given here are some examples of pipelines and a brief explanation of how they can be used to direct the standard output and standard error streams to file:

- `command > output.txt`&nbsp;&ndash; the standard output stream from `command` is redirected to the `output.txt` file only, it will not be visible in the terminal. If the file already exists, it gets overwritten.

- `command >> output.txt`&nbsp;&ndash; the standard output stream from `command` is redirected to the `output.txt` file only, it will not be visible in the terminal. If the file already exists, the new data will get appended to the end of the file.

- `command 2> output.txt`&nbsp;&ndash; the standard error stream from `command` will be redirected to the `output.txt` file only, it will not be visible in the terminal. If the file already exists, it gets overwritten.

- `command 2>> output.txt`&nbsp;&ndash; the standard error stream will be redirected to the `output.txt` file only, it will not be visible in the terminal. If the file already exists, the new data will get appended to the end of the file.

- `command &> output.txt`&nbsp;&ndash; both the standard output and standard error stream will be redirected to the `output.txt` file only, nothing will be visible in the terminal. If the file already exists, it gets overwritten.

- `command &>> output.txt`&nbsp;&ndash; both the standard output and standard error stream will be redirected to the `output.txt` file only, nothing will be visible in the terminal. If the file already exists, the new data will get appended to the end of the file..

- `command | tee output.txt`&nbsp;&ndash; standard output stream will be copied to the `output.txt` file, it will still be visible in the terminal. If the file already exists, it gets overwritten.

- `command | tee -a output.txt`&nbsp;&ndash; the standard output stream will be copied to the `output.txt` file, it will still be visible in the terminal. If the file already exists, the new data will get appended to the end of the file.

- `command |& tee output.txt`&nbsp;&ndash; both the standard output and standard error streams will be copied to the `output.txt` file while still being visible in the terminal. If the file already exists, it gets overwritten.

- `command |& tee -a output.txt`&nbsp;&ndash; both the standard output and standard error streams will be copied to the `output.txt` file while still being visible in the terminal. If the file already exists, the new data will get appended to the end of the file.

- `time python -u </path/to/python_script.py> | tee -a <std_output.txt>`&nbsp;&ndash; example with python script `-u` writes line by line not all at once at the end time gives a time for execution.

|   **Syntax**        |  **StdOut (term)** &nbsp;&nbsp;&nbsp; |  **StdErr (term)** &nbsp;&nbsp;&nbsp;|   **StdOut** (file) &nbsp;&nbsp;&nbsp;|  **StdErr (file)** &nbsp;&nbsp;&nbsp;|    **File Action**    |
|-----------------|----------|----------|-----------|---------|---------------|
|     >       &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    |    no    |   yes    |    yes    |    no   |  overwrite    |
|     >>      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    |    no    |   yes    |    yes    |    no   |   append      |
|    2>       &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    |   yes    |    no    |     no    |   yes   |  overwrite    |
|    2>>      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    |   yes    |    no    |     no    |   yes   |   append      |
|    &>       &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    |    no    |    no    |    yes    |   yes   |  overwrite    |
|    &>>      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    |    no    |    no    |    yes    |   yes   |   append      |
| \| tee      &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    |   yes    |   yes    |    yes    |    no   |  overwrite    |
| \| tee -a   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    |   yes    |   yes    |    yes    |    no   |   append      |
| \|& tee     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    |   yes    |   yes    |    yes    |   yes   |  overwrite    |
| \|& tee -a  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    |   yes    |   yes    |    yes    |   yes   |   append      |

# Extra Command Line Utilities
---
As well as having a rich in built set of commands, and added power using Unix pipelines there are many additional utilities that can be used from a bash command line. For example these are some command line utilities that I find particularly useful:

- [htop](https://htop.dev/) - an interactive process viewer.
- [jq](https://stedolan.github.io/jq/) - a command line json processor.
- [mosh](https://mosh.org/) - the mobile shell.
- [ncdu](https://dev.yorhel.nl/ncdu) - Ncdu is a disk usage analyzer with an ncurses interface.
- [nethogs](https://github.com/raboof/nethogs) - NetHogs is a small 'net top' tool. Instead of breaking the traffic down per protocol or per subnet, like most tools do, it groups bandwidth by process.
- [ranger](https://ranger.github.io/) - text based file manager.
- [tig](https://jonas.github.io/tig/) - text mode interface for git.
- [tldr](https://tldr.sh/) - simplified and community driven man pages.
- [tmux](https://tmux.github.io/) -  an open-source terminal multiplexer, it lets you switch easily between several programs in one terminal, detach them (they keep running in the background) and reattach them to a different terminal.
- [tree](https://linux.die.net/man/1/tree) - a recursive directory listing program.
- [visidata](https://www.visidata.org/) - an opensource data multi-tool.
- [z - jump around](https://github.com/rupa/z) - allows you to jump quickly between directories you frequently visit.

# Conclusion
---
Here I've given some background to different shells and described very briefly where the Bourne Again SHell arose from. It forms a very powerful and commonly available interface to Unix systems, but other shells are also worth exploring.

The commands described here could also be put together into scripting `.sh` files and executed as a sequence, this is known as shell scripting, and after learning some of the core functions of Bash is an easy next step to learn. There are many more utilities that can extend the default Bash experience, that make shell extensible and still relevant many years after it's inception.

[^1]: [GNU - what is a shell?](https://www.gnu.org/software/bash/manual/html_node/What-is-a-shell_003f.html)
[^2]: [Wikipedia: Bash Unix Shell](https://en.wikipedia.org/wiki/Bash_(Unix_shell))
[^3]: [Security Intelligence: Shell Shock](https://securityintelligence.com/articles/shellshock-vulnerability-in-depth/)
[^4]: [CVE-2014-6271](https://www.cve.org/CVERecord?id=CVE-2014-6271)
[^5]: [tldr](https://github.com/tldr-pages/tldr)
