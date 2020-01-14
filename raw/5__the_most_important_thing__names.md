# 5. The Most Important thing: Names

## Names, really? Yes. 

In our collective struggle for then cleanest code, I realized that fads come and go. XML was "clean" a long time ago, then JSON was trumpeted as "human readable", then we had YAML sold as JSON "but readable"... We had Object Oriented Programming marketed as a way to have very clear code, then hardcore OOP kind of fell out of fashion in favour of an imperative/functional mix. One thing, however, mantains its importance as the fads come and go: well thought out names. Be it in any programming language, in database design, in Excel or even just organizing files, learning to choose proper names will up your game as a developer forever.

You should be spending about 10-20% of your coding time thinking about, changing, correcting and refactoring names. If you are not, your names probably suck.

There is a very famous quote:

> There are only two hard things in Computer Science: cache invalidation and naming things.
> 
> -- Phil Karlton

Cache invalidation is indeed hard, and I will not event begin commenting on it here. But... naming things seems a bit simpler right? After all, after 5 seconds, you can just choose any name, be on your way and the code will still work! Well, it will work in the computer domain but you have probably failed in the human domain. Names are very important for humans, i mean, REALLY important. How would you feel if your name was "XBGS" ([looking at you Prince](https://www.bbc.com/news/magazine-36107590)). Your childhood would have been worse. Thank your mom and dad for choosing a sensible name! As a software developer you are going to give birth to thousand of functions, products, variables, instances, classes, repositories, etc…. You will give more names than the hospital's nurse. You better be good at it, really good. The good news is that its not that hard to train yourself to be good at it.

<!--
Names are very important in programming because they let you go up and down the abstracion ladder. For example, when I say "jungle" I represent many different objects by it. There are animals and plants, and soil and rain. By "animals" you know I can mean birds, snakes, frogs, apes… By snakes, you know that I could be talking about many different species, but you will intuitively know what they are. Say you are looking for a specific functionality related to "rattlesnake" in your code. You would never even look at a folder named "ocean". But a "jungle" folder would catch your attention, and you would jump to it's "snakes" file happelly. 
!-->

<!-- Todo
## FAQ
 
Name is too long. You are half typewriter, half reader, and half thinker. Let me tell you, i only type those long names once. I use autocomplete all the time, avoiding typos.
!-->


## Writing good names

Now I will give some very pragmatic tips on writing good names for your variables, functions, and files.


<!--
### Good comment, bad name

Comments aren't always a good thing <small><small> (just head to YouTube's comment section; I rest my case)</small></small>. If you comment your code like there's no tomorrow you are not being helpful as your teacher told you are. 
!-->

## Fixing bad names
 
First, lets take a good look at some common problems with names, and how to correct them.

#### x. Bad Order
Are the words in a readable order, do they make sense if spoken out loud? Your code will be read faster if the words are in a sensible order. Also, people will talk about your code out loud, in meetings, in code reviews. Having natural sounding names helps everyone understand faster.

    image_s3_get() => get_image_from_s3()

#### Unpronounceable
Can your variable or product name be easily spoken and understood without typos, doubts or long boring spellings?

If you work with AWS you probably heard about S3, Amazon's cloud "Simple Storage System".

    Simple Storage System => sss => s3

Notice how Amazon uses S3 as the acronym for "Simple Storage System". It is incovenient (and very inapropriate) to say "sss", so they made a right naming choice there!

### Names that lie
What's worse than a name without any meaning? A name with the **wrong** meaning! I call these "liar" names, and you should burn them with fire! Names (like people) can lie in many different, subtle ways. You will need to stay alert!

#### Lying about type
Sometimes, names imply a specific type. For instance, you expect a variable called price to contain a number, because 99% of the time, prices are expressed in currency values. But let's say your price variable is a string, because you want to keep the currency symbol such as:

```python
    price = "US$ 20.00" 
```

This is a soft lie by omission. You need to change the name of the variable to `price_as_string`, as a warning. Or else someone will someday do `item.price + item2.price` and you will get a non-sensicall concatenated string. That's the evil power of lying names. People expect to be able to sum prices, they will end up doing it. (In this case, obviously, the best thing would be to use a `Currency` class, instead of storing plain strings.)

---

Even worse, sometimes names are outright lying about their type! A classic example I see all the time when dealing with data and databases are these below:

Look at this table column's name:

| `chat_date` |
| -------- |
| `2019-01-01 22:23:19`|

Now, is `2019-01-01 22:23:19` a `date`? I'm sorry, but it is not! This is a `timestamp` (also called `datetime`), another similar, but different, [data type](https://www.postgresql.org/docs/current/datatype-datetime.html). So call it `chat_timestamp`, or better yet, call it `chat_creation_timestamp`, or `chat_last_update_timestamp`, so that there is no ambiguity as to what time are we actually talking about. 


---

```python
chat_name = 34234
```

This is not the chat's "name", but clearly its identifier (very commonly abbreviated as `id`). Name usually implies strings, not numbers. It is easy to fix this, just call it `chat_id = 343434`

--- 
What about this?

```python
chat = 34234
```

Obviously chat is an object or an array of messages, but certainly not a number! Same solution, just change it to `chat_id = 343434`

---
Another classic,
```python
base_folder = '/tmp/'
filename = base_folder + 'food'
```

Ooops. That is a path, not a name! `file_path` would be better here.


#### Wrong verbs
Just as nouns suggest certain types for variable names, verbs suggest behavior for functions and methods. For example, a function with the verb "get" usually returns something!

Suppose your function `get_image(image_url)` goes to that url and saves the image in `~/Downloads` and doesn't return anything. Sure, it is "getting" the image in some sense, but it's not good enough, as `get` suggests too strongly that it would return the image to the caller. Just rename it to `save_image_to_disk(image_url)`, or even better, `download_image`. 

	
#### Plural/Singular
All right, this is easy. Just like we've learned at school, when you have many (arrays, lists, sets), use plural. If you have only one (number, string, object), use singular nouns.

```python
chat_id = [123, 3424, 5345]
```
	
This is just plain wrong! Change it to `chat_ids`, if they are all ids to the same chat, or `chats_ids` if each id belongs to a different chat.

---

```python
category = [1020, 1040, 1060]
```

Change it to `categories`, or even better, specify more: `chat_categories`

### Consistency
This is very important. A developer can adapt to your style pretty quick, but make sure your code has a *single* style, or else it is going to be a constant strain on the reader.

**Tip:** you will probably be using the basic CRUD (create, retrieve, update, delete) operations in your code. There are many synonyms, and each one has its own flavors. You can have different synonyms in your code, but make sure they are being used for different thing. For example, you could have `get` for everything local, and use `request` for functions that will make an HTTP/RPC call. Just don't include new verbs in your codebase without any reason.

#### Examples of verbs and their implicit characteristics:

|verb|implicit characteristic|
|----|---------|
|create|fast, in memory|
|send|create somewhere else, like a new message in a remote queue|
|post|create using an HTTP request|
|upload|create in remote server, usually a file|
|save|create a file to disk or create/update object in database|
|||
|get|fast, in memory|
|load/retrieve/fetch|slower, maybe HDD reading|
|request|http request, service call|
|||
|process/calculate|imply that you will create new data based on old data. For example, you could have a function called `calculate_age(birth_date)`.|
|generate|if your new data is not based on any existing data, prefer using generate. For example `generate_chat_id()`|
|||
|update|change part of the object, for example user.update({"age": 10}) will only update the user's age, leaving other information intact.|
|patch|same, but HTTP request context|
|replace / change / set|completely replace the thing, for example: `user.set_address({'street': 'North Street'})` will completely replace the address|
|put|same, but HTTP request context|
|||
|delete|good, universal word|
|kill|usually used for deleting running processes, or machines|
|destroy|dramatic effect can be used to scare people from doing something stupid. <small>(But they will do it anyway 🙂)</small>|
|purge|delete it, and everything related to it, Stalin Style|
|||
|pop|retrieve and item from a container and then remove it|



I will show examples of good and bad API's.
Bad example: pandas API, good example: aws api

<!-- TODO
### Destrutividade do estado / side effects
%%%
calculate_age/update_age
Idempotency
-->

### Useless words
Some words are notorious for the lack of information they carry. They are so generic that could be applied to almost anything and you should avoid them. Words like `data`, `object`, `stuff`, `thing`, `x`.

Take a look at the following code:

```python
response = requests.get(url)
data = response.data
send_email(to='you@email.com', subject="look at my photo", attachment=[data])
```

This code looks ok, but if you had some more lines between 2 and 3, you would forget what that `data` means. Because data is usually a bad word. You can correct that by changing `data` to another word. Lets think through together: First, I thought about `image_data`, that would be enough but i still feel like we can do better than that. What if i take out the `data` and just leave `image`? No, I think just image would suggest that everything about the image is there (the content, the filename, the size, etc…), in other words, it suggests an instance of some custom class Image. This is just the binary content of the image, so what about `image_content`, it seems better, but I still can't be sure if it is the image's binary or maybe a string description of what the image *contains*. So, lets try to choose a word that relates to the binary nature of this data. What about `image_bytes` (%% foot note %% bytes is a type in python that is used for storing binary strings, think C byte arrays)? I like this name, it is very specific and conveys a good amount of information!

```python
response = requests.get(image_url)
image_bytes = response.data
send_email(to='you@email.com', subject="look at my photo", attachment=[image_bytes])
```

The same lessons apply to methods and functions:

```python
def get_data(url):
    # …
```

Explain out loud to someone or to an imaginary friend. What kind of data is this function fetching? "It gets the image's data from an url and returns it to the caller as a bytes". Ok, so use words from your explanation and change it to:


		
```python
def get_image_bytes(url):
    # …
```


Exceptions: There are some cases where using `data` or other generic word is justified, for example in the requests HTTP library you have a `response.data` property, and it is not horrible as an HTTP response's content is quite generic. Another example is in algorithm's implementations such as `def square(x): return x * x`. I could name `x` `number_to_be_squared` but this wouldn't actually help much, especially with the function being that small. Your experience will dictate when you should use the exception card, but always think twice before using those words.

### Avoid reserved words
Depending on your programming language and environment, some words are reserved, or are builtin functions and constructs. For example, in python, `id` is bound to the built-in "id(object)" function. `print`, `type`, `str` are all built-in names in python. However, python does not prevent you from assigning them. For example, you could, do crazy stuff like `str = 4`! Of course, real world examples are not that ridiculous, but they do happen sometimes. For example:

```python
def format_money(amount):
    str = "{}.00".format(amount)
    return str
```

This is more realistic, and it can cause real trouble! Suppose you want to use the original str later on in that function. It would fail spectacularly!

```python
def format_money(amount):
    str = "{}.00".format(amount)
    currency = Dollar()
    str = str(currency) + str  # would break here, str is not a callable anymore, you just assigned a plain string to it!
    return str
```
 
Remember that argument names are also variable bindings, so if you create a function like this:

```python
def make_purchase(item, print=True):
    buy(item)
    if has_ink() and print:
        print_receipt()
```

You have just created a trap from anyone trying to call the good ol' `print` function later on. 

The solution is pretty easy, just think a bit and make the names more specific. Such as `formatted_string` in the first example or `request_printed_receipt` in the second one. It took me 5-10 seconds to think each of these names. It takes some thought but is still pretty cheap price for the confusion you will avoid!

If you absolutely can't avoid using a builtin name, I suggest adding a `_` after it, like that: `class_` or `print_`

### No abbrvtns
When you use abbreviations who is getting anything out of it? It's not the reader! For the reader, it's just easier to read full, correct wds than hvng to decode abbrvtns in real time. So it must be the writer, saving those precious keystrokes! But remember, when people are coding, they spend 80% in reader mode vs 15% in writer mode <small><small>(5% in WTF mode)</small></small>! So reader trumps writer, which means no abbreviations. Just write the long word as fast as you can! If you want to save time, type faster, it's a good skill to learn anyway. 

Exception: there are exceptions to this rule. If you are using a well known abbreviation in your business domain, you are excused. So you can use FBI_agent_id or check_if_RAM_is_full(). Also, for small scope (more on that later) variables I usually allow myself to use `ret` as a placeholder for a function's return value, `req` and `res` for an HTTP request and response respectively, and other similar, non-ambiguous and repetitive cases. But remember: *In case of doubt, write it all out!* <small><small>(it rhymes!)</small></small>

### The scope rule
How often, and who is calling your function/calling your endpoint/accessing your variable/editing your file? Think about it, if people are calling your function from very far away they have very little context of your code.

Basically, the rule is: the larger the scope, the better documented the code should be.

(An extra incentive for you to have lots of small-scoped code and the least possible global and public scoped code)

Here is an approximate hierarchy of how well named and documented your code should be:

---

||
---
|public function/class/method of a public library |
|public function/class/method of a private library | 
doc-string with examples, great stand-alone names 
||
---
|public function/class/ of an application|
great stand-alone names 
||
---
|folder/file name|
|global variable|
great names
||
---
|private function/class/method names|
|private variable|
|local variable|
|local variable in a private function|
good names
||
---
|local variable in a very small (<=2 lines) function/lambda/scope 
single letter variable is ok here

---

You can see that the more public your code is, the larger the scope in which that name is a valid call, the better and the more self-explanatory your name should be. So, a public global variable name that can be accessed anywhere in your program should carry with it all necessary information to understand it at any scope. So you shouldn't call it: 

```python 
GOOD = [200, 201]
```

instead do:
```python 
GOOD_HTTP_STATUS_CODES = [200, 201]
```

But, its ok to call it `GOOD` if its in a small scope in which its meaning is obvious:

```python
def call_external_service(url):
    response = _do_request(url, timeout=3)
    GOOD = [200, 201]
    if response.status_code in GOOD:
        return response
    else:
        return False
```

What about great vs good names? This is just about how much time and effort you will spend thinking and changing that name until you are satisfied. Which leads me to the next point:

### Don't be afraid to change names often
Code evolves, things change, and you also will become more aware and have a better understanding of your functions and variables. As function's responsibilities and variable's contents become evermore clear their name should evolve too. Don't be afraid to stop, think and change names you only just written. I will usually change a function's name about twice, once after 3 minutes of writing it and the next one after a day or so. I will often finish writing a function, and then, when I try to call it somewhere I realize the name is not clear in that context, so I change it. And then after a good night's rest, I will look at that code and take too long to understand it. I will think about what information I had to deduce, and then try to encode that information in the object's name.

### Final thoughts
Basically, if you are spending only 1% of your time thinking about names, simply writing the first thing that comes to mind, and you haven't changed the names of any function or variable in the last 2 hours programing, your names probably suck. Why exactly are you in such a hurry? You are expected to deliver, good, quality code here! Attention to detail will pay off in the long run for sure. Your future self and coworkers will thank you.
