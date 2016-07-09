# angular2-rest
Angular2 HTTP client to consume RESTful services. Built on angular2/http with TypeScript.  
**Note:** this solutions is not production ready, it's in a very basic alpha state. Any ideas or contributions are very welcomed :)

## Installation

```sh
npm install angular2-rest
```

## Example

```ts

import {Request, Response} from '@angular/http';
import {
  RESTClient, GET, PUT, POST, DELETE, BaseUrl,
  Headers, DefaultHeaders, Path, Body, Query,
  Produces, MediaType
} from 'angular2-rest';
import {Todo} from './models/Todo';

@Injectable()
@BaseUrl("http://localhost:3000/api/v1/")
@DefaultHeaders({
    'Accept': 'application/json',
    'Content-Type': 'application/json'
})
export class TodoRESTClient extends RESTClient {

    @Produces(MediaType.JSON)
    @GET("todo/")
    public getTodos( @Query("sort") sort?: string): Observable { return null; };

    @Produces(MediaType.JSON)
    @GET("todo/{id}")
    public getTodoById( @Path("id") id: string): Observable { return null; };

    @HEADERS({'Authorization': 'Basic 123QWEASDZXC'})
    @Produces(MediaType.JSON)
    @POST("todo")
    public postTodo( @Body todo: Todo): Observable { return null; };

    @HEADERS({'Authorization': 'Basic 123QWEASDZXC'})
    @Produces(MediaType.JSON)
    @PUT("todo/{id}")
    public putTodoById( @Path("id") id: string, @Body todo: Todo): Observable { return null; };

    @HEADERS({'Authorization': 'Basic 123QWEASDZXC'})
    @DELETE("todo/{id}")
    public deleteTodoById( @Path("id") id: string): Observable { return null; };

}
```

### Using it in your component


``` ts
@Component({
  selector: 'to-do',
  viewProviders: [TodoRESTClient],
})
@View({
  templateUrl: 'components/to-do-template.html',
})
export class ToDoCmp {

  constructor(private todoRESTClient: TodoRESTClient) {
    this.sampleUsage()
  }

  //Use todoRESTClient
  sampleUsage(){
    this.todoRESTClient.getTodos().subscribe(data=>{
      console.log(data)
    })
  }  
}
```
## API Docs

### RESTClient
#### Methods:
- `getBaseUrl(): string`: returns the base url of RESTClient
- `getDefaultHeaders(): Object`: returns the default headers of RESTClient in a key-value pair

### Class decorators:
- `@BaseUrl(url: string)`
- `@DefaultHeaders(headers: Object)`

### Method decorators:
- `@GET(url: String)`
- `@POST(url: String)`
- `@PUT(url: String)`
- `@DELETE(url: String)`
- `@Headers(headers: Object)`

### Parameter decorators:
- `@Path(key: string)`
- `@Query(key: string)`
- `@Header(key: string)`
- `@Body`

# License

MIT
