# Screen

`screen` is a "terminal multiplexer", it enables a number of terminals \(or windows\) to be accessed and controlled from a single terminal. `screen` is a great way to save an interactive session between connections to oscar. You can reconnect to the session from anywhere!

## Screen commands

Common commands are:

* start a new screen session with session name: `screen -S <name>`
* list running sessions/screens: `screen -ls`
* attach to session by name: `screen -r <name>`  
* detach: `Ctrl+a d`
* detach and logout \(quick exit\): `Ctrl+a d d`  
* kill a screen session: `screen -XS session_name quit`

## Reconnecting to your screen session

{% hint style="warning" %}
There are several login nodes in Oscar, and the node from where you launched `screen` matters! That is, you can only reconnect from the login node in which you launched `screen` from
{% endhint %}

In order to reconnect to a running `screen` session, you need to be connected to the same login node that you launched your `screen` session from. In order to locate and identify your `screen` sessions correctly, we recommed the following:

* Create a directory to store the information of your screen sessions.  You only need do this once.

```text
mkdir ~/.screen && chmod 700 ~/.screen
```

* Put the following line into your /.bashrc.  This tells the screen program to save the information of your screen sessions  in  the directory created in the previous step . This allows you to query your screen sessions across different login nodes. To make this change effective in your current sessions, you need run 'source /.bashrc' in each of your current session . However, you do not need to run 'source /bashrc' in your new sessions. 

```text
export SCREENDIR=$HOME/.screen
```

* **Name your new screen session** using the name of the login node. For instance, start your screen with a commnd similar to

```text
screen -S experiment1-login003
```

