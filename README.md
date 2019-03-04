### leaf
---
https://github.com/name5566/leaf

```go
log.Debug("1")

var res string

skeleton.Go(func() {
  time.Sleep(1 * time.Second)
  
  res = "3"
}, func() {
  log.Debug(res)
})

log.Debug("2")


func AfterFunc(d Duration, f func()) *Timer


skeleton.AfterFunc(5 * time.Second, func() {
})


LogFlag = log.Lshortfile


type Test struct {
  Id int "index"
  Arr [4]int
  Str string
}

var RfTest = readRf(Test{})

func init() {
  r := RfTest.Index(1)
  
  if r != nil {
    row := r.(*Test)
    
    log.Debug("%v %v %v", row.Id, row.Arr, row.Str)
  }
}


package internal

import (
  "github.com/name5566/leaf/gate"
)

func init() {
  skeleton.RegisterChanRPC("NewAgent", rpcNewAgent)
  skeleton.RegisterChanRPC("CloseAgent", rpcCloseAgent)
}

func init() {
  skeleton.RegisterChanRPC("NewAgent", rpcNewAgent)
  skeleton.RegisterChanRPC("CloseAgent", rpcCloseAgent)
}

func rpcNewAgent(args []interface{}) {
}

func rpcCloseAgent(args []interface{}) {
}

package internal

import (
  "github.com/name5566/leaf/module"
  "server/base"
)

var (
  skeleton = base.NewSkeleton()
  ChanRPC = skeleton.ChanRPCServer
)

type Module struct {
  *module.Skeleton
}

func (m *Module) OnInit() {
  m.Skeleton = skeleton
}

func (m *Module) OnDestroy() {
}


package game

import (
  "server/game/internal"
)

var (
  Module = new(internal.Module)
  ChanRPC = internal.ChanRPC
)


var ws = new WebSocket('ws://127.0.0.1:3653')

ws.onopen = function() {
  ws.send(JSON.stringify({Hello: {
    Name: 'leaf'
  }}))
}



package main

import (
  "encoding/binary"
  "net"
)

func main() {
  conn, err := net.Dial("tcp", "127.0.0.1:3563")
  if err != nil {
    panic(err)
  }
  
  data := []byte(`{
    "Hello": {
      "Name": "leaf"
    }
  }`)
  
  m := make([]bute, 2+len(data))
  
  binary.BigEndian.PutUint16(m, uint16(len(data)))
  
  copy(m[2:], data)
  
  conn.Writer(m)
}


package internal

import (
  "github.com/name5566/leaf/log"
  "github.com/name5566/leaf/gate"
  "reflect"
  "server/msg"
)

func init() {
  handler(&msg.Hello{}, handleHello)
}

func handler(m interface{}, h interface{}) {
  skeleton.RegisterChanRPC(reflect.TypeOf(m), h)
}

func handleHello(args []interface{}) {
  m := args[0].(*msg.Hello)
  a := args[1].(gate.Agent)
  log.Debug("hello %v", m.Name)
  a.WriteMsg(&msg.Hello{
    Name: "client",
  })
}


package gate

import (
  "server/game"
  "server/msg"
)

func init() {
  msg.Processor.SetRouter(&msg.Hello{}, game.ChanRPC)
}

package msg

import (
  "github.com/name5566/leaf/network/json"
)

var Processor = json.NewProcessor()

func init() {
  Processor.Register(&Hello{})
}

type Hello struct {
  Name string
}


package msg

import (
  "github.com/name5566/leaf/network"
)

var Processor network.Processor

func init() {
}

type Module interface {
  OnInit()
  OnDestroy()
  Run(closeSig chan bool)
}

leaf.Run(
  game.Module,
  gate.Module,
  login.Module,
)
```

```
{
  "LogLevel": "debug",
  "LogPath": "",
  "TCPAddr": "127.0.0.1:3563",
  "WSAddr": "127.0.0.1:3653",
  "MaxConnNum": 20000
}
```

```
go get github.com/name5566/leaf
go install server
```


