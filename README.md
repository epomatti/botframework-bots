# Microsoft Bot Framework Exercise

Demonstrate the core capabilities of the Microsoft Bot Framework

This bot has been created using [Bot Framework](https://dev.botframework.com), it shows how to create a simple bot that accepts input from the user and echoes it back.

## To run the bot

There are multiple ways of making your bot session data persistent.

Choose your storage strategy according to the [storage factory](factories/storageFactory.js).

- Option 1: Memory, no need to create resources

- Option 2: Cosmos DB:

```sh
group='rg-bot'
location='eastus2'
cosmosAccount='cosmos-botframework-999'
cosmosDatabase='greetingbot'

az group create -n $group -l $location
az cosmosdb create -n $cosmosAccount -g $group
az cosmosdb sql database create -a $cosmosAccount -g $group -n $cosmosDatabase

az cosmosdb sql container create \
  -a $cosmosAccount \
  -g $group \
  -d $cosmosDatabase \
  -n 'messages' \
  --partition-key-path '/messages'    
```
- Option 3: Storage Account:

```sh
group='rg-bot'
location='eastus2'
storage='stbotfrmk999'

az group create -n $group -l $location

az storage account create \
  -n $storage \
  -g $group \
  -l $location \
  --kind StorageV2 \
  --sku Standard_LRS

# get the connection string and use it here
az storage container create -n 'messages' --connection-string '<CONNECTION_STRING>'
```

#### Install global CLI dependencies

```bash
# "yo" and "generator-botbuilder"
yarn global add yo generator-botbuilder
```

#### Start the bot

```bash
yarn install
yarn start
```

## Testing the bot using Bot Framework Emulator

[Bot Framework Emulator](https://github.com/microsoft/botframework-emulator) is a desktop application that allows bot developers to test and debug their bots on localhost or running remotely through a tunnel.

- Install the Bot Framework Emulator latest version from [here](https://github.com/Microsoft/BotFramework-Emulator/releases)

### Connect to the bot using Bot Framework Emulator

- Launch Bot Framework Emulator
- File -> Open Bot
- Enter a Bot URL of `http://localhost:3978/api/messages`

## Deploy the bot to Azure

To learn more about deploying a bot to Azure, see [Deploy your bot to Azure](https://aka.ms/azuredeployment) for a complete list of deployment instructions.

## References

[Create a bot using JavaScript](https://docs.microsoft.com/en-us/azure/bot-service/javascript/bot-builder-javascript-quickstart?view=azure-bot-service-4.0)


## Further reading

- [Bot Framework Documentation](https://docs.botframework.com)
- [Bot Basics](https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0)
- [Dialogs](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0)
- [Gathering Input Using Prompts](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-prompts?view=azure-bot-service-4.0)
- [Activity processing](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-concept-activity-processing?view=azure-bot-service-4.0)
- [Azure Bot Service Introduction](https://docs.microsoft.com/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0)
- [Azure Bot Service Documentation](https://docs.microsoft.com/azure/bot-service/?view=azure-bot-service-4.0)
- [Language Understanding using LUIS](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/)
- [Channels and Bot Connector Service](https://docs.microsoft.com/en-us/azure/bot-service/bot-concepts?view=azure-bot-service-4.0)
