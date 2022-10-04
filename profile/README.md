<img alt="FFXIV Venues" src="https://ffxivvenues.com/full-logo.png" height=80 />

We're a team building venue discoverability and community engagement through open-source technology. We use modern technologies and principles to engineer the application suite atop our foundational stack: Azure, C# .NET, and ReactJs. 

Our flagship application is the Venue Index site (https://ffxivvenues.com/), supported by our cute discord bot Veni Ki, and our Dalamud Plugin; all backed by our Restful Web API. 

Join our community discord is at https://discord.gg/a4BMgkZJ4d 🥳.

## Architecture 
```mermaid
    C4Context
      title FFXIV Venues Index C2 Diagram
      
      Person(rper, "Venue Prospective Guest", "A visitor of venues.") 
      Person(manager, "Venue Owner/Manager", "A owner or manager of a FFXIV RP Venue.")
      
      Container_Boundary(clients, "Clients") {
        Container(site, "FFXIV Venues Site", "HTML5/CSS/JS/ReactJs <br>[Azure AppService]", "The main application of the suite; <br/>shows all venues, their details and the  <br/>week's venue schedule")
        Container(plugin, "FFXIV Venues Dalamud Plugin", "C#.NET <br> [Dalamud]", "FFXIV Dalamud plugin to show all <br/> venues, their details, and the week's <br/> venue schedule.")
        Container(veni, "Veni Ki (Bot)", "C#.NET <br> [Containerized in Azure VM]", "Discord Bot with a degree of language <br/> understanding for conversational operations;  <br/>shows venue details and allows venue  <br/>managers to manage their venue on the index.")
      }
      
      Container_Boundary(api, "API") {
        Container(api, "Restful Web API", "C# ASP.NET<br>[Azure AppService]", "The main backbone application of the <br/>platform; allows querying, create, editing and <br/>deleting of venues via restful HTTP web requests.")
      }
      
      Container_Boundary(storage, "Storage") {
        ContainerDb(storage, "Media Storage", "Azure Blob Storage", "Stores venue banners.")
        ContainerDb(database, "Database", "Azure Cosmos SQL", "Stores venue details and <br/>Veni guild configurations.")
      }
      
      Rel(site, api, "Reads venue details via")
      Rel(plugin, api, "Reads venue details via")
      Rel(veni, api, "Read/writes venue details via")
      
      Rel(api, database, "Reads/writes venue details to")
      Rel(api, storage, "Reads/writes venue banner images to")
      Rel(veni, database, "Read/write discord guild configuration to")
      
      Rel(manager, veni, "Manages venue")
      Rel(rper, site, "Looks for venues to visit")
      Rel(rper, plugin, "Looks for venues to visit")
      
      UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="1")
```
