# Build a Alexa App in Python

Amazon Developer Hub [https://developer.amazon.com/alexa](https://developer.amazon.com/alex
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