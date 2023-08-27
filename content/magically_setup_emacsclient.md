---
title: Magically setup emacsclient

date: 2019-05-25
updated: 2019-08-02
taxonomies:
    tags: [tech,]
---
This is a magical way of automatically setting up emacsclient, by [northrupthebandgeek](https://en.reddit.com/user/northrupthebandgeek). If you start emacs for the first time, it will start a server. If the server has already been started, it will delegate to emacsclient. 

One tiny improvement over the function defined on the [reddit post](https://en.reddit.com/r/emacs/comments/4586eq/quick_emacs_snippet_to_automatically_use/), is that this doesn't guess what is the name of the emacs server file. It instead generates the nam
e in the same ways as done by the server package.

```el
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
    ;; from: https://en.reddit.com/r/emacs/comments/4586eq/quick_emacs_snippet_to_automatically_use/
    ;;
    ;; Automagical EmacsClient functionality
    ;;
    ;; Basically, if Emacs is already running, this shunts things over to
    ;; the existing Emacs; otherwise, it readies itself to accept said
    ;; shunting.
    ;;
    ;; This operates by detecting the existence of an Emacs server socket
    ;; file.  If a socket is found, Emacs will
    ;; spin up emacsclient and immediately exit itself.  Otherwise, Emacs
    ;; will start a new server.
    
    
    (defun server-already-running-p ()
      "Is Emacs already running?
    Gets name based on server-force-delete."
           (let ((file (expand-file-name
                        server-name
    		    (if server-use-tcp
    		        server-auth-dir
    		      server-socket-dir))))
             (file-exists-p file)))
    
    (defun server-shunt ()
      "Shunts to emacsclient"
           (let ((args (append '("emacsclient" "-a" "\"\"" "-c" "-n")
                               (cdr command-line-args))))
             (shell-command (substring (format "%S" args) 1 -1))
             (kill-emacs)))
    
    (unless (featurep 'server)
      (unless (boundp 'server-process)
        (require 'server)
        (if (server-already-running-p) (server-shunt) (server-start))))
    ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
```
