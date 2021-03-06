Moltres
=======

Moltres is a Discord bot for reporting, coordinating, and joining Pokemon Go
raids.  It was originally designed and written for [Valor of Boston][vob].

Moltres is location-agnostic and can be set up for use in any region.  It
performs best when its host server is outfitted with taggable regional roles,
so that it can use these roles to organize gyms and notify users of raid calls.

Setup
-----

To run an instance of Moltres for your Discord server, first clone the repo:

    git clone https://github.com/mxw/moltres.git
    cd moltres
    # All of the remaining commands will assume you are in the project folder.

Next, install all the Node package dependencies.

    # If you have not yet built any C libraries from source, you will likely
    # need this:
    sudo apt-get install libtool-bin automake

    npm install

Install MySQL, e.g.,

    sudo apt-get install mysql-server

and create a database `moltresdb` for use by a user named `moltres`.  Then, 
create five tables: `gyms`, `raids`, `calls`, `rsvps`, and `permissions`. 

The script for this is in [setup/moltres.sql](setup/moltres.sql).  Edit the
password to whatever you want, then run at the command line with:

    mysql -u root -p < setup/moltres.sql
    # This will prompt you for the MySQL root password, which is usually
    # prompted for during the installation of mysql-server.  If you never set
    # up a root password, you can try running as the machine's root user.
    # Otherwise, you get to Google how to reset a MySQL root password.

Create a Discord bot account and add it to your server by following 
[these steps][discord-bot].

When adding Moltres to your server, you must grant it the following permissions
in the channels in which it's active:

- Read Messages
- Send Messages
- Manage Messages
- Embed Links
- Read Message History
- Use External Emojis
- Add Reactions

Next, add a file `config.js` in the repo's root directory:

    cp setup/config.example.js config.js
    vim config.js # or nano, emacs, or whatever editor you prefer

You may have noticed several references to guild IDs, channel IDs, and other
IDs that are numbers and not names.  You can get these IDs by enabling
[Developer Mode][discord-dev-mode] in your Discord client, right-clicking the
entities in question, and selecting Copy ID.

Usage
-----

To run Moltres, simply execute

    ./moltres.sh

once all the setup has been completed.  In order for Moltres to be useful,
you'll have to manually add gym records to the `gyms` table, either via MySQL
INSERT queries, or using the `$add-gym` command, e.g.,

    $add-gym galaxy-sphere kendall 42.362374 -71.084384 Galaxy: Earth Sphere

Contribution
------------

Feel free to submit issues or PRs for any bugs or feature requests you may
have.  Please be understanding of rejected feature requests---I am very
intentional about what capabilities to support with a system like this that
integrates with a social-first chat application.

If you're interested in Moltres development or have support questions, please
feel free to ask in [Victory Road][victory-road], Moltres's home server.


[vob]: https://www.valorofboston.com/
[discord-bot]: https://github.com/reactiflux/discord-irc/wiki/Creating-a-discord-bot-&-getting-a-token
[victory-road]: https://discord.gg/hTaVwwr
[discord-dev-mode]: https://support.discordapp.com/hc/en-us/articles/206346498-Where-can-I-find-my-User-Server-Message-ID-
