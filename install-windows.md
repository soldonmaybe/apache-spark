## Windows

Here we'll show you how to install Spark 3.3.0 for Windows.
I installed it in Windows 11 Edition, but it should work
for other versions distros as well

In this tutorial, we'll use [MINGW](https://www.mingw-w64.org/)/[Gitbash](https://gitforwindows.org/) for command line

If you use WSL, follow the instructions from [linux.md](linux.md) 


### Installing Java

Spark could run on java 19. Download it from here: [https://www.oracle.com/java/technologies/downloads/#jdk19-windows](https://www.https://www.oracle.com/java/technologies/downloads/#jdk19-windows). Select “Windows x64 Compressed Archive” (you may have to create an oracle account for that)

Unpack it to a folder with no space in the path. We use `C:/tools` - so the full path to JDK is `/c/tools/jdk-19`


Now let’s configure it and add it to `PATH`:

```bash
export JAVA_HOME="/c/tools/jdk-19"
export PATH="${JAVA_HOME}/bin:${PATH}"
```

Check that Java works correctly:

```bash
java --version
```

If it running and show output for your java, then it works correctly.

### Spark

Now download Spark. Select version 3.3.0 (latest)

```bash
wget https://dlcdn.apache.org/spark/spark-3.3.0/spark-3.3.0-bin-hadoop3.tgz
```

Unpack it in some location without spaces, e.g. `c:/tools/`: 

```bash
tar xzfv spark-3.3.0-bin-hadoop3.tgz
```

Let's also add it to `PATH`:

```bash
export SPARK_HOME="/c/tools/spark-3.3.0-bin-hadoop3"
export PATH="${SPARK_HOME}/bin:${PATH}"
```

### Hadoop

Next, we need to have Hadoop binaries. 

We'll need Hadoop 3.0 winutils.exe which we'll get from [here](https://github.com/steveloughran/winutils/tree/master/hadoop-3.0.0/bin).

Copy files to folder spark-3.3.0-bin-hadoop3

or

Add it to `PATH`:

```bash
export HADOOP_HOME="/c/tools/spark-3.3.0-bin-hadoop3"
export PATH="${HADOOP_HOME}/bin:${PATH}"
```

### Testing it

Go to this directory

```bash
cd spark-3.3.0-bin-hadoop3
```

And run spark-shell:

```bash
./bin/spark-shell.cmd
```

At this point you may get a message from windows firewall — allow it.


There could be some warnings (like this):

```
WARNING: An illegal reflective access operation has occurred
WARNING: Please consider reporting this to the maintainers of org.apache.spark.unsafe.Platform
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
```

You can safely ignore them.

Now let's run this:

```
val data = 1 to 10000
val distData = sc.parallelize(data)
distData.filter(_ < 10).collect()
```

### PySpark

It's the same for all platforms. Go to [pyspark.md](pyspark.md). 
