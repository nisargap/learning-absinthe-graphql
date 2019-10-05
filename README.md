# GraphQL with Absinthe and Dataloader

This is an updated version of the app defined in [this tutorial](https://www.howtographql.com/graphql-elixir/1-getting-started/)

## How to run this

1. Have the latest version of Elixir, Erlang, Phoenix, Postgres installed
2. Clone this project and within it run `mix deps.get`
3. Ensure that the db config is correct in config/dev.exs
4. Run `mix ecto.create` to create the db and `mix ecto.setup`
5. Run `iex -S mix phx.server`
6. Navigate to `localhost:4000/graphiql` in your browser
7. Sample query:

```
query {
  allLinks {
    id
    url
    description
  }
}
```

Returns all links in db

8. Sample create mutation:

```
mutation {
  createLink(description:"nisarga's site", url:"nisarga.io") {
	  id
    url
    description
  }
}
```

9. Sample delete mutation

```
mutation {
  deleteLink(id: "1") {
    id
  }
}
```

How this was created:

## Creation

```
mix phx.new community --no-html --no-webpack
```

In mix.exs the following was added:

```
      {:dataloader, "~> 1.0.0"},
      {:absinthe_plug, "~> 1.4.7"}
```

Ran `mix deps.get`

In config/dev.exs ensure that the db info for postgres is correct
Run mix ecto.create to create your main db for the project

Run the following command to generate a table and CRUD actions:

```
mix phx.gen.context News Link links url:string description:text
```

Added sample data to priv/repo/seeds.exs

```
alias Community.News.Link
alias Community.Repo

%Link{url: "http://graphql.org/", description: "The Best Query Language"} |> Repo.insert!
%Link{url: "http://dev.apollodata.com/", description: "Awesome GraphQL Client"} |> Repo.insert!
```

Ran `mix ecto.setup` to insert sample data into db

Defined GraphQL schema in `lib/community_web/schema.ex`

Modified `lib/community_web/router.ex` to include graphiql route for testing

## Default Readme information

To start your Phoenix server:

- Install dependencies with `mix deps.get`
- Create and migrate your database with `mix ecto.setup`
- Start Phoenix endpoint with `mix phx.server`

Now you can visit [`localhost:4000`](http://localhost:4000) from your browser.

Ready to run in production? Please [check our deployment guides](https://hexdocs.pm/phoenix/deployment.html).

## Learn more

- Official website: http://www.phoenixframework.org/
- Guides: https://hexdocs.pm/phoenix/overview.html
- Docs: https://hexdocs.pm/phoenix
- Mailing list: http://groups.google.com/group/phoenix-talk
- Source: https://github.com/phoenixframework/phoenix
