Mu uses Comint Mode to do its job. This has the added benefit of
providing you with an entire communication infrastructure. Minibuffer
history, moving between prompts, highlighting of SGR (escape sequences
controlling colors on a tty) using Ansi Color, etc.

Use ‘mu-open’ to open a new connection. This will create two buffers
for you. One buffer is the mu connection buffer. All the output from
the host appears here. You can also type your commands here, but this
will get confusing rather quickly as output gets added while your
type.

That’s when the other buffer, the mu input buffer, comes into play.
Whatever you type there will get sent to the mu connection buffer as
well. If you do that, input and output will happen in two different
buffers.

The only important buffer is the mu connection buffer. The mu input
buffer is just for convenience. You can create more mu input buffers
using ‘mu-input-buffer’, or you can kill all mu input buffers. It
doesn’t matter.

Before you can open new connections, you must customize ‘mu-worlds’.
As soon as you have done that, use ‘mu-open’ to play.

== Colors

Use Ansi Color. Here’s how to install it in your ~/.emacs:

    (autoload 'mu-open "mu" "Play on MUSHes and MUDs" t)
    (add-hook 'mu-connection-mode-hook 'ansi-color-for-comint-mode-on)

== Coding System

Switch to the output buffer and use ‘M-x mu-dos’ if your host is
sending you DOS line endings (ie. you have a ^M at the end of every
line). ‘set-process-coding-system’ can be used to set output and input
coding systems. There is probably some smart way of adding this to
‘mu-connection-mode-hook’.

    (defun mu-dos ()
      "Set coding system of the current buffer's process to DOS."
      (interactive)
      (set-process-coding-system 
       (get-buffer-process (current-buffer))
			   'iso-latin-1-dos
			   'iso-latin-1-unix))
