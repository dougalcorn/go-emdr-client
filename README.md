# Simple Go EMDR Client

This is a very simple client for connecting to the
[EVE Market Data Relay](http://www.eve-emdr.com/en/latest/) network.
This is a [ZeroMQ](http://zeromq.org) network of user submitted
information about the player-driven market in
[EVE Online](http://eveonline.com). The messages received are in the
[Unified Uploader Data Interchange Format](http://dev.eve-central.com/unifieduploader/start)
as specified by [EVE Central](http://eve-central.com).

Players voluntarily upload market data as they are playing the game.
When a player makes a market query in game, that data is cached
locally on their computer. This cache can be parsed and uploaded
through various
[clients](http://dev.eve-central.com/unifieduploader/implementations).

![is it live, or memorex?](https://pbs.twimg.com/media/BYzDsJYIcAEYVwo.jpg:large)

This is "drinking from the fire hose". I have seen the messages come
in at over 20 a second. There are two types of messages: orders and
history. The contents of the message depend on its type.

For order messages, you'll have rowsets with a row for each order on
the market. For high volume items, that could be hundreds of rows. For
low volume items, it may only be a few.

For history messages, you'll have a rowset with a row for each day.
How many days depend on the date range the player specified in the
client. It may only be a week's history, or could be a year's history.

You should know what you want to do with this data and only keep the
pieces you need. Keeping it all in a format that's easy to search is
hard and will take a lot of disk space.

I've also published a very similar
[Ruby EMDR Client](http://github.com/dougalcorn/ruby-emdr-client).

## Requirements for ZeroMQ

I had some trouble getting Go to work with ZeroMQ.


1. `brew install zeromq22`
2. `go get "github.com/alecthomas/gozmq"`
3. Apply the [zmq_2_x.go.patch](zmq_2_x.go.patch)
4. `export CC=clang`

The gozmq package won't build on Mac OS 10.9 and ZeroMQ 3.x with Go
1.1.

## Usage

Then you should simply be able to run the client like so:

    go-emdr-client

This will connect to the EMDR and puts out a notice about every
message received:

```
```

It will also puts out the rate at which messages are being received
every 30 seconds:

```
Receiving 9.766227349206408 messages/sec
```


## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
