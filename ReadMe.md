# Build a Alexa App in Python

Amazon Developer Hub [https://developer.amazon.com/alexa](https://developer.amazon.com/alex)

Amazon Console [https://console.aws.amazon.com/lambda](https://console.aws.amazon.com/lambda)

## Intent Schema
```
{
  "intents": [
    {
      "slots": [
        {
          "name": "number",
          "type": "AMAZON.NUMBER"
        }
      ],
      "intent": "UserGuess"
    }
  ]
}
```

"name" can be any string. Use that string in the sample utterance below where you want to keep part of the user's response.
"intent" is the the identify used in Sample Utterance and sent to you function, and used in your function to determine which action to take based on user's response. 

## Sample Utterance
```
UserGuess my guess is {number}
UserGuess {number}
```

## Create an Alexa Skill

On this Screen you can configure Test Events at the top to debug failing error states. This is useful
later when you want to release your own skill. 
Configure your Alexa Skill with the Amazon developer portal.
1. Sign in to the Amazon developer portal at https://developer.amazon.com/. If you haven’t done
so already, you’ll need to create a free account.
2. Select Amazon Alexa.
3. Select Alexa Skills Kit,
4. Select Start a Skill.
5. Name your skill. This is the name displayed to users in the Alexa app. For this example, we’ll call
it Pyladies Bagels. 
6. Create an invocation name. This is the word or phrase that users will speak to activate the skill.
For this walkthrough, we’ll use the skill name Bagels (case-sensitive). Users will say, "Alexa,
open Bagels" to interact with your skill. Choose Save to continue to development for our Alexa Skill.
7. Choose Next to continue to development for our Alexa Skill.
8. In the Intent Schema box, type the following JSON code above.
9. Under Sample Utterances, enter all the phrases that you think users might say to interact with
your skill. The more phrases you enter, the better the results. For examples see above.
10. Choose Next and wait until the interaction model finishes loading, in no more than a few
seconds.


## Build your Lambda Function

To add your code to Amazon Web Services as a Lambda Function.
1. Log in to the AWS Management Console at https://aws.amazon.com/console.
 If you haven’t done so already, you’ll need to create a free account.
2. From the list of services, select Lambda.
3. In the upper right of your screen Click on the region drop-down.
4. Select US East (N. Virginia), which is a supported region for Lambda functions used with the
Alexa Skills Kit.
5. Select Create Function.
6. Select Blueprints
7. In the search filter box, type alexa.
8. Select blueprint alexa-skills-kit-color-expert-python. Make sure to choose the blueprint that
ends in -python.
9. Select Configure.
10. Name your function.
11. For Role Select Create a custom role.
12. This will open the IAM Console
13. Select lambda_basic_execution as your IAM Role.
14. Select Allow to return to AWS Console
15. Refresh your browser
16. Select use existing role
17. Select lambda_basic_execution
18. Code is preconfigured by the chosen blueprint, but in the future you can add your code on this
page.
19. Select Create Function.
20. Copy the Amazon Resource Name (ARN) displayed in the upper-right corner of the console that
starts with arn:aws:lambda....

### We started editing the Lambda function at the meetup, but were not able to finish this month. See our progress in [our Lambda Function](Lambda%20Bagels%20Alexa.py)

Every Alexa skill needs an event handler. In the blueprint at the bottom of the Color Picker code there is a function lambda_handler(event, context) that should not be altered. This will call the on_launch() when the skill is opened or  on_intent when the user gives a response.

```
def lambda_handler(event, context):
    """ Route the incoming request based on type (LaunchRequest, IntentRequest,
    etc.) The JSON body of the request is provided in the event parameter.
    """
    print("event.session.application.applicationId=" +
          event['session']['application']['applicationId'])

    """
    Uncomment this if statement and populate with your skill's application ID to
    prevent someone else from configuring a skill that sends requests to this
    function.
    """
    # if (event['session']['application']['applicationId'] !=
    #         "amzn1.echo-sdk-ams.app.[unique-value-here]"):
    #     raise ValueError("Invalid Application ID")

    if event['session']['new']:
        on_session_started({'requestId': event['request']['requestId']},
                           event['session'])

    if event['request']['type'] == "LaunchRequest":
        return on_launch(event['request'], event['session'])
    elif event['request']['type'] == "IntentRequest":
        return on_intent(event['request'], event['session'])
    elif event['request']['type'] == "SessionEndedRequest":
        return on_session_ended(event['request'], event['session'])

```

These functions call another function that both returns a build response that is sent back to the alexa. It will include session attributes which can include values you want to keep. By default there is no information stored in your lambda function so if you need to store a generated number or other information you must pass it in as a session attribute when you build a response. Each session variable is stored as a { "key": "value"} object. 

```
def build_speechlet_response(title, output, reprompt_text, should_end_session):
    return {
        'outputSpeech': {
            'type': 'PlainText',
            'text': output
        },
        'card': {
            'type': 'Simple',
            'title': "SessionSpeechlet - " + title,
            'content': "SessionSpeechlet - " + output
        },
        'reprompt': {
            'outputSpeech': {
                'type': 'PlainText',
                'text': reprompt_text
            }
        },
        'shouldEndSession': should_end_session
    }
	
def build_response(session_attributes, speechlet_response):
    return {
        'version': '1.0',
        'sessionAttributes': session_attributes,
        'response': speechlet_response
    }
```
	

## Attach the newly created Lambda Function to you Alexa Skill

1. Return to Developer Hub
1. Select the Endpoint AWS Lambda ARN then paste your ARN code from the AWS Lambda
Function.
1. At Provide geographical region endpoints Choose Yes, then select North America as your
region,
1. For Account Linking select No, then choose Next.


## Testing your Alexa Skill
Here you can get responses from your function. Type in "alexa open __ " where __ is whatever you entered as you invocation name 

Since we've not customized it, you should get a response from the color picker. 

As you develop your skill you can test your if it is working. If you get an error, you can copy the Lambda Request generated and add to your Lambda Function as a
Test Event to get more detailed information about what went wrong.

Once your skill passes basic tests, you can test on your echo or if you do not have an echo, you can test
your skill in a web browser at https://echosim.io/welcome.


## Publishing your Alexa Skill.
Once you’ve tested your skill and addressed any bugs, you can complete the Publishing Information.

Select a Category where the Skill be listed.

You can add details in the Testing Instructions that will be sent to your skills reviewer. This will not be
publicly visible.

Know that Alexa approval can take several weeks, and it is common to be rejected once or twice for
edge cases you forgot to test. Also Amazon doesn’t like to publish identical skills, so if your skill already
exists in the Alexa Skills Store, you might have tweak your Skill to differentiate. 