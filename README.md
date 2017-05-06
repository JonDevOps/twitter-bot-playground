# Twitter bot playground

This is a reference for me and anyone else that's interested in Twitter bots in JavaScript

I'm using the `twit`  npm package there are others out there to use

So if you don't know how to use node or have your environment set up to use it take a look at the README.md on my Twitter bot bootstrap which details getting a Twitter application set up and a development environment with c9

A lot of this information is already out there so this may be repeating stuff that is elsewhere I'm doing this for my learning.

Once you have your bot set up you can use the following 

To get a list of followers ids use `.get('followers/ids'...`

```javascript
bot.get('followers/ids', {
  screen_name: 'DroidScott'
}, function (err, data, response) {
  if (err) {
    console.log(err)
  } else {
    console.log(data)
  }
})
```

Or to get a detailed list you can use `.get('followers/list'...` 

Here we print off a list of `user.screen_name`'s

```javascript
bot.get('followers/list', {
  screen_name: 'DroidScott'
}, function (err, data, response) {
  if (err) {
    console.log(err)
  } else {
    data.users.forEach(function (user) {
      console.log(user.screen_name)
    })
  }
})
```

To follow back a follower we can use `.post('friendships/create'...` here the bot following back the user `MarcGuberti`

>A bot should only follow users that follow the bot.

```javascript
bot.post('friendships/create', {
  screen_name: 'MarcGuberti'
}, function (err, data, response) {
  if (err) {
    console.log(err)
  } else {
    console.log(data)
  }
})
```

Like with followers you can get a list of accounts that your bot is followingback

```javascript
bot.get('friends/ids', {
  screen_name: 'DroidScott'
}, function (err, data, response) {
  if (err) {
    console.log(err)
  } else {
    console.log(data)
  }
})
```

And also a detailed list

```javascript
bot.get('friends/list', {
  screen_name: 'DroidScott'
}, function (err, data, response) {
  if (err) {
    console.log(err)
  } else {
    console.log(data)
  }
})
```

Get friendship status this is useful for following new followers, this will give us the relation of a specific user

```javascript
bot.get('friendships/lookup', {
  screen_name: 'ScottDevTweets'
}, function (err, data, response) {
  if (err) {
    console.log(err)
  } else {
    console.log(data)
  }
})
```

If the user follows the bot, then relationship will be:

```shell
[ { name: 'Scott Spence 🌯😴💻♻',
    screen_name: 'ScottDevTweets',
    id: 4897735439,
    id_str: '4897735439',
    connections: [ 'followed_by' ] } ]
```

If the user and the bot are following each other, the relationship will be:

```shell
[ { name: 'Scott Spence 🌯😴💻♻',
    screen_name: 'ScottDevTweets',
    id: 4897735439,
    id_str: '4897735439',
    connections: [ 'following', 'followed_by' ] } ]
```

And if there is no relationship then:

```shell
[ { name: 'Scott Spence 🌯😴💻♻',
    screen_name: 'ScottDevTweets',
    id: 4897735439,
    id_str: '4897735439',
    connections: [ 'none' ] } ]
```

Direct Message a user with `bot.post('direct_messages/new'...`

>A bot should only DM a user that is following the bot account

```javascript
bot.post('direct_messages/new', {
  screen_name: 'ScottDevTweets',
  text: 'Hello from bot!'
}, function (err, data, response) {
  if (err) {
    console.log(err)
  } else {
    console.log(data)
  }
})
```



