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
cayley http --config=cayley.cfg -assets /home/oren/p/go/src/github.com/google/cayley/
cayley repl --config=cayley.cfg
```

Query

```
g.V("character:finn").Out("in love with").All()
```


