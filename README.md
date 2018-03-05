# podcast

simple podcast script written in bash

	podcast -h  help (this text)
	podcast -a  add podcast
	podcast -l  list subscribed podcasts
	podcast -d  delete podcast

## install

Just run the script `podcast`.  It looks for `$HOME/.config/podcast/config`.  If that file doesn't exist, it'll run the install portion of the script.

It will search through your `$PATH` for a writable directory and copy `podcast` to it.  Then it will create a config directory.

The script will try to create the config directory first in `$XDG_CONFIG_HOME/podcast`, but if it's not set in your environment, will default to `$HOME/.config/podcast`, which I'm pretty sure is the same thing, but whatever.

After the config directory is set and the skeleton files are generated, it'll ask you to add a new podcast.  It writes podcast "subscriptions" to `$XDG_CONFIG_HOME/podcast/subscriptions`, one subscription per line in the format of:

	TITLE,URL,USER,PASS

* `TITLE` is the "title" of the podcast
* `URL` is the url of the podcast xml file
* `USER` and `PASS` are for authenticated podcasts

It's just a comma separated value.  You can hand edit this file to bulk add subscriptions or use the script.  Dealers choice.

Note: The authenticated podcast portion of the script is currently untested.

## running

After the script is installed, running `podcast` will try to download whatever podcasts are listed in `$XDG_CONFIG_HOME/podcast/subscriptions`.

By default, all media is downloaded to `$XDG_CONFIG_HOME/podcast/media`. This location can be changed by modifying the `MEDIA` variable in `$XDG_CONFIG_HOME/podcast/config`

## posthook

In `$XDG_CONFIG_HOME/podcast/config` there is a variable called `POSTHOOK`.  You can put additional commands in this variable to be executed after your media finishes downloading.

For instance, you could play audio after your downloads finish, or you could `scp` the media to a server on your network, whatever.  You could also just leave it blank and change the `MEDIA` variable in the `config`.
