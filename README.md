# Minecraft World ID Server Plugin

A plugin for the spigot Minecraft server that can be used to grant users permissions when they verify with World ID. Intended to be used with [LuckPerms](https://luckperms.net/).

## Configuration

The plugin can be configured by editing the `config.yml` file in the `plugins/WorldId` directory of your Minecraft server. The following settings are available:

- worldcoin-app-id: ""
    - REQUIRED
    - The App ID you've gotten from Worldcoin's [Developer Portal](https://developer.worldcoin.org).
- world-id-orb-group-name: "humans"
    - REQUIRED
    - The name of the LuckPerms group that will be granted to users who verify with World ID's Orb Credential. The Orb credential provides a very high level of assurance that the user is a human with only one account.
- world-id-lite-group-name: ""
    - OPTIONAL
    - The name of the LuckPerms group that will be granted to users who verify with World ID Lite. World ID Lite verifies that a user has a unique mobile device, providing medium-strength bot protection that is still easy to use.
- web-url: "https://minecraft.worldcoin.org"
    - REQUIRED
    - The URL to use for the web interface where users will verify with World ID. You shouldn't change this unless you're running the web interface locally for development purposes.

## Dev Quickstart

This project uses [Maven](https://maven.apache.org/) for building. To build the plugin run the following command in the root directory of the project:

````bash
mvn package
```` 

To test the plugin we need a Minecraft server! Run a SpigotMC server (or one of its derivatives) locally -- this exercise is left to the reader. We recommend [PaperMC](https://papermc.io/), and you can [find installation instructions here](https://docs.papermc.io/paper/getting-started). Ensure you also install LuckPerms, and create a group for verified users. By default, this group is called `humans`. You can change this setting in the World ID plugin's `config.yml` file.

Build the plugin and copy the resulting jar file to the `plugins` folder of your server. Restart the server.

In the log produced by the server on the command line watch out for the following lines indicating that the plugin was deployed properly:

```
[22:48:13 INFO]: [World ID] Enabling WorldId v0.0.1
[22:48:13 INFO]: [World ID] Initialized the config.
[22:48:13 INFO]: [World ID] Plugin configured.
[22:48:13 INFO]: [World ID] Added the 'verify' command.
[22:48:13 INFO]: [World ID] Listening for player joins.
``` 

We also need to run [the Web UI](https://github.com/worldcoin/world-id-minecraft-web) locally. Follow the instructions in the README to get it running. 

Once it's up and running, ensure you set the `web-url` in `{MC_SERVER_DIR}/plugins/WorldId/config.yml` to the URL of the web server, typically `http://localhost:3000`. Also set `worldcoin-app-id` to the App ID you've gotten from Worldcoin's [Developer Portal](https://developer.worldcoin.org).

Start the Minecraft client on your computer and connect to the local Minecraft server by specifying `localhost` as Server Address.

Open the command line in Minecraft (by pressing `t`) try the new command and see what happens:
```
/verify
````

Once you're done fiddling with the code don't forget to run `mvn package`, copy the resulting jar file to the `plugins` folder of your server, and restart the server.