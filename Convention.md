# Convention for the standardization Telegram Bots

## Changelog
Version | Date | Note
------------ | ------------- | -------------
1.0 | 2020-08-27 | Initial Release

## Preface
The goal of this document is to define a set of standardized commands which every bot should implement in order to obtain a minimal user experience over different bots

## Application
This document can be applied to any telegram bot that takes in commands from the user. In this document we will assume the default way of entering commands using the command prefix '/' followed by the command and a abatrary number of parameters in the format:
```
/<command-identifier> [<Parameter>...]
```

## Standard Commands
Every bot following this conventions should define the following commands. All commands should be defined lower-case and ideally be a single word. If more than one word is required it should be defined in snake-case (/some_multiword_command)

If a bot receives an unrecognized command it should react with an appropriate help output.

### /start
The start command has to be run in order for the bot to communicate in a private chat. It should primarely be used to start the bot and get ready to interact with the user. A bot should not react to any messages in a group or private chat without being started first. It should not save any data or read any message without being started first.

The bot should react with an appropriate welcome message, introducing the user to the next steps in the bots process

The command may take in parameters for example for deep-linking. If the command requires extra parameters, it should inform the user about such if called without the correct parameters.

### /stop
If a bot has a continious operation (not a predefined process on with end it will self terminate), or if the bot saves data about a user the /stop command should stop all processed in the chat it was send in, it should delete all data about the user issuing the command and about the chat the command was issued in. 

The bot should not keep any privacy sensitive records after this command. It should not react to any messages in that chat and not store any new data until the /start command is issued

### /help
Help should return a list of all commands with a short description of how they are used, as well as a general description about the bot usage

### /help [command]
Calling help with a command identifier should return a usage description of that specific command.

### /about
The command should return the following information about the bot:
 - A short description about the bots usages. Can be the same as passed to botfather
 - The telegram tag of the bot creator or another way to contact the creator of the bot or it's support
 - Optionally a link to the code repository if the bot is open source
 - Optionally a preferred way to handle issue reports

It may also include the following markup to spread awareness about this document as well as informing about the conformity to this document:

```
Conforms to the [Telegram Bot Convention](https://github.com/Chase22/TelegramBotConventions/blob/master/Convention.md)
```

## Additional Command
### /gdpr
This command should return information concerning the european general-data-protection-regulation including information about what privacy sensitive data is stored and what the user can do to get information about this data as well as how this data can be removed (for example by issuing the /stop command)
