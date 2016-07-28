---
layout: post
title:  "Boot and Vagrant"
categories: howto
date:   2016-07-28
tags: clojure boot-clj programming vagrantup
comments: True
---
![boot-clj logo](/assets/boot-logo-3.png)

[Boot](http://boot-clj.com) is a new-ish software build system
designed for and built with [Clojure](http://www.clojure.org) and
[ClojureScript](https://github.com/clojure/clojurescript).  Here are
some notes on using it with a [Vagrant](https://www.vagrantup.com)
session on a Mac.[^TODO]

This is very much a work in progress.  I generally like working with
Vagrant to keep my development environments packaged, isolated, and
repeatably built.  No exception while I learn Clojure / ClojureScript,
and as I decide on the surrounding tooling like `boot`.  The main
hurdles were to get the REPL and reload connections to be exposed to
Vagrant network forwards.

### build.boot
```clojure
;; define dev task as composition of subtasks
(deftask dev
  "Launch Immediate Feedback Development Environment"
  []
  (comp 
   (serve :dir "target")
   (watch)
   (reload :port (int 3001))            ;; ports 3000-3003 are forwarded by Vagrantfile
   (cljs-repl :nrepl-opts {:port 3002 :bind "0.0.0.0"})
   (cljs)
   (target :dir #{"target"})))
```
1. `:port` in `reload` needs to be cast to an int.
2. I failed to get bash to pass the EDN
   parameter `{:port 3002 :bind "0.0.0.0"}` to `cljs-repl` for the
   nREPL port on the command line, so creating a `deftask` 
   is necessary.[^cljs-repl]
3. The `:bind` parameter in `cljs-repl` overrides the default
   `localhost`, which is not visible to Vagrant.
4. Run with `boot dev`.
5. Thank you to
   [modern_cljs](https://github.com/magomimmo/modern-cljs/blob/master/doc/second-edition/tutorial-03.md#enter-deftask)
   tutorial for the source task.

### Vagrantfile
```
  config.vm.network "forwarded_port", guest: 3000, host: 3000 # web server
  config.vm.network "forwarded_port", guest: 3001, host: 3001 # reload browser signaling
  config.vm.network "forwarded_port", guest: 3002, host: 3002 # nREPL 
  config.vm.network "forwarded_port", guest: 3003, host: 3003 # bREPL 
```

### Emacs
To connect to the guest nREPL for the CLJS environment

```
M-x cider-connect
localhost
3002
```
1. `M-x cider-connect` doesn't (yet) bind the host cider environment
   to the guest REPL, so sadly a lot of the magic isn't working yet,
   like `cider-eval-defun-at-point`

In the nREPL, to connect to the bREPL

```
boot.user> (start-repl :port (int 3003) :ip "0.0.0.0")
<< started Weasel server on ws://0.0.0.0:3003 >>
<< waiting for client to connect ... Connection is ws://localhost:3003
Writing boot_cljs_repl.cljs...
(open host browser at http://localhost:3000)
 connected! >>
To quit, type: :cljs/quit
nil
cljs.user> (js/alert "hello")
(dismiss popup in host browser)
```

### Detailed use case

- a Clojure application server in development mode on port 3000
- the guest virtual machine is running Ubuntu Linux.
- web application runs ClojureScript
- web browser is on host Mac
- Emacs running Cider is the development environment running on the
   host Mac
- Cider to nREPL on guest, chained to bREPL to the browser for
debugging / inspection.
- Boot tasks: [serve](https://github.com/pandeiro/boot-http) [watch](https://github.com/boot-clj/boot/blob/master/doc/boot.task.built-in.md#watch)[^watch] [reload](https://github.com/adzerk-oss/boot-reload) [cljs-repl](https://github.com/adzerk-oss/boot-cljs-repl) [cljs](https://github.com/adzerk-oss/boot-cljs)
- Guest OS: Ubuntu Trusty64.  Host OS: MacOS 10.11.5.  Vagrant
   version: 1.8.1.  Provider: vm_fusion.  Hypervisor: VMware
   Fusion 8.1.1.  Clojure: 1.7.0.  Java: SE Runtime build
   1.8.0\_91-b14 and HotSpot 64-bit Server VM build 25.91-b14, mixed
   mode. Emacs: Aquamacs 3.2 GNU Emacs 24.4.51.2

   
[^TODO]: TODO: create a GitHub repo with an auto-provisioning Vagrantfile as a nice template. 
[^cljs-repl]: `boot cljs-repl -n "{:port 3002 :bind \"0.0.0.0\"}"`: clojure.lang.ExceptionInfo: clojure.lang.PersistentVector cannot be cast to java.lang.String.  
[^watch]: The guest filesystem ```watch``` is blind to changes made from the host's Vagrant synced files.  Sadly this currently means that touching a file from the guest to kickoff a build. 


