# Extending the ngx-user-admin Package

Extending the ngx-user-admin package is simple and a safe way to extend the package for usage in your package.

## Extended Component Example: Home Component

Below is an example of an extended version of the ngx-user-admin Home Component. This simple example shows how we can provide a custom HTML template to the component so we can provide a different list of links for the user.  

Here are the two files that make up our custom component:

File: `myhome/myhome.component.ts`

```
...

// Import the component we will extend
import { HomeComponent }   from '@erdiko/ngx-user-admin';

@Component({
  selector: 'app-myhome',
  templateUrl: './myhome.component.html'
})
export class MyhomeComponent extends HomeComponent {

  constructor() {
    super();
  }

}
```

File: `myhome/myhome.component.html`

```
<div class="row">
  <div class="col-xs-12">
    <h1 id="welcome-title">My Extended ngx-user-admin Home Component</h1>
  </div>
</div>
<div class="row">
  <div class="col-xs-12">
    <br />
  </div>
</div>
<div class="row">
  <div class="col-sm-6 col-xs-12">
    <ul class="list-group">
      <li class="list-group-item">
        <a routerLink="/user/">My Create a User</a>
      </li>
    </ul>
  </div>
</div>
```


## Extended Component Example: User Edit 

Below is an example of an extended version of the ngx-user-admin Home Component. This simple example shows how we can provide a custom HTML template to the component so we can provide a different list of links for the user.  

Here are the two files that make up our custom component:


File: `myuseredit/myuseredit.component.ts`

```
...

// Import the components & service we will extend
import { UserEditComponent }    from '@erdiko/ngx-user-admin';
import { AuthService }          from '@erdiko/ngx-user-admin';
import { UsersService }         from '@erdiko/ngx-user-admin';
import { MessageService }       from '@erdiko/ngx-user-admin';

@Component({
  selector: 'app-myusereditcomponent',
  templateUrl: './myuseredit.component.html',
  providers: [AuthService, UsersService, MessageService]
})
export class MyusereditComponent extends UserEditComponent {

    constructor(
            @Inject(UsersService) usersService: UsersService,
            @Inject(ActivatedRoute) route: ActivatedRoute,
            @Inject(Router) router: Router,
            @Inject(MessageService) messageService: MessageService) {

        super(usersService, route, router, messageService);
    }

}
```

File: `myuseredit/myuseredit.component.html`

```
<div class="row">
    <div class="col-xs-12">
        <button class="btn btn-info btn-sm" routerLink="/">
            <i class="fa fa-chevron-left" aria-hidden="true"></i> Back to Home
        </button>
    </div>
</div>
<div class="row">
    <div class="col-xs-12">
        <br/>
    </div>
</div>
<div class="row">
    <div class="col-xs-12">
        <div class="panel panel-default" id="edit-update">

            <h2>My User Edit Component</h2>

            <p>[Form goes here]</p>

        </div>
    </div>
</div>
```

## Setting up your Application module and component

Another required step to extend the ngx-user-admin package is to overload the routes to use your newly created components in your application.

Here is a modified Application module where we point out some unique code to use the extended components.

File: `app/app.module.ts`

```
...

import { UserAdminModule }      from '@erdiko/ngx-user-admin';

import { UsersService }         from '@erdiko/ngx-user-admin';
import { MessageService }       from '@erdiko/ngx-user-admin';

import { AppComponent }         from './app.component';

// Extended components from ngx-user-admin package
import { MyhomeComponent }      from './myhome/myhome.component';
import { MyusereditComponent }  from './myuseredit/myuseredit.component';

/**
  Custom routing to make sure we use our extended components
 */

// clang-format off
const routes: Routes = [
     {
         path: 'user',
         component: MyusereditComponent
     },
     {
         path: '',
         component: MyhomeComponent
     },
     {
         path: '**',
         redirectTo: ''
     }
];
// clang-format on

@NgModule({
  declarations: [
    AppComponent,

    // Declare our custom components
    MyhomeComponent,
    MyusereditComponent
  ],
  imports: [

    ...

    // Import our custom routes
    RouterModule.forRoot(routes),
  ],
  providers: [

  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

File: `app/app.component.html`

```
<h1>
  {{title}}
</h1>
<div class="page-content">
    <router-outlet></router-outlet>
</div>
```

