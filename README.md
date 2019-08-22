### airline
---
https://github.com/airlift/airline

```java
public class Git
{
  public static void main(String[] args)
  {
    CliBuilder<Runnable> builder = Cli.<Runnable>builder("git")
      .withDescription("the stupid content tracker")
      .withDefaultCommand(Help.class)
      .withCommands(Help.class, Add.class);
    
    builder.withGroup("remote")
      .withDescription("Manage set of tracked repositories")
      .withDefaultCommand(RemoteShow.class)
      .withCommands(RemoteShow.class, RemoteaAdd.class);
      
    Cli<Runnable> gitParser = builder.builder();
    
    gitParser.parse(args).run();
  }
  
  public static class GitCommand implements Runnable
  {
    @Option(type = OptionType.GLOBAL, name = "-v", description = "Verbose mode")
    public boolean verbose;
    
    public void run()
    {
      System.out.println(getClass().getSimpleName());
    }
  }
  
  @Command(name = "add", description = "Add file contents to the index")
  public static class Add extends GitCommand
  {
    @Arguments(description = "Patterns of files to be added")
    public List<String> patterns;
    
    @Option(name = "-i", description = "Add modified contents interactively.")
    public boolean interactive;
  }
  
  @Command(name = "show", description = "Gives some information about the remote <name>")
  public static class RemoteShow extends GitCommand
  {
    @Arguments(description = "Do not query remote heads")
    public boolean noQuery;
    
    @Arguments(description = "Remote to show")
    public String remote;
  }
  
  @Command(name = "add", description = "Adds a remote")
  public static class RemoteAdd extends GitCommand
  {
    @Option(name = "-t", description = "Track only a specific branch")
    public String branch;
    
    @Arguments(description = "Remote repository to add")
    public List<String> remote;
  }
}

@Command(name = "ping", description = "network test utility")
public class Ping
{
  @Inject
  public HelpOption helpOption;
  
  @Option(name = {"-c", "--count"}, description = "Send count packets")
  public int count = 1;
  
  public static void main(String... args)
  {
    Ping ping = SingleCommand.singleCommand(Ping.class).parse(args);
    
    if (ping.helpOption.showHelpIfRequested()) {
      return;
    }
    
    ping.run();
  }
  
  public void run()
  {
    System.out.println("Ping count: " + count);
  }
}


```

```sh
ping
ping -c 5
ping --help
ping -h
```

```
```


