<img alt="FFXIV Venues" src="https://ffxivvenues.com/full-logo.png" height=80 />

We're a team building venue discoverability and community engagement through open-source technology. We use modern technologies and principles to engineer the application suite atop our foundational stack: Azure, C# .NET, and ReactJs. 

Our flagship application is the Venue Index site (https://ffxivvenues.com/), supported by our cute discord bot Veni Ki, and our Dalamud Plugin; all backed by our Restful Web API. 

Join our community discord is at https://discord.gg/a4BMgkZJ4d 🥳.

## Architecture 
```mermaid
    C4Context
      title FFXIV Venues C2 Diagram
      
      Person(manager, "Venue Owner/Manager", "A owner or manager of a FFXIV RP Venue.")
      Person(rper, "Venue Prospective Guest", "A visitor of venues.") 
      
      Enterprise_Boundary(clients, "Clients") {
        Container(site, "FFXIV Venues Index Site", "HTML5/CSS/JS/ReactJs <br>[Azure AppService]")
        Container(plugin, "FFXIV Venues Dalamud Plugin", "C#.NET <br> [Dalamud]")
        Container(veni, "FFXIV Venues Discord Bot (Veni Ki)", "C#.NET <br> [Containerized in Azure VM]")
      }
      
      Enterprise_Boundary(api, "API") {
        Container(api, "ASP.NET Web API", "C#.NET<br>[Azure AppService]")
        ContainerDb(database, "Database", "Azure Cosmos SQL", "Stores venue details.")
        ContainerDb(storage, "Media Storage", "Azure Blob Storage", "Stores venue banners.")
      }
      
      
      Rel(site, api, "")
      Rel(plugin, api, "")
      Rel(veni, api, "")
      
      Rel(api, database, "")
      Rel(api, storage, "")
      
      Rel(manager, veni, "Manages venue")
      Rel(rper, site, "Looks for venues to visit")
      Rel(rper, plugin, "Looks for venues to visit")
```
