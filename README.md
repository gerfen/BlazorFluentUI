# BlazorFluentUI
Simple port of Fluent UI (formerly Office Fabric) React components and style to Blazor

## Client-side Demo (web assembly)
https://blazorfluentui.github.io/BlazorFluentUI/

Next version preview:
https://delightful-wave-040459e1e.azurestaticapps.net/

## Server-side Demo (SignalR)
https://blazorfluentui.azurewebsites.net/

## Telegram dev channel
https://t.me/blazorfabric

## See the wiki for all usage notes
https://github.com/BlazorFluentUI/BlazorFluentUI/wiki

## Status of Controls

### Basic Inputs
| Control     | State | Information      |
| :---------- | :---: | :--------------- |
| Button      | Done  |                  |
| Checkbox    | Done  | except for icons |
| ChoiceGroup | ToDo  |                  |
| ComboBox    | ToDo  |                  |
| Dropdown    | Done  |                  |
| Label       | Done  |                  |
| Link        | Done  |                  |
| Rating      | Done  |                  |
| SearchBox   | ToDo  |                  |
| Slider      | ToDo  |                  |
| SpinButton  | ToDo  |                  |
| TextField   | Done  | except masking   |
| Toggle      | Done  |                  |

### Galleries & Pickers
| Control           | State | Information |
| :---------------- | :---: | :---------- |
| Calendar          | Done  |             |
| ColorPicker       | ToDo  |             |
| DatePicker        | Done  |             |
| PeoplePicker      | ToDo  |             |
| Pickers           | ToDo  |             |
| SwatchColorPicker | ToDo  |             |

### Items & Lists
| Control      | State | Information                         |
| :----------- | :---: | :---------------------------------- |
| ActivityItem | ToDo  |                                     |
| DetailsList  | Done  |                                     |
| DocumentCard | ToDo  |                                     |
| Facepile     | ToDo  |                                     |
| GroupedList  | Done  |                                     |
| HoverCard    | ToDo  |                                     |
| List         | Done  | supports `INotifyCollectionChanged` |
| Persona      | Done  |                                     |

### Commands, Menus & Navs
| Control        | State | Information |
| :------------- | :---: | :---------- |
| Breadcrumb     | ToDo  |             |
| CommandBar     | Done  |             |
| ContextualMenu | Done  |             |
| Nav            | Done  |             |
| OverflowSet    | Done  |             |
| Pivot          | Done  |             |

### Notification & Engagement
| Control        | State | Information |
| :------------- | :---: | :---------- |
| Coachmark      | ToDo  |             |
| MessageBar     | Done  |             |
| TeachingBubble | ToDo  |             |

### Progress
| Control           | State | Information |
| :---------------- | :---: | :---------- |
| ProgressIndicator | Done  |             |
| Shimmer           | ToDo  |             |
| Spinner           | Done  |             |

### Surfaces
| Control        |    State    | Information                                                                                         |
| :------------- | :---------: | :-------------------------------------------------------------------------------------------------- |
| Callout        |    Done     |                                                                                                     |
| Dialog         |    Done     | can't drag                                                                                          |
| Modal          |    Done     | no modeless version                                                                                 |
| Panel          |    Done     |                                                                                                     |
| ScrollablePane |    ToDo     |                                                                                                     |
| Tooltip        | In Progress | limited functionality.  will show, but can't interact with it yet, doesn't respond to overflow yet. |

### Utilities
| Control          |    State    | Information                           |
| :--------------- | :---------: | :------------------------------------ |
| Announced        |    ToDo     |                                       |
| FocusTrapZone    |    Done     |                                       |
| FocusZone        |    Done     |                                       |
| Icon             |    Done     | only MS icons                         |
| Image            |    Done     |                                       |
| Keytips          |    ToDo     |                                       |
| Layer            | In Progress | only layers at root window right now. |
| MarqueeSelection |    ToDo     |                                       |
| Overlay          |    ToDo     |                                       |
| ResizeGroup      |    Done     |                                       |
| Selection        |    ToDo     |                                       |
| Separator        |    ToDo     |                                       |
| Stack            |    Done     |                                       |
| Text             |    Done     |                                       |
| Themes           |    ToDo     |                                       |

