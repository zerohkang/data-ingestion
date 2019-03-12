# flume exercise 09231 younghun knag 강영훈

## 1.Create a new flume configuration file with the following

*Ans
### spooldir.conf: A Spooling Directory Source

### Name the components on this agent
agent1.sources = mySource\
agent1.sinks = mySink\
agent1.channels = myChannel\

### Describe/configure the source
agent1.sources.mySource.type = netcat\
agent1.sources.mySource.bind = localhost\
agent1.sources.mySource.port = 44444\

### Describe the sink
agent1.sinks.mySink.type = logger

### Use a channel which buffers events in memory
agent1.channels.myChannel.type = memory\
agent1.channels.myChannel.capacity = 1000\
agent1.channels.myChannel.transactionCapacity = 100\

### Bind the source and sink to the channel
agent1.sources.mySource.channels = myChannel\
agent1.sinks.mySink.channel = myChannel\

## 2. Start the agent.

*Ans
flume-ng agent \
--conf /etc/flume-ng/conf \
--conf-file $DEVSH/exercises/flume/new_spooldir.conf \
--name agent1 \
-Dflume.root.logger=INFO,console

## 3. From another terminal start telnet and connect to port 4444. Start typing and you should see the results from the other terminal. Provide a screenshot of your results.

*Ans
[training@localhost ~]$ telnet localhost 44444\
Trying 127.0.0.1...\
Connected to localhost.\
Escape character is '^]'.\
hello\
OK\

**i have screenshot as flume_agentlog.png

# .end

