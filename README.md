# Up and running

[Forked from this blog post.](http://nsomar.io/java-elixir/)

First build the java executable.

You will need to update the path to your jinterface file in `build.gradle` via the `OTP_ERLANG_JAR` env var:

```
export OTP_ERLANG_JAR="~/.asdf/installs/erlang/24.2/lib/jinterface-1.12.1/priv/OtpErlang.jar"
````

## Building

Next build it,

```
$ gradle build
```

## Running it

First, run an iex terminal,

```
$ iex --sname anyname --cookie secret
```

Then, run the compiled java program,

```
java -jar build/libs/JavaErlang-1.0-SNAPSHOT.jar
```

## Pinging Java

```
iex(anyname@your-machine-name)1> Node.ping(:"server@your-machine-name")
:pong
```

## Sending messages from iex

Using the name of your system, send a message like so,

```
iex(anyname@your-machine-name)1> send({:"java-server", :"server@your-machine-name"}, {self(), :"settext", "Hello from elixir"})
{#PID<0.88.0>, :settext, "Hello from elixir"}
```

You should see the message appear in the Java window.

## Receiving a message in iex

Hit the 'Send Message' button. Then in `iex` run the following to fetch the mailbox,

```
iex(anyname@your-machine-name)3> receive do msg -> IO.inspect(msg) end
'Hello from java'
```
