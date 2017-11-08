---
title:  Write Your Story With Code
navigation_weight: 4
---



# Step 4: Write Your Story With Code

## Learn about Javascript Data Types
Javascript can understand many different types of data, but you often need to tell it what kind of data you're using. For example you can tell Javascript to do 4 + 4. Javascript can do math so you'd expect 8 right? But if you wrap the "4+4" in quotes Javascript will instead return "4+4". If you wrap the fours themselves in strings like "4" + "4" Javascript will return "44". That's because the quotes tell Javascript your four is a "string", which is like a word, rather than a number. Yeah, you'd understand if I asked you "4+4" but Javascript is just a computer language, so it sometimes doesn't understand. 

The reason this is important for our bots is that we need to send Facebook messages that it understands. Our writing can be seen as data as well. It needs to be the right type and also formatted correctly. The data types we'll be using are: objects, arrays, and strings mainly.

We already learned about strings, but what about objects? You can think of objects as just a categorized list. For example you could make an object to organize a phone book. What kind of data would you put in a phone book? Can you think of an example entry?

So like 
> First name: Melissa

> Last name: McEwen

> Phone number : 555-555-555

To turn that into something JS will understand, let's create an object. 

First we want to declare a variable, the variable stores our data. So we can just use the variable in other things rather than writing the data over and over again. You can store any data type in a variable. And you can name it most anything, except you cannot use spaces and certain other characters in JS. 

So I'll just name it Melissa. And to start an object all if have to do is use some "curly braces". 
```javascript
var melissa = {}

```

OK inside those curly braces I'll put my data. Each piece of data has a "key" which tells me what the data is for. Like what kind of data is "McEwen"?

I can use any word I want for this- last name, surname but it is also a variable, it's just like a variable inside the melissa variable, so I'll need to write it as a variable. Then I use a colon and then I the data that is stored - so in this case "McEwen." This is a piece of data and I'm going to use the string type since it's a word. I might also want to use that type for "555-555-5555" because otherwise JS will think it's 555 minus 555 minus 5555 and I want it to just leave it alone and not do math on it :) 
```javascript
phone : "555-555-5555",
firstname: "melissa"
lastname : "mcewen"

```
Now I'll stick all that stuff into my Melissa variable

```javascript
var melissa = {
 phone : "555-555-5555",
 firstname: "melissa",
 lastname : "mcewen",
}

```
Tada! Now you have an object!

We'll also use arrays. Arrays are like lists and they can also contain any data, but they do not have keys like objects do. Think of your favorite foods. We'll turn them into an array.

Arrays use brackets like this and we'll also put our new array in a variable
```javascript
var favFoods = []

```

Now we'll add a bunch of foods in there, as many as we want, the only rule is we separate them by a comma. What kind of data should we format our foods as?

If you said strings you're right!
```javascript
var favFoods = ["pizza", "hot dogs", "lettuce"]

```

These lists can also go inside our object


```javascript
var melissa = {
 phone : "555-555-5555",
 firstname: "melissa",
 lastname : "mcewen",
 favFoods : ["pizza", "hot dogs", "lettuce"]
}

```
## Learn About Documentation

Most APIs have something called documentation, which tell you the correct way to use them. You can find Facebook Messenger's [here](https://developers.facebook.com/docs/messenger-platform/). I'll tell you a bit about how to use it, but feel free to browse around. 

For now let's take a look at [Button Template](https://developers.facebook.com/docs/messenger-platform/send-messages/template/button). The Button Template is one of several different message templates available for Facebook chatbot messages. You saw it used in our test messages. If you scroll down you'll see what you need to send to the API to create one. Take a look at it. While it might look a bit complicated, it's made up of what we just saw before. What data types do you see?

```javascript
curl -X POST -H "Content-Type: application/json" -d '{
  "recipient":{
    "id":"<PSID>"
  },
  "message":{
    "attachment":{
      "type":"template",
      "payload":{
        "template_type":"button",
        "text":"What do you want to do next?",
        "buttons":[
          {
            "type":"web_url",
            "url":"https://www.messenger.com",
            "title":"Visit Messenger"
          },
          {
            ...
          },
          {...}
        ]
      }
    }
  }
}' "https://graph.facebook.com/v2.6/me/messages?access_token=<PAGE_ACCESS_TOKEN>"
```

:tada: **Activity** :tada:
Discuss what the example  parts might mean and what data structures they contain. 