### Non-Fabric-Component
| Control          |    State    | Information                           |
| :--------------- | :---------: | :------------------------------------ |
| ResponsiveLayout |    Done     |                                       |
| RichTextEditor   | In Progress | Works with limited styles available   |
| GlobalCS		   | In Progress |                                       |
| LocalCS		   | In Progress |                                       |

## Info
There are no MergeStyles in this port.  It's just each control packaged into its own project so you can limit what gets added to your Blazor project. 

## To use
1. Install NuGet package for the control you want.  _BlazorFluentUI.*_  (be sure to select preview packages)
2. The Blazor team has been inconsistent with how static files from component libraries are added to projects in the past.  Going forward, you'll need to **add all javascript assets from the component packages manually**.  You can just copy/paste the section from the test app's index.html.
You can also use my helper VSIX extension (may have major bugs!  Be sure to compile once for assets to show up.): https://marketplace.visualstudio.com/items?itemName=LeeMcPherson.BlazorLibraryAssetHelper&ssr=false#overview  
3. Optionally, add Microsoft's assets package to your index.html or \_Hosts.cshtml file.

`<link rel="stylesheet" href="https://static2.sharepointonline.com/files/fabric/office-ui-fabric-core/11.0.0/css/fabric.min.css" />`

**OR**

Use the tool here to generate your own MS font package: https://uifabricicons.azurewebsites.net/

(Remember that the assets package has a more restrictive license.  You are required to use it with/for some type of Microsoft product.  However, one of their engineers said that using it hosted on Azure would be enough... but I'm not a lawyer, so use caution.)

4. Add "AddBlazorFabric" to ServiceProvider

ServerSide: Startup.cs
```
public void ConfigureServices(IServiceCollection services)
{
	...;
	services.AddBlazorFluentUI();
	...;
}
```

ClientSide up to version 'Blazor WebAssembly 3.1.0' : Startup.cs
```
public void ConfigureServices(IServiceCollection services)
{
	...;
	services.AddBlazorFluentUI();
	...;
}
```

ClientSide from version 'Blazor WebAssembly 3.2.0 Preview 1'  : Program.cs
```
public static async Task Main(string[] args)
{
	...;
	builder.Services.AddBlazorFluentUI();
	...;
}
```

5. Add css-class tag in

ServerSide: Pages/_Host.cshtml
```
<head>
	...;
	<component type="typeof(GlobalRules)" render-mode="ServerPrerendered" />
	...;
</head>
```
ClientSide: wwwroot/index.html
```
<head>
	...;
	<style id="staticcs"></style>
	...;
</head>
```
You may need to add an `@using BlazorFluentUI` to the top of your `_Hosts.cshmtl` to avoid a 'GlobalRules could not be found` error.

6. Add following to get controll over css-classes tag you created before

ServerSide: isn't needed

ClientSide up to version 'Blazor WebAssembly 3.1.0' : Startup.cs
```
 public void Configure(IComponentsApplicationBuilder app)
{
	...;
	app.AddComponent<GlobalRules>("#statics");
	...;
}
```

ClientSide from version 'Blazor WebAssembly 3.2.0 Preview 1'  : Program.cs
```
public static async Task Main(string[] args)
{
	...;
	builder.RootComponents.Add<BFUGlobalRules>("#statics");
	...;
}
```

7. For Theme's add following in `App.razor` as most outside Component. You can have a look in Demo application's `App.razor`

```
<FabricTheme>
	<...>
		<Router AppAssembly="typeof(Startup).Assembly" />
	</...>
</FabricTheme>
```

8. If you're using any component that requires a `Layer` as part of its inner-workings (i.e. `Modal`, `Callout`, etc... anything that pops up over already drawn stuff), you need to wrap the `Router` with a `LayerHost`.
```
<LayerHost Style="display:flex; flex-direction: row;width:100vw">
    <Router AppAssembly="typeof(Startup).Assembly" />
</LayerHost>
```


