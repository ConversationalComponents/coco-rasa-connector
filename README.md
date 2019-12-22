# CoCo Rasa Connector

CoCo Rasa connector is a [Flask](http://flask.palletsprojects.com/en/1.1.x/ "Flask") application which allows you to expose your [Rasa](https://www.rasa.com/ "Rasa") bots as a components at the [CoCo marketplace](https://marketplace.conversationalcomponents.com/ "CoCo marketplace").

### Deployment Flow:

1. Deploy Rasa Bot(Do not forget to enable the API).
2. Place the bot API URL in a JSON format at the following directory at the CoCo Rasa Connector source:
`/RasaManager/components` - Each file represent a component which can be accessed through an http call to` https://<host>/api/exchange/<file name - no extension>/<session ID>`
3. Map the 3 intents from Rasa bot at the config.py file(Create new
record for your component):
	- **Done Action** - Action which will be triggered when the bot/`component` achived it's goal.
	- **Failed Action** - Action which will be triggered when the bot/`component` will not complete it's goad.
	- **Out Of Context** - Action which will be triggered when the conversation went out of context.
4. Upload the Flask app to a cloud service(Google app engine is recommende - yaml file included.)

### Deployment Flow:

#### 1. Deploy Rasa bot, look at the Rasa get started page:

    https://rasa.com/docs/getting-started/

### 2,3. Create config for the component and place it at the components directory.
 ![Create component config.](/Screenshots/1CreateConfig.png)

### 4. Map client commands to component states at config.py.

config.py:
```
    ACTIONS_MAPPING_CONFIG = {
        "default": {
            "COMPLETE_ACTION": "goodbye",
            "FAILED_ACTION": "deny",
            "OUT_OF_CONTEXT_ACTION": "bot_challenge"
        },
        "default_bot": {
            "COMPLETE_ACTION": "goodbye",
            "FAILED_ACTION": "deny",
            "OUT_OF_CONTEXT_ACTION": "bot_challenge"
        }
    }
```

#### 5. Upload the Flask app to a cloud service.

 Open bash, configure gcloud tools and then run the following command:

    ```gcloud app deploy```



