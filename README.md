# Using controller and blazor razor forms from class libraries

## Start
Just create solution with `FormAndControllerFromClassLibrary` name and delete project that is created inside it so you will have only clear solution

## Adding class library for controllers
1. Add ***razor*** class library, give it name - "ControllersLibrary", here we will store controllers
2. ***Check*** the flag "Support pages and view"
![image](https://github.com/user-attachments/assets/11c25f09-91f0-4681-ba7c-91b0084f195c)

## Adding class library for blazor pages(forms)/components
1. Add ***razor*** class library, give it name - "FormsLibrary", here we will store pages(forms)/components
2. ***Uncheck*** the flag "Support pages and view"
![image](https://github.com/user-attachments/assets/e51f4de3-8141-4302-a94a-bd2caaefe975)

## Adding executable project for testing
I have added project `FormAndControllerFromClassLibrary.WebAPI` in order to test `ControllersLibrary` and `FormAndControllerFromClassLibrary.Blazor` in order to test `FormsLibrary`

## Moving form and controller to class libraries
- When you created `FormAndControllerFromClassLibrary.WebAPI` you can move folder `Controllers` where `WeatherForecastController` is and don't forget to move `WeatherForecast` model too.
- After you created `FormAndControllerFromClassLibrary.Blazor` you can create folder `Pages` in `FormsLibrary` and move there page `Counter` from the `FormAndControllerFromClassLibrary.Blazor`(don't forget to delete page `Counter` from the `FormAndControllerFromClassLibrary.Blazor` at the end)

## How to use class libraries?

- In case of controllers you just add reference of the `ControllersLibrary` to the `FormAndControllerFromClassLibrary.WebAPI` so that's all. ASP will find this controller by itself
- In case of forms you add reference of the `FormsLibrary` to the `FormAndControllerFromClassLibrary.Blazor` and edit your `App.razor` like this:
> You can see that `Router` now has new attribute `AdditionalAssemblies`
```
<Router AppAssembly="@typeof(App).Assembly" AdditionalAssemblies="new[]{typeof(FormsLibrary.Pages.Counter).Assembly}">
    <Found Context="routeData">
        <RouteView RouteData="@routeData" DefaultLayout="@typeof(MainLayout)" />
        <FocusOnNavigate RouteData="@routeData" Selector="h1" />
    </Found>
    <NotFound>
        <PageTitle>Not found</PageTitle>
        <LayoutView Layout="@typeof(MainLayout)">
            <p role="alert">Sorry, there's nothing at this address.</p>
        </LayoutView>
    </NotFound>
</Router>
```

## How to test?
Just run `FormAndControllerFromClassLibrary.Blazor` and `FormAndControllerFromClassLibrary.WebAPI` and you will see that you will be able to navigate to `Counter` page and see `WeatherForecastController` in `Swagger` respectively. Even though nor `Counter` page or `WeatherForecastController` not in `FormAndControllerFromClassLibrary.Blazor` and `FormAndControllerFromClassLibrary.WebAPI` respectively
