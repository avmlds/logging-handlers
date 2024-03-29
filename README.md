# Custom handlers
> Async handlers to throw logs to telegram and discord via Telegram Bot API and Discord Webhook.
>
> **Note!** These handlers are asynchronous, so the `order of the logs is not guaranteed!`
>
>
> `pip install external-logging-handlers`
>
> [PyPi Link](https://pypi.org/project/external-logging-handlers/)

## Usage:
> Specify these environment variables: 
> 
> `TELEGRAM_CHANNEL_ID` - telegram user of channel id \
> `TELEGRAM_TOKEN` - token, that you can obtain from BotFather\
> `SERVER_NAME` - Machine name (useful, if you want to receive logs from different machines) \
> `DISCORD_WEBHOOK_URL` - Webhook url for discord\
> 
>> Special discord parameters [Open Discord docs](https://birdie0.github.io/discord-webhooks-guide/discord_webhook.html) \
>> SENDER_NAME \
>> REGULAR_MESSAGE_TEXT \
>> EMBEDS_TITLE

### You also can configure handlers directly

```python
from custom_handlers.logging_handlers import DiscordHandler, TelegramHandler
import logging
from logging import Formatter

logger = logging.getLogger(__name__)
logger.setLevel("DEBUG")

handler = TelegramHandler(token="ABCD",
                          channel_id="1234567890",
                          formatter=Formatter("%(asctime)s - "))
handler.setLevel("DEBUG")
logger.addHandler(handler)

d_handler = DiscordHandler(sender_name="Again testing",
                           regular_message_text="regular message",
                           embeds_title="Embedded title",
                           )

d_handler.setLevel("DEBUG")
logger.addHandler(d_handler)


logger.error("Error log message")
logger.info("Info log message")
logger.debug("Debug log message")
logger.warning("Warning log message")
logger.critical("Critical log message")
```