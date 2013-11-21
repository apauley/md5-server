# A Simple TCP Server Programming Exercise

This exercise assumes you are a candidate applying for a job as a programmer.
The purpose of this exercise is to determine how you solve problems and what you believe is good code.

## The Task

Write a simple line-terminated TCP server that listens on some port and calculates the
MD5 sum of the data received, returning it as a hex-encoded string.

Please provide detailed instructions on how to quickly get your code
up and running.

Assuming your server is listening on port 7000, we can test it using
the netcat command-line utility:

```bash
$ echo 'Hello, MD5 server!' | nc localhost 7000
fb7983521dee01530fbb5b52993bda42
```

Since our TCP server is line-terminated, sending multiple lines will return multiple hashes:

```bash
$ echo -n -e 'Hello, MD5 server!\nGoodbye, MD5 server!\n' | nc localhost 7000
fb7983521dee01530fbb5b52993bda42
639db52c22b6d642ecfd8ff215be8379
```

We can verify if it is correct by comparing it with a command-line
md5 utility:

```bash
$ SERV_OUT=$(echo 'Hello, MD5 server!' | nc localhost 7000)
$ echo $SERV_OUT
fb7983521dee01530fbb5b52993bda42
$ CLI_OUT=$(echo 'Hello, MD5 server!' | md5)
$ echo $CLI_OUT
fb7983521dee01530fbb5b52993bda42
$ [ $SERV_OUT = $CLI_OUT ] && echo "Great, our MD5 server seems to be working"
Great, our MD5 server seems to be working
```

Your server should allow multiple concurrent connections.
We can test this by connecting to the server from multiple shells at
the same time:

```bash
$ nc localhost 7000
Hello from shell 1
ed3f45a52f2485dae6c98af5ddb290e8
```

```bash
$ nc localhost 7000
Hello from shell 2
3b00c548dbaba28d4799e9234735dcb7
```

## Online Resources

You are welcome to use any library or code you find online to assist you,
but please indicate clearly where you found such code and which parts are your own work.

For this exercise it may be helpful to look at TCP echo server implementations.

## Evaluation Criteria

Firstly, the code has to be correct. But working code is only the
first step in any program.

Some other criteria can be:

 * Reliability. What happens if things fail?
 * Simplicity. See "Reliability" above.
 * Performance. What happens if we put your server under load?

It is basically up to you to implement a solution that shows off your
skill level and what you believe is good code.
