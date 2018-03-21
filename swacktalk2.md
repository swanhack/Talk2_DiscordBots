# Building a Discord bot

## Make a Discord server for testing

When testing bots for Discord, it's usually a good idea to create a new server
or guild to keep development spam away from prying eyes.

Open up the [Discord application page](https://discordapp.com/channels/@me) and
hit the plus at the bottom of the server list to create a new server. You can
name it whatever you want, and for us the region doesn't matter either, so
usually accepting the default is fine.

## Register a Discord application 

A common thing when interacting with external services will be the need to
register your application so it can communicate with that service.

Discord is no different in this regard. Open up the [Discord developers
page](https://discordapp.com/developers/applications/me) and hit the New App
button. Give your bot a name, and hit Create App.

You'll need to ensure that the name you choose is fairly unique, as the name of
your bot account will be the same as that of the app. Don't use simple names
like "test" or "asdf", you will have issues.

Next, scroll down and click Create a Bot User. This informs Discord that we are
actually writing a bot, and will give us the necessary token to be able to talk
to Discord from our bot.

## Add the bot to your Discord server

On the same page, click the "Generate OAuth 2 URL" button. This will redirect
you to a tool that will let you generate the URL you need to copy into another
tab to be able to add your bot to your server.

OAuth2 is an exceptionally common method for authenticating yourself to external
services. It comes up practically everywhere nowadays, so understanding how it
works is very useful.

The generator will pre fill all the fields you need to be able to add the bot,
    which is the client ID (a unique ID for your application) and the bot
    "scope" which defines what your application should be able to do, in this
    case "be a bot".

Copy the URL that the generator has made for us into another tab or window, and
click through to allow your bot access to the server you made earlier.

## Installing and using discord.js

Now we get to write some code! Open up your terminal of choice, or PowerShell if
you're on Windows. Make a new directory for your bot.

```shell
mkdir MyAwesomeBot
cd MyAwesomeBot
npm init
```

Once we're done clicking through all the NPM prompts, we can install the magic
sauce that lets us work with Discord, discord.js!

```shell
npm install --save discord.js
```

Let's now create a new file `index.js` for us to put our code into. Into this
file, we'll import the discord.js library and set up our bot, and log into
Discord!

```js
const discordjs = require('discord.js');
const client = new discordjs.Client();



client.login('<my token>');
```

Where I've placed `<my token>` in the code above, you need to replace this with
the bot token you can get from the Discord developers site. Click the link to
reveal your specific bot code and copy it in place.

If we now run the code using `node index.js`, we can see it... doesn't do much.
Well, we can see if we look at Discord that our bot has come online! This means
that our code is able to connect to and talk to Discord properly

## EventEmitter basics

The discord.js Client is what is known as an EventEmitter. This is a pattern
used extensively in Node, where an object may emit that an event has occurred
and do something in response to that event occurring.

An example in discord.js is the `message` event. Say we want to respond to every
message sent to our server that says 'ping', with a reply of 'pong'.

In the gap between our requires and logging in, add the following:

```js
client.on('message', msg => {
  if(msg.content === 'ping') {
    msg.reply('pong');
  }
});
```

What this code does is register a handler for the `message` event, which will
occur every time the bot sees a message be sent. We then define what should
happen when th

What this code does is defines what should happen whenever the bot sees a
message be sent. We'll get a `message` event from Discord, which says who sent
the message, what channel it is in, and some other related metadata. It also
allows us to reply to it using the `.reply` method.

All in all this makes it so any time someone sends the word "ping" in your
Discord server, the bot will respond with the word "pong"

## Further expansion

With the client being an `EventEmitter`, there are a number of events we can go
and listen for and react to. A full list can be found in the [discord.js
documentation](https://discord.js.org/#/docs/main/stable/class/Client). 
