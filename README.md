# SourceMod-SQL-Whois
#### SourceMod plugin that tracks players across multiple servers

I wrote this is 2009-10 when our gaming community was running multiple Team Fortress 2 and Left 4 Dead/L4D2 servers. I tested it tonight on a freshly-installed server, and it still works, although I had to disable strict SQL mode which is now apparently A Thing.

It's a port of Bugblatter's [plugin_blatt_whois](https://web.archive.org/web/20111015055345/http://www.ravenousbugblatterbeast.pwp.blueyonder.co.uk/BugblatterPlugins/plugin_blatt_whois/Docs/index.htm) for Adminmod, the major difference (AM/SM aside) being that it stores in a central database rather than 5 zillion flatfiles.

I had a look at the current crop of Sourcemod plugins and while there are a couple of whois plugins, neither approach the functionality of Bugblatter's original.

It's not perfect, and there's a few things I wanted to add but never got to, but it is really rather good.

## Dependencies
[SQL admins](https://wiki.alliedmods.net/SQL_Admins_(SourceMod)) enabled and running off a MariaDB or MySQL database. Does not work with SQLite!

## Features
- records kicks and bans with reasons on a player's record
- allows you to place/remove a watch on players even if they're not currently connected
- notifies admins when watched players or players on LAN are on the server

The notification timer is set for 2 minutes - you may want to adjust this or disable it altogether if it gets annoying. Editing the timer amount in line 26 (or commenting out with a //) and recompiling will solve that for you.

## Commands
| Command | Description|
|----|----|
| sm_whois \<steamID\|name\> | Show a player's activity |
| sm_lan | Show current players using the same IP address |
| sm_note \<steamID\|name\> \<note\> | Record note on player's record |
| sm_watch \<steamID\|name\> \<reason\> | Record watch against player (reason required) |
| sm_unwatch \<steamID\|name\> \<reason\> | Remove existing watch against player (reason required) |

## Example Output
![Example Whois Output](whois.png)

## Installation
- Edit whois.sp and [recompile](https://www.sourcemod.net/compiler.php) the .smx if needed.
- Turn off Strict SQL mode by adding 'sql_mode=NO_ENGINE_SUBSTITUTION' to your MySQL/MariaDB my.cnf.
- Restart the DB.
- Stop your server.
- Drop whois.smx into your plugins directory.
- Login to the SQL server you're using for sourcemod and run the contents of whois.sql.txt - this will setup all the tables needed.
- Start your server. 
