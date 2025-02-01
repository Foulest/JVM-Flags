# JVM-Flags
If you're anyone like me, you've probably seen and used [Aikar's flags](https://aikar.co/2018/07/02/tuning-the-jvm-g1gc-garbage-collector-flags-for-minecraft) for Minecraft servers before.

They're completely unusable for servers with lower RAM amounts, ballooning your actively used RAM way higher than needed. Server hosts charge based on your RAM amount per month, so save some money and use the JVM flags below:

#### Java 8

```
java -Xms128M -Xmx{{SERVER_MEMORY}}M -XX:+UseConcMarkSweepGC -XX:+UseParNewGC -XX:+CMSClassUnloadingEnabled -XX:ParallelGCThreads=4 -XX:MaxGCPauseMillis=50 -XX:+DisableExplicitGC -XX:+OptimizeStringConcat -XX:+AlwaysPreTouch -XX:+UseFastAccessorMethods -XX:+UseCompressedOops -XX:+AggressiveOpts -XX:+UseBiasedLocking -Dterminal.jline=false -Dterminal.ansi=true -jar {{SERVER_JARFILE}}
```

Compared to Java's default flags, these keep memory extremely low with minimal performance impacts. You should expect solid performance your memory, at it's worst and fullest, to sit right around 70% if all ends well with garbage collection. If you're on higher Java versions than Java 8, I'd advise against using the flags above.

### Things to Change
- Replace `{{SERVER_MEMORY}}M` with your server's memory in megabytes or gigabytes. *(Ex: 2048M or 2G)*
- Replace `{{SERVER_JARFILE}}` with the name of your server's JAR file. *(Ex: server.jar)*

Most server hosts like [HeavyNode](https://heavynode.com) support these placeholders. But, a lot of server hosts don't let you change JVM arguments at all, which is relatively unfortunate. If that's the case for you, this repository doesn't apply to you, and you're stuck with what you've got.
