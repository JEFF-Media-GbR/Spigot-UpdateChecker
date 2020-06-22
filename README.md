# Spigot-UpdateChecker
Integrate automatic update checks into your own plugin!

## Import via maven
First you need to add the UpdateChecker as a dependency to your pom.xml:

```
<repositories>
    <repository>
	    <id>jeff-media-gbr</id>
	    <url>https://repo.jeff-media.de/maven2</url>
    </repository>
</repositories>		

<dependencies>
    <dependency>
        <groupId>de.jeff_media</groupId>
	    <artifactId>PluginUpdateChecker</artifactId>
	    <version>1.0</version>
    </dependency>
</dependencies>
```

## Usage
Now you can create an instance of the PluginUpdateChecker class, e.g. in your onEnable method:

```
import de.jeff_media.PluginUpdateChecker.PluginUpdateChecker;

...

public class MyPlugin extends JavaPlugin implements Listener {

    PluginUpdateChecker updateChecker;

    public void onEnable() {

        // Link to a text file containing the latest version.
        // You can use the Spigot API, just replace the resource id.
        String version = "https://api.spigotmc.org/legacy/update.php?resource=59773";
        String downloadLink = "https://www.chestsort.de"
        String changelogLink = "https://www.chestsort.de/changelog"
        String donateLink = "https://chestsort.de/donate"

        updateChecker = new PluginUpdateChecker(this,version,downloadLink,changelogLink,donateLink,);

        // Check every hour for updates:
        updateChecker.check(3600);

        // ... or check only once:
        updateChecker.check();

        ...
    }

    @EventHandler
    public void onPlayerJoin(PlayerJoinEvent e) {
    
        // Send a message to OPs joining the server, if a new version has been found
        updateChecker.sendUpdateMessage(e.getPlayer());

        ...

    }
}
```