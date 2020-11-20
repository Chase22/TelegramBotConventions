# Convention for the standardization Telegram Bots

## Changelog
Version | Date | Note
------------ | ------------- | -------------
1.0 | 2020-08-27 | Initial Release
1.1 | 2020-11-20 | Clarifications, added Principles section, added /donate command

## Preface
The goal of this document is to define a set of standardized commands which every bot should implement in order to obtain a minimal user experience over different bots

## Application
This document can be applied to any telegram bot that takes in commands from the user. In this document we will assume the default way of entering commands using the command prefix '/' followed by the command and a abatrary number of parameters in the format:
```
/<command-identifier> [<Parameter>...]
```

## Principles
Every bot should follow the following design principles:

### Communicative
A bot should transparently communicate problems to the Users. Any command input send to the bot should be reactor to in some way. 
If it's an invalid command, with a proper output telling the user what the problem is. In case of an error the bot should give 
the user the information to make it possible for the user to fix the problem by himself or to contact the support of the bot

### Liberal
A bot should not reject a command if too many parameters are given or if parameters are given to a command that doesn't require any. 
A bot may give a warning that some parameters are not used, but should still proceed with normal operation if possible

### Sparing
A bot should send messages sparingly. Message should only be send as a reaction to a user action. 
If periodic or event-based messages are a feature of the bot, the user should be informed about them and there should be a instrument for the user to stop those messages from being send.
Long Messages or Messages for a specific user should be send to that users private chat, if the bot operates in a group

## Commands
All commands should be defined as a single lower-case work. If more than one word is required it should be defined in snake-case (/some_multiword_command)

If a bot receives an unrecognized command it should react with an appropriate help output.

## Standard Commands
Every bot following this conventions should define the following commands. 

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
These commands are not part of the basic command set. They should be added as necessary.

### /donate
This command should return information about how the user can support the bot financially. This could include links to donation pages or information about special features unlocked via the telegram payment feature.

This command itself should not initiate a payment transaction

### /gdpr
This command should return information concerning the european general-data-protection-regulation including information about what privacy sensitive data is stored and what the user can do to get information about this data as well as how this data can be removed (for example by issuing the /stop command)