## Learn About Functions
In the previous activity you figured out how a message was formatted with data structures. But you also looked at our first function. A function takes arguments, a type of input, and does things with this. In this case, it took a variable called recipientId as an argument, and took the message and sent it to that recipient. A function can have any name similar to the names allowed for variables.

What a function is called it looks like this:
```javascript
functionName(argument)
```
The function we looked at called another functon 

```javascript
  API.callSendAPI(messageData);
```
Head over to api.js in your Glitch app and take a look at that function. What does it take as an input? What do you think it does?

We also saw that the buttons were an array, that contained a reference to something called a "postback." A postback is just what the button should do when it is pressed, when the button is pressed it has a "payload" which is basically the name of the action triggered. Let's head to actions.js and look at a function there called receivedPostback. What do you think this does?


### :tada: **Activity** :tada:
We're going to practice writing some functions using a site called [jsbin](http://jsbin.com/zuseqe/edit?js,console). See if you can get the myFunction to run and get you the secret code word. Then see if you can write your own function.

```javascript
// example function
function exampleAdd(number1, number2) {
  // console.log just logs the output of our function to the console over here ->
  console.log("hello console")
  // now we'll add the two  numbers
  console.log(number1 + number2);
}

// call the example function
exampleAdd(2, 2);

// declaring a function
function myFunction(argument) {
  //let's store our answer in a variable
  var answer = (argument * 2) - 42;
  //now console.log the answer
  // to combine words we taking strings and using + to put them together
  console.log("look for line " + answer + " in messages.js for the answer");
  
}

// call your function with the number 32 as the argument

// now look in messages.js for the secret code word

// Now let's write your own function to take your first and last name as arguments 
// and log your full name to the console

```


Now take a look at the receivedPostback function in your actions.js file. You're going to see something very important in Javascript. That's the if statement. It looks like this

```javascript
  if (payload === "get_started"){
      Messages.sendGreeting(senderID);
  }
```

Basically what it is doing is saying if the button pressed had the action "get_started" then we do the function in the curly braces {}. What if it's not? Well look at the next if statement. What's that looking for? What do you think we need to do to make all our actions work? 

### :tada: **Activity** :tada:
Check out lines 19-53 in your actions.js, see if you can get your chatbot to respond with the 4 secret messages coded in this code. 




## Add Your Story To A Function
Remember the example from the documentation? Well we won't need to write anything like that because we are using a function that will format our message for us. 

Checkout line 55 in your Glitch app to see the function receivedPostback. Head over to messages.js to check out the function it calls - sendButtons. 
### :tada: **Activity** :tada:
What arguments does sendButtons take? What kind of data does receivedPostback use when it calls sendButtons?


### :tada: **Activity** :tada:
Think of action names for your questions that describe them but are simple lowercase words that are easy to code in, put them on *yellow* :yellow_heart: notecards next to their corresponding question (the :green_heart: *green* cards). 
![adding our variable cards](assets/images/cards-story2.jpg)

The example actions here are:
* get_started
* goodbye
* life
* dislikes
* town
* family
* books
* dreams
* likes


Now we'll add them to our postback function, so that each time a button corresponding to the yellow cards we just created is pressed, the correct message and following buttons are presented:


```javascript
  // if our payload/action is "get_started", send them a message with the following buttons
  if (payload === "get_started"){
     var messageText= "Oh hello! Sorry I didn't notice you, I've been reading this wonderful book. It's my favorite part because—you'll see Here's where she meets Prince Charming But she won't discover that it's him 'til Chapter Three!";
     var buttons = [
     {
      type:"postback",
      payload:"likes",
      title:"Your likes"
    },
    {
      type:"postback",
      payload: "life",
      title: "Your life"
    }
    
    ];
    Messages.sendButtons(senderID, messageText, buttons);
  }
```

The function should refer to the following green cards below it in the outline, or if there are no more left, to the goodbye message
```javascript
  if (payload === "dislikes"){
    var messageText = "Well there is this man in town named Gaston. Boorish, brainless. He thinks I would want to be his wife. Can you imagine?"
    var buttons = [
    {
      type:"postback",
      payload:"goodbye",
      title:"Goodbye"
    }

    ];
    
    Messages.sendButtons(senderID, messageText, buttons);

  }
  
```

These are already coded into the example app, you can simply change the wording. If you need more of them, you can copy and paste. Once you've finished it's time to test your bot out. Does it work? 




```javascript
```
