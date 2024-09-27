# How to install MudBlazor Components in your Blazor Web Application

**Note**: For more information about this sample visit these URLs:

https://mudblazor.com/

https://mudblazor.com/getting-started/installation

## 1. Create a new Blazor Web App with Visual Studio 2022 Community Edition 

Run Visual Studio and create a new project

![image](https://github.com/user-attachments/assets/33b9ab5a-c835-47b6-b6b6-771b0f2e3084)

Select the **Blazor Web App** project template and press the Next button

![image](https://github.com/user-attachments/assets/9234548f-21c7-4e42-a7cb-3890be316348)

Input the project name, project location and press the next button 

![image](https://github.com/user-attachments/assets/0d6b8008-44a7-4939-a591-9ac4d9cefb6e)

Leave all the default values and press the create button

![image](https://github.com/user-attachments/assets/0b711e49-fff9-444b-ae1b-942335f0eeed)

## 2. Load the Nuget package

Add in Visual Studio with the Nuget tool the package **MudBlazor**

![image](https://github.com/user-attachments/assets/294ff746-953f-4cd3-b313-213ecbd35564)

**Important Note**: In order to install the latest MudBlazor library version it is required these dependencies

![image](https://github.com/user-attachments/assets/329b2d26-fc43-4c94-80cc-af5ebdf540b5)

## 3. Modify the _Imports.razor

Add this new line:

```
@using MudBlazor
```

# 4. Add the following references in the App.razor component

Add these **styles** files in the head section:

```
<link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap" rel="stylesheet" />
<link href="_content/MudBlazor/MudBlazor.min.css" rel="stylesheet" />
```

Add the script reference in the body section:

```
<script src="_content/MudBlazor/MudBlazor.min.js"></script>
```

This is the modified App.razor file:

```razor
﻿<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <base href="/" />
    <link rel="stylesheet" href="bootstrap/bootstrap.min.css" />
    <link rel="stylesheet" href="app.css" />
    <link rel="stylesheet" href="BlazorApp1.styles.css" />
    <link rel="icon" type="image/png" href="favicon.png" />
    <link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap" rel="stylesheet" />
    <link href="_content/MudBlazor/MudBlazor.min.css" rel="stylesheet" />
    <HeadOutlet @rendermode="InteractiveServer" />
</head>

<body>
    <Routes @rendermode="InteractiveServer" />
    <script src="_framework/blazor.web.js"></script>
    <script src="_content/MudBlazor/MudBlazor.min.js"></script>
</body>

</html>
```

# 5. Modify the middleware (Program.cs)

Add these two lines:

```
using MudBlazor.Services;
...
builder.Services.AddMudServices();
```

This is the middleware (Program.cs) including the MudBlazor components

```csharp
using BlazorApp1.Components;
using MudBlazor.Services;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddRazorComponents()
    .AddInteractiveServerComponents();

builder.Services.AddServerSideBlazor()
    .AddCircuitOptions(options => { options.DetailedErrors = true; });

builder.Services.AddMudServices();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Error", createScopeForErrors: true);
    // The default HSTS value is 30 days. You may want to change this for production scenarios, see https://aka.ms/aspnetcore-hsts.
    app.UseHsts();
}

app.UseHttpsRedirection();

app.UseStaticFiles();
app.UseAntiforgery();

app.MapRazorComponents<App>()
    .AddInteractiveServerRenderMode();

app.Run();
```

## 6. Modify the MainLayout.razor

Add these new components in the MainLayout.razor. They are always required:

```
<MudThemeProvider />
<MudPopoverProvider />
```

The following components are not mandatory are optiona:

```
@*Needed for dialogs*@
<MudDialogProvider />
```

and

```
@*Needed for snackbars*@
<MudSnackbarProvider />
```

This is the App.razor file including the MudBlazor components:

```razor
﻿@inherits LayoutComponentBase

<MudThemeProvider />
<MudPopoverProvider />

<div class="page">
    <div class="sidebar">
        <NavMenu />
    </div>

    <main>
        <div class="top-row px-4">
            <a href="https://learn.microsoft.com/aspnet/core/" target="_blank">About</a>
        </div>

        <article class="content px-4">
            @Body
        </article>
    </main>
</div>

<div id="blazor-error-ui">
    An unhandled error has occurred.
    <a href="" class="reload">Reload</a>
    <a class="dismiss">🗙</a>
</div>
```

## 7. Add a new razor component (Alert) for testing the MudBlazor components

Note for more info about the MudBlazor Alert component visit this URL: https://mudblazor.com/components/alert

We right click on the Pages folder and then we select the menu option Add New Razor Component and we set the new component name: MudBlazorComponent.razor

![image](https://github.com/user-attachments/assets/9cb5d6c9-d16d-4507-9010-54679d072f6e)

This is the new component code:

```razor
@page "/mudblazorcomponents"

<PageTitle>MudBlazorComponents</PageTitle>

<h1>MudBlazor Components</h1>

<MudGrid>
    <MudItem xs="12">
        <MudAlert Severity="Severity.Normal">The reactor type is RBMK-1000</MudAlert>
    </MudItem>
    <MudItem xs="12">
        <MudAlert Severity="Severity.Info">The reactor was fired up successfully</MudAlert>
    </MudItem>
    <MudItem xs="12">
        <MudAlert Severity="Severity.Success">The reactor is running at optimum temperature</MudAlert>
    </MudItem>
    <MudItem xs="12">
        <MudAlert Severity="Severity.Warning">The reactor temperature exceeds the optimal range</MudAlert>
    </MudItem>
    <MudItem xs="12">
        <MudAlert Severity="Severity.Error">Meltdown is imminent</MudAlert>
    </MudItem>
</MudGrid>
```

## 8 . Add a new menu item in the NavMenu.razor component for navigating to the 

This is the new NavLink code:

```
<div class="nav-item px-3">
     <NavLink class="nav-link" href="mudblazorcomponents">
         <span class="bi bi-list-nested-nav-menu" aria-hidden="true"></span> MudBlazorComponents
     </NavLink>
 </div>
```

See also in the following picture the NavMenu.razor component whole code:

![image](https://github.com/user-attachments/assets/24ea633b-e0a4-4d65-891c-e77da772cb5c)


## 9. Run the Application and see the results

![image](https://github.com/user-attachments/assets/9536df06-95d0-4d03-b3dd-a463cbb3bd1f)



