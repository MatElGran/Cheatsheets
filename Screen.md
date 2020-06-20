
# Screen cheatsheet

tags = #screen #cheatsheet

- start a new session

```shell
screen
```

- detach current session

```shell
^-a d
```

- reattach session

```shell
screen -r [SESSION_ID]
```

- list open windows with ids

```shell
screen -list
```

- list windows in current session

```shell
^-a "
```

- next window in current session

```shell
^-a n
```

- previous window in current session

```shell
^-a p
```

- rename window

```shell
^-a A
```

- kill current window

```shell
^-a k
```
