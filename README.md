# PlayTimeTracker
**PlayTimeTracker** is a Spigot plugin that - as the name suggests - tracks your playtime on a server. It is designed with BungeeCord in Mind and therefore supports MySQL databases.

## How It Works
When a player joins the server, the plugin saves its name along with the current timestamp in a `HashMap`. When the player quits the server, the new timestamp gets subtracted from the one from the `HashMap`. Then the calculated playtime is written to the database.
An example is this screenshot:

![](https://i.imgur.com/OlIOJCb.png)

**You have to put the plugin on every server that you want to track.** The table names _should_ correspond to the names of the servers that are specified in the Bungee-config.


The preferred database structure is like this:
```
playtimetracker (db)
├ vanilla (table)
│ ├ player (column)
│ └ playtime (column)
├ lobby (table)
│ └ ...
└ bedwars (table)
  └ ...
```
and so on. You get the idea.
However, you can customize the database- and columnnames in the config.

## How To Use
First, we have to create the database structure.
Log in to your PHPmyAdmin and click the button on the left that says "New". Enter a name and hit `Create`. For the sake of simplicity, we'll use `playtimetracker` for this tutorial.
Then, create a table with the name of your server you want to track. We'll use `vanilla` for that. Don't forget to set the column count to '2'. Hit 'go' (it's on the lower right).

If you did everything right, you now should see an interface like this:

![](https://i.imgur.com/dqCP623.png)


Please change everything so that it matches the values shown in this screenshot:

![](https://i.imgur.com/Ti6UG2S.png)

_Note: When setting `Index` to `UNIQUE`, just don't change anything in the popup and hit `go`._

Great! Hit 'Save' on the lower right and we're done with the MySQL part! _You now can close your browser tab._

**To start with the setup of the actual plugin, make sure that you've started the plugin at least once**, so that the Config generates.
After that, you can open the config that is located at `/plugins/PlayTimeTracker/config.yml`

This is what you'll see:
```yml
database:
  host: localhost
  port: '3306'
  db: playtimetracker
  username: root
  password: ''
  column: playtime
  table: vanilla
  useSSL: 'false'
```
If you aren't using a very special setup, you should be able to leave everything as-is but the `table` and the credentials (`username` and `password`).
You set the table name to the name you created the table with and the credentials to the ones you used to log in to phpMyAdmin.

Nice! Don't forget to save the config and restart the server! If you join the server and leave it again, you should be able to see the playtime **in Milliseconds** at the database.
If you want to add another server to track, just add the plugin to this server and create a new table (don't forget to modify the table entry in the config!)

If you have any questions/bugs/improvements, please file an issue.
Thanks!
