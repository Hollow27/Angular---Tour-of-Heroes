# AngularTourOfHeroes

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 1.6.5.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `-prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).


# Angular Tutorial Walkthrough

After entering the commands on the command prompt and launching the http://localhost:4200/, we see a page which is called the application shell. The shell is controlled by an Angular component called "AppComponent". Components are the fundamental building blocks of Angular applications. They display data on the screen, listen for user input, and take action based on that input.

The implementation of the shell "AppComponent" is distributed over three files:

<b>- app.component.ts</b> (component class code, written in Typescript)

<b>- app.component.html</b> (component template written in HTML)

<b>- app.component.css</b> (components private CSS styles)


# Heroes Component of the App

Viewing the HeroesComponent (heroes.component.ts file), it seems that we can import the "Component" symbol from the Angular core library and annotate the component class with @component.

@Component is a decorator function that specifies the Angular metadata for the component.

The CLI generated three metadata properties:

<b>1.) selector - the components CSS element selector.</b>

<b>2.) templateUrl - the location of the components template file.</b>

<b>3.) styleUrls - the location of the components private CSS styles.</b>

The CSS element selector, 'app-heroes', matches the name of the HTML element that identifies this component within a parent component's template.

The ngOnInit is a <b>lifecycle hook</b>. Angular calls <b>ngOnInit</b> shortly after creating a component. Its a good place to put initialization logic.

We should always <b>export</b> the component class so we can <b>import</b> it elsewhere...like in the <b>AppModule</b>.

# Two-Way Data Binding

Users should be able to edit the hero name in an <input> textbox.

The textbox should both display the hero's <b>name</b> property and update that property as the user types. That means data flow from the component class out to the screen and from the screen back to the class.

To automate that data flow, setup a two-way data binding between the <input> form element and the <b>hero.name</b> property.

We do this by using [{ngModel}] which is Angular's two-way binding syntax. However, it seems that when we added that to the <b>heroes.component.html</b> file, the browser stopped working. The error displayed the following:

"Template parse errors:
Can't bind to 'ngModel' since it isn't a known property of 'input'."

Although ngModel is a valid Angular directive, it isnt available by default. It belongs to the optional <b>FormsModule</b> and we must opt-in to using it.

# AppModule

Angular needs to know how the pieces of this application fit together and what other files and libraries the app requires. This information is called metadata.

Some of the metadata is in the @Component decorators we added to our component classes that we mentioned earlier. Other critical metadata is in @ngModule decorators. The most important @ngModule decorator annotates the top-level AppModule class. The Angular CLI generated an AppModule class in <b>src/app/app.module.ts</b>. This is where we opt-in to the <b>FormsModule</b>.

# Summary So Far

- You used the CLI to create a second HeroesComponent.
- You displayed the HeroesComponent by adding it to the AppComponent shell.
- You applied the UppercasePipe to format the name.
- You used two-way data binding with the ngModel directive.
- You learned about the AppModule.
- You imported the FormsModule in the AppModule so that Angular would recognize and apply the ngModel directive.
- You learned the importance of declaring components in the AppModule and appreciated that the CLI declared it for you.

# Displaying the Heroes List

In this section, we expanded on the Tour of Heroes app to display a list of heroes, and allow users to select a hero and display the hero's details. First, we need some heroes to display. Eventually, we'll get them from a remote data server but for now we'll create some mock heroes and pretend they came from the server.

We created a file called <b>mock-heroes.ts</b> in the <b>src/app</b> folder and then define a <b>HEROES</b> constant as an array of ten heroes and export it.

To display the list of heroes at the top of the <b>HeroesComponent</b>, we need to import the HEROES const into the <b>heroes.component.ts</b> and then add a heroes property to the class that exposes these heroes for binding.

Now we open the <b>HeroesComponent</b> template file and add a title called "My Heroes" and create an unordered list and insert an 
"li" within the "ul" that displays the properties of a hero.

We then implement Angular's repeater directive, <b>ngFor</b> into the <li> element. It essentially repeats the host element for each element in a list.

# Styling the Heroes

Of course we also want to make the heroes list attractive and it should respond visually when users hover over and select a hero from the list. Earlier in this project, we set the basic styles for the entire application (app.component.css), however that stylesheet didn't include styles for the list of heroes.

What we can do is define private styles for a specific component and keep everything a component needs -- the code, the HTML, and the CSS --together in one place.

This approach makes it easier to re-use the component somewhere else and deliver the component's intended appearance even if the global styles are different. We define private styles either inline in the <b>@Component.styles</b> array or as stylesheet file(s) identified in the <b>@Component.styleUrls</b> array. When the CLI generated the HeroesComponent, it created an empty <b>heroes.component.css</b> stylesheet for the <b>HeroesComponent</b> and pointed to it in <b>@Component.stylesUrls</b> like this.

# Adding a Click Event Binding

When the user clicks a hero in the master list, the component should display the selected hero's details at the bottom of the page. In this section, we'll listen for the hero item click event and update the hero detail.

The following is a click event binding we implemented to the <li> element:

<b>ngFor="let hero of heroes" (click)="onSelect(hero)"</b>

This is an example of Angular's event binding syntax.

The parentheses around "click" tell angular to listen for the <li> element's click event. When the user clicks in the <li>, Angular executes the onSelect(hero) expression.

onSelect() is a HeroesComponent method that you're about to write. Angular calls it with the hero object displayed in the clicked <li>, the same hero defined previously in the *ngFor expression*

# Summary

- The Tour of Heroes app displays a list of heroes in a Master/Detail view.

- The user can select a hero and see that hero's details.

- Used *ngFor* to display a list.

- Used *ngIf* to conditionally include or exclude a block of HTML.

- We can toggle a CSS style class with a class binding.


# Master / Detail Components

At the moment, the HeroesComponent displays both the list of heroes and the selected hero's details.

Keeping all features in one component as the application grows will not be maintainable. You'll want to split up large components into smaller sub-components, each focused on a specific task or workflow.

In this section, we'll take the first step in that direction by moving the hero details into a separate, reusable HeroDetailsComponent.

The HeroesComponent will only present the list of heroes. The HeroDetailsComponent will present details of a selected hero.

# Make the HeroDetailComponent

We'll use the Angular CLI to generate a new component named <b>hero-detail</b>.

      <b>ng generate component hero-detail</b>

The command scaffolds the HeroDetailComponent files and declares the component in AppModule.


........


# Show the HeroDetailComponent

The HeroesComponent is still a master/detail view.

It used to display the hero details on its own, before you cut that portion of the template. Now it will delegate to the HeroDetailComponent.

The two components will have a parent/child relationship. The parent HeroesComponent will control the child HeroDetailComponent by sending it a new hero to display whenever the user selects a hero from the list.

You won't change the HeroesComponent class but you will change its template.

# Updating the HeroesComponent template

The HeroDetailComponent selector is 'app-hero-detail'. We'll add an <app-hero-detail> element near the bottom of the HeroesComponent template, where the hero detail view used to be.

Then we'll bind the HeroesComponent.selectedHero to the element's hero property like this.

  <b><app-hero-detail [hero]="selectedHero"></app-hero-detail></b>

[hero]="selectedHero" is an Angular property binding. It's a one way data binding from the <b>selectedHero</b> property of the HeroComponent to the <b>hero</b> property of the target element, which maps to the <b>hero</b> property of the <b>HeroDetailComponent</b>.

Now when the user clicks a hero in the list, the <b>selectedHero</b> changes. When the <b>selectedHero</b> changes, the property binding updates hero and the <b>HeroDetailComponent</b> displays the new hero.

# What's Changed?

As before, whenever a user clicks on a hero name, the hero detail appears below the hero list. Now the HeroDetailComponent is presenting those details instead of the HeroesComponent.

Refactoring the original HeroesComponent into two components yields benefits, both now and in the future:

  - We simplified the HeroesComponent by reducing its responsibilities.

  - We can evolve the HeroDetailComponent into a rich hero editor without touching the parent HeroesComponent.

  - We can evolve the HeroesComponent without touching the hero detail view.

  - We can re-use the HeroDetailComponent in the template of some future component.

# Summary

- We created a separate, reusable HeroDetailComponent.

- We used a property binding to give the parent HeroesComponent control over the child HeroDetailComponent.

- We used the @Input decorator to make the hero property available for binding by the external HeroesComponent.


# Services

The Tour of Heroes HeroesComponent is currently getting and displaying fake data.

After the refactoring, HeroesComponent will be lean and focused on supporting the view. It will also be easier to unit-test with a mock service.

# Why Services

Components shouldn't fetch or save data directly and they certainly shouldn't knowingly present fake data. They should focus on presenting data and delegate data access to a service.

In this section, we'll create a <b>HeroService</b> that all application classes can use to get heroes. Instead of creating that service with <b>new</b>, we'll rely on Angular dependency injection to inject it into the HeroesComponent constructor.

Services are a great way to share information among classes that don't know each other. You'll create a MessageService and inject it in two places:

<li>1.) In HeroService which uses the service to send a message.</li>
<li>2.) In MessagesComponent which displays that message.</li>

# @Injectable() Services

The @Injectable() decorator tells Angular that this service might itself have injected dependencies. It doesn't have dependencies now but it will soon. Whether it does or it doesn't, its good practice to keep the decorator.

# Get Hero Data

The HeroService could get hero data from anywhere - a web service, local storage, or a mock data source.

Removing data access from components means you can change your mind about the implementation anytime, without touching any components. They don't know how the service works.

However, for this project, we'll continue to deliver mock heroes.


# Providing the HeroService

We must provide the HeroService in he dependency injection system before Angular can inject it into the HeroesComponent. There are several ways to provide the HeroService: in the HeroComponent, in the AppComponent, in the AppModule. Each option has its pros and cons.

For this project, we'll choose to provide it in the AppModule.

We'll open the AppModule class, import the HeroService and add it to the @NgModule.providers array.

The providers array tells Angular to create a single, shared instance of HeroService and inject into any class that asks for it. Now the HeroService is ready to plug into the HeroesComponent.

# Update HeroesComponent

We'll go back to the HeroesComponent class file and deleted the HEROES import and import the HeroService instead. Moreover, we'll replace the definition of the heroes property with a simple declaration.

# Inject the HeroService

Now we'll add a private heroService parameter of type HeroService to the constructor. The parameter simultaneously defines a private heroService property and identifies it as a HeroService injection site.

When Angular creates a HeroesComponent, the Dependency Injection system sets the heroService parameter to the singleton instance of HeroService.

# Add getHeroes()

Created a function to retrieve the heroes from the service in HeroesComponent class file.

# Call it in ngOnInit

While we could call getHeroes() in the constructor, thats not the best practice. Reserve the constructor for simple initialization such as wiring constructor parameters to properties. The constructor shouldnt do anything. It certainly shouldnt call a function that makes HTTP requests to a remote server as a real data service would.

Instead, call getHeroes() inside the ngOnInit lifecycle hook and let Angular call ngOnInit at an appropriate time after construction a HeroesComponent instance.

# Observable data

The HeroService.getHeroes() method has a synchronous signature, which implies that the HeroService can fetch heroes synchronously. The HeroesComponent consumes the getHeroes() result as if heroes could be fetched synchronously.

The HeroService must wait for the server to respond, getHeroes() cannot return immediately with hero data, and the browser will not block while the service waits.

HeroService.getHeroes() must have an asynchronous signature of some kind.

It can take a callback. It could return a Promise. It could return an Observable.

In this tutorial, HeroService.getHeroes() will return an Observable in part because it will eventually use the Angular HttpClient.get method to fetch the heroes and HttpClient.get() returns an Observable.

# Observable HeroService

Observable is one of the key classes in the RxJS library.

Later on, we're going to learn that Angular's HttpClient methods return RxJS Observable's. In this project, we'll simulate getting data from the server with the RxJS of() function.

# Subscribe in HeroesComponent

The HeroService.getHeroes method used to return a Hero[]. Now it returns an Observable<Hero[]>.

You'll have to adjust to that difference in HeroesComponent in the getHeroes() method.

Observable.subscribe() is the critical difference.

The previous version assigns an array of heroes to the component's heroes property. The assignment occurs synchronously, as if the server could return heroes instantly or the browser could freeze the UI while it waited for the server's response.

That won't work when the HeroService is actually making requests of a remote server.

The new version waits for the Observable to emit the array of heroes— which could happen now or several minutes from now. Then subscribe passes the emitted array to the callback, which sets the component's heroes property.

This asynchronous approach will work when the HeroService requests heroes from the server.

# Showing Messages

In this section we will:

- add a MessagesComponent that displays app messages at the bottom of the screen.

- create an injectable, app-wide MessageService for sending messages to be displayed

- inject MessageService into the HeroService

- display a message when HeroService fetches heroes successfully.

# Create MessagesComponent

After creating a new component called "MessagesComponent" and its declared in the AppModule, we'll modify the AppComponent template to display the generated MessagesComponent.

# Creating the MessageService

Use the CLI to create the MessageService in src/app. The --module=app option tells the CLI to provide this service in the AppModule.

  "ng generate service message --module=app"

The service exposes its cache of messages and two methods: one to add() a message to the cache and another to clear() the cache.

# Inject it into the HeroService

Re-open the HeroService ands import the MessageService.

Modify the constructor with a parameter that declares a private messageService property. Angular will inject the singleton MessageService into that property when it creates the HeroService.

# Send a message from HeroService

Modify the getHeroes method to send a message when the heroes are fetched.

# Display the message from HeroService

The MessagesComponent should display all messages, including the message sent by the HeroService when it fetches heroes.

Open MessagesComponent and import the MessageService.

Modify the constructor with a parameter that declares a public messageService property. Angular will inject the singleton MessageService into that property when it creates the HeroService.

The messageService property must be public because you're about to bind to it in the template.

Note: Angular only binds to public component properties.


# Binding to the MessageService

We'll replace the CLI-generated MessagesComponent template with the following:

<div ngIf="messageService.messages.length">

  <h2>Messages</h2>
  <button class="clear"
          (click)="messageService.clear()">clear</button>
  <div ngFor='let message of messageService.messages'> {{message}} </div>

</div>

This template binds directly to the component's messageService.

- The ngIf only displays the messages area if there are messages to show.

- An ngFor presents the list of messages in repeated <div> elements.

- An Angular event binding binds the button's click event to MessageService.clear().

The messages will look better when you add the private CSS styles to messages.component.css as listed in one of the "final code review" tabs below.

The browser refreshes and the page displays the list of heroes. Scroll to the bottom to see the message from the HeroService in the message area. Click the "clear" button and the message area disappears.

# Summary

- We refactored data access to the HeroService class.

- We provided the HeroService in the root AppModule so that it can be injected anywhere.

- We used Angular Dependency Injection to inject it into a component.

- We gave the HeroService get data method an asynchronous signature.

- We discovered Observable and the RxJS Observable library.

- We used RxJS of() to return an Observable of mock heroes (Observable<Hero[]>).

- The component's ngOnInit lifecycle hook calls the HeroService method, not the constructor.

- We created a MessageService for loosely-coupled communication between classes.

- The HeroService injected into a component is created with another injected service, MessageService.

# Routing

New Requirements for the App we'll be working on:

- Adding a dashboard view.
- Adding the ability to navigate between the Heroes and Dashboard Views
- When users click a hero name in either view, navigate to a detail view of the selected hero.
- When users click a deep link in an email, open the detail view for a particular hero.

# Adding the AppRoutingModule

An Angular best practice is to load and configure the router in a separate, top-level module that is dedicated to routing and imported by the root, AppModule.

By convention, the module class name is AppRoutingModule and it belong in the app-routing.module.ts in the src/app folder.

We'll use the CLI to generate it:

  "ng generate module app-routing --flat --module=app"

Notes: "--flat" puts the file in src/app instead of its own folder
       "--module=app" tells the CLI to register it in the imports array of the AppModule.


You generally dont declare components in a routing module so you can delete the @NgModule.declarations array and delete CommonModule references too.

We'll configure the router with Routes in the RouterModule so import those two symbols from the @angular/router library. Then we'll add an @NgModule.exports array with RouterModule in it. Exporting RouterModule makes router directives available for use in the AppModule components that will need them

# Adding Routes

Routes tell the router which view to display when a user clicks a link or pastes a URL into the browser address bar. A typical Angular "Route" has two properties:

1.) "path": a string that matches the URL in the browser address bar.
2.) "component": the component that the router should create when navigating to this route.

We intend to navigate to the HeroesComponent when the URL is something like: localhost:4200/heroes.

We'll now import the HeroesComponent so we can reference it in a "Route", then define an array of routes with a single "route" to that component.

Once we've finished setting up, the router will match that URL to path: 'heroes' and display the HeroesComponent.

# RouterModule.forRoot()

We must first initialize the router and start it listening for browser location changes. Add RouterModule to the @NgModule.imports array and configure it with the routes in one step by calling RouterModule.forRoot() within the imports array, like this:

The method is called forRoot() because you configure the router at the application's root level. The forRoot() method supplies the service providers and directives needed for routing, and performs the initial navigation based on the current browser URL.

# Add RouterOutlet

Open the AppComponent template replace the <app-heroes> element with a <router-outlet> element.

You removed <app-heroes> because you will only display the HeroesComponent when the user navigates to it.

The <router-outlet> tells the router where to display routed views.

Note: The RouterOutlet is one of the router directives that became available to the AppComponent because AppModule imports AppRoutingModule which exported RouterModule.

# Add a Navigation Link (routerLink)

Users shouldn't have to paste a route URL into the address bar. They should be able to click a link to navigate.

We'll add a <nav> element and, within that, an anchor element that, when clicked, triggers navigation to the HeroesComponent.

A routerLink attribute is set to "/heroes", the string that the router matches to the route to HeroesComponent. The routerLink is the selector for the RouterLink directive that turns user clicks into router navigations. It's another of the public directives in the RouterModule.

The browser refreshes and displays the app title and heroes link, but not the heroes list.

Click the link. The address bar updates to /heroes and the list of heroes appears.

# Adding a Dashboard View

Routing makes more sense when there are multiples views. So far theres only the heroes view. That being said, we'll add a DashboardComponent using the CLI.

The CLI generates the files for the DashboardComponent and declares it in the AppModule.

The template presents a grid of hero name links.

- The ngFor repeater creates as many links as are in the component's heroes array.

- The links are styled as colored blocks by the dashboard.component.css.

- The links don't go anywhere yet but they will shortly.

The class is simlar to the HeroesComponent class.

- It defines a heroes array property.

- The constructor expects Angular to inject the HeroService into a private heroService property.

- The ngOnInit() lifecycle hook calls getHeroes.

This getHeroes reduces the number of heroes displayed to four (2nd, 3rd, 4th, and 5th).

# Add the Dashboard Route

To navigate to the dashboard, the router needs an appropriate route. We'll import the DashboardComponent in the AppRoutingModule.

After that, then add a route to the AppRoutingModule.routes array that matches a path to the DashboardComponent.

# Add a Default Route

When the app starts, the browsers address bar points to the website's root That doesn't match any existing route so the router doesn't navigate anywhere. The space below the <router-outlet> is blank.

To make the app navigate to the dashboard automatically, add the following route to the AppRoutingModule.Routes array.

The route redirects a URL that fully matches the empty path to the route whose path is './dashboard'.

After the browser refreshes, the router loads the DashboardComponent and the browser address bar shows the /dashboard URL.

# Add dashboard link to the shell

The user should be able to navigate back and forth between the DashboardComponent and the HeroesComponent by clicking links in the navigation area near the top of the page.

Add a dashboard navigation link to the AppComponent shell template, just above the Heroes link.

After the browser refreshes you can navigate freely between the two views by clicking the links.

# Navigating to Hero Details

The HeroDetailsComponent displays details of a selected hero. At the moment the HeroDetailComponent is only visible at the bottom of the HeroesComponent.

The user should be able to get to these details in three ways:

<li>By clicking a hero in the dashboard.</li>
<li>By clicking a hero in the heroes list.</li>
<li>By pasting a "deep link" URL into the browser address bar that identifies the hero to display.</li>

In this section, we'll enable navigation to the HeroDetailComponent and liberate it from the HeroesComponent.

# Delete the hero details from HeroesComponent

When the user clicks a hero item in the HeroesComponent, the app should navigate to the HeroDetailComponent, replacing the heroes list view with the hero detail view. The heroes list view should no longer show hero details as it does now.

Open the HeroesComponent template (heroes/heroes.component.html) and delete the <app-hero-detail> element from the bottom.

Clicking a hero item now does nothing. You'll fix that shortly after you enable routing to the HeroDetailComponent.

# Add a hero detail route

A URL like ~/detail/11 would be a good URL for navigating to the Hero Detail view of the hero whose id is 11.

Open AppRoutingModule and import HeroDetailComponent.

Then add a parameterized route to the AppRoutingModule.routes array that matches the path pattern to the hero detail view.

Note: The colon (:) in the path indicates that :id is a placeholder for a specific hero id.

At this point, all application routes are in place.

# DashboardComponent hero links

The DashboardComponent hero links do nothing at the moment. Now that the router has a route to HeroDetailComponent, fix the dashboard hero links to navigate via the parameterized dashboard route.

We're using Angular interpolation binding within the ngFor repeater to insert the current interation's hero.id into each routerLink.


# HeroesComponent hero links

The hero items in the HeroesComponent are <li> elements whose click events are bound to the component's onSelect() method.

Strip the <li> back to just its ngFor, wrap the badge and name in an anchor element (<a>), and add a routerLink attribute to the anchor that is the same as in the dashboard template.

You'll have to fix the private stylesheet (heroes.component.css) to make the list look as it did before. Revised styles are in the final code review at the bottom of this guide.

# Removing Dead Code

While the HeroesComponent class still works, the onSelect() method and selectedHero property are no longer used.

# Routable HeroDetailComponent

Previously, the parent HeroesComponent set the HeroDetailComponent.hero property and the HeroDetailComponent displayed the hero.

  HeroComponent doesn't do that anymore. Now the router creates the HeroDetailComponent in response to a URL such as ~/detail/11.

The HeroDetailComponent needs a new way to obtain the hero-to-display.

<li>Get the route that created it,</li>
<li>Extract the id from the route</li>
<li>Acquire the hero with that id from the sever via the HeroService</li>

We'll add the following imports to the Hero-Detail.component.ts file:

import { ActivatedRoute } from '@angular/router';
import { Location } from '@angular/common';
import { HeroService }  from '../hero.service';

Now we'll inject the ActivatedRoute, HeroService, and Location services into the constructor, saving their values in private fields.

The <b>ActivatedRoute</b> holds information about the route to this instance of the HeroDetailComponent. This component is interested in the route's bag of parameters extracted from the URL. The "id" parameter is the id of the hero to display.

The <b>HeroService</b> gets hero data from the remote server and this component will use it to get the hero-to-display.

The <b>Location</b> is an Angular service for interacting with the browser. We'll use it later to navigate back to the view that navigate here.

# Extract the id route parameter

In the ngOnInit() lifecycle hook call getHero() and define it as follows:

<b>
ngOnInit(): void {
this.getHero();
}

getHero(): void {
const id = +this.route.snapshot.paramMap.get('id');
this.heroService.getHero(id)
  .subscribe(hero => this.hero = hero);
}
</b>

The route.snapshot is a static image of the route information shortly after the component was created.

The paramMap is a dictionary of route parameter values extracted from the URL. The "id" key returns the id of the hero to fetch.

Route parameters are always strings. The JavaScript (+) operator converts the string to a number, which is what a hero id should be.

The browser refreshes and the app crashes with a compiler error. HeroService doesn't have a getHero() method. Add it now.

# Add HeroService.getHero()

Open HeroService and add this getHero() method.

<b>
getHero(id: number): Observable<Hero> {
  // Todo: send the message _after_ fetching the hero
  this.messageService.add(`HeroService: fetched hero id=${id}`);
  return of(HEROES.find(hero => hero.id === id));
}
</b>

Like getHeroes(), getHero() has an asynchronous signature. It returns a mock hero as an Observable, using the RxJS of() function.

You'll be able to re-implement getHero() as a real Http request without having to change the HeroDetailComponent that calls it.

# Find the Way Back

By clicking the browser's back button, you can go back to the hero list or dashboard view, depending upon which sent you to the detail view.

It would be nice to have a button on the HeroDetail view that can do that.

Add a go back button to the bottom of the component template and bind it to the component's goBack() method.

# Summary

<li>We added the Angular router to navigate among different components.</li>
<li>We turned the AppComponent into a navigation shell with <a> links and a <router-outlet>.</li>
<li>We configured the router in an AppRoutingModule</li>
<li>We defined simple routes, a redirect route, and a parameterized route.</li>
<li>We used the routerLink directive in anchor elements.</li>
<li>We refactored a tightly-coupled master/detail view into a routed detail view.</li>
<li>We used router link parameters to navigate to the detail view of a user-selected hero.</li>
<li>We shared the HeroService among multiple components.</li>


# HTTP

In this last section of the project, we'll add the following data persistence features with help from Angular's HttpClient.

<li>The HeroService gets hero data with HTTP requests.</li>
<li>Users can add, edit, and delete heroes and save these changes over HTTP.</li>
<li>Users can search for heroes by name.</li>

# Enable HTTP Services

HttpClient is Angular's mechanism for communicating with a remote server over HTTP.

To make HttpClient available everywhere in the app,

<li>open the root AppModule</li>
<li>import the HttpClientModule symbol from @angular/common/http,</li>
<li>add it to the @NgModule.imports array.</li>

# Simulate a Data Server

As mentioned throughout this ReadME, this app mimics communication with a remote data ever by using the <b>In-memory Web API module</b>.

After installing the module, the app will make requests to and receive responses from the HttpClient without knowing that the In-memory Web API is intercepting those requests, applying them to an in-memory data store, and returning simulated responses.

This facility is a great convenience for the tutorial. You won't have to set up a server to learn about HttpClient.

It may also be convenient in the early stages of your own app development when the server's web api is ill-defined or not yet implemented.

Note: the In-memory Web API module has nothing to do with HTTP in Angular.

Now we'll import the InMemoryWebApiModule and the InMemoryDataService class and then add the InMemoryWebApiModule to the @NgModule.imports array - after importing the HttpClient, - while configuring it with the InMemoryDataService.

The forRoot() config method takes an InMemoryDataService class that primes the in-memory database.
