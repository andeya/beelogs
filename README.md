## beelogs
beelogs is the upgrade version from beego logs! beelogs add some methods, such as Rest(), GoOn(), StealOne()... 


## How to install?

	go get github.com/henrylee2cn/beelogs


## What adapters are supported?

As of now this logs support console, file,smtp and conn.


## How to use it?

First you must import it

	import (
		"github.com/henrylee2cn/beelogs"
	)

Then init a Log (example with console adapter)

	log := NewLogger(10000,false)
	log.SetLogger("console", map[]interface{"level":2,"writer":os.Stdout})

> the first params stand for how many channel

Use it like this:	
	
    log.Debug("debug")
    log.Informational("info")
    log.Notice("notice")
    log.Warning("warning")
    log.Error("error")
    log.Critical("critical")
    log.Alert("alert")
    log.Emergency("emergency")


## File adapter

Configure file adapter like this:

	log := NewLogger(10000)
	log.SetLogger("file", map[string]interface{}{"filename":"test.log"})


## Conn adapter

Configure like this:

	log := NewLogger(1000)
	log.SetLogger("conn", map[string]interface{}{"net":"tcp","addr":":7020"})
	log.Info("info")


## Smtp adapter

Configure like this:

    log := NewLogger(10000)
    log.SetLogger("smtp", map[string]interface{}{
        "username": "beegotest@gmail.com",
        "password": "xxxxxxxx",
        "host":     "smtp.gmail.com:587",
        "sendTos": []string{
            "xiemengjun@gmail.com",
        },
    })
    log.Critical("sendmail critical")
    time.Sleep(time.Second * 30)



## StealOne

Configure like this:

	log := NewLogger(10000)
    log.SetStealLevel(LevelNotice)
	log.Critical("sendmail critical")
    for level, msg, normal := StealOne(); normal; level, msg, normal = StealOne() {
        fmt.Println(level, msg)
    }
	time.Sleep(time.Second * 30)
