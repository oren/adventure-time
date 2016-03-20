# adventure-time

Install Cayley

```
curl -L https://github.com/google/cayley/releases/download/v0.4.1/cayley_0.4.1_linux_amd64.tar.gz | tar xz
sudo cp cayley_0.4.1_linux_amd64/cayley /usr/local/bin/
rm -r cayley_0.4.1_linux_amd64
```

Run

```
cayley init --config=cayley.cfg
cayley load --config=cayley.cfg --quads=db.nq
cayley repl --config=cayley.cfg
cayley http --config=cayley.cfg
```

## Queries

Find everyone that Ice King has a crush on

```
g.V("character:ice-king").Out("has a crush on").All()

{
  "result": [ {
      "id": "character:marceline-abadeer"
    },
    {
    "id": "character:princess-bubblegum"
    }
  ]
}
```

Find everyone that have a crush on Princess Bubblegum

```
g.V("character:princess-bubblegum").In("has a crush on").All()

{
  "result": [ {
      "id": "character:ice-king"
    }
  ]
}
```

Find all the haters

```
g.V().In("hates").All()

{
  "result": [
    {
    "id": "character:lumpy-space-princess",
    },
    {
    "id": "character:bmo",
    },
    {
    "id": "character:marceline-abadeer",
    },
    {
    "id": "character:finn",
    },
    {
    "id": "character:lady-rainicorn",
    },
    {
    "id": "character:princess-bubblegum",
    },
    {
    "id": "character:jake",
    }
  ]
}
```

Find all the haters (and tag who they hate)

```
g.V().Tag("name").In("hates").All()

{
"result": [
  {
  "id": "character:lumpy-space-princess",
  "name": "character:ice-king"
  },
  {
  "id": "character:bmo",
  "name": "character:ice-king"
  },
  {
  "id": "character:marceline-abadeer",
  "name": "character:ice-king"
  },
  {
  "id": "character:finn",
  "name": "character:ice-king"
  },
  {
  "id": "character:lady-rainicorn",
...
```

Who hates Ice King?

```
g.V().Has("hates", "character:ice-king"").All()

{
  "result": [
    {
    "id": "character:lumpy-space-princess"
    },
    {
    "id": "character:bmo"
    },
    {
    "id": "character:marceline-abadeer"
    },
    {
    "id": "character:finn"
    },
    {
    "id": "character:lady-rainicorn"
    },
    {
    "id": "character:princess-bubblegum"
```

Find all haters that lives with BMO

```
haters = g.V().In("hates")
lives_with_bmo = g.V("character:bmo").In("lives with")
haters.And(lives_with_bmo).All()

{
  "result": [
    {
    "id": "character:finn"
    },
    {
    "id": "character:jake"
    }
  ]
}
```
