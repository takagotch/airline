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
  
}
```

```
```

```
```


