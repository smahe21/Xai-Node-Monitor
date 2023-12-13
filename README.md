[![Twitter URL](https://img.shields.io/twitter/url/https/twitter.com/bukotsunikki.svg?style=social&label=Follow%20%40ShineCryptic)](https://twitter.com/ShineCryptic)

# How to Get Telegram Notifications?

## Setting up the Bot on Telegram

1. Open Telegram and search for `BotFather` with the ID `@BotFather`.
2. Send message to `@BotFather`.
3. Type `/help`.
4. Type or Click `/newbot`.
5. Follow the instructions to create your new bot. Copy token created by BotFather and save it somewhere safely.

## Creating a Group and Adding the Bot

1. Create a group on Telegram.
2. Add bot you created in the previous step as a member of this group.
3. Send a test message to the bot in the group. For example:

   ```
   ## Replace `xai_health_bot` with your bot ID
   /hello @xai_health_bot
   ```

## Finding Out the Chat ID

To find out the chat ID of the group for sending messages:

1. Open browser with below URL, replacing `REPLACE_WITH_BOT_TOKEN` with your telegram bot token:

   ```
   https://api.telegram.org/botREPLACE_WITH_BOT_TOKEN/getUpdates
   ```

   Example (Source [Stack Overflow](https://stackoverflow.com/a/32572159)):

   ```
   https://api.telegram.org/bot123456789:jbd78sadvbdy63d37gda37bd8/getUpdates
   ```

2. Look for the **"chat"** object in the response, similar to this example:

   ```
   {"update_id":8393,"message":{"message_id":3,"from":{"id":7474,"first_name":"AAA"},"chat":{"id":"CHAT ID","title":""},"date":25497,"new_chat_participant":{"id":71,"first_name":"NAME","username":"YOUR_BOT_NAME"}}}
   ```

   **Important:** Copy id `"CHAT ID"` received in `"chat":{id:"-123456789"}`.

3. Save the "id" from the "chat" object.
4. If you encounter issues (e.g., getting `{"ok":true,"result":[]}`), try removing and adding the bot again to the group.

# Running XAI Node Sentry with Screen -L

## Updated Command to Open a New Screen Session

To all our screen commands we are going to append **`-L`** flag.

Use `screen -L -S xai` to start a new screen session for the XAI node. This command enables logging, so all output is saved for later review.

    screen -L -S xai

## Attaching to the XAI Session

To reattach to the XAI session, use the following command. This allows you to view and interact with the session again.

    screen -L -r xai

## Setting Up Notification Script on VPS

To set up a script on VPS for XAI node notifications:

1. Open VPS and create a new screen session to run our monitor script in the background.
2. We will monitor XAI node and notify user on telegram if an error is found.
3. Follow these steps:

```

screen -S monitor
curl -L -o xai_monitor.sh https://github.com/smahe21/Xai-Node-Monitor/blob/master/xai_monitor.sh

chmod +x xai_monitor.sh


```

Replace `TELEGRAM_TOKEN` and `TELEGRAM_CHAT_ID` created in telegram setup step.

```
nano ./xai_monitor.sh
```

Save file

Press `CTRL + X`
Type `Y` and Enter

Alternatively you can review script file on github ([Github](https://github.com/smahe21/Xai-Node-Monitor))

```
https://github.com/smahe21/Xai-Node-Monitor
```

### Test Telegram

Test whether our script is able to send message to our telegram or not.

```
./xai_monitor.sh --test-telegram
```

### Start Monitoring

If you have successfully received message on telegram then we are ready to start our monitoring script.

Run and deattach screen session

```
./xai_monitor.sh
```

4. Detach from this screen session, press `Ctrl` + `A` + `D`.

## Follow me

If you find this guide helpful, consider following me on Twitter for more tips and updates: ([ShineCryptic](https://twitter.com/ShineCryptic))
