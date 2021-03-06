
## protocol
This is a signal protocol support by [protoo](https://protoojs.org/#protoo)


## 1 join room

### request

```
method:join
data:{
    "rid":"$roomid"
}
```

### response
```
//success
ok:true
data:{}

//failed
ok:false
errCode:-1

```
when publisher join success, SFU broadcast "onPublish" to him

## 2) leave room
### request

```
method:leave
data:{
    "rid":"$roomid"
}
```

### response
```
//success
ok:true
data:{}

//failed
ok:false
errCode:-1
```
## 3) publish
### request

```
method:publish
data:{
    "jsep": {"type": "offer","sdp": "..."}
}
```

### response
```
//success
ok:true
data:{
    "jsep": {"type": "answer","sdp": "..."}
}

//failed
ok:false
errCode:-1
```

## 4) onPublish

when publisher published success, SFU broadcast "onPublish" to others
### request

```
method:onPublish
data:{
    "pubid": "$pubid"
}
```

### response
```
//success
ok:true
data:{}

//failed
ok:false
errCode:-1
```

## 5) subscribe

client can subscribe $pubid when it get "onPublish"
### request
```
method:subscribe
data:{
    "pubid:"$pubid",
    "jsep": {"type": "offer","sdp": "..."}
}
```

### response
```
//success
ok:true
data:{
    "jsep": {"type": "answer","sdp": "..."}
}

//failed
ok:false
errCode:-1
```
## 6) onUnpublish

when publisher leave room, SFU broadcast "onUnpublish"

subscribers need to delete this pc and player when they receive "onUnpublish"
###request
```
method:onUnpublish
data:{
    "pubid": "$pubid"
}
```

###response
```
//success
ok:true
data:{}

//failed
ok:false
errCode:-1
```
## 7) control [WIP]
publishers can control their devices, like "muted" "close camera"..
